---
status: picked
found: 2026-11-23
title: eyeline
pitch: A browser overlay and CLI that finds icons sitting inside buttons, chips and avatars on a live page, measures where their visual weight really sits, and flags the ones that look off-centre even though the CSS says they are centred, with the exact nudge to fix each one.
demo: Open a demo app's toolbar of 40px icon buttons where the play, send and chevron icons look low or shifted; turn on the eyeline overlay and watch each icon get a crosshair for its box centre and a dot for its visual centre, with the worst ones outlined; click one to see "nudge 1px up, 1px right" and apply it live; then run `npx eyeline http://localhost:5173` in a terminal, get the same list with selectors, and write a CSS patch that clears it.
sources:
  - https://x.com/typedbynikolas/status/2124313824287162738  # posted 2026-11-22
  - https://x.com/typedbynikolas/status/2124469172851921308  # posted 2026-11-22
---

Nikolas's posts above describe a fix he keeps having to remind Cursor about: a 16px icon in a 40px button that is mathematically centred still looks low, so he nudges it a pixel or two toward the heavier side by hand, one icon at a time. Agents and CSS both centre the bounding box, and the eye centres the visual mass, so every agent-built UI ships a few of these. Nothing tells you which ones, in context, on the page you actually render.

## Scope for about a week

1. **Measuring engine.** A TypeScript library that rasterises an element (inline SVG, icon font glyph, img or mask-image) at device pixel ratio, weights pixels by alpha and luminance against the container's background, and returns the visual centre, the box centre and the offset in CSS px. Fixture tests with known shapes (triangle, play, heart, chevron, circle).
2. **Detection.** Walk the DOM for small graphic elements inside fixed-size interactive containers (buttons, icon buttons, chips, avatars, badges), skip text-only ones, and score each offset against a threshold relative to the container size.
3. **Browser overlay.** A Manifest V3 extension (Vite, React) that draws the crosshair and visual-centre dot over every flagged icon, a side panel listing them by severity, and a click-to-preview that applies a translate nudge live.
4. **CLI.** `npx eyeline <url>` with Playwright: crawl given routes and viewports, print a table of selector, offset and suggested nudge, exit non-zero above a threshold for CI, and write JSON plus an HTML report with before/after crops.
5. **Fix output.** Emit a CSS patch of per-selector `translate` nudges, and a hint for the source SVG when every use of the same icon is off by the same amount, so the fix goes into the asset once.
6. **Demo app, README and recording.** A small React toolbar seeded with off-centre icons, the GIF, and docs.

## Fit

Squarely in Jack's frontend lane: rendering, pixels, React, a browser extension and a Node CLI, and it is the kind of design-engineering detail that reads well to other frontend people. It needs no paid API, key or sign-up.

## Already-built check

Checked the web, npm and GitHub on 23 Nov 2026. optical-center (npm and opticalcenter.dev) shifts SVG viewBoxes at build time, but it works on source SVGs, not on what a page actually renders, and it is small (about 2 GitHub stars, 84 npm downloads in the last month). IconAlign (iconalign.com) measures one uploaded icon at a time. Snake Eyes and UI Inspect check gaps, padding and edge alignment, not optical balance. None audits a live page's icons in their containers or emits per-selector fixes. The npm name `eyeline` is free.
