# P01 · Booking Confirmation Email

**Section:** 01 — Pre-arrival & Booking
**Workflow step:** Step 1 of 3
**Current version:** v1.1
**Status:** Tested
**Last updated:** 6 August 2026

---

## Prompt Text (v1.1 — current)
**Placeholders to fill:**

| Placeholder | Source | Example |
|---|---|---|
| [GUEST_NAME] | PMS booking record | Sarah Nguyen |
| [ROOM_TYPE] | PMS room category | Deluxe Sea-view |
| [CHECK_IN_DATE] / [CHECK_OUT_DATE] | PMS booking record | 15–18 August 2026 |
| [BOOKING_REF] | PMS-generated reference | LB-48213 |
| [RATE_PER_NIGHT] | PMS rate field | AUD 245 |
| [CANCELLATION_POLICY] | Static — rate policy table | Free cancellation up to 48 hrs before check-in |

---

## Intended Workflow or Task

- **Trigger:** New booking confirmed in the Property Management System (PMS)
- **Actor:** Front Desk coordinator reviews and sends
- **Timing:** Within 1 hour of booking confirmation
- **Next step:** P02 (pre-arrival upsell offer) sent 3 days before check-in
---

## Problem Being Solved

Front Desk staff currently draft each confirmation manually, estimated at **~8–10 minutes per booking**. During weekend peak periods (est. 25–30 bookings/day), this creates a backlog that delays guest confirmations by several hours. Manually drafted emails also vary in completeness — cancellation policy is occasionally omitted, leading to guest disputes at cancellation time.

**Pain points addressed:**
- Slow confirmation turnaround during peak periods
- Inconsistent inclusion of cancellation policy
- Variable tone/formatting across staff members

---

## Automation Potential

**Level: High**

| Dimension | Assessment |
|---|---|
| Repetitiveness | Very high — every booking requires this step |
| Data availability | All fields exist in the PMS |
| Human judgment needed | Low — mainly a review-before-send check |
| Integration possibility | Could trigger automatically from PMS booking-confirmed event |
| Estimated time saving | Estimated ~70–80% reduction (8–10 min → ~2 min review), assuming PMS data is complete |

**Human-in-the-loop role:** Front Desk coordinator confirms all fields resolved correctly (no unexplained "TBC") before sending.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Model invents a detail not supplied (e.g. guesses a rate) | Medium | "Using ONLY... do not invent" constraint; "TBC" fallback for missing fields |
| Cancellation policy misquoted or paraphrased incorrectly | Medium | Prompt requires exact policy text as supplied, not a rewritten version |
| PMS data error carried into email uncorrected | Low-Medium | Front Desk review step retained before send |
| Guest receives email with unresolved "TBC" fields | Low | Coordinator checklist includes a "no TBC" check before sending |

**Overall risk rating: LOW-MEDIUM** — suitable for high automation with a lightweight human review step retained.

---

## Version History

### v1.0 — Initial draft
**Prompt:** `Write a booking confirmation email for a hotel guest.`
**Output:** Generic templated email with placeholder fields (e.g. [Hotel Name], [Guest Name]). No connection to Lantern Bay Hotel specifically; sections such as "Rate Summary" and "Hotel Address" were entirely self-determined by the model rather than specified.
**Observed effect:** Not usable without significant rewriting — no defined role, no real booking data, no format constraints.
**Lesson learned:** Vague prompts leave the model to invent structure and content. Needed an explicit role, real booking data, and output constraints.

### v1.1 — Added RACE structure + grounding constraint ✅ Current
**Change:** Added role (Front Desk coordinator at Lantern Bay Hotel), explicit placeholder fields, "using only / do not invent" constraint, TBC fallback, 150-word limit, and exact cancellation-policy requirement.
**Test input:** Sarah Nguyen / Deluxe Sea-view / 15–18 August 2026 / 2 guests / LB-48213 / AUD 245 / free cancellation up to 48 hrs.
**Output:** Complete, hotel-branded, accurate email including all supplied details in the required order, exact cancellation wording retained, no invented content, within the word limit.
**Observed effect:** Ready to send with only a brief review — a substantial improvement over v1.0.
**Lesson learned:** Explicit grounding instructions and a defined role reliably prevent the model from filling structural or content gaps with generic, unbranded assumptions.

---

## Related Prompts

- **Next in chain:** P02 — Pre-arrival upsell offer
- **Parent section:** 01-pre-arrival-booking/README.md
