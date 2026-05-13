# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A single-file Pomodoro timer web app: `pomodoro.html`. No build step, no dependencies to install, no test suite. Open directly in a browser to run it.

## Fonts

The UI uses two Google Fonts loaded from CDN:
- **Orbitron** (700, 900) — timer digits and the main "POMODORO" title
- **Press Start 2P** — all other labels, buttons, and small text

## Architecture

Everything lives in `pomodoro.html` as three sections:

- **CSS** — neon glow achieved via layered `text-shadow` / `box-shadow`. Mode state (work vs. break) is toggled by adding/removing the `brk` class on `.timer-box`, `.digits`, and `.prog-fill`. Running state is the `running` class on `.digits`; paused state is the `paused` class.
- **Background layers** — three stacked `position: fixed` divs: `.grid-floor` (CSS perspective grid), `.scanlines` (repeating-linear-gradient overlay), `.vignette` (radial-gradient).
- **JS** — plain vanilla, no framework. Key globals: `mode`, `running`, `timeLeft`, `total`, `sessions`, `tid` (interval ID), `audioCtx`. `switchMode(m)` is the single source of truth for resetting UI state when changing modes. The Web Audio `AudioContext` is intentionally created on the first `start()` call (user gesture) to satisfy browser autoplay policy.
