# P03 - Pre-arrival FAQ Response

**Section:** 01 - Pre-arrival & Booking
**Workflow step:** Step 3 of 3
**Current version:** v1.0
**Status:** Draft - needs revision
**Last updated:** 6 August 2026

---

## Prompt Text (v1.0 - initial draft)

```
Answer a hotel guest's question about their upcoming booking.
```

**Test input used:** "Hi, I booked a room at your hotel for 20-22 August. Can I bring my dog? Also does the room have a bathtub?"

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Answer a hotel guest's question about their upcoming booking.`
**Output:** The model identified itself as an AI assistant without access to real booking or hotel information, and declined to answer, instead suggesting the guest contact the hotel directly.
**Observed effect:** Not usable for the workflow - without a defined role and supplied data, the model correctly avoids inventing an answer, but this means the prompt cannot function as an automated FAQ response tool.
**Lesson learned:** A prompt intended for automated business use must explicitly assign a role and supply the relevant policy and booking data directly - it cannot rely on the model to look up or assume information.
