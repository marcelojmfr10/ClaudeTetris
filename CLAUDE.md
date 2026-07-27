# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Vanilla JavaScript Tetris. No build step, no package manager, no external dependencies — all logic lives in four files: `index.html`, `style.css`, `game.js`, `README.md`.

## Running Locally

Open `index.html` directly in a browser, or serve it:

```bash
python3 -m http.server 8000
# or
npx serve .
```

## Code Style

- `'use strict'` is enabled at the top of `game.js` — keep it.
- ES6+: `const`/`let`, arrow functions, spread, `Array.from()`. No `var`.
- No linter or formatter configured.

## Game Constants (top of game.js)

| Constant | Purpose |
|---|---|
| `COLS`, `ROWS` | Board dimensions in cells |
| `BLOCK` | Pixel size per cell |
| `COLORS` | Hex colors for the 7 piece types |
| `LINE_SCORES` | Points awarded for 1–4 simultaneous line clears |
| `dropInterval` | Initial fall speed in ms (1000) |

## Canvas Scaling Gotcha

If you change `COLS`, `ROWS`, or `BLOCK` in `game.js`, you **must** also update the canvas `width`/`height` attributes in `index.html` to match:

- `#board` → `width = COLS × BLOCK`, `height = ROWS × BLOCK`
- `#next-canvas` → independent 120×120 px preview canvas

The game does not auto-scale — mismatched values cause rendering artifacts.
