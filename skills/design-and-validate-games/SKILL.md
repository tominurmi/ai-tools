---
name: design-and-validate-games
description: Design and review games across genres using reusable principles and patterns, validate mechanics and game logic, and plan or analyze player testing. Use for game concepts, core loops, rules, economies, progression, balance, exploits, state transitions, playtest plans, onboarding, accessibility, and evidence-based game reviews in English or Norwegian. Do not use for unrelated software testing or playing a game.
metadata:
  author: Tomi Nurmi
  web: https://tominurmi.net
---

# Design and Validate Games

Route work into three complementary workflows. Respond in the user's language and preserve the game's audience, genre, priorities, and documented exceptions.

## Select references

| Task | Read | Deliver |
| --- | --- | --- |
| Design a concept, core loop, or system; choose patterns | [Principles and patterns](references/game-design-principles.md) | Project brief or design decision with tradeoffs and testable assumptions |
| Validate rules, formulas, state, economy, or implementation | [Mechanics and logic](references/game-mechanics-validation.md) | Specification questions, validation cases, available executed results, and risks |
| Plan playtests or analyze player evidence | [User testing](references/game-user-testing.md) | Neutral test plan or evidence-based findings with retest actions |
| Review an entire game or release readiness | All three references | Separate design, mechanics, and player-evidence assessments |

Read only needed references. For validation and testing, also read the principles reference when the experience promise or relevant principle IDs are not established. Combine workflows for mixed requests without conflating their evidence.

## Establish context

1. Read the provided brief, rules, artifacts, build, and existing evidence.
2. Identify audience, platform, player role, experience promise, core activity, development stage, and constraints.
3. Ask only for missing information that materially affects the task; otherwise state assumptions and proceed.
4. Select relevant principles P01–P14. Explain not-applicable items and deliberate tradeoffs rather than requiring particular mechanics.
5. Identify the decision to inform and the largest uncertainty.

## Design workflow

1. Complete or refine the project brief from the principles reference.
2. Connect the core loop, systems, and incentives to the experience promise.
3. Choose patterns for specific problems; compare alternatives and common failure modes.
4. Record decisions, tradeoffs, assumptions, and the smallest useful prototype or experiment.
5. Route correctness questions to mechanics validation and player-experience questions to user testing.

Treat design rationale as a hypothesis until appropriate evidence exists. Do not infer enjoyable play from a polished concept.

## Mechanics workflow

1. Specify inputs, preconditions, transitions, costs, rewards, timing, randomness, invalid actions, and invariants.
2. Separate contradictory specifications from implementation defects and balance hypotheses.
3. Derive expected outcomes independently of the implementation.
4. Select meaningful checks for critical paths, boundaries, interactions, exploits, persistence, and multiplayer where applicable.
5. Execute available, authorized checks when a working artifact exists. Record build, state, inputs, seed or trace, expected versus actual results, and evidence.
6. Mark unavailable checks untested or blocked. Provide concrete cases instead of claiming success.
7. Assess impact and specify fixes, regression coverage, and retest criteria.

Use simulations to investigate specified strategies and distributions; do not treat them as real-player evidence.

## User-testing workflow

1. Define a research question and the decision it informs.
2. Choose audience, method, neutral scenario, observable criteria, measures, and intervention rules.
3. Plan consent and appropriate handling of recordings and participant data.
4. Produce a plan when no player evidence exists. Do not pretend to conduct human playtests.
5. Analyze actual evidence by separating observations, player statements, and interpretations. Record denominators, assistance, contradictions, and limitations.
6. Prioritize findings by impact and recommend changes or focused follow-up tests.
7. Use fresh participants for redesigned first-time experiences and returning participants for retention or mastery questions where appropriate.

Prepare plans within the requested scope. Do not contact, recruit, or record people without explicit authorization.

## Report and preserve evidence

Use the templates in the relevant references. Scale detail to the task. For combined reviews, report context and assumptions, design decisions, mechanics results, player findings, evidence limits, prioritized actions, and retest triggers separately.

Use mechanics statuses: untested / pass / fail / blocked / not applicable. Use player-evidence statuses: untested / supported / concern / fails criterion / not applicable. Document intentional exceptions with rationale, risk, and review trigger; never convert contrary evidence into success.

Keep severity separate from status. Never invent tests, participants, quotes, or observations. Do not average statuses into a universal quality score or infer whole-game correctness, universal accessibility, enjoyment, or commercial success from limited evidence.

Keep project-specific records in the game's documentation and honor established locations such as `docs/`. Follow the environment's artifact-saving rules for requested standalone deliverables. Do not change bundled references during ordinary game work; update this framework only when the user requests a skill update.
