# P01 - Booking Confirmation Email

**Section:** 01 - Pre-arrival & Booking
**Workflow step:** Step 1 of 3
**Current version:** v1.0
**Status:** Draft - needs revision
**Last updated:** 6 August 2026

---

## Prompt Text (v1.0 - initial draft)

```
Write a booking confirmation email for a hotel guest.
```

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Write a booking confirmation email for a hotel guest.`
**Output:** Generic templated email using only placeholder fields (e.g. [Hotel Name], [Guest Name]). The model independently added extra sections not requested - Payment Summary, Hotel Address, and a "Good to Know" list covering cancellation, Wi-Fi/breakfast inclusions, and ID requirements - none grounded in any supplied business data.
**Observed effect:** Not usable - no connection to Lantern Bay Hotel, no real booking data, and several invented policy-like sections that could be inaccurate if sent as-is.
**Lesson learned:** Without a defined role and real booking data, the model invents both content and structure, including policy-sensitive sections (payment, cancellation) that must not be fabricated. Needed an explicit role, real booking data, and constraints against inventing structure or policy content.
