# Chris's submission checklist

Prepared September 12, 2026. Chris executes this checklist. Repository preparation and a pull request are not a marketplace submission or approval.

## Shared listing copy

| Field | Value |
| --- | --- |
| Display name | Aluvia |
| Handle / plugin name | `aluvia` |
| Organization / publisher | Aluvia LLC |
| Contact | [support@aluvia.io](mailto:support@aluvia.io) |
| Website | [aluvia.io](https://aluvia.io) |
| Documentation | [aluvia.io/docs](https://aluvia.io/docs) |
| GitHub organization | [aluvia-connect](https://github.com/aluvia-connect) |
| Repository | [aluvia-connect/aluvia-plugin](https://github.com/aluvia-connect/aluvia-plugin) |
| License | MIT, Copyright (c) 2026 Aluvia LLC |
| Plugin price | Free |
| Category, if offered | Developer Tools (`developer-tools`) |
| Keywords | aluvia, proxies, proxy, proxy-ip, datacenter-ip, residential-proxy, residential-proxies |
| PNG logo | [assets/logo.png on main](https://raw.githubusercontent.com/aluvia-connect/aluvia-plugin/main/assets/logo.png) |
| SVG logo | [assets/logo.svg on main](https://raw.githubusercontent.com/aluvia-connect/aluvia-plugin/main/assets/logo.svg) |
| Privacy | [Privacy Policy](https://aluvia.io/privacy-policy) |
| Service terms | [Terms and Conditions](https://aluvia.io/terms-and-conditions) |

**Short description**

Aluvia lets Grok Bot access websites through residential proxy IPs instead of its datacenter IP. Choose a country and help your browser workflows get past CAPTCHAs, bot blocks, and geo restrictions when the IP address is the cause.

**Long description**

Aluvia helps your cloud agent browse from the country you need. Use this skill with Cursor agents or Grok Bot when a website shows the wrong country's prices or catalog, or blocks the agent because of its datacenter IP. A residential IP in the right country sometimes clears a 403, CAPTCHA, or Cloudflare challenge. Access is not guaranteed.

Run `npx aluvia-cli setup` on the browser's host, then use `aluvia geos` and `aluvia proxy-on --geo US` to select an available country. Reload the page and check the content. Use `aluvia rotate-ip` for another IP, or `aluvia proxy-off` to return to the original connection. The CLI needs Node.js 18 or later, Chrome or Chromium, and command access to the browser's host. Initial setup can restart the browser.

The plugin is free and skill-only, with no MCP server or connector. The separate Aluvia proxy service includes 10 MB free without an account, API key, or payment to start. Further proxy/network data is $2/GB, not a plugin fee. The user decides whether to buy data. Country-level selection only. This is not a human VPN, streaming tool, login bypass, or fingerprint, TLS, or canvas bypass.

Publisher: Aluvia LLC. Contact: support@aluvia.io. Website: https://aluvia.io. Docs: https://aluvia.io/docs.

**Publisher / reviewer note**

Publisher: Aluvia LLC. Skill-only plugin (no MCP). Contact support@aluvia.io. The free MIT plugin provides one agent skill. The CLI is a separate npm package that runs locally on the browser's host and routes the configured browser's traffic through a proxy. All tabs in that browser are affected. Proxy data beyond the 10 MB trial is a separate $2/GB service charge. No plugin access fee applies.

## Before either submission

- [ ] Review and merge the PR into `main` when satisfied. Use the merged commit, not an unmerged branch or the old root manifest.
- [ ] Confirm the repository is public and `.cursor-plugin/plugin.json`, README, skill, MIT license, SECURITY, and both logos are visible on `main`.
- [ ] Record the merged commit SHA. In a fetched checkout: `git rev-parse origin/main`. Compare it with `git ls-remote origin refs/heads/main`.
- [ ] Open both raw logo links above after merge. Confirm they show the square Aluvia mark.
- [ ] Review the PR's validation proof. Complete any outstanding Cursor reload or browser-host check from the README. Check the target page before claiming the proxy workflow succeeded.
- [ ] Confirm the listing has the company contact and the free-plugin / paid-data distinction. Review the current publisher terms before accepting them.

## A. Official Cursor Marketplace

- [ ] Open [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish). Use the plugin flow in Grok Bot Settings > Marketplace > Plugins where available.
- [ ] Expect Owner to show `Individual · biggyc@gmail.com` for Chris's signed-in account. This account label is expected from Chris's current form context. Cursor staff describe company switching as a limitation of that form. Keep Aluvia LLC in the organization field, manifest author, README, license, and reviewer note.
- [ ] Enter the shared identity fields above: organization **Aluvia LLC**, handle **aluvia**, contact **support@aluvia.io**, website **https://aluvia.io**, and the plugin repository URL.
- [ ] Include the merged commit SHA in the review notes, plus the raw logo URL and publisher note above. Select free for the plugin price wherever asked.
- [ ] Review the completed application. Chris accepts any terms and clicks Submit.
- [ ] Save the confirmation screenshot, submission date, repo URL, commit SHA, and any application ID in Chris's private records.
- [ ] If a status follow-up is needed, Chris emails [marketplace-publishing@cursor.com](mailto:marketplace-publishing@cursor.com) with plugin name `aluvia`, repo URL, submission date, and application ID. Do not send repeated applications.

Cursor describes the marketplace as curated and manually reviews plugins for security, data handling, and quality. Its publisher terms also describe identity and business legitimacy checks. All marketplace plugins must be open source, and updates are reviewed. These are published requirements, not a promise of approval. [Security policy](https://cursor.com/help/security-and-privacy/marketplace-security), [Publisher Terms](https://cursor.com/marketplace-publisher-terms).

## B. cursor.directory

- [ ] Open [cursor.directory/plugins/new](https://cursor.directory/plugins/new).
- [ ] Try the GitHub repository import with the same repository URL. The current page offers automatic detection or manual entry. If import does not recognize the single Cursor manifest, use manual entry with the fields above.
- [ ] Use **Aluvia LLC**, **support@aluvia.io**, and the same website, docs, logo, license, and pricing disclosure. Do not accept an imported personal author or a paid-plugin label without correcting it.
- [ ] Choose the closest actual category offered by the form. Do not invent a category value if Developer Tools is absent.
- [ ] Review the listing preview, then Chris submits and saves the confirmation, date, and listing URL.

Directory and the official Marketplace are separate submission queues. A submission to one does not submit to or establish approval in the other. The two submissions can coexist. Cursor staff recommend Directory as the faster community path; this is routing advice, not a review-time guarantee. [Staff guidance](https://forum.cursor.com/t/cursor-plugin-submission/166867/5), [company submission discussion](https://forum.cursor.com/t/cursor-plugin-submit-as-company-not-individual/156274).

## C. Do not

- Add MCP, connectors, hooks, rules, or agents to make this plugin appear more complete.
- Charge for plugin installation, access, or use through the Marketplace. Keep proxy data pricing separate and visible. See Publisher Terms section 3.1.
- Claim guaranteed access, city selection, unlisted carrier coverage, or a login or browser-signature bypass.
- Claim marketplace approval, a review deadline, or unpublished review criteria.
- Submit or resubmit without Chris, accept terms for him, send outreach, or post about a listing before he accepts it.

## Reference check

The repository preparation used these sources in order, checked September 12, 2026:

1. [Cursor plugins overview](https://cursor.com/docs/plugins).
2. [Cursor plugin reference and submission checklist](https://cursor.com/docs/reference/plugins).
3. [Marketplace security](https://cursor.com/help/security-and-privacy/marketplace-security).
4. [Publisher Terms](https://cursor.com/marketplace-publisher-terms), particularly sections 2.2, 3.1, and 4.5.
5. [Plugin template](https://github.com/cursor/plugin-template), including README, `docs/add-a-plugin.md`, `starter-simple`, and the template validator. Revision: `46216072ac5750f782f95bb325b4d12b7c3ae9c9`.
6. [Official plugins](https://github.com/cursor/plugins), including `create-plugin`, `cli-for-agent`, `grok-voice`, and the JSON schema. Revision: `889ec4b68fa5aab0e867dad71ec3fdf386ae48f3`.
7. [Live product](https://aluvia.io) and [llms.txt](https://aluvia.io/llms.txt), then the shipping CLI package and source skill.
8. [Current plugin repository](https://github.com/aluvia-connect/aluvia-plugin). Starting revision: `9b99388`.

The upstream template validator assumes a multi-plugin marketplace file. This repository intentionally has no such file. Validation uses the official single-plugin schema, path and frontmatter checks, copy and credential review, and a local Cursor install. See the PR for actual results and any limits.
