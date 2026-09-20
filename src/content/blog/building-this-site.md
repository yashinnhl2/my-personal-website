---
title: 'Building this site with Astro and zero animation libraries'
description: 'The starfield, the scroll reveals and the bento cards, all done with plain CSS and a few small scripts.'
date: 2026-09-19
tags: ['astro', 'css', 'animation']
---

I wanted this site to feel alive without shipping a heavy animation library. Astro plus plain CSS turned out to be enough.

## The starfield

The background is a single `<canvas>` redrawn with `requestAnimationFrame`. Each star gets its own twinkle phase and a depth value, and depth drives the parallax on scroll and pointer movement.

```ts
const twinkle = 0.35 + 0.65 * (0.5 + 0.5 * Math.sin((t / 1000) * star.speed + star.phase));
ctx.globalAlpha = twinkle * (0.35 + star.depth * 0.65);
```

## Reveal on scroll

Elements with a `.reveal` class start hidden. An `IntersectionObserver` adds `.in` when they enter the viewport, and CSS handles the rest. The hidden state only applies when JavaScript is running, so the page still works without it.

## The cursor glow

Every card tracks the pointer with two CSS variables, `--mx` and `--my`, and a `radial-gradient` follows them. It is a few lines of JavaScript and one pseudo-element.

## Respecting reduced motion

One `prefers-reduced-motion` block turns the movement off for people who ask for it. It is the cheapest accessibility win in the whole project.
