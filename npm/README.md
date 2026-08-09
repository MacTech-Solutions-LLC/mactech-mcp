# mactech-compliance-mcp

An offline MCP server for CMMC / NIST SP 800-171 and DISA STIG work. **No
account, no API key, and no network access** — the entire corpus is compiled
into the package.

```sh
claude mcp add --transport stdio mactech-compliance -- npx -y mactech-compliance-mcp
```

Or in any MCP client's JSON config:

```json
{
  "mcpServers": {
    "mactech-compliance": {
      "command": "npx",
      "args": ["-y", "mactech-compliance-mcp"]
    }
  }
}
```

Requires Node 20 or newer.

## What it serves

12 tools, 2 prompts, and resource templates over:

- **NIST SP 800-171 Rev 2** — all 110 requirements with the official DoD
  Assessment Methodology (Annex A) point weights, and exact SPRS scoring
  (+110 to −203). This is the revision DoD actually requires: class deviation
  2024-O0013 R1 pins DFARS 252.204-7012 to Rev 2 until rescinded.
- **NIST SP 800-171A** — the 320 assessment objectives, i.e. what an assessor
  tests rather than what the control title says.
- **NIST SP 800-171 Rev 3** — 97 active requirements, 88 ODPs and 422
  objectives, served as **advisory only** and clearly marked as not currently
  binding for DoD contracts. Scoring Rev 3 is refused rather than approximated,
  because no DoD methodology for it exists.
- **DISA STIGs** — 2,029 rules across 15 benchmarks (RHEL 8/9, Ubuntu 22.04
  LTS, Windows 11, Windows Server 2022, and Cisco IOS/NX-OS/ISE) with official
  check and fix text, CCI mappings, and `.ckl` checklist export for STIG Viewer
  and eMASS.
- **FAR/DFARS clauses** — what 52.204-21, 252.204-7012/7019/7020/7021 and
  252.239-7010 actually oblige, what flows down, and the reporting deadlines.
- **Assessment scoping** — DoD's asset categories and what each obliges.
- **Crosswalks** — NIST 800-53 / FedRAMP Moderate, CSF 2.0, SOC 2.

## Why offline

Every hosted compliance MCP server runs in commercial cloud, and Microsoft
publishes none for GCC High or the DoD sovereign clouds. Contractors working
inside a CUI enclave or an air-gapped network cannot reach any of them. This
package is the same corpus over stdio.

For a genuinely disconnected host, download the single-file build instead —
one file, no npm registry access needed:

```sh
curl -O https://www.mactechsolutionsllc.com/downloads/mactech-compliance-mcp.mjs
curl -O https://www.mactechsolutionsllc.com/downloads/mactech-compliance-mcp.mjs.sha256
sha256sum -c mactech-compliance-mcp.mjs.sha256
```

## What it does not do

The federal-market tools (SAM.gov, USASpending) are **absent by design** —
they proxy live government APIs an air-gapped host cannot reach, and shipping
them would offer a capability that fails at the moment of use. They are
available on the hosted server at
`https://www.mactechsolutionsllc.com/api/mcp/market`.

There is **no telemetry**. A server running inside someone else's CUI boundary
has no business phoning home.

## Currency

The corpus is compiled in and therefore frozen at publish time. DISA revises
STIG benchmarks quarterly, and CMMC policy is moving — Phase II was suspended
on 13 July 2026. The server states this where it matters, but an offline build
cannot tell you it is stale. Check `list_stig_benchmarks` against DISA's
current release and <https://dowcio.war.gov/CMMC/> for CMMC status.

## Not a certification

Reference data and arithmetic. A score is only as good as the implementation
state you describe, and no tool substitutes for an assessment.

MIT licensed. <https://www.mactechsolutionsllc.com/mcp>
