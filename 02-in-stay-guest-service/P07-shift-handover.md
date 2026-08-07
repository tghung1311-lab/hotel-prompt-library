# P07 - Housekeeping Shift Handover

**Section:** 02 - In-stay Guest Service
**Workflow step:** Step 4 of 4
**Current version:** v1.1
**Status:** Tested
**Last updated:** 6 August 2026

---

## Prompt Text (v1.1 - current)

```
You are a Housekeeping shift supervisor at Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne.

Using ONLY the notes provided below, convert them into a shift handover checklist. Do not add any task, action, or detail not stated in the notes.

Shift handover notes:
[HANDOVER_NOTES]

Required output:
- Heading "HOUSEKEEPING HANDOVER"
- Group items into time-based sections in chronological order (e.g. "Before [time]", "At [time]")
- Each item as a checkbox with the relevant room number and exact task
- Preserve all stated times, room numbers, and special requirements exactly as written
- End with two sign-off lines: "Outgoing staff: ____" and "Incoming staff: ____"
Do not invent quantities, comparisons, replacement items, or steps not explicitly stated in the notes.
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|---|---|---|
| [HANDOVER_NOTES] | Outgoing shift supervisor's raw notes | Room arrivals, delivery times, VIP requirements, lost property |

---

## Intended Workflow or Task

- **Trigger:** End of a housekeeping shift
- **Actor:** Outgoing supervisor reviews and posts; incoming supervisor confirms receipt
- **Timing:** At shift changeover
- **Next step:** Incoming shift actions items in chronological order

```
Shift ends -> Supervisor compiles raw notes -> [P07 runs] -> Supervisor reviews -> Checklist posted
                                                                                  -> Incoming shift signs off and actions items
```

---

## Problem Being Solved

Handover notes are currently compiled manually into free-text messages or verbal handovers, which can omit details or fail to clearly flag time-sensitive tasks. Incomplete information (e.g. a missing room number) is sometimes carried forward without being flagged, risking a missed or misdirected task.

**Pain points addressed:**
- Inconsistent handover format between supervisors
- Time-sensitive tasks not clearly distinguished from routine ones
- Incomplete information not flagged for follow-up before the next shift acts on it

---

## Automation Potential

**Level: High**

| Dimension | Assessment |
|---|---|
| Repetitiveness | High - required at every shift change |
| Data availability | Raw notes are available from the outgoing supervisor |
| Human judgment needed | Low - mainly a review-before-post check |
| Integration possibility | Could integrate with a shift-log or task-management system |
| Estimated time saving | Estimated moderate saving in compiling and formatting time; exact figures require measurement |

**Human-in-the-loop role:** Outgoing supervisor reviews the checklist before posting; incoming supervisor confirms and resolves any flagged missing information (e.g. unrecorded room numbers) before actioning.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Model adds an unconfirmed task or action (confirmed in v1.0 test) | Medium | "Do not add any task... not stated" constraint; resolved in v1.1 testing |
| Missing information (e.g. room number) actioned incorrectly by next shift | Medium | v1.1 explicitly flags missing information rather than omitting or inventing it |
| Time-sensitive task misclassified as routine or vice versa | Low | Chronological grouping requirement; supervisor review before posting |
| Sign-off not actually completed by staff | Low | Sign-off lines included as a physical/procedural prompt; enforcement remains a staff process matter, not a prompt control |

**Overall risk rating: LOW-MEDIUM** - suitable for high automation with a lightweight supervisor review step retained.

---

## Evaluation Criteria

- No tasks or details added beyond the source notes
- Correct chronological grouping
- Missing information flagged, not invented or silently omitted
- Sign-off lines present
- Format and heading compliance

---

## Test Cases

| Case | Input summary | Expected behaviour | Result |
|---|---|---|---|
| 1. Normal | 5 mixed tasks: 2 timed arrivals, 1 timed delivery, 2 untimed (maintenance check, VIP requirements, lost property) | Correct chronological grouping, no invented tasks, sign-off included | Pass |
| 2. Missing data | VIP room requirements supplied but room number not recorded | Should flag missing room number, not invent one | Pass - flagged clearly with an explicit follow-up note |

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Turn these housekeeping notes into a handover checklist.`
**Output:** Well-organised checklist, but the model added actions not present in the source notes - "check quantity against order" for the linen delivery, and "replace with unscented alternatives" for the VIP room. No sign-off lines included.
**Observed effect:** Not fully usable - added tasks not confirmed by the source notes could lead staff to perform unnecessary or incorrect actions.
**Lesson learned:** Even a well-structured, readable output can still contain invented content. Needed an explicit "do not add tasks not stated" constraint, a defined chronological format, and sign-off lines.

### v1.1 - Added grounding constraint, chronological format, and sign-off lines - Current
**Change:** Added role, explicit "do not add tasks not stated" constraint, required chronological grouping format, and mandatory sign-off lines.
**Testing:** 2 test cases run - normal case with mixed timed/untimed tasks, and a missing-data case (VIP room number not recorded).
**Observed effect:** Normal case produced accurate, well-grouped output with no invented tasks. Missing-data case correctly flagged the unrecorded room number with an explicit note to confirm before actioning, rather than inventing or silently omitting it.
**Lesson learned:** The grounding constraint not only prevented invented tasks but also produced an unprompted, useful safety behaviour - explicitly flagging missing data for staff attention rather than silently dropping it.

---

## Related Prompts

- **Previous in chain:** P06 - Safety-incident follow-up
- **Parent section:** 02-in-stay-guest-service/README.md
- **Note:** This completes Section 2 (In-stay Guest Service). Section 3 (Post-stay & Reporting) begins with P08.
