---
title: Install
description: Install Podcli on macOS, Linux, or Windows. Platforms, scoring auth, and the PyPI name collision.
group: Start
order: 2
---

No prerequisites. The installer fetches a self-contained binary. The first run
of the studio or `podcli process` provisions Python, Node, FFmpeg, whisper.cpp,
and models into a managed folder.

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

## Platforms

macOS (Apple Silicon), Linux (x64 and arm64), and Windows (x64). Intel Macs
aren't supported.

## Not the PyPI package

`pip install podcli` installs an unrelated terminal podcast client. Podcli is
not on PyPI. Use the installer above.

## Scoring auth

Clip scoring uses Claude Code or Codex login, or an Anthropic API key. Without
those it falls back to heuristics. Speaker diarization needs `HF_TOKEN`.

Transcription and rendering always run locally. Scoring is optional.

## First run and MCP

The first run of `podcli`, `process`, `studio`, `transcribe`, or `multicam`
provisions the engine. `podcli mcp` does not — stdout is JSON-RPC — so run
`podcli setup` before pointing an agent at it.

```bash
podcli setup
podcli mcp install
```

`podcli mcp install` registers the server with Claude Code and Codex, whichever
CLI is on PATH. Config snippets for those and for Cursor are on the
[MCP server](https://podcli.com/docs/mcp-server) page.

## Check the install

```bash
podcli doctor --json
```
