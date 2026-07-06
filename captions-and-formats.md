---
title: Captions and formats
description: Podcli ships four caption styles and three aspect ratios. Captions scale to each canvas instead of floating mid-frame.
group: Guides
order: 4
---

Every clip is captioned and cropped to a target aspect ratio. Pick these in the
[studio](/docs/the-studio) (New episode → Settings), with [CLI flags](/docs/cli),
or via the `create_clip` [MCP tool](/docs/mcp-server).

## Caption styles

| Style | Look |
| --- | --- |
| `branded` | Clean white text with the active word in a dark chip. |
| `hormozi` | Bold text with the active word punched in yellow. |
| `karaoke` | Word-by-word fill as the line is spoken. |
| `subtle` | Understated text for a calmer, editorial look. |

Set it with `--caption-style`:

```bash
podcli process episode.mp4 --caption-style hormozi
```

## Formats

| Format | Where it goes |
| --- | --- |
| Vertical 9:16 | TikTok, Reels, and Shorts. The default. |
| Horizontal 16:9 | YouTube and landscape players. |
| Square 1:1 | Feed posts. |

Captions scale to each canvas, so text stays anchored instead of floating
mid-frame. Set the format with `--format`:

```bash
podcli process episode.mp4 --format square
```

## Cropping

Podcli frames the clip on whoever is talking.

- `center`: a fixed center crop.
- `face`: face-tracking crop with an exponential-smoothing camera.
- `speaker`: mouth-motion speaker tracking for split-screen and
  Riverside-style layouts, with a scene-cut guard against jittery pans.

```bash
podcli process episode.mp4 --crop speaker
```
