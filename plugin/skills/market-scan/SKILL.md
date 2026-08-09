---
description: Search live federal contract opportunities on SAM.gov and analyze historical awards from USASpending. Use when someone asks what contracts they could bid, who won similar work, what an agency spends, or to look up an entity's registration.
allowed-tools: mcp__mactech-market__search_opportunities, mcp__mactech-market__lookup_entity, mcp__mactech-market__search_awards, mcp__mactech-market__get_award, mcp__mactech-market__find_agency, mcp__mactech-market__find_naics, mcp__mactech-market__spending_by_category
---

# Federal market scan

Live SAM.gov opportunities and entity registrations, plus keyless USASpending award history.

`$ARGUMENTS` may describe the capability, agency, or NAICS to look at. If empty, ask what they sell before searching — an untargeted opportunity search returns noise.

## Resolve codes before searching

Use `find_naics` and `find_agency` first. Searching by a guessed agency name or NAICS code silently returns nothing, which reads as "no opportunities" rather than "wrong code" — the most common way this analysis goes wrong.

## Two different questions

- **What can I bid now?** → `search_opportunities` (SAM.gov, live postings).
- **Who wins this work and at what size?** → `search_awards`, `get_award`, `spending_by_category` (USASpending, historical).

The second is usually the more valuable one and it is keyless and unlimited, so lead with it when someone is deciding whether a market is worth entering. Incumbency, typical award size, and set-aside patterns tell them more than a list of open solicitations.

## On quota

SAM.gov tools run on a shared key with a per-client daily allowance. If a quota error comes back, say so plainly and offer the two real options: supply their own free SAM.gov key (Account Details → API Key at sam.gov, passed as the `sam_api_key` argument), or use the keyless USASpending tools. Do not retry in a loop.

## Connecting to compliance

Many opportunities carry DFARS 252.204-7012 or a CMMC level requirement. When one does, say what that obliges — and note that eligibility is a precondition for the bid, not paperwork to sort out after award.
