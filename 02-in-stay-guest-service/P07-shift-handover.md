# P07 - Housekeeping Shift Handover

**Section:** 02 - In-stay Guest Service
**Workflow step:** Step 4 of 4
**Current version:** v1.0
**Status:** Draft - needs revision
**Last updated:** 6 August 2026

---

## Prompt Text (v1.0 - initial draft)

```
Turn these housekeeping notes into a handover checklist.
```

**Test input used:** Rooms 210 and 314 have 11am early arrivals; Room 402 needs final bathroom check after shower repair; linen delivery at loading dock 9:30am; VIP room 501 requires hypoallergenic pillows and no fragranced amenities; sunglasses found in room 108 to go to front desk as lost property.

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Turn these housekeeping notes into a handover checklist.`
**Output:** Well-organised checklist grouped into logical sections, but the model added actions not present in the source notes - "check quantity against order" for the linen delivery, and "replace with unscented alternatives" for the VIP room, implying an action (replacement) that was not stated. No sign-off lines included.
**Observed effect:** Not fully usable - added tasks not confirmed by the source notes could lead staff to perform unnecessary or incorrect actions (e.g. checking a delivery order that may not exist in this form).
**Lesson learned:** Even a well-structured, readable output can still contain invented content. Needed an explicit "do not add tasks not stated" constraint, a defined chronological format, and sign-off lines for accountability.
