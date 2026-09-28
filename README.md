# OpenCode Codex Auth — local fork

![OpenCode Codex OAuth local fork](assets/readme-hero.svg)

This repository is an unpublished working fork of [Numman Ali's upstream project](https://github.com/numman-ali/opencode-openai-codex-auth). The inherited package name is `opencode-openai-codex-auth`, but this fork is not published to npm. Running `npx -y opencode-openai-codex-auth@latest` downloads the upstream npm release; it does not install this checkout.

## Install this fork

Requirements: OpenCode, Node.js 20 or newer, and npm.

Run these commands from a terminal:

```bash
git clone https://github.com/Mindrocket42/fork-opencode-codex-auth.git
cd fork-opencode-codex-auth
npm ci
npm run build
node scripts/install-opencode-codex-auth.js
```

For OpenCode v1.0.209 and older, use `node scripts/install-opencode-codex-auth.js --legacy` on the last line.

The installer backs up and updates your global OpenCode configuration, adds this checkout's built `dist/index.js` as a local plugin, and clears the OpenCode plugin cache. Keep the checkout in place after installation. If you move it, uninstall first, then build and install from the new location.

Then authenticate and test:

```bash
opencode auth login
opencode run "write hello world to test.txt" --model=openai/gpt-5.5 --variant=medium
```

With the legacy config, use `--model=openai/gpt-5.5-medium` instead of `--variant=medium`.

## Configure it manually

If you manage OpenCode configuration yourself, the `plugin` entry must be a file URL for this checkout's built entrypoint. Replace the example with the absolute path on your machine:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "file:///absolute/path/to/fork-opencode-codex-auth/dist/index.js"
  ]
}
```

On Windows, for example, `C:\work\fork-opencode-codex-auth\dist\index.js` becomes `file:///C:/work/fork-opencode-codex-auth/dist/index.js`. Add the provider model definitions from `config/opencode-modern.json` or `config/opencode-legacy.json`, matching your OpenCode version. The repository installer does this merge for you.

## Update and remove

To update the local fork, run these from the checkout:

```bash
git pull
npm ci
npm run build
node scripts/install-opencode-codex-auth.js
```

`npm ci` is only needed when dependencies or the lockfile change. The installer can also refresh the config after a rebuild.

To remove the plugin and its model presets, run `node scripts/install-opencode-codex-auth.js --uninstall` from the checkout. Add `--all` only if you also want to delete this plugin's saved OAuth token, settings, logs, and cached instructions.

## Development checks

```bash
npm run typecheck
npm test
npm run build
```

## Documentation

- [Getting started](docs/getting-started.md)
- [Configuration reference](docs/configuration.md)
- [Troubleshooting](docs/troubleshooting.md)
- [Privacy and data handling](docs/privacy.md)
- [Changelog](CHANGELOG.md)
- [Original upstream npm package](https://www.npmjs.com/package/opencode-openai-codex-auth) — separate from this fork

This plugin uses OpenAI's OAuth flow for individual use with your own ChatGPT subscription. It is not an OpenAI product. See [LICENSE](LICENSE) and the upstream project for attribution.
