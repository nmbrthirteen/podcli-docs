# podcli docs

The documentation content for [podcli](https://github.com/nmbrthirteen/podcli),
the open-source AI podcast clipper. These Markdown files are rendered at
[podcli.com/docs](https://podcli.com/docs).

## Editing

Each page is a single Markdown file with frontmatter:

```markdown
---
title: Getting started
description: One-line summary used for the page metadata.
group: Start
order: 1
---

Page content in Markdown.
```

- `title`: page heading and nav label.
- `description`: shown under the title and in page metadata.
- `group`: sidebar section (`Start`, `Guides`, ...).
- `order`: sort order within the sidebar.
- `index.md` renders at `/docs`; every other file renders at `/docs/<filename>`.

Images use standard Markdown (`![alt](/docs/name.png)`) and render as framed,
click-to-zoom screenshots. Fenced code blocks are click-to-copy, so keep them to
the runnable command with no inline comments.

## Contributing

Spot something wrong or out of date? Edit the file and open a pull request. The
site rebuilds from this repo.
