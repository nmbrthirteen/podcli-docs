---
title: CLI reference
description: Drive the whole Podcli pipeline from your terminal. One command transcribes, picks moments, crops to the speaker, and burns captions in.
group: Guides
order: 3
---

Everything the [studio](https://podcli.com/docs/the-studio) does is available from the terminal.
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
| `--caption-style <style>` | `branded`, `hormozi`, `karaoke`, or `subtle`. See [captions and formats](https://podcli.com/docs/captions-and-formats). |
| `--crop <mode>` | `center`, `face`, or `speaker`. |
| `--format <ratio>` | `vertical` (9:16), `horizontal` (16:9), or `square` (1:1). |
| `--logo <asset or file>` | Overlay a logo on every clip. Accepts a registered asset name or a path. |
| `--intro <asset or file>` | Prepend an intro video before every clip. |
| `--outro <asset or file>` | Append an outro video after every clip. |
| `--thumbnails` / `--no-thumbnails` | Force thumbnail generation on or off. |

Logo, intro, and outro all accept a **registered asset name** (see [Assets](#assets))
or a direct file path. Leave them off to use whatever you've marked as the
default asset.

## Presets

Save a set of render settings once and reuse it:

```bash
podcli presets save my-show
podcli process episode.mp4 --preset my-show
```

## Assets

Register logos, outros, intros, and music once, then reference them by name
anywhere. The same library backs the [studio Assets page](https://podcli.com/docs/the-studio#assets)
and the `manage_assets` [MCP tool](https://podcli.com/docs/mcp-server).

```bash
podcli assets add my-logo ~/branding/logo.png       # register a file by name
podcli assets add-url outro https://example.com/outro.mp4   # download and register
podcli assets default my-logo                        # make it the default logo
podcli assets list                                   # show everything, defaults marked
podcli assets export my-logo ~/Desktop/logo.png      # copy a registered asset out
```

Then use a name instead of a path:

```bash
podcli process episode.mp4 --logo my-logo --intro show-intro --outro outro
```

Other actions: `podcli assets rename <old> <new>`, `podcli assets undefault
<name>`, and `podcli assets remove <name>`.

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
