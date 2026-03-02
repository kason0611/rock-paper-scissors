# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A zero-dependency, single-file browser game. Open `index.html` directly in any browser — no build step, no server needed.

## Architecture

Everything lives in `index.html` as a self-contained file with three sections:

- **`<style>`** — All CSS, using CSS custom animations (`pop`, `shake`) and utility classes (`.win`, `.lose`, `.tie`) applied dynamically by JS.
- **`<body>`** — Static HTML structure: scoreboard → arena (player vs computer display) → result message → choice buttons → reset button.
- **`<script>`** — Vanilla JS game logic at the bottom of the file.

## Game Logic (`<script>`)

| Constant | Purpose |
|---|---|
| `CHOICES` | Array of valid move keys: `['rock', 'scissors', 'paper']` |
| `EMOJI` / `NAME` | Maps move key → display emoji / Chinese label |
| `BEATS` | Maps move key → the key it defeats |

Core functions:
- `play(playerChoice)` — Entry point called by button `onclick`. Picks a random CPU move, determines outcome via `BEATS`, updates DOM and scores.
- `setDisplay(id, emoji)` — Updates a choice display circle and re-triggers the `pop` CSS animation via reflow trick (`void el.offsetWidth`).
- `updateScoreboard()` / `resetScore()` — Score state management.

Score state is held in the module-level `scores` object `{ player, tie, computer }` and resets on page reload or `resetScore()`.

## Deployment

Hosted on GitHub Pages. To enable: go to repo **Settings → Pages → Source → Deploy from branch → master / root**.
