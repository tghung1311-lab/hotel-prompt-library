# Section 2: In-stay Guest Service

Four prompts supporting guest service during a stay, covering complaints, service requests, safety incidents, and internal shift handovers. This section contains the two highest-risk prompts in the library.

## Prompts in this section

| ID | Prompt | Automation | Risk |
|---|---|---|---|
| P04 | Guest complaint response | Medium | High |
| P05 | Service request triage | Very High | Medium |
| P06 | Safety-incident follow-up | Low-Medium | High |
| P07 | Housekeeping shift handover | High | Low-Medium |

## Chain

```
Guest raises an issue -> P04 (complaint response) -> if physical safety incident: P06
Service request received -> P05 (triage) -> routed to department
Shift ends -> P07 (handover checklist)
```

## Section-level risk note

P04 and P06 are the only prompts in the library developed to v1.2, following testing that revealed fault-admitting language and missing escalation handling for legally sensitive cases. Both prompts require mandatory human review before every send and do not make autonomous compensation or escalation decisions - the model flags risk signals for human attention only.
