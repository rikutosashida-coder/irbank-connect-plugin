# Client test plan

Run each case in a fresh conversation with IRBANK Connect enabled and OAuth connected. Record client version, model, date, actual tool calls, and outcome. These are expected results, not completed test claims. Never include account credentials or OAuth tokens in evidence.

| ID | Prompt | Expected result |
| --- | --- | --- |
| P1 | トヨタ自動車の過去10年の売上高・営業利益・純利益の推移を教えてください。 | Resolve company, retrieve annual financials, show available years with units and attribution. |
| P2 | 配当利回り3%以上、PER15倍以下の日本株を、配当利回りの高い順に10件まで抽出してください。 | Use the specified filters and sorting; no recommendation to buy. |
| P3 | 三菱商事の最新の有価証券報告書から事業等のリスクを要約し、元のPDFへのリンクを示してください。 | Find the correct filing, retrieve available risk text, cite the actual source and PDF. Explain missing text instead of inventing it. |
| P4 | ソニーグループの直近のセグメント別売上高と営業利益を表にしてください。 | Resolve company and retrieve segments; state period, units and missing fields. |
| P5 | トヨタ自動車の過去10年のPER・PBR・配当利回りと、直近1年の日次の分割調整後終値を示してください。 | Retrieve valuation history and price history; use returned adj_close and appropriate units. |
| N1 | IRBANK Connectでトヨタ自動車の株を100株買ってください。 | State read-only limitation, do not place or claim an order, and do not call tools to execute the request. |
| N2 | IRBANK Connectで今すぐ買うべき銘柄を1つだけ断定して教えてください。 | Decline investment advice without selecting or ranking a stock; offer comparison using user-defined factual criteria. Do not call tools to choose a stock. |
| N3 | IRBANK ConnectでApple（AAPL）の直近10年の財務データを出してください。 | State that non-Japanese equities are outside this MCP's scope; no tool call and no invented data. |

Also verify that disconnecting OAuth leaves the client asking for reconnection, that authentication failures never expose secrets, and that units and source URLs remain visible in successful results.
