# P10 - Guest Feedback Theme Summary

**Section:** 03 - Post-stay & Reporting
**Workflow step:** Step 3 of 3
**Current version:** v1.0
**Status:** Draft - needs revision
**Last updated:** 6 August 2026

---

## Prompt Text (v1.0 - initial draft)

```
Summarise the themes in these guest feedback comments.
```

**Test input used:** 8 guest comments covering pool/views, check-in speed, breakfast options, staff service, room noise, location, checkout, and wifi.

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Summarise the themes in these guest feedback comments.`
**Output:** Correctly grouped comments into positive/negative themes with source references, but used overgeneralising language ("Guests are consistently happy...") despite each theme being supported by only one comment, and proactively recommended an operational review beyond the scope of theme identification.
**Observed effect:** Not fully usable - overgeneralising a small qualitative sample risks misrepresenting guest sentiment to management, and the unsolicited operational recommendation exceeds the intended scope of this reporting step.
**Lesson learned:** With small samples, the model tends to imply broader consistency than the data supports and to suggest actions beyond the requested task. Needed an explicit small-sample framing, a prohibition on consistency language and recommendations, and a fixed output format.
