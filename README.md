# phvv-me.github.io

This repository exists to **anchor the `phvv.me` custom domain on GitHub Pages**. It does not host the website.

## What serves what

- **`phvv.me`** (homepage, `/dictionary`, `/projects`, …) is a SvelteKit app deployed to **Cloudflare Workers** (repo: `Pedrexus/my`).
- **`phvv.me/<project>`** docs are GitHub Pages **project sites** from their own repos (`chefe`, `lote`, `mainboard`, `icip2025`, `frame-representation-hypothesis`). They resolve under `phvv.me` only because this repo holds the org-level custom domain.

## Do not delete or disable

Removing this repo, turning off its Pages, or deleting the `CNAME` file un-binds `phvv.me` from GitHub Pages and **breaks every `phvv.me/<project>` docs link**. Keep Pages enabled (build from `main`, root) with `CNAME = phvv.me`.

The previous Jekyll homepage lives on the [`archive`](../../tree/archive) branch.
