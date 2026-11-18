# Game Design Principles and Patterns

Version: 2.0  
Updated: 2026-10-03  
Scope: Any game genre, platform, or audience.

## Contents

- [Purpose and companion documents](#purpose-and-companion-documents)
- [Project brief — complete for each game](#project-brief--complete-for-each-game)
- [Principles](#principles)
- [Pattern toolbox](#pattern-toolbox)
- [Design decision template](#design-decision-template)
- [Design milestone checklist](#design-milestone-checklist)
- [Instructions for collaborators and AI assistants](#instructions-for-collaborators-and-ai-assistants)

## Purpose and companion documents

Use this guide to decide what experience to create and which design choices support it. Principles are design considerations; patterns are optional tools. Neither guarantees an enjoyable game.

This is the design document in a three-document framework:

| Document | Main question |
| --- | --- |
| [Principles and patterns](game-design-principles.md) | What makes this design appropriate and coherent? |
| [Mechanics and logic validation](game-mechanics-validation.md) | Do the rules and systems behave as intended? |
| [User testing](game-user-testing.md) | Do players understand and experience what we intend? |

Define the project brief, choose priorities, review proposed mechanics, and then use both companion documents for evidence. Keep project-specific decisions and results in each game's own documentation.

Do not require every game to include competition, combat, progression, failure, randomness, or difficult choices. Record why a principle is not applicable or deliberately traded off. Preserve principle IDs P01–P14 when connecting decisions to validation and testing.

## Project brief — complete for each game

- **Game and build:**
- **Target players and their needs:**
- **Platform, controls, and play context:**
- **Expected session length:**
- **Player role:** Who is the player within the experience?
- **Experience promise:** What should the player feel, do, or discover?
- **Core activity:** What will the player do most often?
- **Core loop:** Action → response → new situation or motivation → next action.
- **Goals or sources of direction:** Include player-created goals where appropriate.
- **Three design priorities:**
- **Explicit exclusions:** What is outside the intended experience?
- **Main design uncertainty:**
- **Constraints:** Team, time, technology, budget, and content capacity.
- **Success evidence:** Observable behavior that would support the experience promise.

## Principles

### P01 — Deliver a coherent experience

Mechanics, presentation, narrative, and interface should support the experience promise. Intentional shifts in tone should have a clear purpose.

**Review:** Can we explain how each major system contributes to the desired experience? Are there systems pulling the player toward conflicting behaviors?


### P02 — Make the core activity worth doing

The repeated activity should provide satisfaction, curiosity, expression, mastery, connection, or another intended value. Rewards should reinforce that value.

**Review:** Why would a player want to repeat the activity? Is repetition developing the experience or merely extending playtime?


### P03 — Give players meaningful agency

Players should have appropriate influence over actions, interpretation, goals, or outcomes. Agency may come from timing, movement, creativity, exploration, social interaction, or strategic decisions.

**Review:** What can the player influence? Where choices are important, are alternatives useful under different circumstances? Are apparent choices misleading?


### P04 — Communicate actions and consequences

Players need enough feedback to understand inputs, important state changes, and relevant consequences. Mystery can conceal information intentionally while keeping interaction understandable.

**Review:** Can players distinguish success, failure, pending actions, and unavailable actions? Can they connect a result to its cause? Is delayed feedback traceable?


### P05 — Introduce complexity at a usable pace

Teach what players need when they need it. Build on learned concepts, support experimentation, and make help available when appropriate.

**Review:** What must a new player understand first? Can they start meaningful play before mastering every system? Are advanced interactions discoverable?


### P06 — Match challenge and uncertainty to the promise

Difficulty, ambiguity, and risk should create the intended tension. Random outcomes should support the experience and offer suitable ways to anticipate, respond, or recover where agency matters.

**Review:** What makes an obstacle difficult? Is frustration caused by the intended challenge or by unclear rules, controls, or feedback? What role should luck play?


### P07 — Make consequences proportionate and understandable

Successes and setbacks should fit the stakes of the experience. Recovery, retrying, persistence, and irreversible outcomes should be deliberate design choices.

**Review:** What does a setback cost in time and progress? Does it create learning or an interesting new situation? Are major irreversible actions communicated appropriately?


### P08 — Shape pacing and player direction

Arrange intensity, discovery, repetition, and rest to support the intended rhythm. Players should have suitable direction, whether authored or self-created.

**Review:** Where do players feel urgency, relief, anticipation, or completion? Can they identify something worthwhile to do next? Can a session end at a sensible point?


### P09 — Reward the behavior the game values

Rewards, progression, and resource systems should encourage the intended activities. Meaningful development can involve knowledge, relationships, expression, or mastery as well as numerical growth.

**Review:** What behavior is most profitable or efficient? Does that behavior match the experience promise? Do unlocks create useful possibilities or only inflate numbers?


### P10 — Prefer useful depth and coherent rules

Each rule should justify its learning, implementation, and maintenance cost. Interacting rules can create depth, but complexity is not automatically valuable.

**Review:** Can players transfer knowledge between similar situations? Does a new system enable worthwhile behavior? Could a simpler rule achieve the same purpose?


### P11 — Support the intended players and play context

Controls, readability, accessibility, session structure, and performance should let the target audience participate in the intended experience.

**Review:** What capabilities does the game assume? Consider text size, contrast, color-independent cues, audio alternatives, motion, control remapping, timing demands, language, and interruptions where relevant.


### P12 — Respect player time and trust

Make important commitments and transactions understandable. Avoid unnecessary friction and incentives that undermine the experience or pressure players into unwanted participation.

**Review:** Are waiting, repetition, purchases, and time limits serving a clear purpose? Are costs and rewards clear? If monetized, how do payments affect fairness and progression?


### P13 — Make shared play sustainable when applicable

Multiplayer systems should support the intended cooperation, competition, and social norms. Rules, matchmaking, communication, and handling of disruption should reinforce that experience.

**Review:** What happens with unequal skill, disconnections, inactivity, griefing, or conflicting goals? Can players communicate and participate at the intended level?


### P14 — Keep the design buildable and maintainable

Scope should fit the resources available. Technical reliability and content production are part of delivering the experience.

**Review:** Which features are essential to the promise? What are the largest technical and content risks? Can the team produce enough variety without unsustainable effort?


## Pattern toolbox

Choose patterns because they solve a specific design problem. No pattern is required merely because it is common.

| Pattern | Useful for | Common failure to check |
| --- | --- | --- |
| Limited resources | Priorities and tradeoffs | Scarcity produces chores or stalls |
| Risk versus reward | Tension and decision-making | One option dominates or risk is unreadable |
| Gradual information reveal | Curiosity and discovery | Players cannot make informed actions |
| Multiple solutions | Expression and experimentation | Alternatives exist but are not viable |
| Interacting simple rules | Emergence and mastery | Combinations become opaque or exploitable |
| Escalating pressure | Adaptation and urgency | Escalation outpaces learning or permits no recovery |
| Safe practice spaces | Learning and confidence | Practice does not transfer to actual play |
| Checkpoints and retries | Experimentation and recovery | Repetition adds unnecessary downtime |
| Persistent consequences | Ownership and meaningful history | Unclear outcomes punish uninformed actions |
| Unlocks and progression | Direction and growing possibilities | Interesting play is delayed behind repetition |
| Player-created goals | Creativity and autonomy | Players lack tools or inspiration to begin |
| Alternating intensity and rest | Pacing and anticipation | Rest becomes boredom or pressure becomes exhausting |
| Asymmetric roles | Identity and cooperation | Some roles have little agency or contribution |
| Event-driven world changes | Responsiveness and new situations | Events feel arbitrary, repetitive, or impossible to respond to |

## Design decision template

```markdown
### Decision: [mechanic or design choice]
- Game / date / owner:
- Experience promise:
- Relevant principle IDs:
- Problem to solve:
- Proposed rule or pattern:
- Alternatives considered:
- Why this choice supports the promise:
- Tradeoffs and possible failure modes:
- Not-applicable principles or intentional exceptions, with rationale:
- Assumptions requiring evidence:
- Mechanics validation required:
- User testing required:
- Decision and review trigger:
```

## Design milestone checklist

- [ ] Define audience, player role, experience promise, core activity, and constraints.
- [ ] Explain the core loop and intended motivation to repeat it.
- [ ] Select three priorities and resolve conflicting incentives.
- [ ] Justify major systems and patterns in terms of the promise.
- [ ] Identify the biggest uncertainty and smallest useful prototype.
- [ ] Check scope against actual implementation and content capacity.
- [ ] Update the brief and decisions when the design changes.

Concept review establishes coherence. Working-system checks belong in mechanics validation; claims about comprehension, enjoyment, or player preference require user testing.

## Instructions for collaborators and AI assistants

Read the project brief before judging a design. Do not impose a genre or checklist of mandatory mechanics. Explain concerns through the experience promise and relevant principle IDs. Distinguish design rationale from tested evidence, preserve documented exceptions, and recommend the smallest useful change or experiment. Update this guide only for lessons that generalize across games.
