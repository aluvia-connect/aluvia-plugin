# Security

Aluvia LLC maintains this plugin. Website: [aluvia.io](https://aluvia.io). Product documentation: [aluvia.io/docs](https://aluvia.io/docs).

## Report a vulnerability

Send reports about this plugin or the Aluvia CLI to [support@aluvia.io](mailto:support@aluvia.io). Include the affected version or commit, a description, the likely impact, and steps to reproduce. Remove API keys, install identifiers, proxy credentials, account details, and private browsing data.

Please report exploitable issues privately instead of opening a public issue. Aluvia LLC will investigate reports and coordinate fixes and disclosure with the reporter.

For issues with a Cursor Marketplace plugin, Cursor also accepts reports at [security-reports@cursor.com](mailto:security-reports@cursor.com). See [Cursor's marketplace security policy](https://cursor.com/help/security-and-privacy/marketplace-security).

## Scope and data handling

This repository contains one skill, metadata, documentation, and static logos. It contains no MCP server, connector, hook, or executable runtime. Installing the plugin alone does not launch a process or route browser traffic.

The skill guides an agent to install and run the separate `aluvia-cli` npm package on its browser's host. Setup writes local state, installs CLI skill files, starts a local proxy, and can restart Chrome. When enabled, the configured browser's traffic, including other tabs, uses the selected proxy. Use `aluvia proxy-off` to return to the original connection.

The CLI uses an install identifier for the free trial and contacts Aluvia for connection, account, and usage functions. Where an attribution token is configured, it can report setup and first-request attribution events. The plugin has no separate telemetry. Do not infer that local execution means all data stays on the host.

Never publish keys, install identifiers, passwords, or credential-bearing proxy URLs. Use sanitized command results for support. Read the [Privacy Policy](https://aluvia.io/privacy-policy) and [Terms and Conditions](https://aluvia.io/terms-and-conditions) for the proxy service.

## Maintenance

Use the latest plugin version and review [CHANGELOG.md](CHANGELOG.md) when updating. CLI releases are separate from plugin releases. Recheck CLI behavior and product claims when refreshing the skill.

Cursor manually reviews marketplace plugins and their updates. A repository change does not establish marketplace approval or mean an installed marketplace copy has updated.
