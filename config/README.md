# Configuration templates

This directory contains model configuration templates for this unpublished fork. The plugin itself must load from your local checkout; the npm package identifier in upstream documentation does not install this fork.

## Choose a template

| File | OpenCode version | Purpose |
| --- | --- | --- |
| [`opencode-modern.json`](./opencode-modern.json) | v1.0.210 and newer | Model variants configuration |
| [`opencode-legacy.json`](./opencode-legacy.json) | v1.0.209 and older | Separate model entries for reasoning levels |
| [`minimal-opencode.json`](./minimal-opencode.json) | Any | Minimal example; not the recommended full model setup |

## Recommended setup

From the repository root, run the local installer after building the plugin:

```bash
npm ci
npm run build
node scripts/install-opencode-codex-auth.js
```

Use `--legacy` with the installer for OpenCode v1.0.209 and older. The installer backs up the existing global config, merges the selected model presets, writes a local file URL for this checkout's `dist/index.js`, and clears the plugin cache.

## Manual setup

If you apply a template by hand, replace its `plugin` entry with a file URL pointing to the absolute path of this checkout's `dist/index.js`. For example:

```json
"plugin": [
  "file:///C:/work/fork-opencode-codex-auth/dist/index.js"
]
```

Use your own checkout path. Do not leave the placeholder path or use `opencode-openai-codex-auth` as the plugin entry; that package name resolves to the upstream npm release. Merge the template's `provider.openai` settings into your existing config instead of overwriting unrelated settings.

See [Getting Started](../docs/getting-started.md) and the [Configuration Guide](../docs/configuration.md) for complete instructions.
