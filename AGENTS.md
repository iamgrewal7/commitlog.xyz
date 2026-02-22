# AGENTS.md

Guidelines for AI coding agents working on commitlog.xyz - an Astro-based technical blog with a git commit log theme.

## Commands

```bash
npm run dev          # Start dev server at localhost:4321
npm run build        # Production build to ./dist/
npm run preview      # Preview production build locally
npm run astro check  # Type-check the project
```

No test suite configured. If added, use Vitest: `npm run test` for all, `npm run test -- path/to/test.spec.ts` for single files.

## Project Structure

```
src/
├── components/      # blog/, layout/, search/, ui/
├── content/blog/    # MDX posts + config.ts (schema)
├── layouts/         # BaseLayout.astro
├── pages/           # Static and dynamic routes
└── styles/          # global.css (Tailwind + theme)
```

## Code Style

### Astro Components

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
import type { CollectionEntry } from 'astro:content';

interface Props {
  post: CollectionEntry<'blog'>;
}

const { post } = Astro.props;
---

<div class="flex items-center gap-4 p-6 text-text-primary bg-bg-secondary rounded-lg">
  <!-- content -->
</div>
```

- Use TypeScript with explicit types
- Define `Props` interface at top of frontmatter
- Destructure props immediately
- Use semantic HTML (article, nav, section, main)
- Use Tailwind classes exclusively - no inline styles

### Import Order

1. Astro/framework imports
2. Third-party packages
3. Local components (relative paths)
4. Content collections
5. Types (`import type`)

### TypeScript

- Use `interface` for Props, `type` for object shapes
- Avoid `any`; use `unknown` when uncertain
- Use const assertions for readonly objects

```typescript
const branchColors = {
  main: 'text-accent-green',
  backend: 'text-accent-purple',
} as const;
```

### Tailwind CSS

- Use theme colors: `text-text-primary`, `bg-bg-secondary`, `text-accent-green`
- Never use hex values directly in templates
- Group classes: layout → spacing → typography → colors → effects

### MDX Posts

```yaml
---
title: string           # Required
description: string     # Required (max 160 chars)
date: YYYY-MM-DD        # Required
branch: main | frontend | backend | devops
tags: string[]
hash: string            # Optional commit hash
readingTime: number     # Optional minutes
draft: boolean          # Hide from listings
---
```

- Use `##` for sections, `###` for subsections
- Always specify language for code blocks

### Dynamic Routes

```typescript
export async function getStaticPaths() {
  const posts = await getCollection('blog');
  return posts.map((post) => ({
    params: { slug: post.id },
    props: post,
  }));
}

const post = Astro.props;
```

### Error Handling

```typescript
const posts = (await getCollection('blog'))
  .filter((post) => !post.data.draft)
  .sort((a, b) => b.data.date.valueOf() - a.data.date.valueOf());
```

## Naming Conventions

- Components: PascalCase (`CommitCard.astro`)
- Pages: lowercase (`[branch].astro`)
- Props interface: `Props`
- Variables: camelCase
- CSS: kebab-case via Tailwind utilities

## Theme Colors

| Variable | Hex | Usage |
|----------|-----|-------|
| `bg-primary` | `#0d1117` | Main background |
| `bg-secondary` | `#161b22` | Cards, terminals |
| `bg-tertiary` | `#21262d` | Hover, inputs |
| `text-primary` | `#c9d1d9` | Main text |
| `text-secondary` | `#8b949e` | Muted text |
| `accent-green` | `#3fb950` | Primary accent |
| `accent-blue` | `#58a6ff` | Links |
| `accent-yellow` | `#d29922` | Commit hashes |
| `accent-purple` | `#a371f7` | Backend branch |
| `accent-cyan` | `#39c5cf` | DevOps branch |
| `border` | `#30363d` | Dividers |

## Deployment

Static HTML output in `dist/`. Deploy to Vercel, Netlify, or any static host.
