---
name: Screen and decision a customer
description: Screen a person or business against sanctions/watchlists with Enigma, then look up and update the screening decision.
api: mcp/enigma-analytics-mcp.yml
surface: mcp
operations: [screen_customer, screen_business, screen_entity_search, find_decision, find_decisions, update_decision]
---

# Sanctions screening and decisioning with Enigma

Use Enigma's Screening MCP tools to run watchlist/sanctions checks and manage the resulting
decisions. Every tool below is a real Enigma MCP tool.

## Steps
1. **Screen the subject.** For an individual call `screen_customer` (name, DOB, country, or passport);
   for an organization call `screen_business` (name, country, address, or BIC). Screens against OFAC
   SDN, EU, UN and other sanctions lists.
2. **Inspect any hit.** For each returned entity match, call `screen_entity_search` with the entity ID
   to retrieve the full sanctions profile before adjudicating.
3. **Find the decision.** Call `find_decision` with the screening request ID (or `find_decisions` with
   date-range/status/assignee filters) to load the current decision record.
4. **Adjudicate.** Call `update_decision` to set status (e.g. clear / escalate), assign an owner, and
   attach notes documenting the rationale.

## Rules
- Auth: Authorization bearer token tied to an Enigma API key (Console → Agent tools).
- Never auto-clear a true-positive sanctions hit without human review; record the reviewer in the note.
- Preserve request IDs end-to-end so decisions are auditable.
