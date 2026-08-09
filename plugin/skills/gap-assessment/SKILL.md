---
description: Run a NIST SP 800-171 / CMMC gap assessment — determine the required level, find unmet requirements, and produce a POA&M. Use when someone asks whether they are CMMC ready, what level applies to them, or what they still have to do.
allowed-tools: mcp__mactech-cmmc__determine_cmmc_level, mcp__mactech-cmmc__list_controls, mcp__mactech-cmmc__lookup_control, mcp__mactech-cmmc__get_assessment_objectives, mcp__mactech-cmmc__generate_poam_entries, mcp__mactech-cmmc__calculate_sprs_score, mcp__mactech-cmmc__crosswalk_control
---

# Gap assessment

Work out which CMMC level applies, which requirements are unmet, and what the plan to close them is.

`$ARGUMENTS` may describe the organization or the scope. If empty, start by establishing what data they handle.

## Establish the level first

Call `determine_cmmc_level`. The distinction is what data crosses their boundary:

- **FCI only** → Level 1, the 17 practices, annual self-assessment.
- **CUI** → Level 2, all 110 requirements of 800-171 Rev 2.

Getting this wrong wastes the entire engagement, so do not assume Level 2 because someone is a defense contractor. Ask what contract data they actually receive.

## Assess against objectives, not control titles

A requirement is met only if every one of its assessment objectives is met. Use `get_assessment_objectives` — 320 of them — rather than judging from the requirement text. This is how an assessor will test it, and a control that "sounds implemented" routinely fails on a single objective, most often the documented-and-reviewed ones.

Work family by family (`list_controls`) so coverage is systematic rather than whatever came to mind.

## Produce the plan

Use `generate_poam_entries` for the gaps, and `calculate_sprs_score` for where they stand now.

Rank the remediation by points per unit of effort, not by control number — that is the order that moves the score fastest.

State plainly which items are **not** POA&M-eligible for a Level 2 assessment: 3.5.3 (MFA), 3.13.11 (FIPS) and most 5-point requirements must be closed before assessment, not planned. Presenting risk acceptance in place of remediation is an assessment disqualifier.

If they already hold SOC 2 or ISO 27001, use `crosswalk_control` to identify evidence they can reuse. Say clearly that overlap reduces work but does not substitute for the 800-171 objectives.
