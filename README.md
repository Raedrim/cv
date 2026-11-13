# CV

[![Build & publish CV](https://github.com/Raedrim/cv-source/actions/workflows/publish.yml/badge.svg)](https://github.com/Raedrim/cv-source/actions/workflows/publish.yml)

My CV, compiled from LaTeX by a reproducible CI pipeline. This repository holds **no source code**; it only distributes the built PDFs through [Releases](../../releases).

## Download

| Variant | Direct link |
| --- | --- |
| Primary CV | [`cv.pdf`](../../releases/latest/download/cv.pdf) |
| Role-specific variant `<name>` | `https://github.com/Raedrim/cv/releases/download/<name>/cv.pdf` |

Role-specific variants (for example `backend`, `sysarch`) are published as pre-releases so they have permanent URLs without cluttering the main release list. See [all releases](../../releases).

## How it is built

The LaTeX source lives in a private repository. Every push triggers a GitHub Actions workflow that:

1. **Compiles deterministically.** It uses a version-pinned TeX Live container. Timestamps come from the commit (`SOURCE_DATE_EPOCH`), not the wall clock, so the same commit gives the same PDF.
2. **Maps the branch to a release.** `main` publishes to the `latest` release. `feat/<name>` publishes to the pre-release tagged `<name>`.
3. **Publishes.** It uploads the PDF to this repository's release, overwriting the previous one.
