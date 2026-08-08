# Lantern Bay Hotel - Workflow Automation Prompt Library

A 10-prompt library supporting workflow automation for Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne. Developed as part of BUS4005 Assessment 1.

## What This Library Does

Lantern Bay Hotel currently handles most guest communications and internal reporting manually, resulting in delayed responses, inconsistent tone, and increased risk in sensitive situations (complaints, safety incidents). This reflects a broader industry pattern: Deloitte's 2025 European Hotel Industry and Investment Survey identifies workforce constraints as the hospitality sector's leading operational risk, alongside growing investment in automation to manage service delivery more efficiently (Deloitte, 2025). This library provides 10 tested, RACE-structured prompts across three connected workflow sections to address these operational gaps, while keeping humans in control of all compensation, escalation, and safety-related decisions.

## Library Summary Table

| ID | Prompt | Section | Automation | Risk | Versions |
|---|---|---|---|---|---|
| P01 | Booking confirmation email | Pre-arrival & Booking | High | Low-Medium | v1.0-v1.1 |
| P02 | Pre-arrival upsell offer | Pre-arrival & Booking | Medium | Medium | v1.0-v1.1 |
| P03 | Pre-arrival FAQ response | Pre-arrival & Booking | High | Low-Medium | v1.0-v1.1 |
| P04 | Guest complaint response | In-stay Guest Service | Medium | High | v1.0-v1.2 |
| P05 | Service request triage | In-stay Guest Service | Very High | Medium | v1.0-v1.1 |
| P06 | Safety-incident follow-up | In-stay Guest Service | Low-Medium | High | v1.0-v1.2 |
| P07 | Housekeeping shift handover | In-stay Guest Service | High | Low-Medium | v1.0-v1.1 |
| P08 | Review response draft | Post-stay & Reporting | High | Medium | v1.0-v1.1 |
| P09 | Weekly occupancy briefing | Post-stay & Reporting | Medium | Low | v1.0-v1.1 |
| P10 | Guest feedback theme summary | Post-stay & Reporting | Medium | Low-Medium | v1.0-v1.1 |

## Prompt Chaining Map

**Section 1: Pre-arrival & Booking**
```
Guest books -> P01 (confirmation) -> P02 (upsell offer, 4 days before check-in)
Guest emails a question -> P03 (FAQ response)
```

**Section 2: In-stay Guest Service**
```
Guest raises an issue -> P04 (complaint response) -> if physical safety incident: P06
Service request received -> P05 (triage) -> routed to department
Shift ends -> P07 (handover checklist)
```

**Section 3: Post-stay & Reporting**
```
Review posted -> P08 (response draft) -> theme noted for P10
Week ends -> P09 (occupancy briefing)
Reporting cycle -> P10 (feedback theme summary)
```

## Prompting Strategies Used

- **RACE structure** (Role, Action, Context, Expected output) applied consistently across all 10 prompts, following the framework introduced in the unit's Week 2 tutorial.
- **Grounding constraints** ("using ONLY the information provided... do not invent") used in every prompt to reduce hallucination risk, particularly for pricing (P01, P02), policy (P03), and factual incident details (P04, P06).
- **Structured output (JSON)** used in P05 to support system integration for automated ticket routing, rather than free-text output.
- **Explicit scope restrictions** used to prevent the model from exceeding its intended role - e.g. P04 and P06 prohibit offering compensation, P05 and P08 prohibit suggesting remedies/operational changes beyond the task.
- **Fault-language prohibition** developed specifically for P04 and P06 after testing revealed the model would use subtly liability-admitting language (e.g. "no guest should experience this") even when explicit compensation was already restricted.
- **Escalation-check pattern** added to P04 and P06 (v1.2) after testing with legal-signal test cases revealed neither prompt originally differentiated a legally sensitive complaint from a routine one.
- **Small-sample framing** used in P10 to prevent the model from overgeneralising conclusions from a small number of guest comments, consistent with the "overgeneralising small samples" risk identified in the unit's workshop guide.

## Risk and Automation Philosophy

Automation levels and testing depth in this library are intentionally proportionate to risk, not applied uniformly. P04 and P06 (both rated Overall Risk: HIGH) received the most extensive testing - including adversarial (prompt injection) and legal-signal test cases - and are the only two prompts developed to v1.2. Lower-risk prompts (P01, P03, P09) required only one round of revision once grounding and format constraints were added. This reflects the unit's guidance that "complexity is not the goal" and that revisions should address specific, observed failures rather than be applied uniformly across all prompts.

No prompt in this library is treated as a complete organisational control. Safety- and complaint-related prompts (P04, P06) explicitly require full human review before every send; none of the automation levels assigned imply autonomous action on compensation, legal, or safety matters.

## Iteration Evidence

Full version history, test cases, and observed outputs for each prompt are documented within each prompt file (see `/01-pre-arrival-booking`, `/02-in-stay-guest-service`, `/03-post-stay-reporting`). Commit history for this repository provides an additional chronological record of development.

## References

- Anthropic. (2026). *RACE Framework for Business Prompting* [BUS4005 Week 2 Tutorial Workbook]. La Trobe University.
- [Course provider]. (2026). *Workflow Automation Prompt Library: Worked Examples and Workshop Workbook* [BUS4005 Assessment 1 resource]. La Trobe University.
- Deloitte. (2025). *The 2025 European Hotel Industry and Investment Survey*. Deloitte UK. https://www.deloitte.com/uk/en/Industries/consumer/research/european-hotel-industry-and-investment-survey.html
- Deloitte. (2025). *Future of Hospitality: AI-Driven Industry Trends*. Deloitte US. https://www.deloitte.com/us/en/Industries/consumer/articles/future-of-hospitality-ai-innovation.html

## Repository Structure

```
hotel-prompt-library/
├── 01-pre-arrival-booking/       (P01, P02, P03)
├── 02-in-stay-guest-service/     (P04, P05, P06, P07)
├── 03-post-stay-reporting/       (P08, P09, P10)
└── README.md                     (this file)
```
