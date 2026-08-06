# P02 - Pre-arrival Upsell Offer

**Section:** 01 - Pre-arrival & Booking
**Workflow step:** Step 2 of 3
**Current version:** v1.0
**Status:** Draft - needs revision
**Last updated:** 6 August 2026

---

## Prompt Text (v1.0 - initial draft)

```
Write an email offering a room upgrade to a hotel guest before their stay.
```

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Write an email offering a room upgrade to a hotel guest before their stay.`
**Output:** Generic templated email with placeholder brand name [Hotel Name]. The model invented an entire upgrade structure not grounded in any real data - four example features, a sample price ("$49 per night"), and a fabricated deadline. Language used high-pressure phrasing ("limited-time offer", "we recommend confirming soon").
**Observed effect:** Not usable - contains fabricated pricing and availability claims that could mislead a guest if sent as-is. No connection to Lantern Bay Hotel or any real upgrade offer.
**Lesson learned:** Without a defined role, real upgrade data, and explicit constraints, the model invents commercially risky content (fake prices, urgency language). Next version needs a "do not invent" constraint and an explicit instruction against pressure-selling language.
