---
name: Run risk due diligence on a business
description: Combine Enigma negative-news, government-archive, and card-transaction analytics to build a risk picture of a business.
api: mcp/enigma-analytics-mcp.yml
surface: mcp
operations: [search_business, search_negative_news, search_gov_archive, get_brand_card_analytics]
---

# Risk due diligence on a business with Enigma

Use Enigma's MCP tools to assemble a risk and health picture of a business for underwriting or
ongoing monitoring. Every tool below is a real Enigma MCP tool.

## Steps
1. **Resolve the business.** Call `search_business` (name, website, phone, or address) to get the
   Brand ID and baseline firmographics (revenue, growth, industry, locations).
2. **Adverse media.** Call `search_negative_news` with the business name and address to surface risk
   indicators across legal, financial, labor, and compliance categories.
3. **Public records.** Call `search_gov_archive` to query registrations, permits, licenses, health
   inspections, court filings, and professional records for red flags.
4. **Financial health.** Call `get_brand_card_analytics` with the Brand ID for up to 60 months of
   card-transaction history — revenue, growth rate, customer counts — to gauge trajectory and stability.

## Rules
- Auth: Authorization bearer token tied to an Enigma API key (Console → Agent tools).
- Weight results by edge `rank` and recency (`lastObservedDate`); cite `datasetIds` for each finding.
- Treat negative-news and gov-archive hits as leads to verify, not conclusions.
