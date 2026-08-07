# P03 - Pre-arrival FAQ Response

**Section:** 01 - Pre-arrival & Booking
**Workflow step:** Step 3 of 3
**Current version:** v1.1
**Status:** Tested
**Last updated:** 6 August 2026

---

## Prompt Text (v1.1 - current)

```
You are a Front Desk guest-services assistant at Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne.

Using ONLY the hotel policies and booking details provided below, answer the guest's question. Do not invent policies, amenities, or details not supplied. If the question cannot be answered from the supplied information, say so and direct the guest to contact Front Desk directly.

Hotel policies:
[HOTEL_POLICIES]

Booking details:
Booking reference: [BOOKING_REF]
Check-in date: [CHECK_IN_DATE]
Check-out date: [CHECK_OUT_DATE]
Room type: [ROOM_TYPE]

Guest question:
[GUEST_QUESTION]

Required output:
- Warm, helpful tone, maximum 100 words
- Answer each part of the guest's question separately and clearly
- Reference the booking details only where relevant
- If any part of the question cannot be answered from supplied information, state this explicitly and provide the Front Desk contact method
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|---|---|---|
| [HOTEL_POLICIES] | Static policy database (pet policy, room amenities, etc.) | Pet policy, bathtub availability by room type |
| [BOOKING_REF] | PMS booking record | LB-55201 |
| [CHECK_IN_DATE] / [CHECK_OUT_DATE] | PMS booking record | 20-22 August 2026 |
| [ROOM_TYPE] | PMS booking record | Standard |
| [GUEST_QUESTION] | Guest email/enquiry form | "Can I bring my dog? Does the room have a bathtub?" |

---

## Intended Workflow or Task

- **Trigger:** Guest sends a pre-arrival question via email or enquiry form
- **Actor:** Reservations coordinator reviews and sends
- **Timing:** Within a few hours of enquiry received
- **Next step:** If question cannot be answered from supplied policy data, escalated to Front Desk supervisor

```
Guest question received -> [P03 runs] -> Reservations reviews -> Reply sent
                                                                -> If unanswerable: escalate to Front Desk
```

---

## Problem Being Solved

Pre-arrival questions (pet policy, room amenities, parking, etc.) are currently answered manually by checking multiple internal references or asking a colleague, causing delayed responses - particularly outside business hours. Response consistency also varies, as different staff may not be aware of all current policies.

**Pain points addressed:**
- Delayed responses to routine pre-arrival questions
- Inconsistent or incomplete answers depending on which staff member responds
- Risk of staff guessing an answer instead of checking current policy

---

## Automation Potential

**Level: High**

| Dimension | Assessment |
|---|---|
| Repetitiveness | High - pet policy, amenities, and parking are common recurring questions |
| Data availability | Policies are static and can be maintained in a reference document |
| Human judgment needed | Low for supplied-policy questions; escalation needed for anything outside supplied data |
| Integration possibility | Could integrate with a guest enquiry form or email inbox |
| Estimated time saving | Estimated moderate saving per enquiry, though exact figures require measurement once deployed |

**Human-in-the-loop role:** Reservations coordinator reviews the reply and confirms escalation is used when a question falls outside supplied policy data.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Model invents a policy not in the supplied policy data | Medium | "Using ONLY... do not invent" constraint; explicit fallback to escalate unanswerable questions |
| Model declines to answer entirely without role/context (as seen in v1.0) | Low (once mitigated) | Explicit role and hotel-specific context added in v1.1 |
| Model proactively offers unsolicited suggestions (e.g. upgrade offer) beyond the question asked | Low-Medium | Human review step checks whether additional suggestions are appropriate before sending |
| Guest policy question relates to a sensitive topic (e.g. accessibility, medical needs) | Medium | Escalation path required for anything outside standard supplied policies |

**Overall risk rating: LOW-MEDIUM** - suitable for high automation with policy data kept current and an escalation path retained.

---

## Evaluation Criteria

- Both parts of a multi-part question answered
- No invented policies or amenities
- Correct escalation for unanswerable questions
- Booking details referenced accurately where relevant
- Word limit compliance

---

## Test Cases

| Case | Input summary | Expected behaviour | Result |
|---|---|---|---|
| 1. Normal | Guest asks about pet policy and bathtub availability, Standard room | Both questions answered accurately from supplied policy data | Pass |

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Answer a hotel guest's question about their upcoming booking.` (tested with a sample guest question about pet policy and bathtub availability)
**Output:** The model identified itself as an AI assistant without access to real booking or hotel information, and declined to answer, instead suggesting the guest contact the hotel directly.
**Observed effect:** Not usable for the workflow - without a defined role and supplied data, the model correctly avoids inventing an answer, but this means the prompt cannot function as an automated FAQ response tool.
**Lesson learned:** A prompt intended for automated business use must explicitly assign a role and supply the relevant policy and booking data directly - it cannot rely on the model to look up or assume information.

### v1.1 - Added role, hotel policy data, and escalation fallback - Current
**Change:** Added role (Front Desk guest-services assistant), explicit hotel policy data, real booking details, "using only / do not invent" constraint, and an explicit escalation instruction for unanswerable questions.
**Test input:** Booking LB-55201, Standard room, 20-22 August 2026; guest question about pet policy and bathtub availability.
**Output:** Answered both parts of the question accurately using only supplied policy data, correctly noted the Standard room has a shower only, and appropriately mentioned upgrade rooms with bathtubs (grounded in supplied data, not invented).
**Observed effect:** Ready to send with brief review. Resolved the core failure of v1.0 (refusal to answer) while remaining grounded in supplied information.
**Lesson learned:** Assigning a role and supplying policy data directly resolves both the hallucination risk and the "unhelpful refusal" risk seen when a prompt lacks business context entirely.

---

## Related Prompts

- **Previous in chain:** P02 - Pre-arrival upsell offer
- **Parent section:** 01-pre-arrival-booking/README.md
- **Note:** This completes Section 1 (Pre-arrival & Booking). Section 2 (In-stay Guest Service) begins with P04.
