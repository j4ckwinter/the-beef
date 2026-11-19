---
status: found
found: 2026-11-18
title: issue ratio
pitch: A small browser extension that shows open against total on a GitHub repo's Issues and Pull requests tabs, like 2/231, so a low open count reads as well looked-after rather than ignored.
demo: Open a busy repo and a tiny one on GitHub, watch the Issues tab change from a bare open count to open/total (for example 2/231) with a small closed-share bar, hover it for the exact open and closed numbers, then click through to the closed list.
sources:
  - https://x.com/tanujnotes/status/2122671016145207600 # posted 2026-11-17
---

Tanuj's post above wishes GitHub showed open and closed issue counts side by side, because the open number on its own makes a repo look either dead or buggy. I judge repos by that tab all the time, so I'd use this every day.

Scope for a day: a Manifest V3 extension in TypeScript and Vite for Chrome and Firefox. A content script finds the repo tab counters on `github.com/<owner>/<repo>` pages and rewrites them as open/total, with a tooltip giving the exact numbers. The closed counts come from GitHub's public search API (`total_count` of `repo:<owner>/<repo> is:issue is:closed`, and `is:pr is:closed`) with no token. Results are cached per repo for an hour in extension storage, so the 10-requests-a-minute unauthenticated limit never shows up while browsing. It keeps working through GitHub's client-side navigation and leaves the page alone if a request fails. Tests cover the counter parsing against saved page fixtures, and the formatting.

Checked on 18 November 2026: Refined GitHub's feature list has nothing like it. The npm registry has no `issue-ratio` package and nothing similar. GitHub and web searches turned up only small or dormant tools (Github-Insights-Extension, gitsnap, Repo Reality Check, and the `gh issue-stats` CLI extension). They put stats in a popup, a separate score or the terminal, not on the tab counters you see when you land on a repo.
