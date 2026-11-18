---
status: found
found: 2026-11-18
title: qr-svg
pitch: A one-page web app that turns any text or link into a QR code and downloads it as a clean SVG, with no account and nothing sent to a server.
demo: Paste a URL, watch the QR preview update while changing colour and margin, click download, open the SVG and zoom in to show it stays sharp, then scan it with a phone.
sources:
  - https://x.com/Wrenderiing/status/2122373073349271778 # posted 2026-11-16
---

The poster was furious that a big design vendor's free QR generator dropped SVG export. This is a small React and Vite page that generates the code in the browser with an MIT-licensed QR library and offers SVG and PNG downloads. It works offline once loaded.

Scope for a day: one screen, a few options (colours, margin, error-correction level), a test that the downloaded SVG decodes back to the input.
