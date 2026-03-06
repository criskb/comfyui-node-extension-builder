---
name: comfyui-node-extension-builder
description: Design and implement ComfyUI custom nodes, frontend extensions, hybrid node packs, registry-ready packages, workflow templates, and migration work for existing ComfyUI extensions. Use when Codex needs to create or update Python nodes, `WEB_DIRECTORY` JavaScript extensions, `pyproject.toml` registry metadata, `example_workflows`, node docs, i18n files, V1 `INPUT_TYPES` nodes, V3 `comfy_api` schema nodes, or ComfyUI Manager/Registry publishing assets. Refresh official `docs.comfy.org` pages and current ComfyUI repos before coding when the task depends on latest APIs, Nodes 2.0, beta behavior, or version-sensitive packaging.
---

# ComfyUI Node Extension Builder

## Overview

Create and update ComfyUI custom nodes, frontend extensions, hybrid node packs, registry metadata, workflow templates, and migration work. Refresh official sources first, prefer stable APIs by default, and opt into V3 or beta-only features only when the task actually needs them.

## Refresh Official Sources

1. Re-open the official docs pages that match the task before coding.
2. Reconfirm current repo heads and version signals if the user asks for latest, beta, nightly, or migration-sensitive work.
3. Treat `references/current-platform-snapshot.md` as a dated starting point, not a substitute for checking live sources.

Read only the references needed for the task:
- `references/source-map.md`: map task types to the right docs pages and repos.
- `references/backend-node-authoring.md`: V1 and V3 backend node patterns.
- `references/frontend-extension-authoring.md`: `WEB_DIRECTORY`, hooks, settings, commands, routes, i18n, docs panels, and subgraphs.
- `references/distribution-publishing.md`: `pyproject.toml`, registry, Manager, CI/CD, and standards.
- `references/workflow-assets-and-templates.md`: `example_workflows`, official templates, and blueprints.
- `references/current-platform-snapshot.md`: March 6, 2026 snapshot of versions, repo heads, and beta notes.

## Choose The Smallest Correct Architecture

- Use a V1 backend node for maximum compatibility with current installs and third-party packs.
- Use a V3 schema node only when the user explicitly wants `comfy_api`, `ComfyExtension`, node replacement, built-in V3 UI helpers, auth-token hidden inputs, or other beta/latest-only features.
- Use a frontend extension when the task is UI behavior, menus, commands, settings, docs panels, subgraphs, or client-server interaction.
- Use a hybrid pack when the feature crosses server and client boundaries. Keep the Python node and JS extension loosely coupled unless real-time interaction is required.
- Use registry and workflow-template work only when the deliverable is meant to be installed, published, shared, or demoed.

## Implementation Rules

- Start from the existing repo structure when editing an existing node pack.
- For new packs, prefer the official scaffold path (`comfy node scaffold`) or the official Comfy templates referenced in the docs instead of inventing a layout from scratch.
- Pin a numbered `comfy_api.vX_Y_Z` import when shipping V3 code unless the user explicitly wants `comfy_api.latest`. Explain when choosing `latest`, because the docs explicitly treat it as under active development.
- Prefer official extension hooks and documented APIs over prototype hijacking, DOM scraping, or LiteGraph internals.
- Treat Nodes 2.0 as a live compatibility target for UI-affecting work. Test both Nodes 2.0 and the LiteGraph renderer when the feature touches node rendering, canvas behavior, menus, or widgets.
- Add `pyproject.toml` metadata early for publishable work. Use semver, `project.urls.Repository`, `tool.comfy.PublisherId`, and `requires-comfyui` when compatibility needs to be explicit.
- Add a `comfyui-frontend-package` dependency range when the pack relies on a specific frontend API level.
- Add `example_workflows/` and matching thumbnails for user-facing nodes whenever a demo workflow materially improves usability.
- Add `WEB_DIRECTORY/docs` markdown and `locales/` when the node has non-trivial UI, settings, or onboarding needs.
- Avoid imports or logic that assume the install directory matches the GitHub repo name. Manager now normalizes the folder name from `project.name`.
- Follow registry standards: no `eval`, no `exec`, no runtime `pip install` via subprocess, no code obfuscation.

## Task Playbooks

### Backend Node

1. Read `references/backend-node-authoring.md`.
2. Decide V1 versus V3 before writing code.
3. Implement the smallest viable node shape first, then add hidden inputs, lazy evaluation, list behavior, previews, expansion, or replacements only if required.
4. Verify tensor shapes, caching behavior, and output tuple shape.

### Frontend Extension

1. Read `references/frontend-extension-authoring.md`.
2. Register through `WEB_DIRECTORY` and `app.registerExtension`.
3. Prefer official hooks, settings, commands, and menu APIs.
4. Add cleanup for event listeners and subgraph listeners.

### Hybrid Node Pack

1. Read both backend and frontend references.
2. Default to workflow data flow between server and client.
3. Add websocket messages or custom routes only when live interaction during execution is actually required.

### Publishing Or Registry Work

1. Read `references/distribution-publishing.md`.
2. Verify `pyproject.toml`, versioning, dependency model, and standards before release work.
3. If the task includes discoverability or onboarding, also read `references/workflow-assets-and-templates.md`.

## When Official Sources Conflict

Follow the current official docs and repo behavior over this skill's summaries. When the task depends on "latest" or "beta" behavior, restate the exact version, branch, or date you verified before implementing.
