# P04 - Guest Complaint Response

**Section:** 02 - In-stay Guest Service
**Workflow step:** Step 1 of 4
**Current version:** v1.0
**Status:** Draft - needs revision
**Last updated:** 6 August 2026

---

## Prompt Text (v1.0 - initial draft)

```
Write a response to a hotel guest's complaint.
```

**Test input used:** "The air conditioning in my room (412) has been making a loud rattling noise all night and I couldn't sleep. This is unacceptable for what I'm paying."

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Write a response to a hotel guest's complaint.`
**Output:** The model independently offered specific compensation options (full refund, complimentary night, or discount), promised a maintenance timeframe not confirmed by any policy, and committed to a personal follow-up later that day - none of which were authorised or supplied.
**Observed effect:** Not usable - the draft makes unauthorised financial commitments and operational promises that only a Duty Manager should approve. Sending this as-is could commit the hotel to compensation without management review.
**Lesson learned:** For complaint responses, the model will invent compensation offers and specific commitments if not explicitly restricted. This is the highest-risk prompt in the library so far and requires an explicit prohibition on offering compensation, plus a mandatory escalation instruction.
