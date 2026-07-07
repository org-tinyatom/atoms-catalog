# TinyAtom public atom catalog

This repository hosts the **public catalog** for [TinyAtom](https://github.com/org-tinyatom/tinyatom) — the
list of reviewed atoms the app offers in its Marketplace.

## What's here

- **`catalog.json`** — the catalog the app fetches, served via GitHub Pages at
  `https://org-tinyatom.github.io/atoms-catalog/catalog.json`.
- **`catalog.json.sig`** — a detached, base64-encoded Ed25519 signature over the exact `catalog.json`
  bytes, produced with the TinyAtom **owner** signing key. The app verifies this signature on every fetch
  and refuses a catalog that fails it (in packaged builds), and rejects a catalog older than the last one
  it accepted (rollback protection).
- Atom packages (`*.tgz`) are published as **GitHub Releases** on this repo, not committed files. Each
  `catalog.json` entry's `packageUrl` points at its Release asset.

## Read-only except the owner and the publish pipeline

Nobody edits this repo by hand. Creators open pull requests against
**`org-tinyatom/atom-submissions`**; an owner reviews and merges; a trusted **post-merge GitHub Actions
workflow** — holding the owner signing key as a repository secret — then packages, signs, and writes
`catalog.json` + `catalog.json.sig` here and uploads the package as a Release. Fork pull requests never
receive the signing key. The workflow templates live in `scripts/ci/` in the TinyAtom repo.

`main` is branch-protected (no force-push, no deletion); write access is limited to org owners and the
pipeline token.

---

The `catalog.json` currently checked in is an **empty placeholder** so the Pages URL serves valid JSON. The
first real, signed catalog is produced by the publish pipeline once the owner signing key is provisioned.
