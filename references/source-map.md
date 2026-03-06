# Source Map

Use this file to jump straight to the right official sources. Do not read everything by default.

## Core Docs By Task

- Backend node basics:
  - `https://docs.comfy.org/custom-nodes/backend/server_overview`
  - `https://docs.comfy.org/custom-nodes/backend/interface`
  - `https://docs.comfy.org/custom-nodes/backend/more_on_inputs`
  - `https://docs.comfy.org/custom-nodes/backend/datatypes`
  - `https://docs.comfy.org/custom-nodes/backend/lazy_evaluation`
  - `https://docs.comfy.org/custom-nodes/backend/lifecycle`
- Advanced backend behavior:
  - `https://docs.comfy.org/custom-nodes/backend/expansion`
  - `https://docs.comfy.org/custom-nodes/backend/node-replacement`
  - `https://docs.comfy.org/custom-nodes/backend/lists`
  - `https://docs.comfy.org/custom-nodes/backend/images_and_masks`
- Frontend extensions:
  - `https://docs.comfy.org/custom-nodes/js/javascript_overview`
  - `https://docs.comfy.org/custom-nodes/js/javascript_hooks`
  - `https://docs.comfy.org/custom-nodes/js/javascript_settings`
  - `https://docs.comfy.org/custom-nodes/js/javascript_commands_keybindings`
  - `https://docs.comfy.org/custom-nodes/js/javascript_examples`
  - `https://docs.comfy.org/custom-nodes/js/subgraphs`
- Client-server communication:
  - `https://docs.comfy.org/development/comfyui-server/comms_overview`
  - `https://docs.comfy.org/development/comfyui-server/comms_messages`
  - `https://docs.comfy.org/development/comfyui-server/comms_routes`
- Node docs and localization:
  - `https://docs.comfy.org/custom-nodes/help_page`
  - `https://docs.comfy.org/custom-nodes/i18n`
- V3 and beta-sensitive work:
  - `https://docs.comfy.org/custom-nodes/v3_migration`
  - `https://docs.comfy.org/interface/nodes-2`
  - `https://docs.comfy.org/changelog`
- Publishing and packaging:
  - `https://docs.comfy.org/registry/overview`
  - `https://docs.comfy.org/registry/publishing`
  - `https://docs.comfy.org/registry/specifications`
  - `https://docs.comfy.org/registry/standards`
  - `https://docs.comfy.org/registry/cicd`
- Workflow examples and templates:
  - `https://docs.comfy.org/custom-nodes/workflow_templates`

## Official Repos

- ComfyUI core: `https://github.com/Comfy-Org/ComfyUI`
- ComfyUI Manager: `https://github.com/Comfy-Org/ComfyUI-Manager`
- Official workflow templates: `https://github.com/Comfy-Org/workflow_templates`
- Official frontend: `https://github.com/Comfy-Org/ComfyUI_frontend`
- Registry frontend: `https://github.com/Comfy-Org/registry-web`
- Docs source: `https://github.com/Comfy-Org/docs`

## Repo Role Map

- `ComfyUI`: Python execution engine, built-in node patterns, `comfy_api`, server routes, and core examples.
- `ComfyUI_frontend`: extension hooks, renderer behavior, settings UI, commands, keybindings, and release cadence.
- `ComfyUI-Manager`: install/update behavior, registry bridge, path normalization, and special-purpose file handling.
- `workflow_templates`: official templates, subgraph blueprints, and packaging structure for shared examples.
- `registry-web`: registry UI surface and API consumer behavior.
- `docs`: the source of truth for the published docs at `docs.comfy.org`.

## Use Pattern

- Open only the pages that match the current task.
- If the task says "latest", "beta", "nightly", "Nodes 2.0", or "migration", re-open the live docs even if a local reference already summarizes them.
