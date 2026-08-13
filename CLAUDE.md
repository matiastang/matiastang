# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Language

Always respond in **Simplified Chinese （简体中文）** by default.

## What this repository is

This is a **GitHub profile README repository** (`matiastang/matiastang`). There is no application code, build system, or test suite. The rendered `README.md` at the root is the profile page shown on github.com/matiastang.

## Structure and how the pieces connect

- `README.md` — the profile content (**English**, the default GitHub renders). Mostly badges (shields.io), skill icons (skillicons.dev), and an embedded "snake" contribution animation.
- `README.zh-CN.md` — the **Simplified Chinese** version. Both files have a language-switch link at the top (`English | 简体中文`). **When editing profile content, keep both files in sync** — same structure, same badges/icons/snake block, only the prose language differs.
- `.github/workflows/github-snake.yml` — generates the snake animation SVGs referenced by the README.

### The snake animation pipeline (the only non-obvious part)

1. The workflow uses `Platane/snk@v3` to generate SVGs (`github-snake.svg`, `github-snake-dark.svg`, `ocean.gif`) into `dist/`.
2. It then pushes `dist/` to the **`output` branch** (not `main`) via `crazy-max/ghaction-github-pages`.
3. The README's `<picture>` element hot-links to those files on the `output` branch with dark/light `prefers-color-scheme` variants.

**Consequence:** if you change the generated filenames or palettes in the workflow, you must update the matching `srcset` URLs in `README.md` (and vice versa), or the images break.

The workflow runs on a daily cron (03:00 UTC), on push to `main`, and manually via `workflow_dispatch`. It requires the `MT_TOKEN` secret (a PAT, since it must push to the `output` branch) — it does not use the default `GITHUB_TOKEN`.

## Editing conventions

- `README.md` uses an HTML comment header with `@Author`/`@LastEditors`/`@LastEditTime` fields (maintained by the vscode-koroFileHeader extension). Update `@LastEditTime` when editing the file.
- Skill icons come from skillicons.dev, grouped by category with `perline=10`; keep additions within their category row.
