# P04 - Guest Complaint Response

**Section:** 02 - In-stay Guest Service
**Workflow step:** Step 1 of 4
**Current version:** v1.2
**Status:** Tested
**Last updated:** 6 August 2026

---

## Prompt Text (v1.2 - current)

```
You are a Guest Services duty manager at Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne.

Using ONLY the complaint and policy details provided below, draft a response to the guest's complaint. Do not offer any compensation, refund, discount, or free night - these decisions are made by the Duty Manager after review, not by this draft. Do not promise a specific timeframe for maintenance or room changes unless supplied below. Do not use any language that implies the incident should not have happened or that assigns fault, even indirectly (e.g. avoid phrases like "no guest should experience this").

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
- Acknowledge the issue and apologise sincerely, using neutral language that does not assign fault
- State only the available action(s) supplied above, framed as being arranged, not offered as a choice requiring guest approval on compensation
- Do NOT mention or imply any refund, discount, free night, or specific compensation amount
- Close by inviting the guest to contact Guest Services directly with any further concerns

Escalation check:
If the complaint contains language suggesting potential legal action, media 
involvement, or a worsening medical situation (e.g. mentions of "lawyer", 
"legal", "options", "compensation", "media", "press", "sue", or similar), 
add this line at the very end, after the email:

"ESCALATION REQUIRED: [brief reason]. Route to Duty Manager AND General 
Manager, not Duty Manager alone."

If no such language is present, end with: "Escalated to Duty Manager for 
compensation review."
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|---|---|---|
| [GUEST_NAME] | PMS booking record | Rachel Kim |
| [ROOM_NUMBER] | Complaint/incident log | 219 |
| [BOOKING_REF] | PMS booking record | LB-72340 |
| [COMPLAINT_TEXT] | Guest email/call log, verbatim | Slip near lobby entrance complaint |
| [AVAILABLE_ACTIONS] | Duty Manager / relevant department, confirmed before drafting | First-aid staff offered, guest declined |

---

## Intended Workflow or Task

- **Trigger:** Guest complaint logged via phone, email, or in person
- **Actor:** Duty Manager confirms available actions, then reviews and sends the drafted response
- **Timing:** Within 30 minutes of complaint being logged
- **Next step:** If compensation is warranted, Duty Manager approves separately; if escalation-flagged, General Manager is also notified

```
Complaint logged -> Duty Manager confirms available actions -> [P04 runs] -> Duty Manager reviews -> Response sent
                                                                                                     -> Compensation decision made separately
                                                                                                     -> If flagged: General Manager also notified
```

---

## Problem Being Solved

Complaint responses are currently drafted individually by whichever staff member is available, leading to inconsistent tone and, in some past cases, verbal compensation promises made without management approval. There is also no consistent method for flagging complaints with legal or media risk for senior management attention.

**Pain points addressed:**
- Delayed complaint acknowledgement during busy periods
- Risk of staff making unauthorised compensation commitments
- Inconsistent tone, including subtle fault-admitting language
- No standard mechanism to flag legally sensitive complaints for escalation beyond Duty Manager level

---

## Automation Potential

**Level: Medium**

| Dimension | Assessment |
|---|---|
| Repetitiveness | High - complaints are frequent, though content varies |
| Data availability | Complaint text and available actions must be manually confirmed first |
| Human judgment needed | High - compensation decisions and available-actions confirmation remain fully human |
| Integration possibility | Could integrate with a complaint-logging system once actions are confirmed |
| Estimated time saving | Estimated moderate saving on drafting time; exact figures require measurement, and the confirmation step still requires human time |

**Human-in-the-loop role:** Duty Manager confirms available actions before the prompt runs, reviews the drafted response, and makes all compensation decisions separately. The escalation flag prompts additional human attention; it does not autonomously notify anyone.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Model offers unauthorised compensation (confirmed in v1.0 test) | High | Explicit prohibition on mentioning refund/discount/compensation; resolved in v1.1 testing |
| Model uses subtle fault-admitting language (confirmed in v1.1 legal-signal test) | High | Explicit prohibition on indirect fault language added in v1.2; resolved in retest |
| Legal/media risk signal not escalated beyond standard Duty Manager review (confirmed in v1.1 legal-signal test) | High | Escalation check added in v1.2; resolved in retest |
| Escalation keyword list is not exhaustive - differently phrased risk signals may be missed | Medium | Escalation flag supplements, does not replace, Duty Manager judgment; full human review remains mandatory for every complaint |
| Complaint involves a legal, safety, or media-sensitive issue beyond this prompt's scope | High | For complaints overlapping with physical safety incidents, use P06 instead |

**Overall risk rating: HIGH** - always requires human confirmation of available actions and full human review before sending; this prompt assists drafting only and does not make any commitment or escalation decisions itself.

---

## Evaluation Criteria

- No compensation offered or implied
- No fault-admitting language, direct or indirect
- Only supplied available actions stated, none invented
- Correct escalation flagging, with no false positives on routine complaints
- Format and word-limit compliance

---

## Test Cases

| Case | Input summary | Expected behaviour | Result |
|---|---|---|---|
| 1. Normal (v1.0/v1.1) | AC rattling noise complaint, room 412 | No compensation offered, only supplied actions stated | Pass (v1.1) |
| 2. Legal-signal | Guest slipped near lobby, wrist swollen, mentions "speak to a lawyer" | No fault-admitting language; should flag escalation | v1.1: fault language found, no escalation flag (gap). v1.2: both issues resolved |

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Write a response to a hotel guest's complaint.`
**Output:** The model independently offered specific compensation options (full refund, complimentary night, or discount), promised a maintenance timeframe not confirmed by any policy, and committed to a personal follow-up later that day - none of which were authorised or supplied.
**Observed effect:** Not usable - the draft makes unauthorised financial commitments and operational promises that only a Duty Manager should approve.
**Lesson learned:** For complaint responses, the model will invent compensation offers and specific commitments if not explicitly restricted. Required an explicit prohibition on offering compensation, plus a mandatory escalation instruction.

### v1.1 - Added role, compensation prohibition, and constrained action list
**Change:** Added role (Guest Services duty manager), explicit prohibition on mentioning any compensation, a constrained list of available actions the model must choose from, and a mandatory escalation line for compensation review.
**Testing:** Normal case (AC noise) passed cleanly. A second test with a legal-signal complaint (guest mentioning "speak to a lawyer") revealed two further issues: subtle fault-admitting language ("no guest should experience this") and no differentiated escalation for the legal risk signal - both treated identically to a routine complaint.
**Observed effect:** Resolved the original compensation-offering risk, but testing beyond the initial case uncovered a second, more subtle risk pattern consistent with a similar finding in P06.
**Lesson learned:** Testing only a single routine case can miss risks that only appear in higher-risk scenarios - extending testing to a legal-signal case surfaced failure modes the normal case did not reveal, reinforcing the value of testing beyond the first successful case for high-risk prompts.

### v1.2 - Added indirect fault-language prohibition and escalation check - Current
**Change:** Added explicit prohibition on indirect fault-admitting language (with an example phrase to avoid), and the same legal/media escalation check mechanism used in P06.
**Testing:** Retested the legal-signal case (Rachel Kim) that revealed both issues in v1.1.
**Observed effect:** Fault-admitting language was replaced with neutral wellbeing-focused language, and the escalation flag was correctly added with an accurate stated reason, routing to both Duty Manager and General Manager.
**Lesson learned:** The same escalation-check pattern developed for P06 transferred directly to P04, confirming that legal/media risk signals are a recurring risk category across guest-facing response prompts in this library, not an isolated case - suggesting this pattern may be worth applying consistently to any future prompt handling guest-reported incidents or complaints.

---

## Related Prompts

- **Next in chain:** P05 - Service request triage
- **Related (escalation path):** P06 - Safety-incident follow-up (for complaints involving physical safety, legal, or media risk)
- **Parent section:** 02-in-stay-guest-service/README.md
