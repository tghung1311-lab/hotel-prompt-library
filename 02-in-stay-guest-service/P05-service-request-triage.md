# P05 - Service Request Triage

**Section:** 02 - In-stay Guest Service
**Workflow step:** Step 2 of 4
**Current version:** v1.1
**Status:** Tested
**Last updated:** 6 August 2026

---

## Prompt Text (v1.1 - current)

```
You are a service-request intake classifier at Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne.

Classify the guest service request using ONLY the information in REQUEST_TEXT. Do not suggest remedies, compensation, or room changes - this is a routing step only.

Allowed category - choose exactly one:
- Maintenance/Plumbing
- Maintenance/Electrical
- Maintenance/HVAC
- Housekeeping
- Front Desk/Administrative
- Other

Urgency rules:
- High: safety hazard (flooding, electrical fault, gas smell), guest requests same-day resolution, or issue prevents normal room use
- Medium: functional issue without safety risk or same-day requirement
- Low: cosmetic or non-urgent request

REQUEST_TEXT:
[REQUEST_TEXT]
ROOM_NUMBER:
[ROOM_NUMBER]

Respond with valid JSON only:
{
  "category": "one allowed category",
  "urgency": "Low, Medium, or High",
  "safety_flag": true or false,
  "routing_department": "Engineering, Housekeeping, or Front Desk",
  "one_sentence_rationale": "brief explanation grounded in the request text"
}
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|---|---|---|
| [REQUEST_TEXT] | Guest call/app/in-person log, verbatim | "Shower drain blocked, water pooling" |
| [ROOM_NUMBER] | Guest-provided or PMS lookup | 305 |

---

## Intended Workflow or Task

- **Trigger:** Guest submits a service request via phone, app, or in person
- **Actor:** System runs the prompt automatically; Housekeeping/Engineering supervisor spot-checks routing
- **Timing:** Immediately on request receipt
- **Next step:** JSON output populates the ticketing system and routes to the correct department queue

```
Request received -> [P05 runs] -> JSON populates ticket -> Routed to department queue
                                                          -> Supervisor spot-checks High-urgency/safety-flagged tickets
```

---

## Problem Being Solved

Service requests are currently triaged manually by whichever staff member answers the phone or app notification, leading to inconsistent categorisation and occasional delays in flagging safety-relevant issues (e.g. water hazards) as high priority. During busy periods, low-urgency requests can also be escalated unnecessarily due to inconsistent judgement.

**Pain points addressed:**
- Inconsistent categorisation and urgency labelling across staff
- Delayed identification of safety-relevant requests
- Manual routing adds delay before the correct department is notified

---

## Automation Potential

**Level: Very High**

| Dimension | Assessment |
|---|---|
| Repetitiveness | Very high - every service request requires this step |
| Data availability | Request text is available at point of submission |
| Human judgment needed | Low for routine routing; supervisor spot-check retained for High-urgency and safety-flagged cases |
| Integration possibility | JSON output can populate a ticketing system directly and trigger department routing rules |
| Estimated time saving | Estimated significant reduction in manual triage time; exact figures require measurement once deployed |

**Human-in-the-loop role:** Supervisor spot-checks a sample of routine tickets and reviews all High-urgency or safety-flagged tickets before dispatch is confirmed.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Safety-relevant request misclassified as low urgency | High | Explicit High-urgency safety triggers; supervisor review of all safety-flagged tickets |
| Category inconsistency across similar requests (confirmed issue in v1.0) | Medium | Fixed category list in v1.1 resolves this |
| Invalid or malformed JSON breaks system integration | Medium | Schema validation on receipt; failed outputs routed to manual queue |
| Request text is ambiguous or covers multiple issues | Medium | "Other" category and rationale field flag ambiguous cases for review |
| Privacy / data security - guest request text and room number sent to an external model | Medium | Limit input to request text and room number only - no guest name or booking reference required for triage; route through an enterprise/private deployment with data-retention controls |
| Bias in urgency classification based on how a request is phrased (e.g. non-native English, brevity, indirect phrasing) | Medium (untested) | This is the highest-bias-risk prompt in the library, since urgency directly affects response priority; not yet stress-tested with requests written in varying English proficiency or phrasing styles; recommend targeted bias testing (same request content, varied phrasing) before wider rollout, alongside routine supervisor spot-checks across a diverse sample of routine tickets, not only High-urgency ones |

**Overall risk rating: MEDIUM** - high automation is appropriate for routing, provided safety-flagged and High-urgency tickets always receive human review before action is taken, and phrasing-based bias in urgency classification is tested before full deployment.

---

## Evaluation Criteria

- Valid JSON matching required schema
- Category chosen from fixed list only
- Urgency and safety flag correctly applied per stated rules
- No suggested remedies or compensation
- Consistent classification across different urgency levels

---

## Test Cases

| Case | Input summary | Expected behaviour | Result |
|---|---|---|---|
| 1. High urgency/safety | Blocked shower drain, water pooling, room 305, guest requested same-day fix | High urgency, safety flag true, routed to Engineering | Pass |
| 2. Low urgency, routine | Guest requested extra towels and pillows, room 218, explicitly "no rush" | Low urgency, safety flag false, routed to Housekeeping | Pass |

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Classify this hotel guest service request.`
**Output:** Model produced a well-formatted table with its own self-determined categories ("Maintenance - Plumbing", "Clogged drain / drainage blockage"), correctly flagged high priority and a safety concern, but also proposed an operational remedy (room change) beyond the scope of a classification step.
**Observed effect:** Not usable for automated routing - output is a human-readable table, not a machine-readable format, and category labels are not drawn from a fixed taxonomy, risking inconsistent labelling across different requests.
**Lesson learned:** Triage prompts feeding into a routing system need a fixed category list, explicit urgency rules, a structured (JSON) output format, and a scope limit preventing the model from proposing remedies beyond classification.

### v1.1 - Added fixed taxonomy, urgency rules, and JSON schema - Current
**Change:** Added role, a fixed category list, explicit urgency rules with safety triggers, a required JSON output schema, and an explicit scope restriction against suggesting remedies.
**Test case 1 (high urgency/safety):** Blocked shower drain, water pooling, room 305, guest requested same-day fix.
**Output 1:** `{"category": "Maintenance/Plumbing", "urgency": "High", "safety_flag": true, "routing_department": "Engineering", "one_sentence_rationale": "Blocked shower drain causing water to pool on the floor is a same-day flooding/slip hazard that prevents normal use of the bathroom."}`
**Test case 2 (low urgency, routine):** Guest requested extra towels and pillows, room 218, explicitly "no rush".
**Output 2:** `{"category": "Housekeeping", "urgency": "Low", "safety_flag": false, "routing_department": "Housekeeping", "one_sentence_rationale": "Guest requested extra towels and pillows with no urgency, explicitly stating no rush."}`
**Observed effect:** Valid JSON in both cases, correct category and urgency classification at both ends of the urgency scale, no suggested remedies in either output.
**Lesson learned:** A fixed taxonomy and explicit urgency rules produce consistent, schema-valid classification across both high-risk and routine request types, confirming the prompt generalises beyond a single test case.

---

## Related Prompts

- **Previous in chain:** P04 - Guest complaint response
- **Next in chain:** P06 - Safety-incident follow-up
- **Parent section:** 02-in-stay-guest-service/README.md
