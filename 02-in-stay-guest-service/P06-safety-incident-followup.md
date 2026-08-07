# P06 - Safety-Incident Follow-up

**Section:** 02 - In-stay Guest Service
**Workflow step:** Step 3 of 4
**Current version:** v1.0
**Status:** Draft - needs revision
**Last updated:** 6 August 2026

---

## Prompt Text (v1.0 - initial draft)

```
Write a follow-up message about a safety incident at a hotel.
```

**Test input used:** Guest Michael Torres slipped on wet pool deck, mild ankle pain, declined medical assistance, incident ref INC-2026-0731.

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Write a follow-up message about a safety incident at a hotel.`
**Output:** Professional, empathetic tone, but included the phrase "we sincerely apologize for the inconvenience this caused" - language that implicitly assigns cause and could be read as an admission of liability.
**Observed effect:** Not usable - this is the highest-risk failure type identified in the library so far: not an obvious hallucination, but subtle liability-admitting language that reads as professional and could easily be sent without staff noticing the legal risk.
**Lesson learned:** Safety-incident prompts need an explicit, specific prohibition on cause/fault language (not just a general "professional tone" instruction), because plausible-sounding empathetic phrasing can still constitute an implicit admission of fault.
