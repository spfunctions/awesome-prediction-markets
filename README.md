# Awesome Prediction Markets [![Awesome](https://awesome.re/badge-flat.svg)](https://awesome.re)

> APIs, datasets, tools, and research for building on prediction markets. For developers and AI agents, not dashboards.

Prediction markets are the best real-time source of calibrated probability for world events. This list focuses on what you need to **build** with that data — APIs to fetch it, tools to process it, datasets to train on, and research to understand it.

Pull requests welcome. See [contributing guidelines](#contributing).

## Contents

- [Exchanges & Platforms](#exchanges--platforms)
- [APIs & SDKs](#apis--sdks)
- [MCP Servers](#mcp-servers)
- [CLI Tools](#cli-tools)
- [Agent Frameworks & Examples](#agent-frameworks--examples)
- [Data & Datasets](#data--datasets)
- [Aggregators & Cross-Venue](#aggregators--cross-venue)
- [Analytics & Research Tools](#analytics--research-tools)
- [Selected Reading](#selected-reading)
- [Academic Papers](#academic-papers)
- [Community](#community)

---

## Exchanges & Platforms

Active prediction market platforms with programmatic access.

| Platform | API | Markets | Settlement |
|----------|-----|---------|------------|
| [Kalshi](https://kalshi.com) | [REST + WebSocket](https://trading-api.readme.io/reference/getting-started) | Economics, politics, weather, science | CFTC-regulated, USD |
| [Polymarket](https://polymarket.com) | [CLOB API](https://docs.polymarket.com) | Politics, crypto, global events | Polygon, USDC |
| [Metaculus](https://metaculus.com) | [API](https://www.metaculus.com/api/) | Science, technology, geopolitics | Reputation-based |
| [Manifold Markets](https://manifold.markets) | [API](https://docs.manifold.markets/api) | Anything (user-created) | Play money + sweepstakes |
| [PredictIt](https://predictit.org) | [API](https://www.predictit.org/api/marketdata/all/) | US politics | CFTC no-action letter, USD |
| [Smarkets](https://smarkets.com) | [API](https://docs.smarkets.com/) | Politics, sports, current affairs | UK-regulated, GBP |
| [Futuur](https://futuur.com) | API | Global events | Play money + real money |
| [Insight Prediction](https://insightprediction.com) | API | Global events | Crypto |

## APIs & SDKs

### Multi-Venue

- [SimpleFunctions API](https://simplefunctions.dev/docs) — Unified REST API for Kalshi + Polymarket. Thesis management, edge detection, what-if scenarios, track record feedback. Free during beta.
- [SimpleFunctions CLI](https://github.com/spfunctions/simplefunctions-cli) — 42 terminal commands for prediction market intelligence. Scan, watch, trade, agent mode.

### Kalshi

- [Kalshi Official API](https://trading-api.readme.io/reference/getting-started) — REST + WebSocket. Requires account for trading endpoints; market data is public.
- [kalshi-python](https://github.com/Kalshi/kalshi-python) — Official Python client.
- [KalshiClientsGo](https://github.com/Kalshi/kalshi-clients) — Official Go client.
- [kalgon](https://github.com/jkerkhoff/kalgon) — Unofficial Python SDK with order management.

### Polymarket

- [Polymarket CLOB API](https://docs.polymarket.com) — Central limit order book. REST + WebSocket.
- [py-clob-client](https://github.com/Polymarket/py-clob-client) — Official Python client for the CLOB.
- [clob-client](https://github.com/Polymarket/clob-client) — Official TypeScript client.
- [polymarket-rs](https://github.com/Polymarket/polymarket-rs) — Rust SDK.

### Metaculus

- [Metaculus API](https://www.metaculus.com/api/) — Public question and forecast data.
- [metaculusr](https://github.com/logicalclocks/metaculusr) — R client for Metaculus data.

### Manifold

- [Manifold API](https://docs.manifold.markets/api) — Full market CRUD, betting, comments.
- [manifoldpy](https://github.com/vluzko/manifoldpy) — Python client.
- [PyManifold](https://github.com/gappleto97/PyManifold) — Alternative Python client.

## MCP Servers

Connect LLMs to prediction market data via the Model Context Protocol.

- [SimpleFunctions MCP](https://simplefunctions.dev/api/mcp/mcp) — 25 tools: thesis management, edge detection, market search, trading, what-if scenarios. Works with Claude Code, Cursor, Windsurf.
  ```bash
  claude mcp add simplefunctions --url https://simplefunctions.dev/api/mcp/mcp
  ```
- [prediction-market-mcp-example](https://github.com/spfunctions/prediction-market-mcp-example) — Minimal 50-line MCP server for learning. Search markets, get context, price changes.

## CLI Tools

- [SimpleFunctions CLI](https://github.com/spfunctions/simplefunctions-cli) — `sf scan`, `sf edges`, `sf watch`, `sf agent`, `sf intent`. Covers Kalshi + Polymarket.
  ```bash
  npm i -g @spfunctions/cli && sf setup
  ```
- [polymarket-cli](https://github.com/polymarket/polymarket-cli) — Official Polymarket CLI for order placement.

## Agent Frameworks & Examples

Building AI agents that reason over prediction market data.

### Frameworks

- [LangChain](https://github.com/langchain-ai/langchain) — Wrap any prediction market API as a LangChain tool. [SimpleFunctions integration guide](https://simplefunctions.dev/technicals/langchain-prediction-market-agent).
- [CrewAI](https://github.com/joaomdmoura/crewAI) — Multi-agent crews for market analysis. [SimpleFunctions integration guide](https://simplefunctions.dev/technicals/crewai-prediction-market-agent).
- [AutoGen](https://github.com/microsoft/autogen) — Microsoft's multi-agent framework. Works with any REST API.
- [OpenAI Agents SDK](https://github.com/openai/openai-agents-python) — Lightweight agent framework with handoffs and guardrails.

### Example Projects

- [prediction-market-context](https://github.com/spfunctions/prediction-market-context) — Fetch structured market context for any LLM. One function call.
- [causal-tree-decomposition](https://github.com/spfunctions/causal-tree-decomposition) — Standalone probability engine. Decompose a thesis into a causal tree, compute weighted confidence.
- [kalshi-price-monitor](https://github.com/spfunctions/kalshi-price-monitor) — Terminal price alert monitor for Kalshi markets.
- [polymarket-marketmaking](https://github.com/elielieli909/polymarket-marketmaking) — Market making bot for Polymarket.
- [nevbot](https://github.com/neverix/nevbot) — Manifold market maker using OpenAI to answer questions.

## Data & Datasets

### Live Data

- [SimpleFunctions `/api/changes`](https://simplefunctions.dev/api/changes) — Real-time cross-venue price changes. No auth required.
- [SimpleFunctions `/api/public/context`](https://simplefunctions.dev/api/public/context) — Structured market context for any topic. No auth required.
- [Kalshi Market Data](https://trading-api.readme.io/reference/getmarkets-1) — All active markets, orderbook, trade history.
- [Polymarket CLOB Data](https://docs.polymarket.com/#get-markets) — Markets, orderbook, trades.
- [Metaculus API](https://www.metaculus.com/api/) — Questions, forecasts, community predictions.
- [MetaForecast](https://metaforecast.org/) — Aggregated forecasts across platforms.

### Historical Datasets

- [Kalshi Historical Data](https://kalshi.com/history) — Settlement data for resolved markets.
- [Polymarket Subgraph](https://thegraph.com/hosted-service/subgraph/polymarket/polymarket-matic) — On-chain data via The Graph.
- [Manifold Markets Data](https://docs.manifold.markets/api#get-v0markets) — Full market history including bets.
- [Good Judgment Open](https://www.gjopen.com/) — Crowd forecasting data with track records.
- [Metaculus Data Export](https://www.metaculus.com/questions/download/) — Historical question and resolution data.

## Aggregators & Cross-Venue

- [SimpleFunctions](https://simplefunctions.dev) — Kalshi + Polymarket unified. Edge detection across venues.
- [MetaForecast](https://metaforecast.org/) — Aggregates Metaculus, Polymarket, Manifold, Good Judgment, and more.
- [Oddpool](https://oddpool.com) — Cross-venue odds, spreads, liquidity, arbitrage detection.
- [BaseRateTimes](https://baseratetimes.com) — News through the lens of prediction markets.
- [Electionbettingodds.com](https://electionbettingodds.com) — Aggregated political prediction market odds.

## Analytics & Research Tools

- [Polymarket Analytics](https://www.loki.red/polymarket/) — Market stats and analytics.
- [PolymarketStats](https://github.com/bodino/PolymarketStats) — Open source Polymarket analytics.
- [Kalshi Research](https://kalshi.com/research) — Market insights and analysis from Kalshi.

## Selected Reading

### Primers

- [Prediction Market FAQ](https://astralcodexten.substack.com/p/prediction-market-faq) — Scott Alexander's comprehensive overview.
- [Information Markets, Decision Markets, Attention Markets, Action Markets](https://astralcodexten.substack.com/p/information-markets-decision-markets) — Taxonomy of market types.
- [The Making of a Top Forecaster](https://www.infer-pub.com/blog/top-forecaster-techniques) — Techniques from top INFER forecasters.
- [Play Money and Reputation Systems](https://astralcodexten.substack.com/p/play-money-and-reputation-systems) — When play money markets work.

### Strategy & Structure

- [Market Mechanics](https://manifoldmarkets.substack.com/p/above-the-fold-market-mechanics) — How prediction market mechanics work.
- [Incentive Problems with Forecasting](https://www.lesswrong.com/posts/tyNrj2wwHSnb4tiMk/incentive-problems-with-current-forecasting-competitions) — Why prediction markets have structural biases.
- [Amplifying Research via Forecasting (Part 1)](https://www.lesswrong.com/posts/cLtdcxu9E4noRSons) and [Part 2](https://www.lesswrong.com/posts/FeE9nR7RPZrLtsYzD/part-2-amplifying-generalist-research-via-forecasting) — Using forecasters to evaluate research claims.

### AI & Prediction Markets

- [Building World-Aware Agents with Prediction Market Data](https://simplefunctions.dev/technicals/mcp-server-prediction-markets-claude-code) — Using MCP to give agents market intelligence.
- [LLMs as Forecasters](https://arxiv.org/abs/2402.18563) — Can language models predict the future?
- [Approaching Human-Level Forecasting with Language Models](https://arxiv.org/abs/2402.18563) — GPT-4 calibration on forecasting tasks.

## Academic Papers

- [Prediction Markets: Theory, Evidence, and Applications](https://doi.org/10.1257/jep.18.2.107) — Wolfers & Zitzewitz (2004). The canonical survey.
- [The Wisdom of Crowds](https://doi.org/10.1257/jel.20221713) — Surowiecki. Why aggregated forecasts beat experts.
- [Prediction Markets for Economic Forecasting](https://doi.org/10.1016/B978-0-444-53683-9.00010-4) — Handbook chapter on using markets for macro forecasting.
- [Manipulating Prediction Markets: Evidence from the Field](https://doi.org/10.1016/j.jfineco.2017.06.001) — How hard is it to move a prediction market?
- [Information Aggregation in Dynamic Markets with Strategic Traders](https://doi.org/10.1111/j.1468-0262.2005.00553.x) — Ostrovsky (2012). Theory of information aggregation.

## Community

- [Metaculus Community](https://metaculus.com) — Active forecasting community with scoring and track records.
- [r/predictionmarkets](https://reddit.com/r/predictionmarkets) — Reddit community.
- [Manifold Discord](https://discord.gg/manifold) — Active developer community.
- [Polymarket Discord](https://discord.gg/polymarket) — Trading and data discussion.
- [Scott Alexander's Mantic Monday](https://astralcodexten.substack.com/) — Weekly prediction market commentary.

---

## Contributing

1. Fork this repo
2. Add your resource to the appropriate section
3. Keep descriptions short (one line)
4. Include a link to source code or documentation
5. Submit a PR

**What belongs here:** APIs, SDKs, datasets, code, tools, research, papers. Things developers use to build.

**What doesn't belong:** Consumer dashboards, portfolio trackers, copy-trading services, news aggregators without an API. Check [Awesome Prediction Market Tools](https://github.com/aarora4/Awesome-Prediction-Market-Tools) for those.

## License

MIT
