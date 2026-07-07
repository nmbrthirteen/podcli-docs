---
title: Getting started
description: Install Podcli, drop in an episode, and get captioned clips, a content package, and performance analytics. A guided walkthrough with real screenshots.
group: Start
order: 1
---

Podcli runs on your laptop. Drop in a podcast episode and it transcribes,
finds the moments worth clipping, crops to the speaker, and burns captions in.
Nothing leaves your machine.

This walkthrough covers the whole flow, start to finish.

## Install

No prerequisites. The installer fetches a self-contained binary, and the first
run provisions everything it needs (Python, Node, FFmpeg, whisper.cpp, models)
into a managed folder.

**macOS and Linux**

```bash
curl -fsSL https://podcli.com/install.sh | sh
```

**Windows (PowerShell)**

```powershell
irm https://podcli.com/install.ps1 | iex
```

Then run `podcli` and choose Open Web UI. The studio opens at
`http://localhost:3847`.

```bash
podcli
```

Prefer the terminal? Everything here also works from the [CLI](https://podcli.com/docs/cli).

## 1. Drop in your episode

Open the studio and go to **New episode**. Drag in a local video, or paste a
YouTube or direct link and Podcli downloads it. Pick a transcript engine
(Whisper, or paste your own), then set caption style, crop, and format, and drop
in a logo, intro, or outro from your [brand kit](https://podcli.com/docs/the-studio#assets). The
phone preview updates live.

![The New episode page: video input, transcript engine, caption and format settings, and a live 9:16 preview.](https://podcli.com/docs/studio-new-episode.png)

## 2. Get clips automatically

Podcli scores the transcript against your knowledge base, finds the moments
worth clipping, and cuts filler into multi-segment clips. Every clip comes out
captioned, framed on the speaker, and on-brand. Review them in the **Library**,
grouped by episode.

![The Library grouping generated clips by episode, each card a captioned vertical thumbnail.](https://podcli.com/docs/studio-library.png)

## 3. Generate the content package

Open any clip for a publish-ready package: title options, a description, tags,
hashtags, and a thumbnail you can regenerate or reframe. Copy what you need, or
change the caption style and re-render.

![A clip detail page with title options, description, tags, hashtags, and a thumbnail editor.](https://podcli.com/docs/studio-clip-detail.png)

## 4. Track what actually works

Link clips to YouTube and sync views, retention, and CTR back into the studio.
**Analytics** shows what holds viewers by content type, caption style, and
length, so the next batch is better than the last.

![The Analytics page with retention, CTR, and views broken down by content type, caption style, and length.](https://podcli.com/docs/studio-analytics.png)

## Where to next

- [Tour the studio](https://podcli.com/docs/the-studio): every page, one at a time.
- [CLI reference](https://podcli.com/docs/cli): drive the whole pipeline from your terminal.
- [MCP server](https://podcli.com/docs/mcp-server): run it from Claude Code, Codex, or Cursor.
- [Captions and formats](https://podcli.com/docs/captions-and-formats): the four styles and three aspect ratios.
