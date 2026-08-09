# MacTech CMMC & Federal Compliance — Claude Code plugin

Four commands over MacTech's three public MCP servers. No account, no API key, no
sign-up — the servers are open on purpose.

```
/plugin marketplace add MacTech-Solutions-LLC/mactech
/plugin install mactech-cmmc@mactech
```

## Commands

| Command | What it does |
| --- | --- |
| `/mactech-cmmc:sprs-score` | Exact SPRS score under the DoD Assessment Methodology, including the 3.5.3 and 3.13.11 sliding scales |
| `/mactech-cmmc:gap-assessment` | Level determination, gaps judged against the 320 assessment objectives, and a POA&M |
| `/mactech-cmmc:stig-harden` | 2,029 DISA STIG rules across 15 benchmarks, official check/fix text, mapped back to 800-171 |
| `/mactech-cmmc:market-scan` | Live SAM.gov opportunities and USASpending award history |
| `/mactech-cmmc:stig-checklist` | Export a DISA `.ckl` checklist — the artifact STIG Viewer opens and eMASS ingests |

## What it connects to

| Server | Endpoint |
| --- | --- |
| `mactech-cmmc` | `https://www.mactechsolutionsllc.com/api/mcp` |
| `mactech-market` | `https://www.mactechsolutionsllc.com/api/mcp/market` |
| `mactech-stig` | `https://www.mactechsolutionsllc.com/api/mcp/stig` |

The CMMC and STIG servers are static reference data and have no quota. The SAM.gov
half of the market server runs on a shared key with a per-client daily allowance;
pass your own free key (sam.gov → Account Details → API Key) as `sam_api_key` to
bypass it entirely. The USASpending tools are keyless and unlimited.

## What this is not

Reference data and arithmetic, not a certification. A score computed here is only
as good as the implementation state you describe, and no tool substitutes for an
assessment. See <https://www.mactechsolutionsllc.com/mcp>.

## Local development

```sh
claude plugin validate ./plugin
claude --plugin-dir ./plugin
```
