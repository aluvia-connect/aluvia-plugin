# Aluvia

This plugin is the Aluvia skill for Cursor and Grok Bot. It tells an agent when to pick a country for Chrome.

The product is a local CLI. A cloud agent picks a country, and the existing browser leaves through a residential or mobile IP there. Country only, not city.

Homepage: [https://aluvia.io](https://aluvia.io)  
Docs: [https://aluvia.io/docs](https://aluvia.io/docs)

## Install

Once per machine. Node.js 18 or later.

```bash
npx aluvia-cli setup
```

If `aluvia` is not on PATH, prefix later commands with `npx aluvia-cli`.

| Goal | Command |
| --- | --- |
| Use Aluvia | `aluvia proxy-on` then reload |
| Pick a country | `aluvia geos`, then `aluvia proxy-on --geo US`, then reload |
| New exit IP | `aluvia rotate-ip` then reload |
| Back to the VM IP | `aluvia proxy-off` then reload |

Every command prints JSON on stdout. Follow `next`. Never print API keys.

## Pricing

The first 10 MB is free, started from an install id. No account and no API key to begin. After that, Aluvia network data is $2/GB. That is proxy data, not a plugin fee.

## This plugin is skill-only

Not an MCP. Not a human VPN. Not streaming. Not a login bypass.

## Local test

Copy this folder to `~/.cursor/plugins/local/aluvia` (copy, do not symlink off that directory). Reload, then confirm the Aluvia skill in Customize.
