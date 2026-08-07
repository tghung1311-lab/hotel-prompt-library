# P08 - Review Response Draft

**Section:** 03 - Post-stay & Reporting
**Workflow step:** Step 1 of 3
**Current version:** v1.1
**Status:** Tested
**Last updated:** 6 August 2026

---

## Prompt Text (v1.1 - current)

```
You are a Guest Relations coordinator at Lantern Bay Hotel, an 82-room boutique hotel in St Kilda, Melbourne.

Using ONLY the review text provided below, draft a public response. Do not promise specific operational changes, improvements, or timelines - acknowledge feedback without committing to future action. Do not offer compensation or a discount.

Review text:
[REVIEW_TEXT]
Rating: [RATING]

Required output:
- Maximum 100 words
- Thank the guest for their feedback
- Acknowledge both positive and negative points mentioned, without over-promising fixes
- Warm, professional tone suitable for a public review platform
- Invite the guest to contact Guest Relations directly for further discussion
- Sign off as "Lantern Bay Hotel Guest Relations Team" (no individual name)
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|---|---|---|
| [REVIEW_TEXT] | Review platform (Google, TripAdvisor, etc.), verbatim | 3-night stay review text |
| [RATING] | Review platform star rating | 3/5 stars |

---

## Intended Workflow or Task

- **Trigger:** New review posted on a review platform
- **Actor:** Marketing/Guest Relations coordinator reviews and posts
- **Timing:** Within 24-48 hours of review being posted
- **Next step:** Response posted publicly on the review platform; recurring themes fed into P10 (feedback theme summary)

```
Review posted -> [P08 runs] -> Coordinator reviews -> Response posted publicly
                                                      -> Theme noted for P10
```

---

## Problem Being Solved

Review responses are currently drafted inconsistently, with response time varying depending on staff availability. Some past responses have made specific improvement commitments (e.g. changes to breakfast or noise management) without confirming these with the relevant department first, risking public commitments the hotel cannot guarantee.

**Pain points addressed:**
- Inconsistent response time to guest reviews
- Risk of publicly promising operational changes not yet approved
- Variable tone and structure across different responses

---

## Automation Potential

**Level: High**

| Dimension | Assessment |
|---|---|
| Repetitiveness | High - responses required for most reviews, especially critical ones |
| Data availability | Review text is available directly from the platform |
| Human judgment needed | Low-Medium - mainly reviewing tone and confirming no promises were introduced |
| Integration possibility | Could integrate with review-platform management tools |
| Estimated time saving | Estimated moderate saving in drafting time; exact figures require measurement |

**Human-in-the-loop role:** Marketing/Guest Relations coordinator reviews each draft before posting publicly, particularly checking that no operational commitments have been implied.

---

## Risks and Limitations

| Risk | Level | Mitigation |
|---|---|---|
| Model promises specific operational changes (confirmed in v1.0 test) | High | Explicit prohibition on promising changes/timelines; resolved in v1.1 testing |
| Response appears generic or insincere for detailed/emotional reviews | Medium | Human review before posting; escalate highly negative or detailed reviews for a manually drafted response instead |
| Public response conflicts with a private resolution already offered to the guest | Low-Medium | Coordinator checks guest correspondence history before posting |
| Response could be seen as dismissive if not proportionate to review severity | Low | Human review step retained for tone-checking before every post |

**Overall risk rating: MEDIUM** - suitable for high automation with human review retained, given responses are public and permanent once posted.

---

## Evaluation Criteria

- No specific operational commitments or timelines promised
- Both positive and negative points acknowledged
- Correct sign-off format (team name, not individual)
- Word limit compliance
- Tone appropriate for public platform

---

## Test Cases

| Case | Input summary | Expected behaviour | Result |
|---|---|---|---|
| 1. Normal (mixed review) | 3/5 stars - clean room and good staff praised; pool noise and limited breakfast criticised | Acknowledges both positive and negative points, no promised fixes, correct sign-off | Pass |

---

## Version History

### v1.0 - Initial draft
**Prompt:** `Write a response to this hotel review.`
**Output:** Well-structured response, but committed to specific unconfirmed operational changes - "we'll look into ways to better manage this... whether through timing adjustments or clearer communication about nearby events."
**Observed effect:** Not usable as-is - promising specific operational fixes without management approval creates a public, written commitment the hotel may not be able to deliver on.
**Lesson learned:** Similar to the complaint-response prompt (P04), the model tends to offer unauthorised commitments when responding to negative feedback. Needed an explicit constraint against promising specific changes or timelines, and a word limit suited to a public review platform.

### v1.1 - Added role, no-promises constraint, and public-platform format - Current
**Change:** Added role, explicit prohibition on promising operational changes or timelines, no-compensation constraint, 100-word limit, and required team-only sign-off.
**Test input:** Same 3/5-star mixed review used in v1.0 test, for direct comparison.
**Output:** Acknowledged both positive and negative points without promising any specific fix, correctly signed off as the team rather than an individual, within word limit.
**Observed effect:** Ready to post with brief review - resolved the unauthorised-commitment risk identified in v1.0 while retaining a warm, appropriate tone.
**Lesson learned:** As with P04, an explicit prohibition on promising future action (not just a general tone instruction) is necessary to prevent the model from over-committing in response to negative feedback - this appears to be a recurring pattern across guest-facing response prompts.

---

## Related Prompts

- **Previous section:** P07 - Housekeeping shift handover (Section 2)
- **Next in chain:** P09 - Weekly occupancy briefing
- **Parent section:** 03-post-stay-reporting/README.md
