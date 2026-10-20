# Repository Guidelines

## Project Structure & Module Organization

- `SKILL.md` defines slide-generation instructions, typography, composition, and delivery checks.
- `CFFEX-starter.html` contains the reusable HTML, CSS, and JavaScript template. Change this source when updating defaults; editing generated examples alone does not update the template.
- `assets/brand/` holds reusable CFFEX PNG artwork.
- `output/` contains generated decks, their assets, PDFs, and review images.
- The parent checkout provides `../scripts/`, `../references/`, and the Node.js review runtime. This directory has no dedicated unit-test suite.

## Build, Test, and Development Commands

Open the starter or a generated HTML file directly in a browser; no build step is required. Prefix shell commands with `rtk`. From this directory, with the parent checkout available:

`rtk proxy npm --prefix .. ci` installs review dependencies; Node.js 20+ is required.

`rtk proxy npm --prefix .. run setup:render` installs Chromium for Playwright.

`rtk proxy node ../scripts/validate-deck.mjs CFFEX-starter.html --allow-placeholders` checks template structure, registered layouts, and image references.

`rtk proxy node ../scripts/review-deck.mjs output/clear-work/index.html /tmp/cffex-review` validates a finished deck and renders numbered contact sheets, four slides per sheet by default. Use `--batch-size=2` for dense pages and `--overview` for an optional deck overview. Omit placeholder allowances for finished decks.

## Coding Style & Naming Conventions

Follow existing indentation: two spaces in CSS and nested JavaScript blocks; match surrounding HTML indentation. Use descriptive kebab-case CSS classes and existing color variables. No formatter or linter is configured.

Preserve the 1600 × 900 canvas, fixed brand geometry, and registered `data-layout` values. Content pages retain `.template-body.layout-centered` with a direct `.layout-composition` child. Keep template dimensions and `SKILL.md` guidance consistent; allow content-driven composition within those boundaries.

## Confirmed Visual Direction

This project serves a central state-owned enterprise presentation context. Use a composed, substantial visual style. Carry forward the confirmed preferences in [央企演示的视觉分量](references/visual-composition.md#央企演示的视觉分量), especially plain or light central labels and clearly weighted blue connectors. Blue remains dominant; use brand gold sparingly on a few key phrases or local structural details. Treat these as the default for subsequent design work in this repository.

For scene and case-study pages, carry forward [已确认案例的构图经验](references/visual-composition.md#已确认案例的构图经验), drawn from the approved Feishu deck's original pages 4–7 (now pages 5 and 8–10). Use their content relationships and visual finish as a reference; choose compositions to suit each new case.

## Testing Guidelines

Run structural validation after skill, script, or template changes. Render on the 1600 × 900 canvas and inspect every page through grouped contact sheets, normally four pages per sheet; use two for dense pages. Inspect individual pages or crops only when a sheet reveals a problem or lacks readable detail. Do not retain individual PNGs or open every page separately by default. After a fix, inspect affected groups again. Keep full-deck automatic checks and actual-font, overflow, spacing, narrow-screen, keyboard/touch, page-jump, and fullscreen checks. Report unavailable browser checks explicitly. There is no coverage threshold or unit-test naming convention.

## Commit & Pull Request Guidelines

History uses imperative subjects, sometimes prefixed with `feat:`. Keep commits focused. PRs should explain the resulting behavior, list validation performed, link relevant issues, and include before/after screenshots for visual changes.

## Asset & Environment Rules

Store images as PNGs under `assets/` and reference them relatively; never embed Base64 or data URIs. Put bundled fonts in `assets/fonts/`. Manage Python environments and dependencies with `uv`. Do not add hashes or integrity metadata to `references/source-inventory.md`.
