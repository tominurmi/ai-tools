# Game User Testing

Version: 1.0  
Created: 2026-10-03  
Scope: Evidence about player comprehension, usability, accessibility, and experience for any game.

## Contents

- [Purpose and boundaries](#purpose-and-boundaries)
- [1. Define the question before recruiting](#1-define-the-question-before-recruiting)
- [2. Recruit relevant players](#2-recruit-relevant-players)
- [3. Select a suitable method](#3-select-a-suitable-method)
- [4. Run the session neutrally](#4-run-the-session-neutrally)
- [5. Observe the intended experience](#5-observe-the-intended-experience)
- [6. Ask useful follow-up questions](#6-ask-useful-follow-up-questions)
- [7. Analyze evidence and choose actions](#7-analyze-evidence-and-choose-actions)
- [8. Retest and review milestones](#8-retest-and-review-milestones)
- [Reporting checklist](#reporting-checklist)
- [Instructions for collaborators and AI assistants](#instructions-for-collaborators-and-ai-assistants)

## Purpose and boundaries

Use this guide to discover how intended players experience a working game and whether it delivers its experience promise. Observe behavior and gather player explanations; developer intuition and automated checks are insufficient for these claims.

Use [principles and patterns](game-design-principles.md) to define intent and [mechanics and logic validation](game-mechanics-validation.md) to investigate rule and implementation defects. Passing logic checks does not prove enjoyment; a positive playtest does not prove rule correctness.

Keep project-specific plans, anonymized findings, and decisions in each game's documentation. Apply only relevant methods and record limitations.

## 1. Define the question before recruiting

Choose a focused uncertainty, such as whether first-time players understand an action's consequences or whether a full session has the intended rhythm.

```markdown
### Test plan: [ID and title]
- Game / build / date / owner:
- Experience promise and relevant principle IDs:
- Research question and hypothesis:
- What decision the result will inform:
- Intended audience and recruitment criteria:
- Participants and rationale for sample size:
- Method, session length, platform, and input device:
- Starting state, scenario, and neutral tasks:
- Observable criteria defined before the test:
- Measures and operational definitions:
- Moderator script and intervention rules:
- Consent, recording, and data handling:
- Known build defects and study limitations:
```

Choose thresholds for the project before testing. Define measures precisely: for example, when time to first meaningful action starts and ends, or what counts as independent task completion. No universal pass percentage or participant count applies to every game.

## 2. Recruit relevant players

- [ ] Include players representative of the target audience and play context.
- [ ] Distinguish first-time, returning, novice, and experienced participants where relevant.
- [ ] Include relevant accessibility needs, devices, and input methods.
- [ ] Record previous exposure to the build, genre, or developer.
- [ ] Use real groups for social or cooperative experiences where feasible.
- [ ] State recruitment gaps and avoid treating friends or team members as representative by default.

Small qualitative studies can reveal problems and generate hypotheses. Claims about prevalence or population differences require a suitable study design and sample. Recruit additional fresh participants when evaluating a redesigned first-time experience; previous exposure changes the task.

## 3. Select a suitable method

| Method | Good for | Limitation |
| --- | --- | --- |
| First-time moderated play | Discoverability, learning, confusion | Moderator presence can affect behavior |
| Unmoderated natural play | Independent use and session flow | Less context for interpreting behavior |
| Focused task session | A control, feature, or recovery flow | Task wording may reveal too much |
| Full-session play | Pacing, fatigue, motivation, stopping points | One session may miss long-term effects |
| Repeat-session study | Progression, return motivation, knowledge retention | Attrition and prior exposure affect interpretation |
| Group playtest | Cooperation, conflict, contribution | Group composition matters |
| Comparison study | Compare specific alternatives | Order, novelty, and participant differences can confound results |
| Interview or survey after play | Player interpretation and preferences | Self-report alone does not explain actual behavior |

Think-aloud can expose reasoning but also change timing, concentration, and immersion. Use quiet observation or retrospective questions when those effects matter. Counterbalance comparison order where appropriate and keep conditions comparable.

## 4. Run the session neutrally

1. Explain the session, obtain consent for participation and any recording, and allow the participant to stop.
2. State that the game is being evaluated and that honest responses are useful.
3. Establish the intended starting state and give only the instructions planned for this test.
4. Observe without teaching the solution. Use neutral prompts such as “What are you trying to do?”
5. Record timestamps, actions, errors, hesitation, workarounds, and requests for help.
6. Intervene according to the plan, including when the participant wants to stop; record every intervention.
7. Ask follow-up questions after relevant moments or after the session without suggesting the desired answer.

Separate assisted completion from independent completion. Do not intentionally expose participants to unnecessary discomfort to finish a task. Gather only needed personal data, use participant IDs in reports, and set a retention and access plan for recordings.

## 5. Observe the intended experience

| Principle | Evidence to seek |
| --- | --- |
| P01 — Coherence | What players do and how they describe the experience relative to the promise |
| P02 — Core activity | Voluntary repetition, engagement, disengagement, and reasons for continuing |
| P03 — Agency | Player goals, different approaches, and perceived influence on outcomes |
| P04 — Feedback | Whether players explain actions, state changes, and consequences accurately |
| P05 — Learning | Time to meaningful action, repeated errors, help needed, and later retention |
| P06 — Challenge | Sources of difficulty, novice versus expert experience, and responses to uncertainty |
| P07 — Consequences | Understanding of setbacks, recovery behavior, and willingness to continue |
| P08 — Pacing | Session rhythm, fatigue, downtime, direction, and sensible stopping points |
| P09 — Incentives | Actual reward-seeking behavior, repetition, avoidance, and optimized strategies |
| P10 — Depth | Predictions, discoveries, transferable knowledge, and confusion between interacting rules |
| P11 — Participation | Control use, readability, accessibility settings, devices, and interruption handling |
| P12 — Trust | Understanding of commitments and costs, perceived pressure, and friction workarounds |
| P13 — Shared play | Contribution, communication, conflict, exclusion, and disrupted-session recovery |
| P14 — Feasibility | Experienced performance problems; production feasibility also requires team evidence |

Use the rows relevant to the test question rather than attempting to measure everything at once. Enjoyment, retention, and long sessions are different signals; none alone proves the intended experience.

## 6. Ask useful follow-up questions

- What were you trying to achieve at that moment?
- What did you expect would happen? What actually happened?
- How did you decide what to do next?
- Which parts felt satisfying, confusing, tiring, or frustrating, and why?
- Was there anything you wanted to do but could not?
- What would make you want to continue or stop?

Ask open questions before offering specific possibilities. Avoid questions such as “Did you enjoy our exciting event system?” Treat feature requests as clues to underlying needs, then investigate those needs.

## 7. Analyze evidence and choose actions

Separate direct observations, player statements, and interpretations. Use counts with denominators where useful, such as “3 of 5 participants requested help”; do not generalize that fraction to the whole audience. Record contradictory evidence and alternative explanations, including known bugs, task wording, and moderator help.

```markdown
### Finding: [ID and title]
- Test / game / build / date:
- Relevant principle IDs:
- Observation and evidence reference:
- Participant statement, if useful:
- Affected participants / denominator / contexts:
- Interpretation and alternative explanations:
- Criterion status: untested / supported / concern / fails criterion / not applicable
- Impact and severity:
- Confidence and evidence limitations:
- Decision: keep / change / remove / investigate
- Proposed change or next experiment / owner:
- Related mechanics defect or validation case:
- Retest plan and result:
```

Severity is the impact of a problem, not how many participants mentioned it. A single observed progression blocker may deserve urgent attention. Record intentional exceptions with rationale, risk, and review trigger; they do not convert contrary evidence into success.

## 8. Retest and review milestones

- **Concept:** Identify player assumptions and questions. Concept interviews can inform direction but cannot validate an unplayed core loop.
- **Prototype:** Test first-time comprehension, core activity, agency, and immediate feedback.
- **Production:** Test complete sessions, interactions, incentives, accessibility, and repeat play where relevant.
- **Release readiness:** Test representative players on supported configurations, revisit serious concerns, and assign owners to accepted risks.

After changes, retest the affected question and relevant neighboring behaviors. Use fresh participants for discoverability and first-time learning; use returning participants for retention and evolving mastery. Preserve earlier findings with their build context rather than overwriting history.

## Reporting checklist

- [ ] Identify build, audience, methods, tasks, participant count, and test conditions.
- [ ] Report what was observed, what was inferred, and what remains untested.
- [ ] Include assistance, known defects, contradictory findings, and recruitment limits.
- [ ] Prioritize actions by impact and evidence; avoid a universal quality score.
- [ ] Link decisions to principles and route implementation defects to mechanics validation.
- [ ] Define owners and retest triggers for important unresolved questions.

## Instructions for collaborators and AI assistants

Prepare plans, neutral tasks, and analysis structures when requested. Never invent participants, quotes, observations, or completed tests. Use actual evidence to assess the experience promise. Preserve uncertainty and minority findings, distinguish player preferences from observed usability problems, and recommend actionable changes or focused follow-up studies. Do not claim that one playtest proves enjoyment, universal accessibility, or commercial success.
