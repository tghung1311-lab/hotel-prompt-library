# Lantern Bay Hotel - Workflow Automation Prompt Library

A 10-prompt library supporting workflow automation for Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne. Developed as part of BUS4005 Assessment 1.

## What This Library Does

Lantern Bay Hotel currently handles most guest communications and internal reporting manually, resulting in delayed responses, inconsistent tone, and increased risk in sensitive situations (complaints, safety incidents). This reflects a broader industry pattern: Deloitte's 2025 European Hotel Industry and Investment Survey identifies workforce constraints as the hospitality sector's leading operational risk, alongside growing investment in automation to manage service delivery more efficiently (Deloitte, 2025a). This is consistent with broader findings that AI in hospitality is moving from experimentation toward measurable operational value in guest communications (Deloitte, 2025b). This operational focus also carries strategic weight: industry benchmarking shows hotels' review response speed correlates directly with their Global Review Index, a widely used measure of guest satisfaction and online reputation (Shiji Group, 2025).

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

- **RACE structure** (Role, Action, Context, Expected output) applied consistently across all 10 prompts to ensure each prompt defines a clear role, a single precise action, sufficient business context, and a checkable expected output.
- **Grounding constraints** ("using ONLY the information provided... do not invent") used in every prompt to reduce hallucination risk, particularly for pricing (P01, P02), policy (P03), and factual incident details (P04, P06). This technique - restricting the model to supplied information only - is a documented practice for reducing hallucination in production LLM systems (Anthropic, n.d.).
- **Structured output (JSON)** used in P05 to support system integration for automated ticket routing, rather than free-text output.
- **Explicit scope restrictions** used to prevent the model from exceeding its intended role - e.g. P04 and P06 prohibit offering compensation, P05 and P08 prohibit suggesting remedies/operational changes beyond the task.
- **Fault-language prohibition** developed specifically for P04 and P06 after testing revealed the model would use subtly liability-admitting language (e.g. "no guest should experience this") even when explicit compensation was already restricted.
- **Escalation-check pattern** added to P04 and P06 (v1.2) after testing with legal-signal test cases revealed neither prompt originally differentiated a legally sensitive complaint from a routine one.
- **Small-sample framing** used in P10 to prevent the model from overgeneralising conclusions from a small number of guest comments.

## Risk and Automation Philosophy

Automation levels and testing depth in this library are intentionally proportionate to risk, not applied uniformly. P04 and P06 (both rated Overall Risk: HIGH) received the most extensive testing - including adversarial (prompt injection) and legal-signal test cases - and are the only two prompts developed to v1.2. Lower-risk prompts (P01, P03, P09) required only one round of revision once grounding and format constraints were added.

No prompt in this library is treated as a complete organisational control. Safety- and complaint-related prompts (P04, P06) explicitly require full human review before every send; none of the automation levels assigned imply autonomous action on compensation, legal, or safety matters. This precaution reflects a wider pattern identified by McKinsey: as generative AI adoption accelerates, most organisations still lack basic governance structures for managing AI risk, such as a body with authority over responsible AI decisions (McKinsey & Company, 2024).

## Iteration Evidence

Full version history, test cases, and observed outputs for each prompt are documented within each prompt file (see `/01-pre-arrival-booking`, `/02-in-stay-guest-service`, `/03-post-stay-reporting`). Commit history for this repository provides an additional chronological record of development.

## References

- Anthropic. (n.d.). *Reduce hallucinations*. Claude Platform Docs. https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/reduce-hallucinations
- Deloitte. (2025a). *The 2025 European hotel industry and investment survey*. Deloitte UK. https://www.deloitte.com/uk/en/Industries/consumer/research/european-hotel-industry-and-investment-survey.html
- Deloitte. (2025b). *Future of hospitality: AI-driven industry trends*. Deloitte US. https://www.deloitte.com/us/en/Industries/consumer/articles/future-of-hospitality-ai-innovation.html
- McKinsey & Company. (2024). *The state of AI in early 2024: Gen AI adoption spikes and starts to generate value*. https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai-2024
- Shiji Group. (2025, October 16). *Shiji releases Q3 2025 Guest Experience Benchmark: Global satisfaction climbs, but 3-star hotels lead the charge* [Press release]. https://www.shijigroup.com/press-news/shiji-releases-q3-2025-guest-experience-benchmark-global-satisfaction-climbs-but-3-star-hotels-lead-the-charge

## Repository Structure

```
hotel-prompt-library/
├── 01-pre-arrival-booking/       (P01, P02, P03)
├── 02-in-stay-guest-service/     (P04, P05, P06, P07)
├── 03-post-stay-reporting/       (P08, P09, P10)
└── README.md                     (this file)
```
