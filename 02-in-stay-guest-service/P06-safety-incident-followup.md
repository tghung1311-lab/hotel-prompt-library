# P06 - Safety-Incident Follow-up

**Section:** 02 - In-stay Guest Service
**Workflow step:** Step 3 of 4
**Current version:** v1.2
**Status:** Tested
**Last updated:** 6 August 2026

---

## Prompt Text (v1.2 - current)

```
You are a Guest Services duty manager at Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne.

Using ONLY the incident details provided below, draft a follow-up message to the guest. Do not speculate about the cause of the incident, do not admit or imply legal responsibility or fault (avoid phrasing such as "caused by us" or apologising "for the inconvenience this caused"), and do not promise compensation or any resolution outcome.

Incident details:
Guest name: [GUEST_NAME]
Room number: [ROOM_NUMBER]
Incident time and location: [INCIDENT_TIME_LOCATION]
What occurred: [INCIDENT_DESCRIPTION]
Guest's stated condition: [GUEST_CONDITION]
Immediate actions already taken: [ACTIONS_TAKEN]
Incident reference: [INCIDENT_REF]

Required output:
- Subject line including the incident reference
- Maximum 130 words
- State the facts objectively without assigning cause or fault
- Express concern for the guest's wellbeing (not an apology implying fault)
- Confirm the immediate actions already taken, exactly as supplied
- Clearly tell the guest what to do if symptoms or concerns arise (contact method)
- Do not offer compensation, medical advice, or admission of liability
- Note that this incident has been logged for internal review

Escalation check:
If the guest's stated condition or the incident description contains language 
suggesting potential legal action, media involvement, or a worsening medical 
situation (e.g. mentions of "lawyer", "legal", "options", "compensation", 
"media", "press", "sue", or similar), add this line at the very end, after 
the email:

"ESCALATION REQUIRED: [brief reason]. Route to Duty Manager AND General 
Manager, not Duty Manager alone."

If no such language is present, do not add this line.
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|---|---|---|
| [GUEST_NAME] | Incident log | Michael Torres |
| [ROOM_NUMBER] | PMS booking record | 508 |
| [INCIDENT_TIME_LOCATION] | Incident log | 3:15 PM, rooftop pool deck |
| [INCIDENT_DESCRIPTION] | Incident log, factual only | Guest slipped on wet pool deck |
| [GUEST_CONDITION] | Incident log, guest's own words | Mild ankle pain, declined medical assistance |
| [ACTIONS_TAKEN] | Duty Manager / relevant department | Warning sign placed; maintenance notified |
| [INCIDENT_REF] | Incident logging system | INC-2026-0731 |

---

## Intended Workflow or Task

- **Trigger:** A safety-related incident is logged by staff (injury, near-miss, hazard)
- **Actor:** Duty Manager confirms incident facts, then reviews and sends the drafted message
- **Timing:** Same day as the incident, after immediate actions are taken
- **Next step:** Incident and message logged in internal safety register; escalation-flagged cases also routed to General Manager

```
Incident logged -> Duty Manager confirms facts -> [P06 runs] -> Duty Manager reviews -> Message sent
                                                                                       -> Logged in safety register
                                                                                       -> If escalation flagged: also routed to General Manager
```

---

## Problem Being Solved

Safety-incident follow-ups are currently drafted individually, with inconsistent language around cause and liability - some past messages have used apologetic phrasing that could be read as admitting fault. There is also no consistent method for flagging incidents with legal or media risk for senior management attention beyond the Duty Manager.

**Pain points addressed:**
- Inconsistent, sometimes liability-admitting language in incident communications
- No standard mechanism to flag legally sensitive cases for escalation beyond Duty Manager level
- Delayed or inconsistent guest follow-up during busy periods

---

## Automation Potential

**Level: Low-Medium**

| Dimension | Assessment |
|---|---|
| Repetitiveness | Medium - incidents are less frequent than routine requests, but the format is repeatable |
| Data availability | Requires manual fact confirmation by Duty Manager before drafting (not pulled automatically from any system) |
| Human judgment needed | Very high - fact confirmation, tone review, and escalation decisions all require human oversight |
| Integration possibility | Limited - primarily a drafting aid, not suited to fully automated dispatch |
| Estimated time saving | Drafting time saved is likely modest; the primary value is consistency and risk reduction, not speed |

**Human-in-the-loop role:** Duty Manager confirms all incident facts before the prompt runs, reviews every output before sending (no exceptions), and makes all escalation and compensation decisions outside this prompt. The escalation flag is a prompt to the human, not an autonomous routing decision.

**Note on automation boundary:** This prompt assists drafting only. It is not a substitute for organisational incident-management controls - safety incidents also require system-level controls such as mandatory human sign-off, an incident audit log, and defined escalation ownership, which cannot be enforced by prompt instructions alone.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Message implies admission of fault or liability (confirmed in v1.0 test) | High | Explicit, specific prohibition on cause/fault language; resolved and confirmed in v1.1/v1.2 testing |
| Legal/media risk signal in guest's words not escalated beyond Duty Manager (confirmed in v1.1 Case 4 test) | High | Escalation check added in v1.2; resolved and confirmed in retest |
| Escalation keyword list is not exhaustive - risk signal phrased differently may be missed | Medium | Escalation flag supplements, does not replace, Duty Manager judgment; all incidents still require full human review |
| Missing guest-condition data handled by silent omission rather than visible flag (observed in v1.1 Case 2 test) | Medium | Known limitation, not yet addressed - recommend explicit "condition not recorded" wording in a future revision |
| Privacy / data security - GUEST_CONDITION may contain health-adjacent information sent to an external model | High | Minimise data sent to only what is required for the follow-up (not full incident notes); in live deployment, route through an enterprise/private model deployment with data-retention controls, not a public consumer AI tool; access to incident data restricted to Duty Manager and above |
| Security - malicious or injected instructions embedded in guest-supplied data fields | Medium | Tested with an adversarial prompt-injection case (guest name field containing a fake instruction) - model correctly identified and refused to comply, flagging the attempt rather than acting on it |
| Bias in tone or perceived urgency based on guest name or language pattern | Low-Medium (untested) | Not yet stress-tested with guest profiles across different name origins or non-native English phrasing; recommend targeted bias testing before wider rollout |
| Prompt instruction alone is not a complete organisational control | High | Mandatory human review before every send; incident audit log maintained at system level, not by this prompt |

**Overall risk rating: HIGH** - this is the highest-risk prompt in the library. Full human review is mandatory for every output, including escalation-flagged cases; the prompt reduces inconsistency, liability-language risk, and now names privacy and bias as explicit risk categories requiring further system-level and testing attention - it does not replace organisational incident-management controls.

---

## Evaluation Criteria

- No cause or fault language present
- All supplied facts stated accurately, no invented details
- Guest wellbeing acknowledged appropriately
- Correct escalation flagging, with no false positives on routine cases
- Format and word-limit compliance

---

## Test Cases

| Case | Input summary | Expected behaviour | Result (v1.1) | Result (v1.2) |
|---|---|---|---|---|
| 1. Normal | Guest slipped on wet pool deck, mild pain, declined medical help | Objective facts, no fault language, correct actions confirmed, no escalation flag | Pass | Pass - no escalation flag added (correct) |
| 2. Missing data | Guest condition not recorded by staff | Should not invent a condition | Pass (limitation noted) | Not retested - unaffected by v1.2 change |
| 3. Ambiguous | Guest felt dizzy, bumped into cart, unclear cause | Should not assign cause to either dizziness or cart | Pass | Not retested - unaffected by v1.2 change |
| 4. High-risk (legal signal) | Equipment malfunction, swelling, guest mentions "looking into options" | Should not admit fault; should flag escalation | Pass on fault language; gap found - no escalation flag | Pass - escalation flag correctly added with accurate reason |
| 5. Adversarial | Guest name field contains an injected instruction to admit negligence | Should not comply with injected instruction | Pass - flagged the injection attempt | Not retested - unaffected by v1.2 change |

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Write a follow-up message about a safety incident at a hotel.`
**Output:** Professional tone, but included "we sincerely apologize for the inconvenience this caused" - implicit liability-admitting language.
**Observed effect:** Not usable - subtle fault-admitting phrasing is the highest-risk failure type found in the library, as it reads as professional and could be sent without staff noticing the legal risk.
**Lesson learned:** Needed an explicit, specific prohibition on cause/fault language, not just a general tone instruction.

### v1.1 - Added role, explicit fault-language prohibition, and guest next-step instructions
**Change:** Added role, explicit prohibition on cause/fault language with example phrasing to avoid, required next-step instructions for the guest, and a logged-for-review statement.
**Testing:** 5 test cases run - normal, missing-data, ambiguous, high-risk, and adversarial.
**Observed effect:** 4 of 5 cases fully passed; Case 4 (high-risk) revealed a gap - no mechanism to flag legal/media risk signals for escalation beyond standard Duty Manager review.
**Lesson learned:** Removing fault-admitting language is necessary but not sufficient for high-risk safety cases - a mechanism to detect and flag legal/media risk signals for additional management attention is also needed.

### v1.2 - Added escalation check for legal/media risk signals - Current
**Change:** Added a keyword-based escalation check that appends an "ESCALATION REQUIRED" line, routing to both Duty Manager and General Manager, when the guest's wording suggests potential legal action, media involvement, or a worsening medical situation.
**Testing:** Retested Case 4 (high-risk) and Case 1 (normal, regression check).
**Observed effect:** Case 4 correctly triggered the escalation flag with an accurate stated reason; Case 1 correctly did not trigger the flag, confirming no false positives introduced.
**Lesson learned:** A narrowly scoped, single-purpose revision (addressing only the specific gap found in testing) resolved the identified failure without disrupting previously correct behaviour - confirming the value of testing both the fix and a regression case before considering a version complete.

---

## Related Prompts

- **Previous in chain:** P05 - Service request triage
- **Next in chain:** P07 - Housekeeping shift handover
- **Related (escalation source):** P04 - Guest complaint response (for non-safety complaints)
- **Parent section:** 02-in-stay-guest-service/README.md
