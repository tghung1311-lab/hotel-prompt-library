# Section 3: Post-stay & Reporting

Three prompts supporting post-stay guest engagement and internal operational reporting, covering individual review responses, weekly occupancy reporting, and aggregated feedback theme analysis.

## Prompts in this section

| ID | Prompt | Automation | Risk |
|---|---|---|---|
| P08 | Review response draft | High | Medium |
| P09 | Weekly occupancy briefing | Medium | Low |
| P10 | Guest feedback theme summary | Medium | Low-Medium |

## Chain

```
Review posted -> P08 (response draft) -> theme noted for P10
Week ends -> P09 (occupancy briefing)
Reporting cycle -> P10 (feedback theme summary)
```

## Section-level risk note

P08 is guest-facing and public (posted on review platforms), so it carries the highest risk in this section - primarily the risk of promising unconfirmed operational changes, which testing confirmed and resolved. P09 and P10 are internal reporting tools; their main risk is misrepresenting data (e.g. overgeneralising a small feedback sample) rather than direct guest impact.
