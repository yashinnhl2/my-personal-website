# my-personal-website

Yasin Farmani's personal site and blog — built with [Astro](https://astro.build), plain CSS, and a canvas starfield background. No UI framework, no animation library.

Live structure: a single-page bento-grid portfolio (`/`) plus a Markdown-powered blog (`/blog`).

## Project structure

```text
/
├── public/
│   ├── favicon.svg / favicon.ico
│   └── Yasin-Farmani-Resume.pdf   # served as a static file, linked from the Contact section
├── src/
│   ├── components/                # one .astro file per section/widget, styles scoped inline
│   ├── content/
│   │   └── blog/                  # blog posts, one Markdown file per post
│   ├── content.config.ts          # the `blog` content collection schema
│   ├── data/
│   │   └── profile.ts             # all site copy: name, roles, experience, skills, links
│   ├── layouts/
│   │   ├── Layout.astro           # shared <head>, global styles, the contact modal
│   │   └── BlogLayout.astro       # nav + starfield + footer wrapper for /blog pages
│   ├── pages/
│   │   ├── index.astro            # assembles the home page from the components
│   │   └── blog/
│   │       ├── index.astro        # post list
│   │       └── [...slug].astro    # single post page
│   ├── styles/global.css          # design tokens (colors, fonts, easing), reset, bento grid
│   └── utils/blog.ts              # getPosts(), formatDate(), readingTime()
└── astro.config.mjs
```

## Development

```sh
npm install
npm run dev          # http://localhost:4321
```

When starting the dev server from an agent/CI context, prefer background mode:

```sh
astro dev --background
```

Manage it with `astro dev stop`, `astro dev status`, and `astro dev logs`.

| Command | Action |
| --- | --- |
| `npm run dev` | Start the local dev server |
| `npm run build` | Build the production site to `./dist/` |
| `npm run preview` | Preview the production build locally |
| `npm run astro ...` | Run any Astro CLI command (e.g. `astro check`) |

## Writing a new post

Add a Markdown file to `src/content/blog/`:

```md
---
title: 'My post'
description: 'One line that appears on the card.'
date: 2026-10-01
tags: ['frontend']
---

Post body in Markdown.
```

It shows up automatically on `/blog`, sorted newest first (`getPosts()` in [`src/utils/blog.ts`](src/utils/blog.ts)). Set `draft: true` in the frontmatter to keep a post out of production builds while you work on it — drafts still render in `npm run dev`.

## Editing site content

Almost everything on the home page — name, roles, experience, education, skills, links — lives in [`src/data/profile.ts`](src/data/profile.ts). Change it there rather than in the components.

## Contact form

The "Contact me" button opens a modal (`src/components/ContactModal.astro`) that POSTs to a form backend. Set `PUBLIC_CONTACT_ENDPOINT` in `.env` (see `.env.example`) to a service like Formspree or Web3Forms. Without it, submitting falls back to opening the visitor's email client with the message prefilled.

## Documentation

- [Astro docs](https://docs.astro.build)
- [Content collections](https://docs.astro.build/en/guides/content-collections/)
- [Astro components](https://docs.astro.build/en/basics/astro-components/)
