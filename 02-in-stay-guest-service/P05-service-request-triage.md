# P05 - Service Request Triage

**Section:** 02 - In-stay Guest Service
**Workflow step:** Step 2 of 4
**Current version:** v1.0
**Status:** Draft - needs revision
**Last updated:** 6 August 2026

---

## Prompt Text (v1.0 - initial draft)

```
Classify this hotel guest service request.
```

**Test input used:** "Room 305 here, the shower drain is completely blocked and water is pooling on the floor. Can someone come fix this today?"

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Classify this hotel guest service request.`
**Output:** Model produced a well-formatted table with its own self-determined categories ("Maintenance - Plumbing", "Clogged drain / drainage blockage"), correctly flagged high priority and a safety concern, but also proposed an operational remedy (room change) beyond the scope of a classification step.
**Observed effect:** Not usable for automated routing - output is a human-readable table, not a machine-readable format, and category labels are not drawn from a fixed taxonomy, risking inconsistent labelling across different requests.
**Lesson learned:** Triage prompts feeding into a routing system need a fixed category list, explicit urgency rules, a structured (JSON) output format, and a scope limit preventing the model from proposing remedies beyond classification.
