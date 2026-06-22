# Slides — Build a team agent in Claude Code

A self-contained [reveal.js](https://revealjs.com) deck you talk through. 22 slides:
intro (you + Stacklist) → why agents exist → the fast evolution (loop → workflows →
dynamic → platform) → what we'll build → the phased build → close.

## Fill in the [bracketed] bits first

A few slides have `[your ... ]` placeholders (your name/bio, the Stacklist pitch,
your handle). Search `index.html` for `fill` / `[` and replace them. Everything
else is ready.

## Present it

```bash
open slides/index.html
# or serve it:  cd slides && python3 -m http.server 8000  → http://localhost:8000
```

- **→ / Space** next · **←** back · **Esc** overview · **F** fullscreen
- **S** — speaker view: the talk-through notes (`Say:` / `Do:`) + timer + next-slide
  preview. Keep it on your laptop; mirror the main window to the projector.

## PDF backup (offline)

Open `slides/index.html?print-pdf` in Chrome → Print → Save as PDF → Margins
**None**, Background graphics **on**. Keep it on a USB stick in case the venue
Wi-Fi dies.

## Fully offline (no CDN)

```bash
cd slides && npm init -y && npm install reveal.js@5.1.0 highlight.js@11.9.0
```
Then repoint the three CDN `<link>`/`<script>` URLs at `node_modules/...`. (Or just
rely on the PDF.)

## Re-skin

The theme is the `<style>` block at the top of `index.html` — change `--accent`,
`--bg`, `--ink` to recolor the whole deck. Slides are plain `<section>`s; code
slides use `<pre><code class="language-...">`.
