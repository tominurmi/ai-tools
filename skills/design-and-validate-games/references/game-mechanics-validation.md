# Game Mechanics and Logic Validation

Version: 1.0  
Created: 2026-10-03  
Scope: Rules, state, system interactions, and implementation correctness for any game.

## Contents

- [Purpose and boundaries](#purpose-and-boundaries)
- [1. Specify the mechanic before validating it](#1-specify-the-mechanic-before-validating-it)
- [2. Review the rules](#2-review-the-rules)
- [3. Validate state and transitions](#3-validate-state-and-transitions)
- [4. Validate resources, formulas, and incentives](#4-validate-resources-formulas-and-incentives)
- [5. Validate randomness and simulations](#5-validate-randomness-and-simulations)
- [6. Validate interactions and edge cases](#6-validate-interactions-and-edge-cases)
- [7. Choose validation methods](#7-choose-validation-methods)
- [Validation case template](#validation-case-template)
- [Milestones and decisions](#milestones-and-decisions)
- [Instructions for collaborators and AI assistants](#instructions-for-collaborators-and-ai-assistants)

## Purpose and boundaries

Use this guide to check whether a game's rules are complete, consistent, and implemented correctly. Validate the design specification and the working implementation separately: a correct implementation can still faithfully reproduce a flawed rule.

Use [principles and patterns](game-design-principles.md) for design intent and [user testing](game-user-testing.md) for player comprehension, usability, and experience. Logic checks and simulations can expose balance risks; they cannot establish that a game feels fair or enjoyable.

Apply only relevant checks. Explain not-applicable items and intentional exceptions. Keep specifications, test cases, and results in the individual game's documentation.

## 1. Specify the mechanic before validating it

```markdown
### Mechanic: [name / ID]
- Game / specification revision / build:
- Owner:
- Purpose and relevant principle IDs:
- Inputs and player actions:
- State read and state changed:
- Preconditions and legal actions:
- Costs, rewards, caps, and units:
- Timing, action order, and conflict priority:
- Randomness and probability rules, if any:
- Expected transition and visible feedback:
- Invalid-action behavior:
- Completion, failure, cancellation, and recovery:
- Dependencies and interacting systems:
- Invariants: conditions that must always hold:
- Intentional exceptions and open questions:
```

An invariant is a precise constraint, such as “an item cannot occupy two inventory slots simultaneously.” Do not assume resource conservation, positive balances, reversibility, or deterministic outcomes unless the design requires them.

## 2. Review the rules

- [ ] Every legal action has defined preconditions and outcomes.
- [ ] Invalid actions have defined behavior and do not partially apply costs or rewards unintentionally.
- [ ] States, transitions, timing, and simultaneous-action priority are unambiguous.
- [ ] Goals, completion, failure, cancellation, and recovery are defined where applicable.
- [ ] Rule dependencies do not create unintended circular prerequisites or unreachable content.
- [ ] Comparable situations follow consistent rules or documented exceptions.
- [ ] Feedback and displayed values represent the authoritative state accurately.
- [ ] Each major rule supports its intended design purpose.

## 3. Validate state and transitions

Enumerate important states and permitted transitions. Test normal sequences and attempts to cross forbidden transitions.

- [ ] Actions enter and leave the expected states.
- [ ] Invariants hold before and after actions, cancellations, and failures.
- [ ] Repeated, rapid, delayed, or out-of-order inputs behave as specified.
- [ ] Interruptions cannot leave the game unintentionally stuck between states.
- [ ] Reset, retry, undo, and restart restore the correct state where supported.
- [ ] Victory, defeat, and other terminal states handle later actions correctly.
- [ ] Required goals remain reachable; unintended softlocks and deadlocks have been investigated.
- [ ] Event queues, timers, cooldowns, and simultaneous effects follow the specified ordering.

For open-ended games, define valid ongoing operation rather than inventing a mandatory victory condition. For intentionally unwinnable states, verify that their reachability and consequences are intended.

## 4. Validate resources, formulas, and incentives

- [ ] Units, signs, rounding, caps, and numerical boundaries are specified.
- [ ] Costs and rewards apply at the intended time and exactly as specified.
- [ ] Insufficient resources, zero values, maximum values, and empty collections are handled.
- [ ] Transfers do not unintentionally duplicate or destroy resources.
- [ ] Sources and sinks support the intended economy and progression.
- [ ] Repeated action loops cannot create unintended unlimited rewards or bypass costs.
- [ ] Progression prerequisites and unlocks behave correctly, including alternate routes.
- [ ] Compare typical strategies, extreme strategies, and optimized play for dominant options.

Balanced does not necessarily mean equal. Asymmetric roles and choices may be intentional. Identify assumptions and use player testing to evaluate their practical effect.

## 5. Validate randomness and simulations

- [ ] Probabilities, sampling method, and eligibility rules match the specification.
- [ ] Mutually exclusive, independent, and conditional outcomes are distinguished.
- [ ] Impossible outcomes remain impossible and eligible outcomes can occur.
- [ ] Record random seeds or event traces where supported for reproducibility.
- [ ] Inspect unfavorable streaks, rare outcomes, and recovery options.
- [ ] Compare simulated distributions with expected results using an appropriate method.

Use multiple seeds for random-system coverage; a fixed seed is useful for reproducing a case. Record sample size and uncertainty. Simulated agents represent specified behavior, not every real player's strategy. For replay determinism, record all relevant inputs, timing, configuration, and external state; a seed alone may be insufficient.

## 6. Validate interactions and edge cases

| Area | Example cases to consider |
| --- | --- |
| Action boundaries | Just below, at, and just above a threshold; exact expiry time |
| Input | Repeated clicks, held controls, conflicting commands, invalid targets |
| Rule combinations | Stacked effects, cancellation during resolution, chained triggers |
| World and content | Missing target, removed entity, inaccessible location, empty content pool |
| Persistence | Save/load during important states, retry after reload, incompatible saves |
| Multiplayer, if present | Disconnect, reconnect, simultaneous claims, duplicate messages, stale state |
| External services, if present | Timeout, failed request, retry, delayed response |
| Long sessions | Accumulation, overflow, memory growth, exhausted content |

Select cases by risk and relevance. For authoritative multiplayer systems, verify authority boundaries, synchronization, and handling of repeated requests. For external operations, prevent unintended duplicate effects on retries.

## 7. Choose validation methods

| Method | Use |
| --- | --- |
| Specification walkthrough | Identify ambiguity and contradictions before implementation |
| Worked examples | Independently calculate expected outcomes |
| Focused automated checks | Check important formulas and transitions against independent expectations |
| Integration checks | Verify actual interactions between systems |
| Property or invariant checks | Exercise many inputs while checking required constraints |
| Simulation or state exploration | Investigate economy, strategy, reachability, or random outcomes |
| Manual exploratory checks | Seek unexpected sequences and exploits |
| Regression checks | Prevent confirmed defects from returning |

Prioritize high-impact, complex, or frequently changed rules. Derive expected results from the specification or independent reasoning rather than copying implementation logic. Record actual coverage; never describe unexecuted checks as passed.

## Validation case template

```markdown
### Case: [ID and title]
- Mechanic / relevant principle IDs:
- Specification revision / build / environment:
- Method and evidence reference:
- Initial state and configuration:
- Inputs, steps, timing, and seed or trace if relevant:
- Expected result and invariant:
- Actual result:
- Status: untested / pass / fail / blocked / not applicable
- Reproduction details:
- Impact and severity:
- Fix or investigation / owner:
- Regression case and retest result:
- Coverage limits or accepted exception:
```

Example: If a purchase costs 3 units and the starting balance is 2, rejection should preserve the balance and inventory. At a balance of 3, success should produce the specified item and leave 0 units. Repeated input must follow the documented purchase rules.

## Milestones and decisions

- **Concept:** Specify core rules, invariants, and unresolved contradictions.
- **Prototype:** Validate the core loop, key transitions, and resource calculations.
- **Production:** Expand interaction, boundary, persistence, and regression coverage.
- **Release readiness:** Verify critical paths on supported configurations, assess unresolved defects, and assign owners to accepted risks.

A pass applies to the stated case and build. Untested and blocked are not passes. Prioritize severity separately from status; critical failures cannot be averaged away. Intentional exceptions require rationale and a review trigger. A mechanics review supports correctness claims only within its evidence and coverage.

## Instructions for collaborators and AI assistants

Read the specification and design priorities. Identify ambiguity before assuming a rule. Separate specification problems from implementation defects and balance hypotheses. Report expected versus actual behavior, reproducibility, severity, and coverage limits. Link player-experience uncertainties to the user-testing guide. Never invent test execution or certify an entire game from a few passing cases.
