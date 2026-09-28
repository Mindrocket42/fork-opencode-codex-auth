# Getting Started

This guide installs the code in this repository. This fork is not published to npm. The inherited `npx -y opencode-openai-codex-auth@latest` command is not a source-checkout install; it cannot install the working tree you are editing. Use the steps below.

## Requirements

- OpenCode installed
- Node.js 20 or newer and npm
- A ChatGPT Plus or Pro subscription for OAuth authentication

## Install from this checkout

Clone the repository, install its dependencies, build the plugin, and run its installer:

```bash
git clone https://github.com/Mindrocket42/fork-opencode-codex-auth.git
cd fork-opencode-codex-auth
npm ci
npm run build
node scripts/install-opencode-codex-auth.js
```

For OpenCode v1.0.209 or older, replace the last command with:

```bash
node scripts/install-opencode-codex-auth.js --legacy
```

The installer backs up your global OpenCode config, merges the matching model presets, points OpenCode at this checkout's `dist/index.js`, and clears the plugin cache. Keep the checkout at the same path. If you move it, uninstall first, then build and install from the new location.

## Authenticate and test

```bash
opencode auth login
opencode run "write hello world to test.txt" --model=openai/gpt-5.5 --variant=medium
```

With the legacy config, use `--model=openai/gpt-5.5-medium` instead of `--variant=medium`.

If the browser callback cannot reach the local machine (for example, over SSH or WSL), choose the manual URL-paste option in the authentication flow and paste the full redirect URL.

## Configuration

The installer selects `config/opencode-modern.json` for OpenCode v1.0.210 and newer, or `config/opencode-legacy.json` for older versions. It merges the model presets into the global config while preserving unrelated providers and settings.

If you configure OpenCode by hand, set the plugin entry to the local built file, not the npm package name:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "file:///absolute/path/to/fork-opencode-codex-auth/dist/index.js"
  ]
}
```

Replace that example with a file URL for the absolute path to your own `dist/index.js`. On Windows, `C:\work\fork-opencode-codex-auth\dist\index.js` becomes `file:///C:/work/fork-opencode-codex-auth/dist/index.js`. Copy the provider model definitions from the appropriate config template into your existing config; avoid replacing a config that contains other settings.

## Update

From the checkout, pull the latest source, rebuild, refresh the OpenCode configuration, then restart OpenCode:

```bash
git pull
npm ci
npm run build
node scripts/install-opencode-codex-auth.js
```

Run `npm ci` only when dependencies or `package-lock.json` change.

## Uninstall

Run this from the checkout:

```bash
node scripts/install-opencode-codex-auth.js --uninstall
```

This removes the local plugin entry and this plugin's model presets. Add `--all` to also delete its saved OAuth token, plugin settings, logs, and cached instructions.

## Verify and develop

```bash
npm run typecheck
npm test
npm run build
```

To confirm the plugin is active, start OpenCode and check for plugin load errors. To inspect request details, run with `ENABLE_PLUGIN_REQUEST_LOGGING=1`; logs are written under `~/.opencode/logs/codex-plugin/`. Never share OAuth tokens or unredacted auth files when reporting an issue.

## Links

- [Configuration reference](configuration.md)
- [Troubleshooting](troubleshooting.md)
- [Architecture](development/ARCHITECTURE.md)
- [Issues for this fork](https://github.com/Mindrocket42/fork-opencode-codex-auth/issues)
- [Upstream source project](https://github.com/numman-ali/opencode-openai-codex-auth)
