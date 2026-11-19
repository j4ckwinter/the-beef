---
status: found
found: 2026-11-19
title: headless.fyi
pitch: A public, nightly scoreboard of the browser engines AI agents use (Kitesurf, Lightpanda, Obscura, agent-browser, Chromium), run against real sites and common tasks, so anyone can see which engine renders, extracts and gets let in, and how that changes release by release.
demo: Open headless.fyi, see one site rendered side by side by four engines with a score under each, switch to the leaderboard and sort by task success, then open an engine's release diff and watch a handful of sites flip from failing to passing.
sources:
  - https://blog.cloudflare.com/kitesurf-open-source/ # published 2026-11-13
  - https://www.helpnetsecurity.com/?p=391308 # published 2026-11
  - https://lightpanda.io/blog/posts/benchmarking-lightpanda-for-agents # date not shown
  - https://jacar.es/en/lightpanda-vs-obscura-headless-browser-benchmark/ # date not shown
---

Cloudflare open-sourced Kitesurf, an experimental agent browser, on 13 November, joining Lightpanda, Obscura and Vercel's agent-browser. Each is lighter than Chromium and breaks on some real sites, but every comparison so far is a one-off, mostly run by the vendors, and Lightpanda's own post asks how it should even be benchmarked. Nobody keeps a neutral, regularly updated record, the way caniuse does for browser features.

Each night, run a few hundred top sites and a fixed set of tasks (find the price, fill the form, read the article) through every engine. Score whether the page rendered, whether the right content came out, whether its accessibility tree was usable, and whether the site blocked the engine. Publish the method and the raw results next to the scores, since the scoring will be argued over. Running real sites every night costs money, and an engine vendor could build its own board, so neutrality and being first are the defence.

The demand evidence is the launch itself and the vendor-run benchmarks. Only the Kitesurf release is dated this month.
