# Awesome Prediction Markets [![Awesome](https://awesome.re/badge-flat.svg)](https://awesome.re)

> APIs, datasets, tools, and research for building on prediction markets. For developers and AI agents, not dashboards.

Prediction markets are the best real-time source of calibrated probability for world events. This list focuses on what you need to **build** with that data — APIs to fetch it, tools to process it, datasets to train on, and research to understand it.

Pull requests welcome. See [contributing guidelines](#contributing).

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/spfunctions/awesome-prediction-markets/blob/main/simplefunctions_quickstart.ipynb) — Interactive notebook: world state, market search, trade ideas, contagion detection, and more.

## Quick Start — Get a Price in 30 Seconds

```bash
# Kalshi — what are the markets?
curl -s "https://trading-api.kalshi.co/trade-api/v2/markets?limit=3" | jq '.markets[] | {title, yes_ask, volume}'

# Polymarket — current markets
curl -s "https://clob.polymarket.com/markets?limit=3" | jq '.[] | {question, tokens[0].price}'

# SimpleFunctions — scan any topic, no auth
curl -s "https://simplefunctions.dev/api/public/scan?q=oil"

# SimpleFunctions — what changed in the last hour
curl -s "https://simplefunctions.dev/api/changes"
```

## API Comparison

Which platform fits your use case?

| | [Kalshi](https://kalshi.com) | [Polymarket](https://polymarket.com) | [Metaculus](https://metaculus.com) | [Manifold](https://manifold.markets) |
|---|---|---|---|---|
| **Auth for market data** | No | No | No | No |
| **Auth for trading** | API key + RSA | Wallet signature | N/A | API key |
| **WebSocket** | Yes | Yes | No | No |
| **Rate limit** | 100/min | 500/min | Undocumented | 1000/min |
| **Historical data** | Settlement CSV | Subgraph + API | Export | Full API |
| **Real money** | Yes (CFTC) | Yes (USDC) | No | Sweepstakes |
| **Market creation** | No (Kalshi only) | No (UMA only) | Community | Anyone |
| **Best for** | US regulated, macro | Crypto-native, global | Research, calibration | Experimentation |

## Contents

- [Exchanges & Platforms](#exchanges--platforms)
- [APIs & SDKs](#apis--sdks)
- [MCP Servers](#mcp-servers)
- [CLI Tools](#cli-tools)
- [Agent Frameworks & Examples](#agent-frameworks--examples)
- [Data & Datasets](#data--datasets)
- [Aggregators & Cross-Venue](#aggregators--cross-venue)
- [Economic & Macro Data](#economic--macro-data)
- [Analytics & Research Tools](#analytics--research-tools)
- [Tutorials & Guides](#tutorials--guides)
- [Strategy & Market Structure](#strategy--market-structure)
- [Selected Reading](#selected-reading)
- [Academic Papers](#academic-papers)
- [Project Ideas](#project-ideas)
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
- [us-gov-open-data-mcp](https://github.com/lzinga/us-gov-open-data-mcp) — 300+ tools across 40+ U.S. government APIs. FRED, Treasury, BLS, Congress, FDA, EPA, SEC. Selective module loading.
- [fred-mcp-server](https://github.com/kablewy/fred-mcp-server) — FRED economic data for Claude/Cursor.
- [mcp-fredapi](https://github.com/Jaldekoa/mcp-fredapi) — FRED API with series search and category browsing.
- [imf-data-mcp](https://github.com/c-cf/imf-data-mcp) — IMF economic data via SDMX 3.0 API.

## CLI Tools

- [SimpleFunctions CLI](https://github.com/spfunctions/simplefunctions-cli) — `sf scan`, `sf edges`, `sf watch`, `sf agent`, `sf intent`. Covers Kalshi + Polymarket.
  ```bash
  npm i -g @spfunctions/cli && sf setup
  ```
- [polymarket-cli](https://github.com/polymarket/polymarket-cli) — Official Polymarket CLI for order placement.

## Agent Frameworks & Examples

Building AI agents that reason over prediction market data.

### Frameworks

- [LangChain](https://github.com/langchain-ai/langchain) — Wrap any prediction market API as a LangChain tool. [Integration guide](https://simplefunctions.dev/technicals/langchain-prediction-market-agent).
- [CrewAI](https://github.com/joaomdmoura/crewAI) — Multi-agent crews for market analysis. [Integration guide](https://simplefunctions.dev/technicals/crewai-prediction-market-agent).
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

## Economic & Macro Data

The context layer for prediction markets — the economic indicators, government data, and macro signals that drive the events prediction markets trade on.

### Aggregator Platforms

- [OpenBB](https://github.com/OpenBB-finance/OpenBB) — Open-source financial data platform (65K+ stars). Covers FRED, World Bank, BLS, Eurostat, and hundreds of other data sources. Python, CLI, and AI agent integration.
- [pandas-datareader](https://github.com/pydata/pandas-datareader) — Extract data from FRED, World Bank, OECD, Eurostat, Stooq, and more into pandas DataFrames. The standard Python library for economic data access.
- [DBnomics](https://db.nomics.world/) — Aggregates 80+ statistical providers (central banks, national statistics offices, international organizations). [R client](https://github.com/dbnomics/rdbnomics), [Julia client](https://github.com/s915/DBnomics.jl), [Stata client](https://github.com/dbnomics-stata/dbnomics). Free API, no auth.
- [findatapy](https://github.com/cuemacro/findatapy) — Download market data from Bloomberg, Eikon, Quandl, FRED and more via a unified interface.

### FRED (Federal Reserve Economic Data)

- [fredapi](https://github.com/mortada/fredapi) — Python client for FRED. `pip install fredapi`. Supports series search, vintages, releases.
- [fredr](https://github.com/sboysel/fredr) — R client for FRED API. On CRAN.
- [fred-rs](https://github.com/mdsabo/fred-rs) — Rust crate for FRED.
- [fredcpp](https://github.com/nomadbyte/fredcpp) — C++ client for FRED.
- [FredApi.jl](https://github.com/markushhh/FredApi.jl) — Julia package for FRED.
- [fredric](https://github.com/DannyBen/fredric) — Ruby library and CLI for FRED.
- [fred-mcp-server](https://github.com/kablewy/fred-mcp-server) — MCP server for FRED data in Claude/Cursor.
- [mcp-fredapi](https://github.com/Jaldekoa/mcp-fredapi) — Another FRED MCP server with search and category browsing.

### Federal Reserve & Central Banks

- [FRB](https://github.com/avelkoski/FRB) — Python client for all Federal Reserve Bank data (not just FRED — includes flow of funds, financial accounts, survey data).
- [econ_data](https://github.com/bdecon/econ_data) — Python notebooks demonstrating FRED, BLS, Census, and BEA API usage with working examples.

### World Bank

- [wbdata](https://github.com/OliverSherouse/wbdata) — Python library for World Bank data. Tested: pulls GDP per capita for any country/date range. No auth.
- [world_bank_data](https://github.com/mwouts/world_bank_data) — Python library with pandas integration. Tested: pulls CPI inflation for US/CN/GB/BR. No auth.
- [WDI](https://github.com/vincentarelbundock/WDI) — R package for World Bank data. On CRAN, 250+ stars.
- [WorldBankData.jl](https://github.com/4gh/WorldBankData.jl) — Julia package for World Bank data.

### BLS (Bureau of Labor Statistics)

- [blscrapeR](https://github.com/keberwein/blscrapeR) — R package for BLS data (unemployment, CPI, wages). 117 stars.
- [blsAPI](https://github.com/mikeasilva/blsAPI) — R client for BLS API. 93 stars.
- [BLS-APIs](https://github.com/MPX0222/BLS-APIs) — Python wrapper for BLS v1/v2 APIs.
- BLS API v1 requires no auth key: `curl https://api.bls.gov/publicAPI/v1/timeseries/data/LNS14000000`

### IMF

- [IMFData](https://github.com/mingjerli/IMFData) — R package for IMF data. 49 stars.
- [imf-data-mcp](https://github.com/c-cf/imf-data-mcp) — MCP server for IMF economic data via SDMX 3.0 API.
- IMF API requires no auth: `https://data.imf.org` (SDMX 3.0)

### Eurostat

- [eurostat-api-client](https://github.com/opus-42/eurostat-api-client) — Python client for Eurostat data.
- [eurostat_downloader](https://github.com/alecsandrei/eurostat_downloader) — Python tool for bulk Eurostat downloads.
- Eurostat API requires no auth: `https://ec.europa.eu/eurostat/api/dissemination/statistics/1.0/data/`

### Multi-Agency / Government

- [us-gov-open-data-mcp](https://github.com/lzinga/us-gov-open-data-mcp) — MCP server + TypeScript SDK for **40+ U.S. government APIs** (300+ tools). Covers FRED, Treasury, BLS, Census, EPA, FDA, SEC, Congress, and more. 20+ APIs need no auth key. 94 stars.

### OECD

- OECD Data API requires no auth: `https://sdmx.oecd.org/public/rest/data/` (SDMX format)

## Analytics & Research Tools

- [Polymarket Analytics](https://www.loki.red/polymarket/) — Market stats and analytics.
- [PolymarketStats](https://github.com/bodino/PolymarketStats) — Open source Polymarket analytics.
- [Kalshi Research](https://kalshi.com/research) — Market insights and analysis from Kalshi.
- [PolyMind](https://polyminds.netlify.app/) — Real-time Polymarket trading alerts with multi-AI analysis. Track whale bets, volume spikes, and 12 signal types.

## Tutorials & Guides

### Getting Started

- [Your First Prediction Market Trade from CLI](https://simplefunctions.dev/technicals/first-prediction-market-trade-cli-walkthrough) — Step-by-step walkthrough from install to trade.
- [Kalshi API Quick Start (JavaScript + Python)](https://simplefunctions.dev/technicals/kalshi-api-quick-start-javascript-python) — Fetch markets, place orders, handle auth.
- [Connect an AI Agent to Prediction Markets in 5 Minutes](https://simplefunctions.dev/technicals/connect-ai-agent-prediction-market-5-minutes) — Fastest path to a working agent.
- [5 Ways to Connect Your AI Agent to Prediction Markets](https://simplefunctions.dev/blog/5-ways-to-connect-your-ai-agent-to-prediction-markets-in-2026) — MCP, REST, CLI, LangChain, CrewAI compared.

### Building Agents

- [How to Build a World-Aware Claude Agent](https://simplefunctions.dev/blog/how-to-build-a-world-aware-claude-agent) — MCP + Claude Code tutorial.
- [How to Build a World-Aware LangChain Agent](https://simplefunctions.dev/blog/how-to-build-a-world-aware-langchain-agent) — Python + LangChain tutorial.
- [How to Build a World-Aware CrewAI Crew](https://simplefunctions.dev/blog/how-to-build-a-world-aware-crewai-crew) — Multi-agent crew tutorial.
- [How to Build a World-Aware OpenAI Agent](https://simplefunctions.dev/blog/how-to-build-a-world-aware-openai-agent) — OpenAI Agents SDK tutorial.
- [How to Build a World-Aware Mistral Agent](https://simplefunctions.dev/blog/how-to-build-a-world-aware-mistral-agent) — Mistral + function calling tutorial.
- [Setting Up Your First Prediction Market Agent](https://simplefunctions.dev/technicals/setting-up-your-first-prediction-market-agent) — Architecture and design patterns.

### Trading Systems

- [How to Build a Prediction Market Trading Bot](https://simplefunctions.dev/blog/how-to-build-prediction-market-trading-bot-2026) — Full architecture from data to execution.
- [Thesis to Execution: Full Trading Loop](https://simplefunctions.dev/technicals/thesis-to-execution-full-trading-loop) — Create thesis → detect edges → size positions → execute.
- [Automate the Thesis Lifecycle](https://simplefunctions.dev/technicals/automate-thesis-lifecycle-create-monitor-trade) — Create, monitor, and trade automatically.
- [Running a 24/7 Trading Agent: Architecture & Costs](https://simplefunctions.dev/technicals/running-247-trading-agent-architecture-costs) — Infrastructure, monitoring, cost breakdown.
- [Pipe Prediction Market Signals into Your Trading System](https://simplefunctions.dev/technicals/pipe-prediction-market-signals-trading-system) — Webhooks, polling, event-driven.

### Orderbooks & Market Microstructure

- [Understanding Prediction Market Orderbooks](https://simplefunctions.dev/technicals/understanding-prediction-market-orderbooks-complete-guide) — Complete guide to reading and interpreting.
- [Reading Prediction Market Orderbooks](https://simplefunctions.dev/technicals/reading-prediction-market-orderbooks) — Practical guide with examples.
- [How to Scan Prediction Market Orderbooks](https://simplefunctions.dev/technicals/how-to-scan-prediction-market-orderbooks) — Programmatic orderbook scanning.
- [Quantitative Orderbook Analysis](https://simplefunctions.dev/technicals/quantitative-orderbook-analysis-prediction-markets) — Depth, imbalance, flow analysis.
- [Prediction Market Orderbook Analysis: Depth, Spread, Liquidity](https://simplefunctions.dev/blog/prediction-market-orderbook-analysis-depth-spread-liquidity) — What the orderbook tells you.

### Edge Detection & Sizing

- [Edge Calculation: Theory to Execution](https://simplefunctions.dev/technicals/edge-calculation-prediction-markets-theory-to-execution) — How to calculate and verify edges.
- [Cross-Venue Edge Detection: Kalshi vs Polymarket](https://simplefunctions.dev/technicals/cross-venue-edge-detection-kalshi-polymarket) — Find mispricings between venues.
- [Position Sizing with Kelly Criterion](https://simplefunctions.dev/technicals/position-sizing-kelly-criterion-prediction-markets) — Optimal bet sizing for prediction markets.
- [How to Backtest a Prediction Market Strategy](https://simplefunctions.dev/technicals/how-to-backtest-prediction-market-strategy) — Backtesting framework and pitfalls.

## Strategy & Market Structure

### How Prediction Markets Work

- [How to Read the World Through Prediction Market Prices](https://simplefunctions.dev/blog/how-to-read-the-world-through-prediction-market-prices) — Prices as compressed beliefs.
- [News Tells You What Happened, Prediction Markets Tell You What's Happening](https://simplefunctions.dev/blog/news-tells-you-what-happened-prediction-markets-tell-you-whats-happening) — Why markets are faster than news.
- [Prediction Markets Are the Best Real-Time Sensor for World Events](https://simplefunctions.dev/blog/prediction-markets-are-the-best-real-time-sensor-for-world-events) — The case for markets as data infrastructure.
- [Three Data Sources: Belief, Action, Sentiment](https://simplefunctions.dev/blog/three-data-sources-belief-action-sentiment) — How prediction markets fit in the data landscape.
- [The Prediction Market Data Stack](https://simplefunctions.dev/blog/the-prediction-market-data-stack-from-raw-prices-to-actionable-intelligence) — From raw prices to actionable intelligence.

### Concepts & Frameworks

- [Why Your AI Agent Needs a Thesis, Not Just Data](https://simplefunctions.dev/blog/why-your-ai-agent-needs-thesis-not-just-data) — Structured beliefs beat raw signals.
- [Causal Tree Decomposition Beats Vibes-Based Trading](https://simplefunctions.dev/blog/causal-tree-decomposition-beats-vibes-based-trading) — Quantify your reasoning.
- [The Most Important Number Is the Delta](https://simplefunctions.dev/blog/the-most-important-number-is-the-delta) — Why changes matter more than levels.
- [Orderbooks Are Fossilized Beliefs](https://simplefunctions.dev/blog/orderbooks-are-fossilized-beliefs) — What resting orders reveal.
- [5 Patterns That Kill Prediction Market Traders](https://simplefunctions.dev/technicals/5-patterns-that-kill-prediction-market-traders) — Common failure modes and how to avoid them.

### Platform Comparisons

- [Kalshi vs Polymarket: Which Should You Trade?](https://simplefunctions.dev/blog/kalshi-vs-polymarket-which-prediction-market-should-you-trade) — Fees, liquidity, regulation, API compared.
- [Kalshi vs Polymarket Technical Comparison](https://simplefunctions.dev/technicals/kalshi-vs-polymarket-comparison) — API, auth, data model differences.
- [SimpleFunctions vs Oddpool vs Raw Kalshi API](https://simplefunctions.dev/blog/simplefunctions-vs-oddpool-vs-raw-kalshi-api-which-prediction-market-tool-should-you-use) — When to use which tool.
- [Prediction Markets vs Polls](https://simplefunctions.dev/opinions/prediction-markets-vs-polls) — Why markets outperform surveys.

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

- [LLMs as Forecasters](https://arxiv.org/abs/2402.18563) — Can language models predict the future?
- [Approaching Human-Level Forecasting with Language Models](https://arxiv.org/abs/2402.18563) — GPT-4 calibration on forecasting tasks.

## Academic Papers

- [Prediction Markets: Theory, Evidence, and Applications](https://doi.org/10.1257/jep.18.2.107) — Wolfers & Zitzewitz (2004). The canonical survey.
- [The Wisdom of Crowds](https://doi.org/10.1257/jel.20221713) — Surowiecki. Why aggregated forecasts beat experts.
- [Prediction Markets for Economic Forecasting](https://doi.org/10.1016/B978-0-444-53683-9.00010-4) — Handbook chapter on using markets for macro forecasting.
- [Manipulating Prediction Markets: Evidence from the Field](https://doi.org/10.1016/j.jfineco.2017.06.001) — How hard is it to move a prediction market?
- [Information Aggregation in Dynamic Markets with Strategic Traders](https://doi.org/10.1111/j.1468-0262.2005.00553.x) — Ostrovsky (2012). Theory of information aggregation.

## Project Ideas

Things you can build with the APIs and tools above.

| Project | Difficulty | Stack |
|---------|-----------|-------|
| **Cross-venue arbitrage detector** — find price differences between Kalshi and Polymarket on the same event | Medium | Python + both APIs |
| **Telegram alert bot** — notify on 10%+ price moves | Easy | Node.js + SimpleFunctions `/api/changes` |
| **Thesis-driven trading agent** — create a causal model, scan for edges, auto-trade | Hard | LangChain + SimpleFunctions MCP |
| **Prediction market dashboard** — real-time prices, orderbook depth, historical charts | Medium | React + WebSocket APIs |
| **Forecasting tournament bot** — auto-submit forecasts to Metaculus/Manifold using LLMs | Medium | Python + OpenAI + Metaculus API |
| **Market sentiment tracker** — correlate prediction market moves with news/X sentiment | Hard | Python + SimpleFunctions + X API |

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

**What belongs here:** APIs, SDKs, datasets, code, tools, research, papers, tutorials. Things developers use to build.

**What doesn't belong:** Consumer dashboards, portfolio trackers, copy-trading services, news aggregators without an API. Check [Awesome Prediction Market Tools](https://github.com/aarora4/Awesome-Prediction-Market-Tools) for those.

## License

MIT
