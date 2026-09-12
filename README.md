<p align="center">
  <img src="assets/logo.svg" width="80" height="80" alt="Aluvia logo">
</p>

# Aluvia

Aluvia lets Grok Bot access websites through residential proxy IPs instead of its datacenter IP. Choose a country and help your browser workflows get past CAPTCHAs, bot blocks, and geo restrictions when the IP address is the cause.

**Publisher: Aluvia LLC** · [support@aluvia.io](mailto:support@aluvia.io) · [aluvia.io](https://aluvia.io)

[Documentation](https://aluvia.io/docs) · [Source](https://github.com/aluvia-connect/aluvia-plugin) · [Changelog](CHANGELOG.md) · [Security](SECURITY.md)

## What it does

Aluvia helps cloud agents use the local version of a website. This plugin gives Cursor agents and Grok Bot a skill for choosing a country and checking the result. The separate Aluvia CLI routes the agent's existing Chrome or Chromium browser through a residential proxy, which gives the browser a different public IP address.

Use it when:

- A page shows the wrong country's prices or product catalog.
- A site says the content is not available in your region.
- You suspect a datacenter IP is causing a 403, CAPTCHA, Cloudflare challenge, or Access Denied page. A residential IP in the right country sometimes clears these blocks.

Country selection is at country level only. Aluvia does not select a city, set GPS, change timezone or browser language, or alter fingerprint, TLS, or canvas behavior. It is not a human VPN, a streaming tool, or a login bypass. A website can still require a login, human check, or other permission.

## Install and use

This repository contains a **free, skill-only Cursor plugin**. It includes no MCP server, connector, hook, rule, agent, or executable runtime. For a local plugin install, use the [steps below](#test-the-plugin-locally). Installing the plugin does not install or start the CLI.

The CLI requires Node.js 18 or later, Chrome or Chromium, and permission to run commands and install software on the browser's host. Some hosted agents do not provide that access. See [the docs](https://aluvia.io/docs) before setup.

Save unfinished browser work first. Initial setup may restart Chrome. Ask your agent to run this on the machine where its browser runs:

```bash
npx aluvia-cli setup
```

No account, API key, payment, or target page URL is required to start. Setup installs the CLI launcher and its bundled skill, starts the local proxy, configures the browser, enables proxy traffic, and checks the connection.

Then ask your agent to choose a country:

```bash
aluvia geos
aluvia proxy-on --geo US
```

Replace `US` with a country code from `aluvia geos`. Reload the target page and check the content you need. `ready: true` confirms connection checks, not access to the target website or completion of your task.

If `aluvia` is not on PATH, replace it with `npx aluvia-cli`. For example, `npx aluvia-cli status`.

## Commands

| Task | Command |
| --- | --- |
| List available countries | `aluvia geos` |
| Turn the proxy on without choosing a country | `aluvia proxy-on` |
| Use a chosen country | `aluvia proxy-on --geo US` |
| Get a new IP without choosing a country | `aluvia rotate-ip` |
| Get a new IP in a chosen country | `aluvia rotate-ip --geo US` |
| Check the connection | `aluvia status` |
| Return to the browser's original connection | `aluvia proxy-off` |

Reload the page after changing the connection. Turning the proxy on or off and rotating the IP keep the browser open. Use `proxy-off` to return to a direct connection. Stopping the daemon while Chrome still points to it can break browsing.

Commands return JSON. Read `next` for recovery instructions. If a page still fails with a working connection, try one IP rotation in the required country, then stop if it still fails. Respect retry periods for 429 or 1015 rate limits. See [troubleshooting](https://aluvia.io/docs).

## Pricing

The plugin is free to install and use. There is no plugin fee or paid plugin tier.

Aluvia's separate proxy service includes **10 MB of free proxy data**, with no account, API key, or payment required to start. After that, proxy/network data costs **$2/GB**. This charge is for network data, not access to the plugin.

If the CLI returns `payment_required`, the agent shows the returned `claim_url`. You decide whether to create an account and buy data. The agent can run `aluvia auth login` to wait for your action. It must not buy data for you.

## Security and privacy

- The plugin supplies Markdown instructions and static assets. It has no runtime or telemetry of its own.
- The CLI is installed separately from npm and runs locally on the browser's host. While enabled, it sends that browser's traffic through the selected proxy. This affects all tabs in the configured browser.
- Setup can restart Chrome and writes local CLI state and skill files. The free trial uses an install identifier. The CLI contacts Aluvia's service for trial, connection, account, and usage functions. An installation can also send setup and first-request attribution events when an attribution token is configured.
- Never print API keys, install identifiers, proxy passwords, or credential-bearing proxy URLs in chat, logs, issues, or screenshots. Use the CLI's account claim flow for paid continuation.

Read [Security](SECURITY.md), [Aluvia's Privacy Policy](https://aluvia.io/privacy-policy), and [Terms and Conditions](https://aluvia.io/terms-and-conditions). These service policies apply to Aluvia's proxy service. The plugin source is [MIT licensed](LICENSE).

## Test the plugin locally

From a checkout of this repository, copy the plugin to Cursor's local plugin directory. This command stops if an install already exists, so you can back it up first:

```bash
mkdir -p "$HOME/.cursor/plugins/local"
if [ -e "$HOME/.cursor/plugins/local/aluvia" ] || [ -L "$HOME/.cursor/plugins/local/aluvia" ]; then
  echo "An Aluvia local install already exists. Back it up before replacing it."
else
  mkdir "$HOME/.cursor/plugins/local/aluvia" &&
  cp -R .cursor-plugin skills assets README.md CHANGELOG.md LICENSE SECURITY.md SUBMIT.md \
    "$HOME/.cursor/plugins/local/aluvia/"
fi
```

1. Restart Cursor or run **Developer: Reload Window** from the command palette.
2. Open **Customize** and confirm Aluvia contains one skill named `aluvia` and no other components. On versions with the older settings layout, inspect **Rules, Skills, Subagents**.
3. Open the plugin's `aluvia` skill and confirm its file comes from `~/.cursor/plugins/local/aluvia/skills/aluvia/SKILL.md`. If other Aluvia user skills exist, distinguish them from the plugin copy. You can use **Try in Chat** to check invocation without running setup.
4. For an end-to-end check on a compatible test browser host, run setup, select a country, reload a page, inspect the requested content, and return to a direct connection with `aluvia proxy-off`.

Local plugin imports must be allowed by your Cursor organization. An installed marketplace plugin with the same name takes precedence over the local copy. See [Cursor's local testing instructions](https://cursor.com/docs/plugins#test-plugins-locally).

## Repository format and maintenance

This is a single Cursor plugin at the repository root. Its only manifest is `.cursor-plugin/plugin.json`. Version 1.1.0 replaces the root Agent Plugins manifest to make this repository unambiguous for Cursor review. No multi-plugin marketplace manifest is needed.

The manifest follows the [Cursor reference](https://cursor.com/docs/reference/plugins), [official schema](https://github.com/cursor/plugins/blob/main/schemas/plugin.schema.json), and `starter-simple` conventions. `displayName`, `category`, and `tags` also appear in official plugin manifests. The category `developer-tools` is used by Cursor's CLI plugin.

For validation, parse the manifest against that schema, check that `logo` and `skills` resolve inside the repository, and check skill frontmatter for `name` and `description`. Run `git diff --check`, scan public files for unsupported claims and credentials, then perform the local test above. The template's `scripts/validate-template.mjs` requires a multi-plugin `marketplace.json`; it does not apply directly to this single-plugin layout. No template validator or runtime script is bundled here.

The skill's command flow was checked against the [shipping source skill](https://github.com/aluvia-connect/aluvia/blob/64163e75631dcf3c9bdcf1c624180af996f817d8/skills/aluvia/SKILL.md), the published `aluvia-cli@1.4.12` package, and [live product docs](https://aluvia.io/docs) on September 12, 2026. Where bundled wording is stale, this plugin follows current product facts and CLI behavior. In particular, it uses residential-only claims, optional setup URLs, and connection checks that do not imply website access. Setup also installs the skill bundled with its CLI version; that file can differ from this plugin's skill.

Publisher submission steps and listing copy are in [SUBMIT.md](SUBMIT.md). Aluvia LLC maintains this plugin under the [aluvia-connect organization](https://github.com/aluvia-connect). For help, contact [support@aluvia.io](mailto:support@aluvia.io).
