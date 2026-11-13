# CV

[![Build & publish CV](https://github.com/Raedrim/cv-source/actions/workflows/publish.yml/badge.svg)](https://github.com/Raedrim/cv-source/actions/workflows/publish.yml)

My CV, compiled from LaTeX by a reproducible CI pipeline. This repository holds **no source code**; it only distributes the built PDFs through [Releases](../../releases).

## How it is built

The LaTeX source lives in a private repository. Every push triggers a GitHub Actions workflow that:

1. **Compiles deterministically.** It uses a version-pinned TeX Live container. Timestamps come from the commit (`SOURCE_DATE_EPOCH`), not the wall clock, so the same commit gives the same PDF.
2. **Publishes.** It uploads the PDF to this repository's release and to GitHub Pages, overwriting the previous one.
