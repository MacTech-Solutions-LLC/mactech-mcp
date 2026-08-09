# MacTech MCP — plugin & marketplace

Claude Code plugin for MacTech Solutions' three public MCP servers: CMMC/NIST
800-171, DISA STIG, and the federal market. **No account, no API key, no
sign-up** — the servers are open on purpose.

```
/plugin marketplace add MacTech-Solutions-LLC/mactech-mcp
/plugin install mactech-cmmc@mactech
```

## Commands

| Command | What it does |
| --- | --- |
| `/mactech-cmmc:sprs-score` | Exact SPRS score under the DoD Assessment Methodology, including the 3.5.3 and 3.13.11 sliding scales |
| `/mactech-cmmc:gap-assessment` | Level determination, gaps judged against the 320 assessment objectives, and a POA&M |
| `/mactech-cmmc:stig-harden` | 2,029 DISA STIG rules across 15 benchmarks with official check/fix text |
| `/mactech-cmmc:stig-checklist` | Export a DISA `.ckl` — the artifact STIG Viewer opens and eMASS ingests |
| `/mactech-cmmc:market-scan` | Live SAM.gov opportunities and USASpending award history |

## The servers

| Server | Endpoint | What it holds |
| --- | --- | --- |
| `mactech-cmmc` | `/api/mcp` | 110 NIST SP 800-171 Rev 2 requirements with official DoD Assessment Methodology (Annex A) weights, exact SPRS scoring (+110 to −203), the 320 800-171A assessment objectives, and crosswalks to 800-53 / CSF 2.0 / SOC 2 |
| `mactech-stig` | `/api/mcp/stig` | 2,029 DISA STIG rules across 15 benchmarks with official check and fix text, CCI mappings, and `.ckl` export |
| `mactech-market` | `/api/mcp/market` | SAM.gov opportunities and entity lookup (BYOK) plus keyless USASpending award data |

All at `https://www.mactechsolutionsllc.com`. Connect any one directly without
the plugin:

```sh
claude mcp add --transport http mactech-cmmc https://www.mactechsolutionsllc.com/api/mcp
```

## Air-gapped and GCC High

Hosted MCP servers run in commercial cloud, so a CUI enclave or an air-gapped
network cannot reach them. The offline build is the CMMC and STIG corpora
compiled into one file — no install, no key, no network:

```sh
curl -O https://www.mactechsolutionsllc.com/downloads/mactech-compliance-mcp.mjs
curl -O https://www.mactechsolutionsllc.com/downloads/mactech-compliance-mcp.mjs.sha256
sha256sum -c mactech-compliance-mcp.mjs.sha256
claude mcp add --transport stdio mactech-compliance -- node ./mactech-compliance-mcp.mjs
```

Verify the checksum on arrival — once the file is inside the enclave there is no
route back out to re-download and compare.

## What this is not

Reference data and arithmetic, not a certification. A score computed here is
only as good as the implementation state you describe, and no tool substitutes
for an assessment. Rules and weights are current as published; DISA revises STIG
benchmarks quarterly, so check `list_stig_benchmarks` against DISA's current
release.

## Links

- Server documentation: <https://www.mactechsolutionsllc.com/mcp>
- MCP registry: `com.mactechsolutionsllc.www/{cmmc,stig,federal-market}`

## License

MIT.
