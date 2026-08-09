---
description: Find and apply DISA STIG hardening rules for RHEL 8/9, Windows 11, Windows Server 2022, or Cisco IOS routers, with the exact check and fix text. Use when someone asks how to harden a system, what a STIG rule requires, or how a STIG maps to NIST controls.
allowed-tools: mcp__mactech-stig__search_stig, mcp__mactech-stig__get_stig_rule, mcp__mactech-stig__list_stig_benchmarks, mcp__mactech-cmmc__lookup_control
---

# STIG hardening

Serve real DISA STIG rules — 2,029 across 15 benchmarks (RHEL 8/9, Ubuntu 22.04 LTS, Windows 11, Windows Server 2022, and Cisco IOS/NX-OS/ISE) — with their official check and fix text.

`$ARGUMENTS` may name a platform, a rule id, or a thing to harden. If empty, ask which platform, since the rules differ entirely between them.

## How to work

Establish the benchmark first (`list_stig_benchmarks`) — RHEL 8 and RHEL 9 rules are not interchangeable and applying the wrong one produces a system that passes nothing.

Use `search_stig` to find candidates, then `get_stig_rule` for the full text of each one you are going to act on. **Quote the official check and fix text rather than paraphrasing it.** An assessor compares against the STIG's own wording, and a paraphrase that drifts is a finding.

Report each rule with its severity (CAT I/II/III). CAT I is the queue that matters first.

## Applying changes

If asked to actually apply hardening:

- Show the fix text and what it changes **before** running anything.
- Never apply a CAT I change to a running system without explicit confirmation — several STIG fixes will lock out remote access if applied out of order or without the corresponding access configured.
- Prefer producing a reviewable script over executing ad hoc commands.

## Tying it back to 800-171

STIG rules carry NIST control mappings. When someone is hardening to satisfy a compliance requirement, use `lookup_control` to state which 800-171 requirement the rule serves and what it is worth. Hardening without knowing which requirement it closes is how effort goes into controls that were already met.
