# Current Platform Snapshot

Snapshot date: March 26, 2026.

Use this file as a dated baseline. Reconfirm live docs and repo heads before coding anything version-sensitive.

## Repo Heads And Version Signals

| Surface | Branch | Version Signal |
| --- | --- | --- |
| `ComfyUI` | `master` | `pyproject.toml` and `comfyui_version.py` show `0.18.1` |
| `ComfyUI-Manager` | `main` | README reflects registry-first flow and path normalization from `project.name` |
| `workflow_templates` | `main` | README continues package-per-media templates and blueprints model |
| `ComfyUI_frontend` | `main` | `package.json` shows `@comfyorg/comfyui-frontend` `1.43.6` |
| `docs` | `main` | Published at `https://docs.comfy.org/` |

## Dependency Signals Worth Remembering

- Core `requirements.txt` pins `comfyui-frontend-package==1.42.8`.
- Core `requirements.txt` also pins ecosystem packages like `comfyui-workflow-templates` and `comfyui-embedded-docs`.
- Frontend source repo version can lead the pip frontend package pin used by core installs.

## Docs Signals Worth Remembering

- The docs say `comfy_api.latest` points to the newest in-development API. Prefer a numbered import for shipped V3 code unless the user explicitly wants latest/beta behavior.
- The docs describe V3 as the forward path for future node-feature work, while V1 remains supported for legacy compatibility.
- `Nodes 2.0` is available in Desktop, portable, and stable releases. Some custom nodes still need updates, and the LiteGraph renderer remains available as a fallback.
- The context-menu migration docs deprecate legacy prototype monkey-patching and recommend `getCanvasMenuItems` / `getNodeMenuItems`.

## Packaging And Publish Signals

- Manager tells developers not to assume the install folder under `custom_nodes` matches the GitHub repo name. It normalizes from `project.name` in `pyproject.toml`.
- Manager supports registry-backed installs and documents `requirements.txt`, `install.py`, and optional `node_list.json`.
- Registry packaging is centered on `pyproject.toml` plus `[tool.comfy]` metadata, semver, and compatibility constraints like `requires-comfyui`.
- Workflow templates continue to separate full templates, blueprints, and template-site assets.

## Use Pattern

- Restate exact dates, versions, or hashes when explaining "latest" behavior.
- Re-open live docs for V3 migration, Nodes 2.0, context-menu migration, or registry work before making implementation choices.
- Treat anything described as `latest`, `experimental`, `dev only`, or `nightly` as unstable until re-verified.
