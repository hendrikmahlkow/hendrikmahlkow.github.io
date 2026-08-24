# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic portfolio website for Hendrik Mahlkow (hendrikmahlkow.com), built with **Quarto** and deployed via **GitHub Pages** from the `/docs` folder.

## Build Commands

-   **Render site:** `quarto render` — builds all `.qmd` files into `/docs`
-   **Preview site:** `quarto preview` — local dev server with live reload
-   **Render single page:** `quarto render <file>.qmd`
-   **Compile CV:** Run `pdflatex` on `src/CV.tex`, then copy the PDF to `files/CV.pdf` (GitHub Actions does both on every push)

## Architecture

-   **Source pages:** `index.qmd`, `about.qmd`, `coding.qmd`, `research.qmd` (Quarto Markdown)
-   **Config:** `_quarto.yml` defines site structure, navbar, theme (Litera), and output settings
-   **Styling:** `styles.scss` (Sass theme overrides, color palette) + `styles.css` (component styles like landing section, highlights)
-   **Output:** `docs/` — generated HTML, should be committed for GitHub Pages deployment
-   **LaTeX CV:** `src/CV.tex` is the source for the downloadable CV PDF; the compiled PDF is stored in `files/CV.pdf` and copied to `docs/files/CV.pdf` by the render
-   **Static assets:** `files/` (PDFs) and `images/` are SOURCE folders declared under `project: resources:` in `_quarto.yml`. `quarto render` clears `docs/`, so nothing may live only there.

## Key Conventions

-   Custom highlight syntax: `==text==` in `.qmd` files renders as `<span class="highlight">` with aquamarine background
-   Color palette: sage green (#D1D9CE / #98A08D), purple (#AE8BD1), cream (#FDFBF7)
-   Font: Jost (loaded from Google Fonts)
-   The `docs/` directory is the publish target — it is rendered and committed automatically by `.github/workflows/render.yml` on every push to `main`; do not edit it by hand
-   `src/CV.tex` is usually the most frequently updated file, as it contains the CV content. After editing, just commit and push — the workflow compiles it and updates `files/CV.pdf` and `docs/files/CV.pdf`.
