---
title: CLI reference
description: Drive the whole Podcli pipeline from your terminal. One command transcribes, picks moments, crops to the speaker, and burns captions in.
group: Guides
order: 3
---

Everything the [studio](/docs/the-studio) does is available from the terminal.
The one command you need most:

```bash
podcli process episode.mp4
```

That transcribes, picks the best moments, crops to the face, burns captions in,
and writes upload-ready clips. Nothing leaves your machine.

## Common flags

Use an existing transcript instead of transcribing, and cap the clip count:

```bash
podcli process episode.mp4 --transcript transcript.txt --top 5
```

Set caption style, crop mode, and output format:

```bash
podcli process episode.mp4 --caption-style karaoke --crop face --format horizontal
```

Force thumbnails on or off:

```bash
podcli process episode.mp4 --thumbnails
podcli process episode.mp4 --no-thumbnails
```

| Flag | What it does |
| --- | --- |
| `--transcript <file>` | Use a `.txt` / `.srt` / `.vtt` transcript instead of transcribing. |
| `--top <n>` | Cap the number of clips. |
| `--caption-style <style>` | `branded`, `hormozi`, `karaoke`, or `subtle`. See [captions and formats](/docs/captions-and-formats). |
| `--crop <mode>` | `center`, `face`, or `speaker`. |
| `--format <ratio>` | `vertical` (9:16), `horizontal` (16:9), or `square` (1:1). |
| `--logo <file>` | Bake a logo onto every clip. |
| `--thumbnails` / `--no-thumbnails` | Force thumbnail generation on or off. |

## Presets

Save a set of render settings once and reuse it:

```bash
podcli presets save my-show
podcli process episode.mp4 --preset my-show
```

## Other commands

`podcli` opens the interactive menu with Open Web UI. `podcli ui` opens the
studio directly at `localhost:3847`.

```bash
podcli
podcli ui
```

`podcli uninstall` removes all managed data by default. Run it with `--dry-run`
first to preview exactly what will be removed.

```bash
podcli uninstall --dry-run
```
