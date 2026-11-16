# CV

[![Build & publish CV](https://github.com/Raedrim/cv-source/actions/workflows/publish.yml/badge.svg)](https://github.com/Raedrim/cv-source/actions/workflows/publish.yml)

My CV, compiled from LaTeX by a reproducible CI pipeline. This repository holds **no source code**; it only distributes the built PDFs through [Releases](../../releases).

## How it is built

The LaTeX source lives in a private repository. Every push triggers a GitHub Actions workflow that:

1. **Compiles deterministically.** It uses a version-pinned TeX Live container. Timestamps come from the commit (`SOURCE_DATE_EPOCH`), not the wall clock, so the same commit gives the same PDF.
2. **Publishes.** It uploads the PDF to this repository's release and to GitHub Pages, overwriting the previous one.

## Verify

Every PDF is signed with my PGP key. The signature is `cv.pdf.asc`, next to each `cv.pdf` in the [Releases](../../releases) (and on Pages). The Releases also carry a signed `SHA256SUMS`.

```sh
curl -sLO https://github.com/Raedrim/cv/releases/latest/download/cv.pdf
curl -sLO https://github.com/Raedrim/cv/releases/latest/download/cv.pdf.asc
curl -s https://github.com/Raedrim.gpg | gpg --import     # or: gpg --import pgp.asc
gpg --verify cv.pdf.asc cv.pdf
```

Expected: `Good signature from "Levente Szajko <raedrimhun@proton.me>"`, with this primary key fingerprint:

```
AB27 02F3 3A44 B442 B493  2E53 F7D1 00E4 9FF1 A296
```

gpg will warn that the key is not certified. Compare the fingerprint against independent sources: this repo (`pgp.asc`), `github.com/Raedrim.gpg`, and `keys.openpgp.org`. Signing happens in CI with a dedicated signing subkey (`EB3E 9F2A A7F9 D55D 00B1  ED63 5F64 27A7 4986 E5FA`, expires 2028-11-15). The primary key stays offline.
