---
title: The studio
description: A tour of every page in the Podcli studio, from the Library to Analytics, each with a screenshot and what you do there.
group: Guides
order: 2
---

The studio is a local web app at `http://localhost:3847`. Launch it with
`podcli` (choose Open Web UI) or `podcli ui`. The sidebar groups pages into
Studio, Workspace, and Insights.

## Library

Every processed episode and clip, grouped by source video. Preview a clip,
re-render it, or delete it. This is the home screen.

![The Library page](/docs/studio-library.png)

## New episode

The core workflow. Set a video (local file or a pasted URL), transcribe with
Whisper or paste your own transcript, pick [caption style, crop, and
format](/docs/captions-and-formats), then export. A live phone preview shows the
captions as you go.

![The New episode page](/docs/studio-new-episode.png)

## Content

Generate titles, descriptions, tags, and hashtags for an episode or clip.
Regenerate any section with your own guidance, or ask for anything custom (a
LinkedIn post, a thread, ten punchier hooks).

![The Content studio page](/docs/studio-content.png)

## Highlights

Detect the standout moments across an episode and assemble a highlight reel with
a visual editor. Trim, reorder, and export in any format.

![The Highlights page](/docs/studio-highlights.png)

## Thumbnails

Generate and refine thumbnails: pick a source frame, edit the text, and cycle
through variations. The chosen thumbnail can be baked into the clip's opening.

![The Thumbnail studio page](/docs/studio-thumbnails.png)

## Knowledge

Your brand brain: voice, banned words, title formulas, and the episode database
Podcli reads when scoring clips. Drag in `.md` files or edit them inline.

![The Knowledge base page](/docs/studio-knowledge.png)

## Config

Paths (AI provider, Hugging Face token), Whisper settings, and config profiles
you can export and activate across machines.

![The Config page](/docs/studio-config.png)

## Integrations

Connect external services, like YouTube for the performance loop and DaVinci
Resolve for FCPXML export.

![The Integrations page](/docs/studio-integrations.png)

## MCP setup

Register Podcli with Claude Code, Claude Desktop, Codex, or Cursor. See the
[MCP server](/docs/mcp-server) guide for the full setup.

![The MCP setup page](/docs/studio-mcp-setup.png)

## Analytics

The YouTube performance loop. Sync views, retention, and CTR, then see what
holds viewers by content type, caption style, and length.

![The Analytics page](/docs/studio-analytics.png)
