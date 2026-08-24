# Hollow Crown — Game Design Document

**System:** Deployment Economy
**Document Status:** Living Document
**Version:** 1.0
**Scope:** Existing Hollow Crown combat system

---

## 1. Design Overview

### Objective

Hollow Crown is a tactical RPG where players build their battlefield roster under a limited deployment budget.

The deployment economy is designed to make **unit cost reflect battlefield value** while preserving meaningful differences between units.

The goal is not to make every unit equally powerful. Instead, each unit should present a meaningful trade-off between:

* Battlefield effectiveness
* Deployment cost
* Matchup strengths
* Matchup weaknesses
* Strategic role

The system should avoid two unhealthy roster states:

* **Auto-include:** a unit whose combination of power, cost, and practical battlefield value makes selecting it the rational choice in most situations.
* **Trap-pick:** a unit whose actual battlefield value does not reasonably justify its cost, role, or expected performance.

---

## 2. Player Experience Goal

The player should feel that every deployment decision involves an opportunity cost.

The intended decision is:

> **"What does this unit give me, what does it cost me, and what am I giving up by deploying it?"**

Players should not feel that there is one universally correct unit or that a particular unit is never worth deploying.

A healthy roster should instead encourage players to consider:

* The opponent
* Unit matchups
* Deployment budget
* Offensive and defensive strengths
* Specialized battlefield roles

The desired experience is **meaningful roster choice**, rather than optimization around a single dominant unit.

---

## 3. Core System Rules

### 3.1 Deployment Budget

Each unit has a deployment `cost`.

Players can only deploy units whose combined cost fits within the available deployment budget.

```text
Total Deployment Cost <= Deployment Budget
```

Cost therefore creates opportunity cost: selecting a high-value unit can limit which other units can be deployed alongside it.

The deployment budget itself is part of the existing Hollow Crown combat setup and is not changed by this balance pass.

---

### 3.2 Cost as Battlefield Value

Deployment cost should broadly correspond to expected battlefield value.

Cost is not intended to be a direct conversion of a single statistic such as ATK, DEF, or HP.

Balance decisions instead consider multiple sources of evidence:

* Overall combat performance
* Matchup performance
* Survivability
* Damage output
* Consistency
* Cost efficiency
* Practical battlefield role

A higher-performing unit can therefore remain stronger than another unit if its increased battlefield value is appropriately reflected by its cost.

---

### 3.3 Combat System Scope

Hollow Crown uses the existing combat rules and resolution implemented by the provided simulator.

This balance pass does **not** introduce new combat mechanics or modify the combat formula.

Changes are limited to:

* Deployment costs
* Targeted unit statistics when required to correct identified balance problems

The deployment economy therefore acts as a balancing layer on top of the existing combat system rather than as a new gameplay feature.

---

## 4. Roster Design Principles

### 4.1 Meaningful Differentiation

Units should remain mechanically and strategically distinct.

Balance changes should correct excessive or insufficient value without flattening the roster into statistically identical units.

Desired trade-offs include:

| Trade-off                                  | Design Intent               |
| ------------------------------------------ | --------------------------- |
| High DEF / lower offensive flexibility     | Durable frontline unit      |
| High offensive power / lower survivability | Burst-oriented unit         |
| High speed / moderate power                | Tempo advantage             |
| Low cost / lower general power             | Economical deployment       |
| Specialized matchup strength               | Situational strategic value |

### 4.2 Cost Before Stat Normalization

When a unit's gameplay identity is healthy but its efficiency is incorrect, deployment cost should be considered before changing its core statistics.

Stat changes should be used when the underlying combat interaction creates an actual gameplay problem that cost alone cannot reasonably solve.

This preserves unit identity while allowing the economy to compensate for differences in battlefield power.

### 4.3 Preserve Matchup Relationships

Balance changes should improve roster cohesion without eliminating meaningful counters.

A unit can be highly effective against certain opponents while remaining vulnerable to others.

The objective is therefore **not perfect matchup symmetry**, but a roster in which strengths and weaknesses create meaningful decisions.

---

## 5. Current Roster Roles

The roster provides different tactical profiles:

| Unit       | Class      | Design Role                   | Key Trade-off                                                            |
| ---------- | ---------- | ----------------------------- | ------------------------------------------------------------------------ |
| Ser Halden | Knight     | Defensive frontline           | High physical durability vs. vulnerability to magic                      |
| Rookwood   | Myrmidon   | Fast offensive fighter        | Strong tempo and offense vs. higher deployment cost                      |
| Wisp       | Cleric     | Support / magic-oriented unit | Strong situational value vs. limited representation in 1v1 testing       |
| Brennan    | Soldier    | General-purpose baseline      | Moderate performance without extreme specialization                      |
| Sable      | Archer     | Ranged specialist             | Strong against vulnerable targets vs. weaker against durable frontliners |
| Pyraxis    | Battlemage | High-magic offensive unit     | High magical damage vs. low speed and survivability                      |

These roles should remain recognizable after balance adjustments.

---

## 6. Balance Targets

The deployment economy should satisfy the following goals.

### 6.1 Avoid Auto-Includes

No unit should be so efficient and universally effective that selecting it becomes the obvious decision regardless of matchup.

A strong unit may still have superior performance, but its cost and weaknesses should create a meaningful opportunity cost.

### 6.2 Avoid Trap-Picks

No unit should require an excessive investment for a level of battlefield performance that consistently fails to justify its role.

A specialized unit can have below-average overall performance if its strengths provide meaningful strategic value.

### 6.3 Preserve Unit Identity

Balance should not remove the characteristics that make each unit strategically distinct.

Changes should prioritize the smallest intervention capable of correcting the identified imbalance.

---

## 7. Current Key Numbers

The following values represent the current balanced roster after two balance iterations.

| Unit       | Final Cost | Key Balance Intent                                                         |
| ---------- | ---------: | -------------------------------------------------------------------------- |
| Ser Halden |      **8** | Higher cost compensates for exceptional physical durability                |
| Rookwood   |      **7** | High offensive and tempo value                                             |
| Wisp       |      **4** | Low-cost support/magic specialist; requires further squad-level validation |
| Brennan    |      **5** | General-purpose baseline                                                   |
| Sable      |      **5** | Ranged specialist with matchup limitations                                 |
| Pyraxis    |      **7** | High magic damage compensated by lower speed and survivability             |

### Key Stat Adjustments

Only two units required direct stat changes during the balancing process:

| Unit       | Change     | Design Purpose                                                                      |
| ---------- | ---------- | ----------------------------------------------------------------------------------- |
| Ser Halden | Cost 6 → 8 | Preserve defensive identity while compensating for excessive battlefield efficiency |
| Pyraxis    | DEF 4 → 7  | Improve survivability so offensive power can convert into meaningful combat value   |
| Pyraxis    | HP 20 → 24 | Support the same survivability objective                                            |
| Pyraxis    | Cost 9 → 7 | Correct remaining cost inefficiency after the survivability adjustment              |

All other unit statistics remain unchanged.

> **Note:** These are current implementation values, not immutable design requirements. Future encounter-level testing may justify further adjustments.

---

## 8. Balance Philosophy

Balance changes should follow a targeted, evidence-based process:

```text
Identify outlier
      ↓
Diagnose mechanical cause
      ↓
Determine whether cost or stats are responsible
      ↓
Apply smallest targeted change
      ↓
Re-simulate
      ↓
Check efficiency + matchups
      ↓
Repeat if necessary
```

The preferred solution is the **smallest change that corrects the identified problem while preserving the unit's intended identity**.

---

## 9. Validation Framework

The deployment economy is evaluated using the existing combat simulator.

Primary indicators are:

* Overall Win%
* WIN% / Cost
* Pairwise matchup performance
* Matchup stability across simulation seeds
* Presence of extreme outliers

Two simulation seeds are used to check that observed results are not caused by random sampling noise.

Balance changes should be evaluated through repeated simulation rather than through a single result.

---

## 10. Current Balance State

The current roster represents the result of two targeted balance iterations.

The final design direction achieved:

* Reduced dominance from Ser Halden.
* Improved Pyraxis survivability and economic efficiency.
* Reduced the overall Win% spread.
* Reduced the WIN%/Cost spread.
* Preserved meaningful matchup relationships.
* Avoided introducing a new major outlier.

The final roster is therefore considered **more economically coherent while retaining differentiated unit identities** within the scope of the current simulator.

---

## 11. Known Limitations

The current simulator primarily models 1v1 combat.

It does not fully represent:

* Team composition
* Positioning
* Map geometry
* Support interactions
* Healing value in team combat
* Ranged positioning
* Objective control
* Multi-unit synergies

Because of this, Wisp's support value and Sable's ranged value cannot be fully evaluated through the current 1v1 model.

Their remaining differences are therefore treated as **investigation points rather than confirmed balance problems**.

Further squad- and encounter-level validation should be performed before making additional balance changes.

---

## 12. Success Criteria

The deployment economy is considered healthy when:

1. No unit is an obvious universal auto-include.
2. No unit is an economically unjustifiable trap-pick.
3. Deployment cost broadly reflects battlefield value.
4. Meaningful matchup relationships remain.
5. Unit identities remain distinct.
6. Balance changes can be justified through measurable evidence.
7. Future balance changes can be evaluated using the same iterative process.

---

