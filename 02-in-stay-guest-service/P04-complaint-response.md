# P04 - Guest Complaint Response

**Section:** 02 - In-stay Guest Service
**Workflow step:** Step 1 of 4
**Current version:** v1.1
**Status:** Tested
**Last updated:** 6 August 2026

---

## Prompt Text (v1.1 - current)

```
You are a Guest Services duty manager at Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne.

Using ONLY the complaint and policy details provided below, draft a response to the guest's complaint. Do not offer any compensation, refund, discount, or free night - these decisions are made by the Duty Manager after review, not by this draft. Do not promise a specific timeframe for maintenance or room changes unless supplied below.

Guest details:
Guest name: [GUEST_NAME]
Room number: [ROOM_NUMBER]
Booking reference: [BOOKING_REF]

Complaint:
[COMPLAINT_TEXT]

Available immediate actions (choose only from this list, do not invent others):
[AVAILABLE_ACTIONS]

Required output:
- Subject line
- Maximum 130 words
- Acknowledge the issue and apologise sincerely
- State only the available action(s) supplied above, framed as being arranged, not offered as a choice requiring guest approval on compensation
- Do NOT mention or imply any refund, discount, free night, or specific compensation amount
- Close by inviting the guest to contact Guest Services directly with any further concerns
- End with a note to escalate to Duty Manager for compensation review
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|---|---|---|
| [GUEST_NAME] | PMS guest record | James Whitfield |
| [ROOM_NUMBER] | PMS booking record | 412 |
| [BOOKING_REF] | PMS-generated reference | LB-61094 |
| [COMPLAINT_TEXT] | Guest email/verbal complaint logged by staff | AC rattling noise, guest couldn't sleep |
| [AVAILABLE_ACTIONS] | Duty Manager/Maintenance-confirmed options | Maintenance inspection within 2 hrs; room change subject to availability |

---

## Intended Workflow or Task

- **Trigger:** Complaint logged by Front Desk or Guest Services staff
- **Actor:** Duty Manager reviews and sends
- **Timing:** As soon as possible after complaint is logged
- **Next step:** Duty Manager separately reviews the case for compensation decision

```
Complaint logged -> Duty Manager confirms available actions -> [P04 runs] -> Duty Manager reviews -> Response sent
                                                                                                    -> Escalated for compensation review
```

---

## Problem Being Solved

Complaint responses are currently drafted individually by whichever staff member is available, with no consistent process for what can and cannot be promised. This creates a real risk of staff verbally or in writing committing the hotel to refunds or compensation without management approval, and inconsistent tone/quality depending on who responds.

**Pain points addressed:**
- Risk of unauthorised compensation commitments by junior staff
- Inconsistent complaint-handling tone and structure
- No standard mechanism to route compensation decisions to the Duty Manager

---

## Automation Potential

**Level: Medium**

| Dimension | Assessment |
|---|---|
| Repetitiveness | Medium-High - complaints are frequent but vary in content |
| Data availability | Complaint text and available actions must be confirmed by staff first |
| Human judgment needed | High - every response requires Duty Manager review before sending |
| Integration possibility | Could integrate with a complaint-logging system, but compensation decision must remain a separate manual step |
| Estimated time saving | Estimated saving on drafting time only; compensation review time is unaffected and remains fully manual |

**Human-in-the-loop role:** Duty Manager confirms available actions before the prompt runs, reviews the drafted response before sending, and separately decides on any compensation.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Model offers unauthorised compensation (confirmed in v1.0) | High | Explicit prohibition on mentioning refund/discount/compensation; escalation line required in output |
| Model invents an available action not confirmed by staff | Medium | "Choose only from this list, do not invent others" constraint |
| Model promises an unconfirmed timeframe | Medium | Timeframe only included if explicitly supplied in [AVAILABLE_ACTIONS] |
| Complaint involves a safety or legal issue beyond this prompt's scope | High | Out of scope for this prompt - routed to P06 (Safety-incident follow-up) instead |

**Overall risk rating: HIGH** - complaint handling is commercially and reputationally sensitive; mandatory human review before every send, with compensation decisions kept fully separate from the drafting step.

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Write a response to a hotel guest's complaint.`
**Output:** The model independently offered specific compensation options (full refund, complimentary night, or discount), promised a maintenance timeframe not confirmed by any policy, and committed to a personal follow-up later that day - none of which were authorised or supplied.
**Observed effect:** Not usable - the draft makes unauthorised financial commitments and operational promises that only a Duty Manager should approve. Sending this as-is could commit the hotel to compensation without management review.
**Lesson learned:** For complaint responses, the model will invent compensation offers and specific commitments if not explicitly restricted. This is the highest-risk prompt in the library so far and requires an explicit prohibition on offering compensation, plus a mandatory escalation instruction.

### v1.1 - Added role, compensation prohibition, and escalation requirement - Current
**Change:** Added role (Guest Services duty manager), explicit prohibition on offering any compensation, restricted available actions to a supplied list only, removed ability to invent timeframes, and required an explicit escalation line for compensation review.
**Test input:** James Whitfield / Room 412 / LB-61094 / AC rattling noise complaint / available actions: maintenance inspection within 2 hrs, room change subject to availability.
**Output:** No mention of compensation anywhere in the response. Only the two supplied actions were presented. Response correctly ended with an escalation note to the Duty Manager for compensation review.
**Lesson learned:** Explicitly prohibiting compensation language (rather than simply omitting a mention of it) reliably prevented the model from reintroducing the unauthorised offers seen in v1.0. This is the most critical constraint in the entire library given the financial and reputational risk involved.

---

## Related Prompts

- **Next in chain:** P05 - Service request triage
- **Related (escalation path):** P06 - Safety-incident follow-up (used when complaint involves safety/legal risk)
- **Parent section:** 02-in-stay-guest-service/README.md
