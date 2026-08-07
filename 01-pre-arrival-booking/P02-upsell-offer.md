# P02 - Pre-arrival Upsell Offer

**Section:** 01 - Pre-arrival & Booking
**Workflow step:** Step 2 of 3
**Current version:** v1.1
**Status:** Tested
**Last updated:** 6 August 2026

---

## Prompt Text (v1.1 - current)

```
You are a Front Desk reservations coordinator at Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne.

Using ONLY the upgrade details provided below, draft a pre-arrival room upgrade offer email. Do not invent any features, prices, or availability claims not supplied. If a detail is missing, write "TBC" for that field.

Guest details:
Guest name: [GUEST_NAME]
Current room type: [CURRENT_ROOM_TYPE]
Check-in date: [CHECK_IN_DATE]
Booking reference: [BOOKING_REF]

Upgrade offer:
Upgraded room type: [UPGRADED_ROOM_TYPE]
Upgrade price: [UPGRADE_PRICE]
Included features: [FEATURES]
Offer deadline: [OFFER_DEADLINE]
Contact method: [CONTACT_METHOD]

Required output:
- Subject line, warm but not pushy tone
- Maximum 120 words
- Present the upgrade as optional, not urgent
- State the price exactly as supplied, do not describe it as a "discount" or "limited-time deal" unless stated
- Do not guarantee availability
- Close with a clear, low-pressure way to respond
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|---|---|---|
| [GUEST_NAME] | PMS booking record | Sarah Nguyen |
| [CURRENT_ROOM_TYPE] | PMS booking record | Standard |
| [CHECK_IN_DATE] | PMS booking record | 15 August 2026 |
| [BOOKING_REF] | PMS-generated reference | LB-48213 |
| [UPGRADED_ROOM_TYPE] | Revenue management, based on availability | Deluxe Sea-view |
| [UPGRADE_PRICE] | Revenue management rate table | AUD 45 per night additional |
| [FEATURES] | Room category feature list | Sea view, larger room, welcome fruit platter |
| [OFFER_DEADLINE] | Business rule | 3 days before check-in |
| [CONTACT_METHOD] | Standard contact channel | Reply to this email or call Front Desk |

---

## Intended Workflow or Task

- **Trigger:** 4 days before a guest's check-in date, if an upgrade is available
- **Actor:** Front Desk coordinator reviews and sends
- **Timing:** Sent after P01 (booking confirmation), ahead of the offer deadline
- **Next step:** Guest replies or calls to confirm; Front Desk updates the booking manually

```
P01 sent -> 4 days before check-in -> [P02 runs] -> Front Desk reviews -> Email sent
                                                                         -> Guest replies or not
```

---

## Problem Being Solved

Upsell offers are currently sent inconsistently - some guests receive them, others do not, depending on staff workload. When offers are sent, wording varies significantly between staff members, and some past emails have used pressure-selling language (e.g. "limited-time offer") without actual time or stock constraints, creating a risk of misleading guests.

**Pain points addressed:**
- Inconsistent outreach - missed upsell revenue opportunity
- Variable, sometimes misleading sales language
- No standard way to present price and availability accurately

---

## Automation Potential

**Level: Medium**

| Dimension | Assessment |
|---|---|
| Repetitiveness | High - applicable to most bookings with upgrade availability |
| Data availability | Depends on Revenue Management confirming upgrade availability and price first |
| Human judgment needed | Medium - deciding which guests/rooms to offer requires business judgment |
| Integration possibility | Could trigger from PMS once Revenue Management flags an available upgrade |
| Estimated time saving | Estimated moderate saving per email (~5-7 minutes), but overall impact depends on adoption rate, which is not yet measured |

**Human-in-the-loop role:** Revenue Management decides which upgrades are offered and at what price; Front Desk reviews wording before sending.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Model invents features, price, or urgency not supplied | Medium | "Using ONLY... do not invent" constraint; explicit ban on "discount"/"limited-time" wording unless stated |
| Guest feels pressured despite low-pressure intent | Low-Medium | Explicit "optional, not urgent" instruction; no guaranteed availability claim |
| Upgrade price becomes outdated if rates change | Medium | Front Desk review step; price must come from current rate table, not memory |
| Guest accepts offer but room is no longer available | Medium | Email explicitly states availability is not guaranteed until confirmed |

**Overall risk rating: MEDIUM** - commercially sensitive content requires human review of pricing and availability before every send.

---

## Evaluation Criteria

- Price stated exactly as supplied, no invented figures
- No pressure-selling or urgency language
- No guaranteed availability claim
- Upgrade presented as optional
- Word limit compliance

---

## Test Cases

| Case | Input summary | Expected behaviour | Result |
|---|---|---|---|
| 1. Normal | Standard to Deluxe Sea-view upgrade, AUD 45/night, 3 named features, deadline 3 days before check-in | Accurate pricing, no invented features, low-pressure optional framing | Pass |

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Write an email offering a room upgrade to a hotel guest before their stay.`
**Output:** Generic templated email with placeholder brand name [Hotel Name]. The model invented an entire upgrade structure not grounded in any real data - four example features, a sample price ("$49 per night"), and a fabricated deadline. Language used high-pressure phrasing ("limited-time offer", "we recommend confirming soon").
**Observed effect:** Not usable - contains fabricated pricing and availability claims that could mislead a guest if sent as-is. No connection to Lantern Bay Hotel or any real upgrade offer.
**Lesson learned:** Without a defined role, real upgrade data, and explicit constraints, the model invents commercially risky content (fake prices, urgency language). Next version needs a "do not invent" constraint and an explicit instruction against pressure-selling language.

### v1.1 - Added RACE structure + grounding + tone constraint - Current
**Change:** Added role, real guest/upgrade data fields, "using only / do not invent" constraint, explicit ban on "discount"/"limited-time" wording unless supplied, "optional not urgent" framing requirement, and no-availability-guarantee rule.
**Test input:** Sarah Nguyen / Standard to Deluxe Sea-view / 15 August 2026 / LB-48213 / AUD 45 per night additional / sea view, larger room, welcome fruit platter / deadline 3 days before check-in.
**Output:** Correctly branded, accurate pricing stated exactly as supplied, no invented features, explicitly optional and non-urgent tone, no availability guarantee, within word limit.
**Observed effect:** Ready to send with only a brief review - no fabricated content or pressure-selling language observed in this test.
**Lesson learned:** Explicitly banning specific pressure-selling phrases (rather than only asking for a general "warm tone") reliably prevented the model from reintroducing urgency language seen in v1.0.

---

## Related Prompts

- **Previous in chain:** P01 - Booking confirmation email
- **Next in chain:** P03 - Pre-arrival FAQ response
- **Parent section:** 01-pre-arrival-booking/README.md
