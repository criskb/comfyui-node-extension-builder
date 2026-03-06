# Current Platform Snapshot

Snapshot date: March 6, 2026.

Use this file as a dated baseline. Reconfirm live docs and repo heads before coding anything version-sensitive.

## Repo Heads And Version Signals

| Surface | Branch | Head | Version Signal |
| --- | --- | --- | --- |
| `ComfyUI` | `master` | `3b93d5d571cb3e018da65f822cd11b60202b11c2` | `pyproject.toml` and `comfyui_version.py` show `0.16.3` |
| `ComfyUI-Manager` | `main` | `008e6ede56fd53f4c617adae25517a3e020131e7` | README reflects registry-first flow and recent security/path changes |
| `workflow_templates` | `main` | `2f4a69987c76b2748b2a6617e47621b3c107ae46` | README describes package-per-media templates and blueprints |
| `ComfyUI_frontend` | `main` | `7cb07f9b2d8b9a7e7947218fd6ddaad41da27e75` | `package.json` shows `@comfyorg/comfyui-frontend` `1.41.13` |
| `registry-web` | `main` | `d1aa6a68d63f47623adab73540095e76857205da` | `package.json` shows `0.1.2` |
| `docs` | `main` | `fe64c04e505ceb8d2345390f1f66d20f5cf48658` | Published at `https://docs.comfy.org/` |

## Docs Signals Worth Remembering

- The docs say `comfy_api.latest` points to the newest in-development API. Prefer a numbered import for shipped V3 code unless the user explicitly wants latest/beta behavior.
- The docs currently describe `comfy_api.v0_0_2` as the first and current V3 API version, and explicitly warn that more changes may still land without warning.
- `Nodes 2.0` is documented as available in Desktop, portable, and stable releases. Some custom nodes still need updates, and the LiteGraph renderer remains available as a fallback.
- The frontend repo documents a release cadence with nightly builds and supports testing the newest frontend with `--front-end-version Comfy-Org/ComfyUI_frontend@latest`.

## Changelog Highlights Around This Snapshot

- `docs.comfy.org/changelog` shows `v0.16.0` and `v0.16.1` updates on March 5, 2026.
- Custom-node-relevant highlights include:
  - new `CURVE` type support
  - continued workflow template updates, including `0.9.8`
  - ongoing API-node and frontend patch activity

## Packaging And Publish Signals

- Manager now tells developers not to assume the install folder under `custom_nodes` matches the GitHub repo name. It normalizes from `project.name` in `pyproject.toml`.
- Manager supports registry-backed installs and documents `requirements.txt`, `install.py`, and optional `node_list.json`.
- Registry packaging is centered on `pyproject.toml` plus `[tool.comfy]` metadata, semver, and compatibility constraints like `requires-comfyui`.
- The workflow templates repo now clearly separates full templates, blueprints, and template-site assets.

## Use Pattern

- Restate exact dates, versions, or hashes when explaining "latest" behavior.
- Re-open live docs for V3 migration, Nodes 2.0, or registry work before making implementation choices.
- Treat anything described as `latest`, `experimental`, `dev only`, or `nightly` as unstable until re-verified.
