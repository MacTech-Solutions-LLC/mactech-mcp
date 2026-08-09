---
description: Compute a DoD SPRS score against NIST SP 800-171 Rev 2 using the official DoD Assessment Methodology weights. Use when someone asks what their SPRS score is, what a control is worth, or how a gap changes their score.
allowed-tools: mcp__mactech-cmmc__calculate_sprs_score, mcp__mactech-cmmc__lookup_control, mcp__mactech-cmmc__list_controls, mcp__mactech-cmmc__get_assessment_objectives
---

# SPRS score

Compute an exact SPRS score from a stated implementation state. The arithmetic is the DoD Assessment Methodology (Annex A), not an approximation: 110 requirements, a 313-point deduction pool, and a range of +110 to −203.

`$ARGUMENTS` may describe what is or isn't implemented. If it is empty, ask what they want scored before doing anything else.

## How to work

Call `calculate_sprs_score` with the implementation state. Never estimate a score yourself — the weights are not uniform (5, 3 and 1 points) and two requirements use sliding scales that are easy to get wrong:

- **3.5.3 (MFA)** — −5 if MFA is absent entirely; −3 if it covers privileged and remote users but not general users.
- **3.13.11 (FIPS)** — −5 if encryption is not employed; −3 if employed but not FIPS-validated.

If the user has not said which of those partial states applies, ask. The difference is worth points and guessing produces a number they may submit to the government.

**3.12.4 (the System Security Plan) carries no point value but gates everything.** Without a current SSP an assessment cannot be completed and no score can be submitted to SPRS at all. If the SSP is missing, say so before reporting any score — the score is unreportable, which matters more than its value.

## Reporting

Give the score, then the largest deductions in descending order, because that is the remediation queue. For each, state the requirement and what it is worth.

Be explicit that a POA&M does **not** restore points: the deduction stands until the control is actually implemented.

If they ask what a specific control requires or how an assessor will test it, use `lookup_control` and `get_assessment_objectives` rather than describing it from memory.
