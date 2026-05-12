# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

Single-page personal portfolio site for Ankit Mansinghani. The entire site is one file: `index.html`. There is no build system, bundler, framework, or package manager — changes take effect immediately.

## Pushing changes

The `origin` remote points to a local proxy that blocks writes. To push, temporarily swap the origin URL to GitHub using the stored PAT, push, then restore:

```bash
git remote set-url origin https://ankitmansinghani:<PAT>@github.com/ankitmansinghani/ankitmansinghani.github.io.git
git push -u origin <branch>
git remote set-url origin http://local_proxy@127.0.0.1:43991/git/ankitmansinghani/ankitmansinghani.github.io
```

Alternatively push to the `github` remote directly:

```bash
git push -u github <branch>
```

## Architecture

Everything lives in `index.html`:

- **CSS custom properties** (`--bg`, `--surface`, `--cyan`, `--heading`, etc.) drive all colours. Dark mode is the default (`:root`); light mode is `html[data-theme="light"]`. Never hardcode colour values — always use a variable.
- **Sections**: hero → about/stats → skills → experience → certifications → contact → footer. Each section has a `section-label` (terminal-style prompt) and a `section-title`.
- **JavaScript** at the bottom of `<body>` handles three things: typewriter animation, scroll-based fade-in via `IntersectionObserver`, and the light/dark theme toggle (reads/writes `localStorage`, falls back to `prefers-color-scheme`).
- **Fonts**: JetBrains Mono (monospace accents), Syne (headings), DM Sans (body) — all from Google Fonts.
