# Distribution And Publishing

## Minimal Registry-Ready Metadata

Use `pyproject.toml` as the canonical package identity.

```toml
[project]
name = "my-node-pack"
version = "0.1.0"
description = "Short summary"
license = { file = "LICENSE" }
requires-python = ">=3.10"
dependencies = []

[project.urls]
Repository = "https://github.com/owner/repo"

[tool.comfy]
PublisherId = "owner"
DisplayName = "My Node Pack"
requires-comfyui = ">=0.16.0"
```

## Packaging Rules

- Use semantic versioning.
- Keep `project.name` stable. It becomes the registry identity and affects install behavior.
- Add `project.urls.Repository` early.
- Add `requires-comfyui` when compatibility is not broad enough to be implicit.
- Add `comfyui-frontend-package` constraints when the pack depends on a specific frontend API range.
- Use `[tool.comfy].includes` when a built frontend artifact such as `dist/` is needed but normally ignored by git.

## Manager And Registry Behavior

- Registry powers ComfyUI-Manager discovery and installation.
- Manager installs by cloning the repo, installing `requirements.txt` when present, and running `install.py` when present.
- Manager documentation explicitly says not to assume the directory under `custom_nodes` matches the GitHub repo name. It normalizes from `project.name`.
- Avoid folder-name-based imports or path logic.

## Special-Purpose Files

- `requirements.txt`: declare Python dependencies that Manager should install.
- `install.py`: run one-time install behavior from the pack root.
- `node_list.json`: declare nodes manually if the export pattern is unconventional.
- `example_workflows/`: provide example workflows for template browsing.

## Publish Flows

- Initialize metadata with `comfy node init`.
- Publish manually with `comfy node publish`.
- Or publish via GitHub Actions with `Comfy-Org/publish-node-action`.
- Bump the version intentionally before publishing. Registry versions are immutable once published.

## Standards To Respect

- Do not use `eval` or `exec`.
- Do not perform runtime `pip install` through subprocess calls.
- Do not ship obfuscated code.
- Do not break other custom nodes' install, update, or removal behavior.
- Provide real community value and keep self-promotion limited.

## CI/CD

- Use `Comfy-Org/comfy-action` to run workflows in CI across environments.
- Prefer CI for regression checks before publishing new versions.
- Use deprecation and migration paths when replacing old nodes instead of silently breaking workflows.

## Practical Default

- Treat `pyproject.toml` as mandatory for anything intended to be installed by other people.
- Add compatibility ranges before release work, not after breakage reports.
