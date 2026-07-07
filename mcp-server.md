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

For the marketing overview and the full tool list, see the
[MCP page](https://podcli.com/mcp).

## Add it to Claude Code

Install Podcli, then register the server:

```bash
podcli mcp install
```

## Add it to Claude Desktop or Codex

The config is one block. Same shape everywhere:

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
