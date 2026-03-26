# Workflow Assets And Templates

## Local Example Workflows In A Node Pack

- Prefer an `example_workflows/` directory in the custom node repo.
- Put `*.json` workflow files there.
- Add optional thumbnails with the same basename, such as `my_flow.jpg`.
- ComfyUI also accepts `workflow`, `workflows`, `example`, and `examples`, but prefer `example_workflows`.
- ComfyUI serves these files through `/api/workflow_templates`.

## When To Ship Local Examples

- Ship local examples when the workflow is tightly coupled to one node pack.
- Add at least one minimal workflow that proves installation success and intended usage.
- Keep examples free of unnecessary third-party dependencies unless the whole pack is built around them.

## Official Templates Repo

The official repository is `https://github.com/Comfy-Org/workflow_templates`.

Current structure highlights from the repo README:
- `templates/` and `packages/`: full standalone workflow templates
- `blueprints/` and `packages/blueprints/`: reusable subgraph blueprints
- `site/`: Astro static site for `https://templates.comfy.org`
- package-per-media packaging for distribution

## Contribution Pattern For Official Templates

1. Create or export the workflow JSON.
2. Prefer creating the workflow with `--disable-all-custom-nodes` when the template is meant to represent core behavior.
3. Capture or generate a thumbnail and compress it aggressively.
4. Add or update the template metadata and bundle assignment.
5. Run the sync script expected by the repo before committing.
6. Embed model metadata so the workflow remains installable and discoverable inside ComfyUI.

## Docs-Specific Workflow Assets

- If adding workflows to docs, upload the workflow asset to the appropriate GitHub repo and use the raw GitHub content URL.
- The docs repo explicitly recommends raw content URLs so drag-and-drop workflow metadata stays intact.

## Practical Default

- Use local `example_workflows/` for node-pack onboarding.
- Use the official `workflow_templates` repo only for broadly reusable templates or blueprints that should ship as official assets.
- Pair workflow assets with publish-grade docs and visuals from `references/readme-and-branding.md` when preparing a public extension repo.
