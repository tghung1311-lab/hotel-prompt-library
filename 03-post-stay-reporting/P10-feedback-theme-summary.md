# P10 - Guest Feedback Theme Summary

**Section:** 03 - Post-stay & Reporting
**Workflow step:** Step 3 of 3
**Current version:** v1.1
**Status:** Tested
**Last updated:** 6 August 2026

---

## Prompt Text (v1.1 - current)

```
You are a Marketing/Guest Relations analyst at Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne.

Using ONLY the guest comments provided below, identify recurring themes. Treat this as a small qualitative sample, not a statistically representative result. Do not use words implying overall consistency (e.g. "consistently", "always", "most guests") and do not recommend operational changes - this is a theme-identification step only.

Guest comments:
[GUEST_COMMENTS]

Required output:
- A table with exactly three columns: Theme | Comment reference(s) | Sentiment (Positive/Negative)
- Maximum 5 themes
- One closing sentence noting this is based on a small sample and is not a statistically representative result
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|---|---|---|
| [GUEST_COMMENTS] | Review platforms, post-stay surveys, numbered for reference | 8 guest comments from recent reviews |

---

## Intended Workflow or Task

- **Trigger:** Weekly or monthly reporting cycle
- **Actor:** Marketing/Guest Relations analyst reviews and distributes
- **Timing:** Aligned with weekly/monthly reporting schedule
- **Next step:** Distributed to Operations/Marketing for improvement planning discussion

```
Reporting cycle due -> Comments compiled -> [P10 runs] -> Analyst reviews -> Summary distributed
                                                                            -> Used in improvement planning discussion
```

---

## Problem Being Solved

Identifying recurring themes across guest feedback is currently done by manually re-reading reviews and comments, which is time-consuming and can lead to inconsistent conclusions about which issues are truly recurring versus isolated incidents.

**Pain points addressed:**
- Time-consuming manual review of scattered feedback
- Risk of overstating how widespread an issue is based on a small number of comments
- Inconsistent theme categorisation between reporting periods

---

## Automation Potential

**Level: Medium**

| Dimension | Assessment |
|---|---|
| Repetitiveness | Medium - produced on a recurring reporting cycle |
| Data availability | Comments available from review platforms and surveys, though compilation may require manual collection |
| Human judgment needed | Medium - interpreting themes in business context and deciding what warrants action remains human |
| Integration possibility | Could integrate with review-platform aggregation tools |
| Estimated time saving | Estimated moderate saving in manual review time; exact figures require measurement |

**Human-in-the-loop role:** Analyst reviews the theme summary for accuracy and decides which themes, if any, warrant escalation to Operations for action - this prompt does not make that recommendation itself.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Overgeneralising a small sample as representative (confirmed in v1.0 test) | Medium | Explicit small-sample framing and prohibition on consistency language; resolved in v1.1 testing |
| Model recommends operational action beyond its scope (confirmed in v1.0 test) | Low-Medium | Explicit scope limit to theme identification only; resolved in v1.1 testing |
| Theme categorisation varies between reporting periods, reducing comparability | Medium | Fixed output format aids consistency, though category labels are not drawn from a fixed list - a known limitation for long-term trend tracking |
| Sample size not stated, so readers may not gauge how many comments informed each theme | Low | Comment reference column shows exact source count per theme |

**Overall risk rating: LOW-MEDIUM** - internal reporting tool with limited direct guest impact; primary risk is misinterpretation of scale rather than guest-facing harm.

---

## Evaluation Criteria

- No overgeneralising language used
- No operational recommendations included
- Correct three-column table format
- Maximum 5 themes
- Small-sample disclaimer included

---

## Test Cases

| Case | Input summary | Expected behaviour | Result |
|---|---|---|---|
| 1. Normal | 8 guest comments covering 6 distinct topics (views, check-in, breakfast, staff, room noise, location, checkout, wifi) | Grouped into themes without overgeneralising language, no operational recommendations, correct table format | Pass |

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Summarise the themes in these guest feedback comments.`
**Output:** Correctly grouped comments into positive/negative themes with source references, but used overgeneralising language ("Guests are consistently happy...") despite each theme being supported by only one comment, and proactively recommended an operational review beyond the scope of theme identification.
**Observed effect:** Not fully usable - overgeneralising a small qualitative sample risks misrepresenting guest sentiment to management, and the unsolicited operational recommendation exceeds the intended scope of this reporting step.
**Lesson learned:** With small samples, the model tends to imply broader consistency than the data supports and to suggest actions beyond the requested task. Needed an explicit small-sample framing, a prohibition on consistency language and recommendations, and a fixed output format.

### v1.1 - Added small-sample framing, scope limit, and fixed table format - Current
**Change:** Added role, explicit small-sample framing, prohibition on consistency language, scope limit against recommending action, fixed three-column table format, and a mandatory small-sample disclaimer.
**Test input:** Same 8 guest comments used in v1.0 test, for direct comparison.
**Output:** Grouped into 5 themes with correct sentiment labelling, no overgeneralising language, no operational recommendations, and the required disclaimer included at the end.
**Observed effect:** Ready to distribute with brief review - resolved both the overgeneralisation and scope-creep issues identified in v1.0.
**Lesson learned:** Explicitly naming the sample as small and non-representative, rather than only instructing the model to be "accurate", reliably prevented overgeneralising language - a specific framing constraint proved more effective than a general accuracy instruction, consistent with the pattern observed in several other prompts in this library.

---

## Related Prompts

- **Previous in chain:** P09 - Weekly occupancy briefing
- **Parent section:** 03-post-stay-reporting/README.md
- **Note:** This completes Section 3 (Post-stay & Reporting) and the full 10-prompt library.
