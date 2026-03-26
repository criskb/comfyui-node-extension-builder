# Backend Node Authoring

## Contents

- Choose V3 Or V1 First
- V3 Minimum Shape
- V3 Checklist
- Useful V3-Only Features
- V1 Minimum Shape
- V1 Checklist
- V1 Hidden And Flexible Inputs
- Data And Tensor Gotchas
- Advanced V1 Features
- Migration Notes
- Practical Default

## Choose V3 Or V1 First

- Choose V3 by default for new node packs and forward-looking work.
- Choose V1 only when compatibility with older installs and legacy custom-node ecosystems is the top requirement.
- If shipping V3 code, prefer a numbered import such as `comfy_api.v0_0_2` over `comfy_api.latest` unless the user explicitly wants beta behavior.

## V3 Minimum Shape

```python
from comfy_api.v0_0_2 import ComfyExtension, io


class MyNode(io.ComfyNode):
    @classmethod
    def define_schema(cls) -> io.Schema:
        return io.Schema(
            node_id="my_pack.MyNode",
            category="my_pack",
            inputs=[io.Image.Input("image")],
            outputs=[io.Image.Output()],
        )

    @classmethod
    def execute(cls, image) -> io.NodeOutput:
        return io.NodeOutput(image)


class MyExtension(ComfyExtension):
    async def get_node_list(self) -> list[type[io.ComfyNode]]:
        return [MyNode]


async def comfy_entrypoint() -> ComfyExtension:
    return MyExtension()
```

## V3 Checklist

- Inherit from `io.ComfyNode`.
- Define all node metadata in `define_schema`.
- Implement `execute` as a classmethod.
- Register nodes through `ComfyExtension.get_node_list()`.
- Export `comfy_entrypoint()`.
- Use `fingerprint_inputs` instead of `IS_CHANGED`.
- Use `validate_inputs` instead of `VALIDATE_INPUTS`.
- Use `check_lazy_status` as a classmethod.
- Use `io.Custom("type_name")` for custom types.
- Use schema flags like `is_output_node`, `is_deprecated`, `is_experimental`, and `is_dev_only` only when the behavior is real and intentional.
- Access hidden values through `cls.hidden`.
- Do not rely on node instance state for execution behavior.

## Useful V3-Only Features

- Built-in UI helpers from `ui`, such as `ui.PreviewImage`, `ui.PreviewMask`, `ui.PreviewText`, and `ui.ImageSaveHelper`.
- Node replacements through `api.node_replacement.register(...)`, usually in `ComfyExtension.on_load`.
- Hidden auth and API token values for ComfyOrg-connected flows.
- Schema-level `accept_all_inputs` for dynamic prompt payloads.

## V1 Minimum Shape

```python
class MyNode:
    @classmethod
    def INPUT_TYPES(cls):
        return {"required": {"image": ("IMAGE", {})}}

    RETURN_TYPES = ("IMAGE",)
    FUNCTION = "run"
    CATEGORY = "my_pack"

    def run(self, image):
        return (image,)


NODE_CLASS_MAPPINGS = {"MyNode": MyNode}
```

## V1 Checklist

- Define `INPUT_TYPES` as a classmethod with `required`, plus `optional` and `hidden` when needed.
- Define `RETURN_TYPES`. Keep the trailing comma for single-output tuples.
- Add `RETURN_NAMES` only when the default lowercase names are not good enough.
- Set `FUNCTION` to the method Comfy should call.
- Set `CATEGORY` to a stable menu path.
- Export `NODE_CLASS_MAPPINGS`, and `NODE_DISPLAY_NAME_MAPPINGS` only when the display name differs from the node id.
- Use `OUTPUT_NODE = True` only for real output nodes.
- Use `SEARCH_ALIASES` for search synonyms.
- Use `VALIDATE_INPUTS` for constant-input validation or custom type validation.
- Use `IS_CHANGED` only when default caching behavior is wrong (it returns a compared value, not a simple boolean "rerun" flag).
- Use `INPUT_IS_LIST` and `OUTPUT_IS_LIST` only when list semantics are actually required.

## V1 Hidden And Flexible Inputs

- Hidden inputs:
  - `UNIQUE_ID`: match server work to a specific node instance.
  - `PROMPT`: inspect the submitted prompt payload.
  - `EXTRA_PNGINFO`: write metadata for downstream saves.
  - `DYNPROMPT`: only for advanced expansion and loop-like behavior.
- Custom datatypes:
  - invent a unique uppercase type name
  - add `{"forceInput": True}` so the frontend shows a socket instead of an unknown widget
- Wildcard inputs:
  - use `"*"` plus `VALIDATE_INPUTS(input_types)` when the node intentionally accepts arbitrary upstream types
- Dynamic inputs:
  - use an `optional` mapping whose `__contains__` always returns `True`
  - collect the values through `**kwargs`

## Data And Tensor Gotchas

- `IMAGE` is a `torch.Tensor` shaped `[B,H,W,C]`.
- `MASK` is usually `[B,H,W]` and may arrive as `[H,W]`.
- `LATENT` is a `dict`; the actual tensor is `latent["samples"]` with shape `[B,C,H,W]`.
- Never rely on tensor truthiness. Use `is not None`, `.any()`, or `.all()`.
- Return tuples, not bare values.

## Advanced V1 Features

- Lazy evaluation:
  - mark an input with `{"lazy": True}`
  - implement `check_lazy_status(self, ...)`
- Node expansion:
  - return `{"result": (...), "expand": graph.finalize()}`
  - prefer `GraphBuilder`
  - use raw links when you need caching-friendly subgraphs
- Connected client-server behavior:
  - add hidden `UNIQUE_ID`
  - send messages with `PromptServer.instance.send_sync(...)`

## Migration Notes

- `RETURN_TYPES` maps to `outputs`.
- `CATEGORY` maps to `category`.
- `OUTPUT_NODE` maps to `is_output_node`.
- `EXPERIMENTAL` maps to `is_experimental`.
- `DEPRECATED` maps to `is_deprecated`.
- `IS_CHANGED` maps to `fingerprint_inputs`.
- V3 node classes should not rely on instance state. `__init__` is not the place for execution-time state.

## Practical Default

- Default to V3 for new work.
- Use V1 intentionally for compatibility targets.
- If the task says "latest" or "beta", state the exact V3 API version and docs date you verified before implementing.
