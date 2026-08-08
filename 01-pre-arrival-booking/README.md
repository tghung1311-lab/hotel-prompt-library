# Section 1: Pre-arrival & Booking

Three prompts supporting the guest journey from booking confirmation through to check-in, covering confirmed bookings, optional upgrades, and pre-arrival questions.

## Prompts in this section

| ID | Prompt | Automation | Risk |
|---|---|---|---|
| P01 | Booking confirmation email | High | Low-Medium |
| P02 | Pre-arrival upsell offer | Medium | Medium |
| P03 | Pre-arrival FAQ response | High | Low-Medium |

## Chain

```
Booking confirmed -> P01 (confirmation email)
                   -> P02 (upsell offer, sent 4 days before check-in)
Guest emails a question -> P03 (FAQ response)
```

## Section-level risk note

All three prompts in this section are guest-facing and commercially sensitive (pricing, policy commitments), but none involve safety or legal risk. Front Desk or Reservations review is retained before every send, primarily to confirm data accuracy rather than to manage high-severity risk.
