---
name: Verify a business (KYB)
description: Resolve and verify a business customer against Enigma's knowledge graph, then pull its locations and legal entities for onboarding.
api: mcp/enigma-analytics-mcp.yml
surface: mcp
operations: [search_business, search_kyb, get_brand_locations, get_brand_legal_entities]
---

# Verify a business (KYB) with Enigma

Use Enigma's MCP server (`https://mcp.enigma.com/mcp`, bearer auth) to onboard and verify a business
customer. Every tool below is a real Enigma MCP tool.

## Steps
1. **Resolve the business.** Call `search_business` with whatever you have — name, website, phone,
   or address. It returns the matching Brand(s) with revenue, growth, industry, tech stack, and
   locations. Keep the resolved Enigma Brand ID.
2. **Run KYB match.** Call `search_kyb` with the business name and address to verify identity against
   state-of-society and other sources. Treat a low-confidence or no match as a verification failure.
3. **Confirm physical footprint.** Call `get_brand_locations` with the Brand ID to pull every physical
   address with revenue and coordinates; check the onboarding address is among them.
4. **Confirm legal standing.** Call `get_brand_legal_entities` with the Brand ID to list linked legal
   entities with registration status, formation dates, and filings. Flag dissolved/inactive entities.

## Rules
- Auth: Authorization bearer token tied to an Enigma API key (Console → Agent tools).
- Every result edge carries `firstObservedDate`/`lastObservedDate`/`rank`/`datasetIds` — prefer
  higher-rank, recently-observed records and record provenance.
- Never fabricate an identifier; only pass IDs returned by a prior tool call.
