---
title: MCP server
description: Add Podcli to Claude Code, Claude Desktop, Codex, or Cursor and clip podcasts by talking to the agent. The MCP server exposes the whole pipeline as tools.
group: Guides
order: 5
---

Podcli ships as a Model Context Protocol server. Plug it into any MCP client and
the agent runs the whole pipeline: transcribe, score clips against your
knowledge base, crop, caption, and export. Say "clip this episode" and it does
the rest.

Run `podcli setup` before `podcli mcp`. The MCP command does not provision,
because stdout is JSON-RPC.

```bash
podcli setup
podcli mcp install
```

`podcli mcp install` registers the server with Claude Code and Codex, whichever
CLI is on PATH. Clip scoring uses Claude Code or Codex login, or an Anthropic
API key. Without those it falls back to heuristics.

For the marketing overview see the [MCP page](https://podcli.com/mcp).

## Add it to Claude Code

```bash
podcli mcp install
```

Or register by hand:

```bash
claude mcp add podcli -- podcli mcp
```

## Add it to Codex

`podcli mcp install` registers with Codex too when the `codex` CLI is on PATH.
To register by hand:

```bash
codex mcp add podcli -- podcli mcp
```

## Add it to Cursor

Project config, `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "podcli": {
      "command": "podcli",
      "args": ["mcp"]
    }
  }
}
```

The same block goes in Claude Desktop's `claude_desktop_config.json`.

## What you say to the agent

Natural language. The agent reads the tool list and figures out the call
sequence.

```text
Transcribe episode-072.mp4 and suggest the top eight clips.
Register logo.png as my default logo, then render the selected clips with it.
Render the selected clips in 1080×1920 with the karaoke caption style.
Check clip 4 against the episode database. Have we shipped anything close before?
```

The `manage_assets` tool keeps a shared library of logos, outros, intros, and
music. Register once and the agent (and the studio and CLI) can reference them
by name in any render.

## Privacy

The MCP server runs locally as a process the agent talks to. The video,
transcript, and renders stay on your machine. The only network calls are the
optional Claude or Codex API calls when you use AI clip scoring.

## Next release

v2.8.1 exposes 30 tools. The next release adds `rank_clip_candidates` and
`process_episode` (32 total), ships `SKILL.md`, and documents the headless CLI
on the [CLI reference](https://podcli.com/docs/cli#headless-next-release). Until
that ships, the original 30 tools work as they do today.

### SKILL.md

`SKILL.md` in the podcli repo is the agent workflow: setup, the headless CLI,
and the short MCP path so the agent does not load the full transcript.

Prefer the short path:

1. `transcribe_podcast` (or `transcribe_start` + `job_status` on a long file)
2. `rank_clip_candidates(video_path)` — about 20 sentence-aligned candidates
3. Pick a subset. `suggest_clips` to store them, or `create_clip` /
   `batch_create_clips` to render
4. `list_outputs` if you only need paths on disk

One-shot when the user wants finished files, not a review pass:

1. `process_episode(video_path)`
2. `job_status(job_id, wait_seconds: 30)` until `done`
3. Read clip paths, durations, scores, titles, captions from `result`

Do not call `get_ui_state(include_transcript: true)` unless you need to rewrite
a range; use `rank_clip_candidates`. Do not run `podcli mcp` as the first
command on a fresh install; run `podcli setup`.

### `rank_clip_candidates`, `process_episode`, and `job_status`

`rank_clip_candidates` returns a shortlist from the cached transcript so the
agent does not have to read the whole thing. It does not call an AI CLI.

`process_episode` runs transcribe, rank, and render as one job. It returns
`{ job_id }` immediately and does not need the studio. The result is the same
JSON `podcli process --json` prints.

`job_status` already exists. Poll any background job (transcription, render,
batch export, `process_episode`) with `wait_seconds` (default 30). Stop when
`done` is true.

### Tool reference

32 tools, generated from the product repo's docs manifest. v2.8.1 is the same
list without `rank_clip_candidates` and `process_episode`.

**Transcription and input**

| Tool | What it does |
| --- | --- |
| `transcribe_podcast` | Transcribe audio/video with Whisper word timestamps + speaker detection |
| `transcribe_start` | Start transcription as a background job, returns a job_id immediately |
| `job_status` | Poll any background job (transcription, render, batch export, process_episode) with long-polling |
| `set_video` | Set the working video without transcribing |
| `import_transcript` | Import an external transcript with word-level timestamps, skips Whisper |
| `parse_transcript` | Parse a speaker-labeled plain text transcript into word-level timestamps |
| `compare_transcription_engines` | Transcribe one sample with two engines and write a side-by-side disagreement report |
| `mine_channel` | List a YouTube channel's uploads or mine one video's existing captions, without downloading the video |

**Clip workflow**

| Tool | What it does |
| --- | --- |
| `get_ui_state` | Read session state (video, transcript, suggestions, settings) and next steps |
| `rank_clip_candidates` | Return ~20 pre-ranked, sentence-aligned clip candidates from the cached transcript (no full transcript in the result) |
| `process_episode` | One-shot job: transcribe, rank, render; poll with `job_status` and read clip paths from the result |
| `suggest_clips` | Submit clip suggestions, assigns clip numbers, pushes them to the web UI |
| `modify_clip` | Adjust a suggested clip: timing, title, caption style, or delete it |
| `toggle_clip` | Select or deselect a suggested clip for export |
| `create_clip` | Render a single clip with burned-in captions and normalized audio |
| `batch_create_clips` | Render multiple clips in one batch |
| `manage_reel` | Build a highlights reel: detect once, edit moments, rebuild without re-detecting |
| `analyze_energy` | Analyze audio energy levels to find high-energy moments |
| `record_decisions` | Record per-episode decisions (clip count, duration range, captions, language, thumbnails, delivery target) so later runs never re-ask |

**Full-episode editing**

| Tool | What it does |
| --- | --- |
| `manage_multicam` | Map camera, mic and call-recording files to people, sync them by audio, auto-cut to the speaker, render, export a studio shoot to Premiere / FCPXML, or hand the edit to the podcli cloud editor |

**Content and configuration**

| Tool | What it does |
| --- | --- |
| `knowledge_base` | Read or manage the `.podcli/knowledge/` context files |
| `manage_assets` | Register and manage reusable assets: logos, intros, outros, music |
| `clip_history` | View previously created clips to avoid duplicates |
| `list_outputs` | List rendered clip files with sizes and dates |
| `update_settings` | Update rendering settings: caption style, crop strategy, logo, outro |
| `manage_presets` | Save, load, list, or delete rendering presets |
| `manage_thumbnail_config` | Show, export, import, or reset the thumbnail template |

**Integrations and environment**

| Tool | What it does |
| --- | --- |
| `manage_integrations` | List, enable, or disable podcli integrations |
| `export_to_davinci_resolve` | Export shorts as a DaVinci Resolve FCPXML project |
| `manage_config` | Manage portable config profiles and legacy path migration |
| `manage_env` | List, set, or unset global podcli settings stored in `.env` |
| `ai_cli_status` | Show whether Claude Code / Codex CLIs are available for AI features |
