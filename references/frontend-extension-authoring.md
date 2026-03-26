# Frontend Extension Authoring

## Load The Extension Correctly

- Export `WEB_DIRECTORY` from the Python package.
- Put one or more `.js` files in that directory.
- Register with `app.registerExtension`.
- Only `.js` files are auto-loaded. Other assets must be fetched from the served extension path at runtime.
- Do not copy extension scripts into ComfyUI core web directories.

## Minimum Shape

```javascript
import { app } from "../../scripts/app.js";

app.registerExtension({
  name: "my_pack.feature",
  async setup() {
    // Add listeners here.
  },
});
```

## Prefer Official Hooks

- `beforeRegisterNodeDef(nodeType, nodeData, app)`:
  - best default hook
  - modify a node type before instances exist
- `nodeCreated(node)`:
  - patch or initialize one node instance
- `init()`:
  - run before nodes register
  - only for early app or graph changes
- `afterConfigureGraph()`:
  - react to a workflow after it loads
- `setup()`:
  - add event listeners, menus, and app-level behavior after startup

Prefer documented hooks over prototype hijacking. If there is no official API, patch the smallest possible surface and preserve original behavior.

## Official UI Surfaces

- Canvas menu: implement `getCanvasMenuItems(canvas)`.
- Node menu: implement `getNodeMenuItems(node)`.
- Topbar menu: use `commands` plus `menuCommands`.
- Settings:
  - provide `settings: [...]`
  - use stable `id` values
  - use `category` when you want presentation to differ from storage
- Commands and keybindings:
  - provide `commands: [...]`
  - provide `keybindings: [...]`
  - avoid core-reserved combos

## Deprecated Patterns To Block In New Code

- `LGraphCanvas.prototype.getCanvasMenuOptions`
- `nodeType.prototype.getExtraMenuOptions`
- broad prototype monkey-patching of app/canvas/node internals for behavior now covered by official hooks

Treat these as migration targets. New code should use `getCanvasMenuItems`, `getNodeMenuItems`, and other documented extension surfaces.

## Client-Server Interaction

- Listen for server messages with `api.addEventListener("message.type", handler)`.
- Send server-side websocket messages with `PromptServer.instance.send_sync(...)`.
- Add custom server routes only when workflow submission-time data flow is not enough.
- Send route requests from the frontend with `api.fetchApi(...)`.
- Pass hidden `UNIQUE_ID` from the node when you need to target a specific node instance.

## Subgraphs

- Use `app.graph` for the full workflow graph.
- Use `app.canvas?.graph` for only the currently visible graph layer.
- Treat three ids differently:
  - `node.id`: local graph id
  - execution id: backend progress id
  - locator id: UI state id
- Use `AbortController` or equivalent cleanup for listeners on subgraph events.
- Expect widget promotion behavior to evolve.

## Node Docs And Localization

- Rich docs:
  - add `WEB_DIRECTORY/docs/NodeName.md`
  - add locale-specific docs like `WEB_DIRECTORY/docs/NodeName/en.md`
- i18n:
  - add `locales/<lang>/main.json`
  - add `nodeDefs.json` for node labels, tooltips, and option labels
  - add `settings.json` and `commands.json` when the extension exposes those surfaces

## Nodes 2.0 Guidance

- Treat Nodes 2.0 as a compatibility target when touching node rendering, widgets, menus, or canvas interactions.
- Prefer official hooks, commands, settings, and public extension APIs over DOM scraping or LiteGraph internals.
- Test both Nodes 2.0 and LiteGraph when the feature is renderer-sensitive.
- Keep fallbacks defensive. Some users will still toggle back to the older renderer.

## Practical Default

- Start with `beforeRegisterNodeDef`, `nodeCreated`, `setup`, settings, commands, and documented menu APIs.
- Add custom routes, subgraph logic, or renderer-sensitive behavior only when the feature really requires it.
- Add a CI check that fails on deprecated menu monkey-patch patterns.
