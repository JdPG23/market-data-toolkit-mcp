# Market Data Toolkit (MCP)

17 live market-data tools for AI agents, served over the [Model Context Protocol](https://modelcontextprotocol.io). One URL connects your agent to real eBay sold prices, luxury watch market analysis, company KYC for the UK and Spain, SEC filings, patents, trademarks, government contracts and public auctions.

This is a **remote MCP server**: the tools run as [Apify Actors](https://apify.com/jdepablos) behind the Apify MCP gateway. There is nothing to install or host. Every tool queries its source live at request time and returns clean, typed JSON.

## Connect

**Claude Desktop / Cursor / any MCP client** (`mcpServers` config):

```json
{
  "mcpServers": {
    "market-data-toolkit": {
      "url": "https://mcp.apify.com?tools=jdepablos/ebay-sold-price-appraiser,jdepablos/second-hand-deal-scanner-es,jdepablos/borme-company-feed,jdepablos/spain-boe-auctions,jdepablos/trademark-watch-tmview,jdepablos/insider-trading-feed,jdepablos/clinical-trials-watch,jdepablos/startup-funding-feed,jdepablos/pokemon-card-price-checker,jdepablos/chrono24-watch-analyzer,jdepablos/catawiki-deal-finder,jdepablos/patent-watch,jdepablos/airbnb-market-analyzer,jdepablos/booking-hotel-price-analyzer,jdepablos/samgov-opportunities-feed,jdepablos/sec-13f-holdings-feed,jdepablos/companies-house-feed"
    }
  }
}
```

**Claude Code**:

```bash
claude mcp add --transport http market-data-toolkit "https://mcp.apify.com?tools=jdepablos/ebay-sold-price-appraiser,jdepablos/second-hand-deal-scanner-es,jdepablos/borme-company-feed,jdepablos/spain-boe-auctions,jdepablos/trademark-watch-tmview,jdepablos/insider-trading-feed,jdepablos/clinical-trials-watch,jdepablos/startup-funding-feed,jdepablos/pokemon-card-price-checker,jdepablos/chrono24-watch-analyzer,jdepablos/catawiki-deal-finder,jdepablos/patent-watch,jdepablos/airbnb-market-analyzer,jdepablos/booking-hotel-price-analyzer,jdepablos/samgov-opportunities-feed,jdepablos/sec-13f-holdings-feed,jdepablos/companies-house-feed"
```

Auth is OAuth in the browser (an [Apify](https://apify.com) account, free tier works). You can also pass a token header instead: `Authorization: Bearer <APIFY_TOKEN>`.

Want fewer tools? Keep only the slugs you need in the `?tools=` list. Also published on [Smithery](https://smithery.ai/server/@jl-depablos/market-data-toolkit).

## The tools

### Pricing and resale

| Tool | What it answers |
|---|---|
| [eBay Sold Price Appraiser](https://apify.com/jdepablos/ebay-sold-price-appraiser) | Real market value of any item from confirmed eBay sold listings: median, percentiles, trend, liquidity, cleaned comps. |
| [Second-hand Deal Scanner](https://apify.com/jdepablos/second-hand-deal-scanner-es) | Underpriced listings on Vinted, Wallapop and Milanuncios vs real eBay sold values, ranked by estimated profit (ES/FR/DE/IT/UK). |
| [Pokemon Card Price Checker](https://apify.com/jdepablos/pokemon-card-price-checker) | What a Pokemon card is actually worth, from confirmed sold listings. |
| [Chrono24 Watch Analyzer](https://apify.com/jdepablos/chrono24-watch-analyzer) | Market analysis for any luxury watch: median asking price, percentiles, market depth, dealer mix. |
| [Catawiki Deal Finder](https://apify.com/jdepablos/catawiki-deal-finder) | Live auction lots trading below Catawiki's own expert estimates. |

### Company intelligence and KYC

| Tool | What it answers |
|---|---|
| [Companies House Feed (UK)](https://apify.com/jdepablos/companies-house-feed) | KYC-grade UK company checks: profile, officers, beneficial owners, charges, filings, risk flags. |
| [BORME Company Feed (Spain)](https://apify.com/jdepablos/borme-company-feed) | Daily acts from Spain's Companies Registry: incorporations, appointments, dissolutions, insolvencies. |
| [Insider Trading Feed](https://apify.com/jdepablos/insider-trading-feed) | Insider buys and sells for any US-listed stock (SEC Form 4). |
| [SEC 13F Holdings Feed](https://apify.com/jdepablos/sec-13f-holdings-feed) | Any fund manager's portfolio: top holdings with weights and quarter-over-quarter changes. |
| [Startup Funding Feed](https://apify.com/jdepablos/startup-funding-feed) | US private funding rounds from SEC Form D, days before the press. |

### Markets, IP and public sector

| Tool | What it answers |
|---|---|
| [Airbnb Market Analyzer](https://apify.com/jdepablos/airbnb-market-analyzer) | Supply and nightly price stats for any city, geo-scoped. |
| [Booking Hotel Price Analyzer](https://apify.com/jdepablos/booking-hotel-price-analyzer) | A city's hotel market: median and percentile rates, supply depth. |
| [Patent Watch](https://apify.com/jdepablos/patent-watch) | New patent publications by keyword or company, worldwide. |
| [Trademark Watch (TMview)](https://apify.com/jdepablos/trademark-watch-tmview) | New trademark filings across USPTO, EUIPO, WIPO and 70+ offices, with opposition deadlines. |
| [Clinical Trials Watch](https://apify.com/jdepablos/clinical-trials-watch) | New and updated clinical trials by condition, sponsor or drug. |
| [SAM.gov Opportunities Feed](https://apify.com/jdepablos/samgov-opportunities-feed) | Live US federal contract opportunities with deadlines and set-aside labels. |
| [Spain BOE Auctions](https://apify.com/jdepablos/spain-boe-auctions) | Spanish judicial and tax auctions with appraisals, charges and asset details. |

## Pricing

Pay per event, on your Apify account. Each tool charges a flat fee per delivered result (from $0.0008 to $0.12 depending on the tool). Failed lookups and empty responses are never charged. No subscription.

## Example prompts

- "What is a Game Boy Micro actually selling for? Should I buy one listed at 60 EUR?"
- "Run a risk check on Greggs plc and summarize the red flags."
- "Which fund managers increased their NVDA position last quarter?"
- "Any new trademark filings close to the name 'Acme' I should worry about?"
- "Find cybersecurity contract opportunities closing in the next 30 days."

## Design principles

- Primary and official sources wherever they exist (SEC EDGAR, Companies House, BOE, TMview, ClinicalTrials.gov, SAM.gov).
- Answers, not raw scrape dumps: valuation stats instead of listing rows, filings parsed into transactions, risk flags computed from register facts.
- Agent-native: typed output schemas, defaults that work with zero configuration, one flat fee per unit of value.

Runnable API examples for every tool (plain `fetch`, no SDK) live in the [Data Actors Cookbook](https://github.com/JdPG23/data-actors-cookbook).
