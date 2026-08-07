# P08 - Review Response Draft

**Section:** 03 - Post-stay & Reporting
**Workflow step:** Step 1 of 3
**Current version:** v1.0
**Status:** Draft - needs revision
**Last updated:** 6 August 2026

---

## Prompt Text (v1.0 - initial draft)

```
Write a response to this hotel review.
```

**Test input used:** 3-night stay review, 3/5 stars - clean room and good check-in staff praised; evening pool noise from nearby event and limited breakfast options criticised.

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Write a response to this hotel review.`
**Output:** Well-structured response acknowledging both positive and negative points, but committed to specific unconfirmed operational changes - "we'll look into ways to better manage this... whether through timing adjustments or clearer communication about nearby events."
**Observed effect:** Not usable as-is - promising specific operational fixes without management approval creates a public, written commitment the hotel may not be able to deliver on.
**Lesson learned:** Similar to the complaint-response prompt (P04), the model tends to offer unauthorised commitments when responding to negative feedback. Needed an explicit constraint against promising specific changes or timelines, and a word limit suited to a public review platform.
