# README And Branding Guide

Use this guide when generating publishable ComfyUI extension repos.

## README Structure (Default)

Create a detailed `README.md` with these sections in order:

1. **Project title + short value statement**
2. **Banner image** (`![banner](assets/banner.svg)`)
3. **Features** (bullet list of concrete node/extension capabilities)
4. **Compatibility**
   - minimum ComfyUI version
   - frontend package constraints when relevant
   - renderer notes (Nodes 2.0 and LiteGraph fallback)
5. **Installation**
   - ComfyUI Manager path
   - manual git clone path
   - dependency install expectations (`requirements.txt`, optional `install.py`)
6. **Quick Start**
   - where to find nodes in menu
   - minimal step-by-step workflow
   - pointer to `example_workflows/`
7. **Configuration / Settings** (if frontend settings exist)
8. **Included Nodes**
   - each node name, inputs, outputs, purpose
9. **Troubleshooting**
   - common install issues
   - version mismatch guidance
10. **Development**
    - local test commands
    - CI/workflow test note
11. **License**

## README Quality Rules

- Prefer concrete behavior over marketing language.
- Include at least one workflow screenshot or thumbnail reference.
- Keep install commands copy-paste friendly.
- Include explicit compatibility ranges (`requires-comfyui`, frontend dependency range).
- Add a short changelog summary block only when the task asks for release notes.

## SVG Banner Guidance

Default path: `assets/banner.svg`.

Banner should be lightweight and static:
- Pure SVG markup (no script tags, no remote fetches).
- Include project name and a short subtitle (for example: "Custom ComfyUI Nodes").
- Use a simple gradient background + high contrast title text.
- Keep file size modest and dimensions repository-friendly (for example 1280x320).
- Avoid embedding raster blobs unless explicitly requested.

## Minimal Banner Template

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="1280" height="320" viewBox="0 0 1280 320" role="img" aria-label="Project banner">
  <defs>
    <linearGradient id="bg" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#0f172a"/>
      <stop offset="100%" stop-color="#1d4ed8"/>
    </linearGradient>
  </defs>
  <rect width="1280" height="320" fill="url(#bg)"/>
  <text x="72" y="150" fill="#ffffff" font-family="Inter,Segoe UI,Arial" font-size="64" font-weight="700">My ComfyUI Extension</text>
  <text x="72" y="210" fill="#cbd5e1" font-family="Inter,Segoe UI,Arial" font-size="30">Custom nodes and UI tools</text>
</svg>
```

## Asset Layout Recommendation

```text
assets/
  banner.svg
  workflows/
    quickstart.jpg
```

## Practical Default

For publishable repos, always generate:
- `README.md`
- `assets/banner.svg`
- at least one `example_workflows/*.json` + thumbnail
