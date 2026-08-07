# P09 - Weekly Occupancy Briefing

**Section:** 03 - Post-stay & Reporting
**Workflow step:** Step 2 of 3
**Current version:** v1.1
**Status:** Tested
**Last updated:** 6 August 2026

---

## Prompt Text (v1.1 - current)

```
You are a Hotel Operations analyst at Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne.

Using ONLY the data provided below, produce a weekly occupancy briefing. Do not infer causes for occupancy changes, and do not suggest additional analysis or projections beyond what is requested.

Occupancy data:
[OCCUPANCY_DATA]

Staffing policy:
[STAFFING_POLICY]

Required output:
- Heading "WEEKLY OCCUPANCY BRIEFING"
- Exactly three labelled sections: "Weekly Average", "Peak and Low Days", "Staffing Action"
- Weekly Average: state the calculated average to one decimal place
- Peak and Low Days: name the highest and lowest occupancy days with their percentages
- Staffing Action: list only the days that trigger the staffing policy, or state "No additional staffing required this week" if none apply
- Maximum 80 words total
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|---|---|---|
| [OCCUPANCY_DATA] | PMS daily occupancy report | Monday-Sunday percentages |
| [STAFFING_POLICY] | Static Operations policy | Add staff above 90% occupancy |

---

## Intended Workflow or Task

- **Trigger:** End of week, once all seven days of occupancy data are available
- **Actor:** Operations Manager reviews and distributes to management
- **Timing:** Monday morning, covering the previous week
- **Next step:** Distributed to management team; informs following week's staffing roster

```
Week ends -> Occupancy data compiled in PMS -> [P09 runs] -> Ops Manager reviews -> Briefing distributed
                                                                                   -> Informs staffing roster
```

---

## Problem Being Solved

Weekly occupancy briefings are currently compiled manually by reviewing PMS data and applying the staffing policy by hand, a repetitive task that takes time each week and can be prone to arithmetic or policy-application errors during busy periods.

**Pain points addressed:**
- Time-consuming manual calculation and formatting each week
- Risk of inconsistent report structure between weeks
- Risk of staffing policy being applied incorrectly under time pressure

---

## Automation Potential

**Level: Medium**

| Dimension | Assessment |
|---|---|
| Repetitiveness | High - produced every week with the same structure |
| Data availability | Occupancy data available directly from the PMS |
| Human judgment needed | Low - primarily a calculation and formatting task |
| Integration possibility | Could pull data directly from the PMS once weekly export is available |
| Estimated time saving | Estimated moderate saving in compilation time; exact figures require measurement |

**Human-in-the-loop role:** Operations Manager verifies the source data is complete and accurate before the prompt runs, and reviews the output before distribution.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Incorrect calculation if source data is incomplete or malformed | Medium | Operations Manager verifies data completeness before running the prompt |
| Model infers a cause for an occupancy change not supported by data | Low | Explicit "do not infer causes" constraint |
| Model suggests unrequested additional analysis (confirmed in v1.0 test) | Low | Explicit scope limit in v1.1; resolved in testing |
| Staffing policy threshold changes but prompt not updated | Low-Medium | Policy text supplied fresh each time as an input, not hardcoded, reducing risk of using an outdated rule |

**Overall risk rating: LOW** - low-consequence, well-structured reporting task suitable for high automation with a light verification step.

---

## Evaluation Criteria

- Calculations accurate (average, peak, low)
- Exactly three required sections present, correctly labelled
- Staffing policy applied correctly to the supplied threshold
- No inferred causes or unrequested additional analysis
- Word limit compliance

---

## Test Cases

| Case | Input summary | Expected behaviour | Result |
|---|---|---|---|
| 1. Normal | 7 days occupancy 68%-97%, staffing policy threshold 90% | Correct average, correct peak/low, correct staffing days identified, fixed structure, no extra analysis suggested | Pass |

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Summarise this hotel's weekly occupancy data.`
**Output:** Calculations were accurate, but output was free-form prose with no repeatable structure, and the model proactively suggested expanding the analysis (e.g. projecting staffing costs) beyond what was requested.
**Observed effect:** Usable for figures, but not suitable as a standard weekly report format - a consistent, scannable structure is needed for a report produced every week.
**Lesson learned:** Numerical accuracy alone is not sufficient for a recurring business report - needs a fixed section structure for consistency, and a scope limit to prevent unrequested additional analysis.

### v1.1 - Added fixed report structure and scope limit - Current
**Change:** Added role, a fixed three-section output structure, explicit "do not infer causes" and "no additional analysis" constraints, and an 80-word limit.
**Test input:** Same occupancy data as v1.0 test, for direct comparison.
**Output:** Correct average (80.9%), correct peak/low days, correct staffing action for both threshold days, delivered in the exact three-section format with no additional suggestions.
**Observed effect:** Ready to distribute with brief review - resolved the formatting inconsistency and scope-creep issues identified in v1.0, while maintaining the calculation accuracy already present.
**Lesson learned:** A prompt can produce numerically accurate output on the first attempt and still require revision - format consistency and scope control are separate quality dimensions from factual accuracy, and both need explicit constraints.

---

## Related Prompts

- **Previous in chain:** P08 - Review response draft
- **Next in chain:** P10 - Guest feedback theme summary
- **Parent section:** 03-post-stay-reporting/README.md
