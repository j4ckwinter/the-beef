---
status: found
found: 2026-11-18
title: stableport
pitch: A tiny Node CLI that gives every project its own stable, free local port worked out from the project's name, so dev servers stop fighting over 3000, 8000 and 8080.
demo: Two sample apps both default to port 3000 and the second one crashes; then each is started through stableport, gets its own fixed port (the same one on every run), and `stableport ls` shows which project holds which port.
sources:
  - https://x.com/Biggest/status/2121634128219230228 # posted 2026-11-14
---

Someone complained that every local project grabs the same three ports and they keep having to work around clashes. stableport hashes the project folder name into a high port range, checks it is free (walking forward if not), and runs the dev command with `PORT` set. A `ls` command lists the common dev ports and which process or project holds each one.

Scope for a day: TypeScript CLI, no dependencies beyond Node's `net` module and a small arg parser, a `.stableport` file to pin an override, tests for the hashing and the free-port check. Nothing leaves the machine.
