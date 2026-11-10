# IRBANK Connect

IRBANK Connect retrieves factual data about Japanese listed companies through 13 read-only MCP tools. It supports financial research, company comparisons and screening by user-specified criteria. It does not execute trades, place orders, or provide investment advice.

日本の上場企業の財務・株価・開示情報を、AIとの対話から確認できます。13個のツールはすべて読み取り専用です。売買・発注・投資助言は行いません。

## Account and usage limits

An IRBANK account with name and address registration is required. Sign in only at [IRBANK](https://app.irbank.net/login); complete the registration at [MCP / API settings](https://app.irbank.net/mcp-api). Do not put credentials, tokens, names or addresses into chat messages or repository files.

The plugin package has no separate installation fee. As of November 10, 2026, IRBANK provides a free account tier with 200 combined MCP/API calls per day. Optional paid IRBANK plans provide 1,000 calls/day (Standard) or 4,000 calls/day (Pro). A single AI question can invoke more than one tool call. See the [current plan and usage details](https://irbank.net/article/irbank/new-irbank-official-release-20261109/) for service terms and changes. Marketplace acceptance of these optional paid service tiers is subject to the provider's review.

IRBANKアカウントへのログインと、氏名・住所の登録後に利用できます。無料プランではMCP・APIを合計1日200回まで利用できます。有料プランでは利用上限が異なります。AIへの質問1回で複数回の取得が発生する場合があります。

## Connection

- Remote endpoint: `https://api.irbank.net/mcp/market`
- Transport: Streamable HTTP
- Authentication: OAuth with Dynamic Client Registration
- No manually entered client ID, client secret, API key or bearer token is bundled or required for this OAuth configuration.

After enabling the plugin, use the client's MCP sign-in flow. Sign in to IRBANK, review the requested access, and grant permission in the browser. If name/address registration is requested, complete it on the IRBANK website and retry the connection.

### Cursor

This repository includes a native `.cursor-plugin/plugin.json`, a setup skill, and an always-applied rule scoped to IRBANK Connect requests. The manifest explicitly points to the shared `mcp_config.json` file. For local testing, copy this directory to `~/.cursor/plugins/local/irbank-connect`, reload Cursor, and inspect the plugin and MCP connection in Customize. Follow [Cursor's plugin documentation](https://cursor.com/docs/plugins) for installation and current UI steps.

### Antigravity

The `.antigravity-plugin/plugin.json` manifest, `mcp_config.json` and `rules/irbank-scope.md` provide the Antigravity configuration.

```sh
agy plugin validate --strict ./irbank-connect-plugin
agy plugin install ./irbank-connect-plugin
agy plugin list --json
```

Then complete the IRBANK OAuth sign-in when prompted. See [Antigravity's plugin guide](https://antigravity.google/docs/build-plugins).

## Included tools

| Tool | Purpose |
| --- | --- |
| `get_organization` | Company profile and summary |
| `get_financials` | Annual and quarterly financial history |
| `screen_securities` | Screen Japanese companies by specified criteria |
| `get_price_history` | Daily prices and adjusted close |
| `get_valuation_metrics_history` | Valuation history |
| `list_disclosures` | Find disclosure documents |
| `get_disclosure` | Retrieve disclosure metadata and sections |
| `get_disclosure_text_block` | Retrieve disclosure text |
| `list_shareholders` | Major shareholders |
| `list_segments` | Segment financial data |
| `list_dividend_history` | Dividend history |
| `get_weekly_margin_balance` | Weekly exchange margin balances |
| `get_jsf_margin_daily` | Daily JSF margin and stock-loan data |

Read the [tool reference](https://irbank.net/article/irbank/connect-tools/) for parameters and supported fields. Use returned company identifiers and units. Preserve attribution and do not fabricate missing values or URLs. Non-Japanese equities such as AAPL are outside this MCP package's scope.

## Examples

- 「トヨタ自動車の過去10年の売上高・営業利益・純利益の推移を教えてください。」
- 「配当利回り3%以上、PER15倍以下の日本株を、配当利回り順に10件まで表示してください。」
- 「ソニーグループのセグメント別営業利益を確認してください。」

The test plan in [docs/test-cases.md](docs/test-cases.md) includes five factual workflows and three out-of-scope cases. A test plan is not a record of completed client testing.

## Support, privacy and terms

- [Setup documentation](https://irbank.net/article/irbank/howto-connect/)
- [Support](https://corp.irbank.net/contact/)
- [Privacy policy](https://corp.irbank.net/privacypolicy/)
- [Service terms](https://corp.irbank.net/terms/)

Contact support for production data-retention or deletion questions not addressed in the published policy. This package does not make additional claims about service-side retention or AI training.

## License

The files in this repository are distributed under the MIT License. The hosted IRBANK service, server implementation and underlying datasets are not included and are governed by their applicable terms. IRBANK names and logos remain trademarks of their respective owner; the MIT copyright license does not grant trademark rights or imply endorsement of modified versions.

## Release status

Version 1.0.2 adapts the existing IRBANK Connect configuration for Cursor and Antigravity. Marketplace listing and approval are separate from availability of this repository. No marketplace endorsement is claimed.
