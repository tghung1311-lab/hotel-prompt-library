# P09 - Weekly Occupancy Briefing

**Section:** 03 - Post-stay & Reporting
**Workflow step:** Step 2 of 3
**Current version:** v1.0
**Status:** Draft - needs revision
**Last updated:** 6 August 2026

---

## Prompt Text (v1.0 - initial draft)

```
Summarise this hotel's weekly occupancy data.
```

**Test input used:** Monday 71%, Tuesday 68%, Wednesday 75%, Thursday 82%, Friday 94%, Saturday 97%, Sunday 79%; staffing policy triggers additional Front Desk staff above 90% occupancy.

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Summarise this hotel's weekly occupancy data.`
**Output:** Calculations were accurate (correct average, correct peak/low days, correct staffing policy application), but output was free-form prose with no repeatable structure, and the model proactively suggested expanding the analysis (e.g. projecting staffing costs) beyond what was requested.
**Observed effect:** Usable for figures, but not suitable as a standard weekly report format - a consistent, scannable structure is needed for a report produced every week.
**Lesson learned:** Numerical accuracy alone is not sufficient for a recurring business report - needs a fixed section structure for consistency, and a scope limit to prevent the model from suggesting additional unrequested analysis.
