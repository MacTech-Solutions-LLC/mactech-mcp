---
description: Produce a DISA .ckl checklist for a platform — the artifact an assessor receives, STIG Viewer opens, and a POA&M is written from. Use when someone asks for a checklist, wants scan results recorded, or needs evidence to submit.
allowed-tools: mcp__mactech-stig__export_stig_checklist, mcp__mactech-stig__list_stig_benchmarks, mcp__mactech-stig__search_stig, mcp__mactech-stig__get_stig_rule, Write
---

# STIG checklist

Build a real `.ckl` — STIG Viewer's format — rather than a prose summary of findings.

`$ARGUMENTS` may name the platform, severity scope, or host. If empty, ask which platform and whether this is a full checklist or CAT I only.

## How to work

Confirm the benchmark with `list_stig_benchmarks` first. The `product` argument is an identifier, not a display name — `rhel9`, `rhel8`, `windows11`, `windows2022`, `cisco_ios_router_ndm` — and a wrong one produces an error rather than a wrong checklist, which is the good outcome.

Call `export_stig_checklist` with the platform, any severity filter, and the asset's hostname. Write the returned `ckl` string to the returned `filename` so the user gets a file they can open, not XML in a transcript.

## The rule that matters

**Never mark a rule as passing that nobody checked.** Rules you do not supply a status for come back `Not_Reviewed`, and that is correct — an unopened checklist asserts nothing. If the user wants a pre-filled checklist, ask what was actually observed for each rule rather than defaulting to `NotAFinding`, which manufactures compliance and is exactly what an assessor will catch.

Status values: `Open` (failed), `NotAFinding` (passed), `Not_Applicable` (out of scope, and it needs a justification in `comments`), `Not_Reviewed`.

Report the `status_counts` back plainly, including how many remain unreviewed. That number is the honest measure of how much assessment is still outstanding.

## After the checklist

Open findings are POA&M input. If the user is working toward CMMC, hand the failed rules to the CMMC server's `generate_poam_entries`, and note which NIST 800-171 requirements they map to — hardening effort spent on already-satisfied controls is the usual waste.
