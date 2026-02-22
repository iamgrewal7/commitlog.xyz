# commitlog.xyz

A technical blog inspired by git commit logs. Each post is styled as a commit with hashes, branches, and tags.

## Features

- **Terminal-style UI** - Monospace fonts, green prompts, dark theme
- **Git commit metadata** - Every post has a hash, author, date, and branch
- **Git graph visualization** - Visual timeline connecting posts
- **Branch navigation** - Browse by category (main, frontend, backend, devops)
- **Tag filtering** - Find posts by topic
- **Syntax highlighting** - Code blocks with Shiki
- **Search** - Press `/` to search (Pagefind)
- **RSS feed** - Subscribe at `/rss.xml`
- **Dark mode** - Optimized for dark theme

## Tech Stack

| Layer | Technology |
|-------|------------|
| Framework | [Astro](https://astro.build) 5.x |
| Content | [MDX](https://mdxjs.com) |
| Styling | [Tailwind CSS](https://tailwindcss.com) 4.x |
| Syntax Highlighting | [Shiki](https://shiki.style) |
| Search | [Pagefind](https://pagefind.app) |
| Deployment | [Vercel](https://vercel.com) |

## Project Structure

```
commitlog.xyz/
├── src/
│   ├── components/
│   │   ├── blog/         # CommitCard, GitGraph, PostMetadata, BranchNav
│   │   ├── layout/       # Header, Footer
│   │   ├── search/       # SearchBar
│   │   └── ui/           # TerminalWindow, CommandPrompt, CodeBlock
│   ├── content/
│   │   └── blog/         # MDX blog posts
│   │   └── config.ts     # Content collection schema
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── pages/
│   │   ├── index.astro        # Homepage
│   │   ├── about.astro        # About page
│   │   ├── branches.astro     # Branch listing
│   │   ├── tags.astro         # Tag listing
│   │   ├── rss.xml.ts         # RSS feed
│   │   └── blog/
│   │       ├── index.astro    # All posts
│   │       └── [slug].astro   # Individual post
│   └── styles/
│       └── global.css    # Tailwind + custom styles
├── public/
│   └── favicon.svg
├── astro.config.mjs
├── tailwind.config.mjs
└── package.json
```

## Commands

| Command | Action |
|:--------|:-------|
| `npm install` | Install dependencies |
| `npm run dev` | Start dev server at `localhost:4321` |
| `npm run build` | Build production site to `./dist/` |
| `npm run preview` | Preview build locally |

## Writing Posts

Create a new `.mdx` file in `src/content/blog/`:

```mdx
---
title: "Your Post Title"
description: "A brief description for SEO and previews"
date: 2026-02-22
branch: "frontend"        # main | frontend | backend | devops
tags: ["react", "typescript"]
hash: "abc123d"           # Optional: custom commit hash
readingTime: 8            # Optional: reading time in minutes
draft: false              # Set true to hide from listings
---

## Your Content Here

Write your post using MDX...
```

### Frontmatter Fields

| Field | Required | Description |
|-------|----------|-------------|
| `title` | Yes | Post title |
| `description` | Yes | Brief description (SEO, previews) |
| `date` | Yes | Publication date |
| `branch` | No | Category: `main`, `frontend`, `backend`, `devops` |
| `tags` | No | Array of tags |
| `hash` | No | Custom commit hash (auto-generated if omitted) |
| `readingTime` | No | Estimated reading time in minutes |
| `draft` | No | Hide from listings when `true` |

## Deployment

### Vercel (Recommended)

```bash
npx vercel
```

Or connect your GitHub repo to Vercel for automatic deployments.

### Other Platforms

The site is static HTML after build. Deploy the `dist/` folder to:
- Netlify
- GitHub Pages
- Cloudflare Pages
- Any static hosting

## Customization

### Colors

Edit the theme in `src/styles/global.css`:

```css
@theme {
  --color-bg-primary: #0d1117;
  --color-bg-secondary: #161b22;
  --color-accent-green: #3fb950;
  --color-accent-blue: #58a6ff;
  /* ... */
}
```

### Branches

Modify branch colors in:
- `src/components/blog/GitGraph.astro`
- `src/pages/branches.astro`
- `src/pages/index.astro`

### Fonts

Fonts are loaded from Google Fonts. Change in `src/layouts/BaseLayout.astro`:
- JetBrains Mono (monospace)
- Inter (sans-serif)

## Analytics

Add Umami or any analytics script to `src/layouts/BaseLayout.astro` in the `<head>` section.

## License

MIT
