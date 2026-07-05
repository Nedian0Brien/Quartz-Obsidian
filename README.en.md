<div align="center">

# Quartz-Obsidian

**A Quartz v4 repository for publishing an Obsidian knowledge base as a static site**

![Quartz v4](https://img.shields.io/badge/Quartz_v4-10B981?style=flat-square) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![Node 22+](https://img.shields.io/badge/Node_22+-339933?style=flat-square&logo=nodedotjs&logoColor=white) ![Markdown](https://img.shields.io/badge/Markdown-000000?style=flat-square&logo=markdown&logoColor=white)

[한국어](./README.md)

</div>

---

## Overview

This repository uses Quartz v4 to publish an Obsidian/Markdown knowledge base as a static website. The previous README was mostly upstream text, while the actual `content/` tree contains notes on Programming, DevOps, Mathematics, AI, Computer Science, Data Engineering, and LawDigest.

Quartz configuration lives in `quartz.config.ts` and enables Obsidian flavored markdown, GFM, Table of Contents, KaTeX, content index, RSS/sitemap, and custom OG images.

## Highlights

| Area | Description |
|---|---|
| Digital garden publishing | Builds Markdown content under `content/` into a Quartz static site. |
| Obsidian-compatible Markdown | Uses Obsidian flavored markdown and shortest link resolution. |
| Search and indexes | Enables ContentIndex, sitemap, and RSS output. |
| Math and code support | Uses KaTeX and syntax highlighting plugins. |
| Knowledge domains | Includes notes across Programming, AI, Computer Science, Data Engineering, and LawDigest. |

## Repository Structure

| Path | Role |
|---|---|
| content/ | Published Markdown knowledge base |
| quartz.config.ts | Quartz site configuration |
| quartz.layout.ts | Quartz layout configuration |
| quartz/ | Quartz CLI and framework source |
| package.json | Node scripts and dependencies |

## Quick Start

### Install dependencies

```bash
npm install
```

### Run Quartz build

```bash
npx quartz build
```

### Serve local preview

```bash
npx quartz build --serve
```

### Type/format check

```bash
npm run check
```

## Verification

| Check | Command |
|---|---|
| Quartz check | `npm run check` |
| Build site | `npx quartz build` |

## Operational Notes

- Requires Node.js 22+ and npm 10.9.2+.
- `content/private`, `content/templates`, and `.obsidian` are ignored by Quartz.
- Update site title, baseUrl, and locale to match the real deployment target before publishing.

## Documentation Sources

This README was written from the following files and documents in this repository.

- `README.md`
- `package.json`
- `quartz.config.ts`
- `content/`
