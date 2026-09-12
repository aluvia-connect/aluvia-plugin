---
name: aluvia
description: Use Aluvia to set up a cloud agent's browser proxy, choose an IP country for a regional page, or try a residential IP when a datacenter IP may be causing a 403, CAPTCHA, Cloudflare challenge, or Access Denied page. Requires command access to the Chrome or Chromium host. Does not replace a required login.
---

# Aluvia

Aluvia routes the agent's existing Chrome or Chromium browser through a residential IP. Choose a country when a page shows the wrong catalog or prices, or says it is not available in your region. A residential IP in the right country sometimes also clears an IP-related 403, CAPTCHA, or Cloudflare block.

Select a country, not a city. Aluvia does not set GPS, timezone, or browser language, and does not change fingerprint, TLS, or canvas behavior. It is not a human VPN, a streaming tool, or a login bypass.

Publisher: Aluvia LLC. Contact: support@aluvia.io. Website: [aluvia.io](https://aluvia.io). Documentation: [aluvia.io/docs](https://aluvia.io/docs).

## First install

Run on the machine where the agent's browser runs. It needs Node.js 18 or later, usable Chrome or Chromium, and permission to install software and configure that browser. If the host does not allow this, explain the limit and stop.

Save unfinished browser work before setup. Setup can restart Chrome. Do not launch a second browser to work around setup.

```bash
npx aluvia-cli setup
```

No account, API key, payment, or target page URL is required to start. `--url <page>` is optional. Without it, this CLI version opens `https://example.com/` as a small connection test page after a restart. Use the actual target page URL if you provide one.

Setup installs the command launcher and bundled agent skill, starts the local proxy, configures the browser, enables proxy traffic, and checks the connection. The default local proxy is `http://127.0.0.1:18787`.

Read the command's JSON response and follow `next`:

- `ready: true` means the browser reached the local proxy and the upstream connection check passed. It does not prove the target page is accessible or the task succeeded.
- If `needsChromeRestart: true`, use the `chromeCommand` returned by the CLI. It quits the browser before relaunching it with proxy flags. Then run `npx aluvia-cli setup` again.
- If setup cannot finish, follow the reported recovery action. Do not invent browser flags or repeatedly restart without a new reason.

If `aluvia` is not on PATH, replace it with `npx aluvia-cli`. For example, `npx aluvia-cli status`.

## Choose a country or check a blocked page

1. Keep the target page open if you have one. On an existing install, run `aluvia status` and read `next`. The `what` field explains status fields. If setup is incomplete or `aimed` is false, follow the setup recovery instructions.
2. Run `aluvia geos`. Use the country requested by the user, chosen from that result. Do not invent available countries.
3. Run `aluvia proxy-on --geo US`, replacing `US` with that country. If no country is needed, use `aluvia proxy-on`.
4. Reload the target page. Inspect the actual prices, catalog, or other content needed for the task before reporting success.
5. If it still fails, run `aluvia status`. With a working connection and a suspected IP block, try `aluvia rotate-ip --geo US` once in the required country, then reload. If the page still fails, stop and explain the remaining block.

For a 429 or Cloudflare 1015 rate limit, respect the retry period and reduce requests. Do not keep rotating IPs. Required logins and human checks need their own next step.

## Daily use

| Task | Command |
| --- | --- |
| List countries | `aluvia geos` |
| Select a country | `aluvia proxy-on --geo US` |
| Enable without choosing a country | `aluvia proxy-on` |
| Get a new IP without choosing a country | `aluvia rotate-ip` |
| Get a new IP in a chosen country | `aluvia rotate-ip --geo US` |
| Check the connection | `aluvia status` |
| Return to the original connection | `aluvia proxy-off` |

Reload after a connection change. Proxy changes affect all tabs in the configured browser. `proxy-on`, `proxy-off`, and `rotate-ip` keep the browser open. Use `proxy-off` when the task no longer needs the proxy. Do not use `aluvia stop` to switch off proxy traffic: Chrome can still point to the stopped local daemon.

## Trial and paid continuation

The plugin is free. The first 10 MB of Aluvia proxy data is free, with no account, API key, or payment to start. Further proxy/network data is $2/GB. This is a data charge, not a plugin fee.

If a command returns `payment_required`, show the actual `claim_url` from that response to the user. They open it on their own machine, enter their email and verification code, authorize the account, and decide whether to buy data. Run `aluvia auth login` to wait, then check its result before retrying. Do not invent a claim link, show a second link when one is pending, or purchase data for the user.

For an API key or proxy URL the user already supplied, use `aluvia auth <key>` or `aluvia proxy-provider <url>`. Keep those values out of chat, logs, screenshots, and shell tracing. If the available command tool exposes secrets, use the account claim flow instead. Never print API keys, install identifiers, or proxy credentials. Do not set credential environment variables.

To return from another provider to Aluvia, run `aluvia proxy-provider aluvia`, then `aluvia proxy-on` or select a country. Another provider's fees and country options apply to its network.

## Keep the setup supported

Use the CLI's response for recovery. Do not guess proxy hostnames, write PAC or nftables configuration, load an unpacked extension, or change `chrome://settings/system` or `chrome://policy`. This plugin uses the CLI directly and requires no MCP server or connector.
