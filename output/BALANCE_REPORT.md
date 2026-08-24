# Hollow Crown — Balance Report

## 1. Executive Summary

### Objective

The objective of this analysis was to rebalance the Hollow Crown roster so that deployment costs better reflect battlefield value while avoiding auto-include and trap-pick units.

### Approach

The balancing process followed:

1. Establish baseline performance.
2. Identify outliers.
3. Diagnose the causes.
4. Propose targeted changes.
5. Simulate the first iteration.
6. Analyze remaining issues.
7. Apply a second iteration.
8. Validate the final roster.

### Final Result

The two balance iterations substantially improved roster cohesion while preserving meaningful unit identities and matchup relationships.

- **Ser Halden:** Cost increased from 6 → 8, reducing WIN%/COST from **13.08 → 9.11** while preserving his intended matchup profile.
- **Pyraxis:** DEF/HP increased from 4/20 → 7/24, raising Win% from **23.8% → 41.5%**; his cost was then reduced from 9 → 7, improving WIN%/COST to **5.93**.
- **Roster cohesion:** Win% spread decreased from **54.7pp → 40.0pp**, while WIN%/COST spread decreased from **10.44 → 6.34**.
- **Stability:** No new major outliers were introduced, and the tested matchup relationships remained stable across seeds.
- **Remaining limitation:** Wisp and Sable remain investigation points because their support/ranged value is not fully represented by the current 1v1 simulator.

---

## 2. Baseline Diagnosis

### 2.1 Starting Roster

Using the two runs of simulation (seed 42 and seed 7 agree within ~1pp on every unit, so the numbers are stable, not noise): That gives us good evidence that these aren't just random fluctuations from the chosen seed/trial count.

| Unit       | Class      | Cost |   Win% | Win%/Cost |
| ---------- | ---------- | ---: | -----: | --------: |
| Ser Halden | Knight     |    6 | ~78.5% |     ~13.1 |
| Rookwood   | Myrmidon   |    7 | ~65.3% |      ~9.4 |
| Wisp       | Cleric     |    4 | ~50.9% |     ~12.7 |
| Brennan    | Soldier    |    5 | ~46.7% |      ~9.3 |
| Sable      | Archer     |    5 | ~34.8% |      ~6.9 |
| Pyraxis    | Battlemage |    9 | ~23.7% |      ~2.6 |

#### Statistical Report:

The roster shows a wide spread in both raw win rate and cost efficiency. WIN% ranges from 23.5% to 78.4%, while WIN%/COST ranges from 2.61 to 13.07.

Importantly, cost significantly changes how unit power should be interpreted. For example, Wisp has a lower WIN% than Rookwood (51.2% vs. 65.3%) but much higher efficiency (12.79 vs. 9.33) because Wisp is cheaper.

### 2.2 Baseline findings about Units (based on cross-reference stats):

1. Halden is the clearest high-power outlier:
His def=12 reduces damage from almost every physical attacker to 1 per hit, while his atk=16 lets him deal heavy damage in return. His high win rate is mainly caused by this defensive advantage, not crits or speed.
2. Pyraxis is the clearest low-power outlier:
It has the highest cost (9) but the lowest win rate (23.7%). Its spd=5 means it is frequently doubled, while its def=4 makes it very vulnerable. Although it is the only unit that seriously threatens Halden's resistance, it still loses the damage race.
3. Wisp is potentially underpriced:
Its win rate is close to 50%, suggesting healthy individual performance, but it costs only 4 and has the second-highest WIN%/COST efficiency. It isn't dominant, but its cost may be too low for its performance.
4. Brennan vs. Rookwood — cost is working as a balancing factor: Rookwood has a much higher win rate (65.5% vs. 46.7%), but also costs more (7 vs. 5), resulting in similar efficiency. This is a useful example of cost successfully compensating for performance.
5. Sable — below-average performer: 
It has the second-lowest win rate (34.8%) at the same cost as Brennan (5). Its relatively low def=7 and unfavorable speed matchups make it weaker overall despite costing the same.

### 2.3 Auto-include and trap-pick:

#### Definition concepts: (Through the game design perspective)
Auto-include: A unit whose combination of power, cost, and practical battlefield value makes including it in most or nearly all viable team compositions the rational choice.
Trap-pick: A unit that appears attractive when making a deployment decision, but whose actual battlefield value is substantially worse than the player reasonably expects from its cost, role, or apparent strengths.

#### Candidates: 
Auto-include: By baseline finding #1, Halden. He has the highest raw combat performance (78.5%). His cost (6) doesn't sufficiently compensate for that power.

Trap-pick: By baseline finding #2, Pyraxis.
The high cost (9) and Strong Stat (MAG 18) creates an expectation of high value that the current combat results don't support. Lowest spd (never doubles, gets doubled by 3 of 5 opponents) + lowest def + highest cost is a compounding, not coincidental, set of disadvantages.

### 2.4 Baseline conclusions: 

1. The roster has clear balance outliers, with Halden and Pyraxis representing the two most urgent issues: one is significantly overperforming, while the other is significantly underperforming.
3. Autoinclude: Halden , Trap-pick: Pyraxis
2. Deployment cost is a meaningful balancing tool, but it is not consistently aligned with unit performance at the roster's extremes.
3. Wisp requires further investigation, since its issue is primarily efficiency rather than raw power.
4. The baseline suggests that targeted changes are preferable to broad stat normalization. The goal should be to correct the major outliers while preserving meaningful differences between units.
5. Further iterations should validate changes through additional simulations and matchup analysis, ensuring that improving one unit does not simply create a new dominant or trap pick.


---

## 3. Balance Strategy

### 3.1 Matchup diagnosis

Matrix matchup was run with both seeds 42 vs 7, also both tables for  
#### Matchup Matrix results:
Win% matrix (row unit's win% vs column unit):

pairwise matchup matrix (trials/pair=5000, seed=42)

| Unit      | Ser Halden | Rookwood | Brennan | Sable  | Wisp   | Pyraxis |
|-----------|------------|----------|---------|--------|--------|---------|
| Ser Halden | —          | 99.0%    | 100.0%  | 100.0% | 13.9%  | 79.9%   |
| Rookwood   | 1.0%       | —        | 70.7%   | 90.0%  | 76.9%  | 86.7%   |
| Brennan    | 0.0%       | 29.3%    | —       | 81.3%  | 63.0%  | 62.8%   |
| Sable      | 0.0%       | 10.0%    | 18.7%   | —      | 70.2%  | 76.3%   |
| Wisp       | 86.1%      | 23.1%    | 37.0%   | 29.8%  | —      | 79.8%   |
| Pyraxis    | 20.1%      | 13.3%    | 37.2%   | 23.7%  | 20.2%  | —       |

pairwise matchup matrix (trials/pair=5000, seed=7)

| Unit       | Ser Halden | Rookwood | Brennan | Sable  | Wisp  | Pyraxis |
|------------|------------|----------|---------|--------|-------|---------|
| Ser Halden | —          | 99.0%    | 100.0%  | 100.0% | 14.1% | 79.7%   |
| Rookwood   | 1.0%       | —        | 71.2%   | 90.1%  | 77.1% | 86.7%   |
| Brennan    | 0.0%       | 28.8%    | —       | 80.9%  | 62.0% | 62.6%   |
| Sable      | 0.0%       | 9.9%     | 19.1%   | —      | 70.7% | 75.8%   |
| Wisp       | 85.9%      | 22.9%    | 38.0%   | 29.3%  | —     | 78.2%   |
| Pyraxis    | 20.3%      | 13.3%    | 37.4%   | 24.2%  | 21.8% | —       |

the matchup matrix is stable across seeds — deviations are consistent with sampling noise at 5,000 trials/pair.

<details>
<summary>Detailed Matchup Statistics SEED 7 </summary>

| Unit A     | Unit B   | A Win% | B Win% | Avg Rnds | A Hit% | B Hit% | A Crit% | B Crit% | A Dmg/Turn | B Dmg/Turn | A Doubles | B Doubles |
|------------|----------|--------|--------|----------|--------|--------|---------|---------|------------|------------|-----------|-----------|
| Ser Halden | Rookwood | 99.0%  | 1.0%   | 5.7      | 49.9%  | 88.2%  | 5.0%    | 14.0%   | 5.5        | 2.3        | no        | yes       |
| Ser Halden | Brennan  | 100.0% | 0.0%   | 5.5      | 67.4%  | 75.8%  | 6.1%    | 8.1%    | 5.3        | 0.9        | no        | no        |
| Ser Halden | Sable    | 100.0% | 0.0%   | 4.5      | 62.1%  | 79.8%  | 6.2%    | 10.0%   | 6.3        | 1.9        | no        | yes       |
| Ser Halden | Wisp     | 13.9%  | 86.1%  | 2.5      | 58.5%  | 74.2%  | 5.2%    | 10.3%   | 7.1        | 13.3       | no        | yes       |
| Ser Halden | Pyraxis  | 79.9%  | 20.1%  | 2.3      | 77.5%  | 76.2%  | 6.9%    | 6.2%    | 10.6       | 12.0       | no        | no        |
| Rookwood   | Brennan  | 70.7%  | 29.3%  | 4.8      | 81.2%  | 51.9%  | 13.0%   | 6.1%    | 5.9        | 4.1        | yes       | no        |
| Rookwood   | Sable    | 90.0%  | 10.0%  | 3.0      | 76.1%  | 56.0%  | 13.3%   | 8.2%    | 8.8        | 4.6        | yes       | no        |
| Rookwood   | Wisp     | 76.9%  | 23.1%  | 4.3      | 73.4%  | 49.5%  | 12.1%   | 8.1%    | 6.4        | 4.0        | no        | no        |
| Rookwood   | Pyraxis  | 86.7%  | 13.3%  | 1.8      | 91.2%  | 51.6%  | 14.0%   | 3.9%    | 15.1       | 7.2        | yes       | no        |
| Brennan    | Sable    | 81.3%  | 18.7%  | 5.4      | 64.0%  | 72.8%  | 7.1%    | 8.7%    | 4.4        | 3.4        | no        | no        |
| Brennan    | Wisp     | 63.0%  | 37.0%  | 3.9      | 61.5%  | 66.9%  | 6.4%    | 8.6%    | 5.6        | 5.5        | no        | no        |
| Brennan    | Pyraxis  | 62.8%  | 37.2%  | 3.0      | 79.7%  | 68.6%  | 7.9%    | 5.3%    | 8.3        | 9.9        | no        | no        |
| Sable      | Wisp     | 70.2%  | 29.8%  | 3.7      | 65.1%  | 62.0%  | 7.9%    | 9.3%    | 6.0        | 4.4        | no        | no        |
| Sable      | Pyraxis  | 76.3%  | 23.7%  | 1.9      | 83.1%  | 64.1%  | 9.7%    | 5.0%    | 15.3       | 8.5        | yes       | no        |
| Wisp       | Pyraxis  | 79.8%  | 20.2%  | 2.9      | 77.1%  | 60.8%  | 10.5%   | 3.5%    | 6.9        | 5.8        | yes       | no        |

</details>

<details>
<summary>Detailed Matchup Statistics SEED 42 </summary>

| Unit A     | Unit B   | A Win% | B Win% | Avg Rnds | A Hit% | B Hit% | A Crit% | B Crit% | A Dmg/Turn | B Dmg/Turn | A Doubles | B Doubles |
|------------|----------|--------|--------|----------|--------|--------|---------|---------|------------|------------|-----------|-----------|
| Ser Halden | Rookwood | 99.0%  | 1.0%   | 5.7      | 50.1%  | 88.0%  | 5.1%    | 14.0%   | 5.5        | 2.3        | no        | yes       |
| Ser Halden | Brennan  | 100.0% | 0.0%   | 5.6      | 66.7%  | 76.3%  | 6.0%    | 8.0%    | 5.2        | 0.9        | no        | no        |
| Ser Halden | Sable    | 100.0% | 0.0%   | 4.5      | 62.3%  | 80.1%  | 6.3%    | 9.7%    | 6.3        | 1.9        | no        | yes       |
| Ser Halden | Wisp     | 14.1%  | 85.9%  | 2.5      | 59.0%  | 74.5%  | 5.4%    | 9.8%    | 7.2        | 13.2       | no        | yes       |
| Ser Halden | Pyraxis  | 79.7%  | 20.3%  | 2.3      | 77.2%  | 76.5%  | 7.0%    | 6.1%    | 10.6       | 12.0       | no        | no        |
| Rookwood   | Brennan  | 71.2%  | 28.8%  | 4.9      | 81.0%  | 52.1%  | 13.0%   | 5.9%    | 5.9        | 4.1        | yes       | no        |
| Rookwood   | Sable    | 90.1%  | 9.9%   | 3.0      | 76.3%  | 56.3%  | 12.9%   | 8.1%    | 8.8        | 4.6        | yes       | no        |
| Rookwood   | Wisp     | 77.1%  | 22.9%  | 4.3      | 73.4%  | 50.0%  | 12.2%   | 7.8%    | 6.4        | 4.0        | no        | no        |
| Rookwood   | Pyraxis  | 86.7%  | 13.3%  | 1.8      | 91.5%  | 52.5%  | 13.6%   | 4.3%    | 15.1       | 7.4        | yes       | no        |
| Brennan    | Sable    | 80.9%  | 19.1%  | 5.4      | 64.3%  | 73.3%  | 7.1%    | 9.0%    | 4.4        | 3.5        | no        | no        |
| Brennan    | Wisp     | 62.0%  | 38.0%  | 3.9      | 61.5%  | 67.2%  | 6.0%    | 9.0%    | 5.5        | 5.6        | no        | no        |
| Brennan    | Pyraxis  | 62.6%  | 37.4%  | 3.1      | 79.4%  | 68.9%  | 7.8%    | 5.0%    | 8.3        | 9.8        | no        | no        |
| Sable      | Wisp     | 70.7%  | 29.3%  | 3.7      | 65.5%  | 62.2%  | 8.1%    | 9.0%    | 6.1        | 4.4        | no        | no        |
| Sable      | Pyraxis  | 75.8%  | 24.2%  | 1.9      | 83.1%  | 64.4%  | 9.6%    | 5.5%    | 15.2       | 8.6        | yes       | no        |
| Wisp       | Pyraxis  | 78.2%  | 21.8%  | 2.9      | 77.3%  | 61.1%  | 9.9%    | 4.2%    | 6.8        | 6.0        | yes       | no        |

</details>

#### Matchup findings per Unit 


| Unit       | Baseline diagnosis                  | Matchup diagnosis                                                                 | Confidence                  |
|------------|-------------------------------------|-----------------------------------------------------------------------------------|-----------------------------|
| **Halden** | Major overperformer                 | Dominant vs physical units, hard-countered by Wisp                              | Strong                      |
| **Pyraxis** | Major underperformer / trap-pick  | Loses every matchup; SPD + low survivability prevent MAG from converting into wins | Strong                   |
| **Rookwood** | Strong performer                 | Broadly dominant except vs Halden; SPD contributes but is confounded by SKL/LCK | Moderate                    |
| **Wisp**   | High efficiency                     | Highly matchup-dependent; 1v1 doesn't capture support value                     | Insufficient for cost change |
| **Brennan** | Near baseline                    | Reasonably balanced reference point                                             | Moderate                    |
| **Sable**  | Low baseline WR                     | Strong vs low-DEF/magic units, weak vs physical frontliners; range not modeled  | Insufficient for stat/cost change |

## 4 Iteration and results diagnosis

### 4.1  Iteration 1: Economic + Survivability Fix
#### Balance change:
**Ser Halden**
- **Cost:** 6 → 8
- **Stats:** Unchanged
- **Rationale:** Halden's combat strength is highly matchup-dependent and primarily comes from his DEF 12 against physical attackers. Increasing his deployment cost addresses his high battlefield value through the economy system without removing his intended strengths or his vulnerability to magic.

**Pyraxis**
- **DEF:** 4 → 7
- **HP:** 20 → 24
- **SPD:** Unchanged at 5
- **Cost:** Unchanged at 9
- **Rationale:** Pyraxis's main issue is not his offensive power, as MAG 18 already produces meaningful damage. The changes improve his survivability so he can convert that offensive potential into wins without removing the existing SPD-based counters from units such as Rookwood, Sable, and Wisp.

**Expected Outcome**
- Reduce Halden's excessive cost efficiency.
- Improve Pyraxis's ability to survive and convert damage into victories.
- Preserve meaningful matchup relationships and unit identities.
- Avoid collateral changes to Wisp and Sable.
- Keep the combat rules unchanged.

| Unit | Changes | Goal |
|---|---|---|
| **Ser Halden** | Cost 6 → 8 | Reduce excessive cost efficiency while preserving his matchup identity. |
| **Pyraxis** | DEF 4 → 7, HP 20 → 24 | Improve survivability without changing his SPD-based counters or MAG identity. |

#### Results: 

| Unit        | Win% (Base → Iter1) | Δ Win%     | Win% / Cost (Base → Iter1) | Δ Eff.    |
|-------------|----------------------|------------|-----------------------------|-----------|
| Ser Halden  | 78.5% → 72.9%       | **−5.6pp** | 13.08 → 9.11                | **−3.97** |
| Rookwood    | 65.7% → 61.6%       | −4.1pp     | 9.39 → 8.80                 | −0.59     |
| Wisp        | 50.6% → 49.1%       | −1.5pp     | 12.65 → 12.27               | −0.38     |
| Brennan     | 46.8% → 42.0%       | −4.8pp     | 9.35 → 8.41                 | −0.94     |
| Sable       | 34.6% → 32.9%       | −1.7pp     | 6.93 → 6.58                 | −0.35     |
| Pyraxis     | 23.8% → 41.5%       | **+17.7pp** | 2.64 → 4.61                | **+1.97** |

Iteration 1 reduced the roster's major outliers without introducing a new extreme. Halden's cost increase substantially improved his cost efficiency while preserving his matchup identity, while Pyraxis's survivability buffs increased his Win% from 23.8% to 41.5% without removing his existing counters. The overall Win% and WIN%/COST spreads both narrowed, indicating improved roster cohesion. 

#### Remining Issue:
Iteration 1 corrected Pyraxis's combat survivability, reducing his Win% gap substantially. However, his high deployment cost remains an efficiency outlier. Because cost is intended to influence squad-building decisions, this remaining discrepancy should be validated in an encounter-level testing before making a larger economic adjustment.

### 4.2 Iteration 2: Economic Cost Correction**

#### Balance change:

**Pyraxis**

- **Cost:** 9 → 7
- **DEF:** Unchanged at 7
- **HP:** Unchanged at 24
- **SPD:** Unchanged at 5

- **Rationale:** Pyraxis's combat performance improved significantly after Iteration 1, but his WIN%/COST remains the largest efficiency outlier at 4.61. A conservative cost reduction addresses this remaining economic imbalance without changing his combat profile or matchup relationships. The current simulator does not fully model squad-level value, so cost 7 is treated as a testable hypothesis rather than a definitive final value.

**Expected Outcome**

- Reduce Pyraxis's cost-efficiency outlier.
- Preserve his current combat performance and matchup structure.
- Avoid collateral changes to other units.
- Keep the combat rules unchanged.
- Provide a conservative basis for further validation.

**Limitation:***
This adjustment wil be treated as a **testable balancing hypothesis**, not as proof that 7 is the definitive correct cost.

Because the current simulator does not fully model squad-level encounters, the remaining question is whether Pyraxis's high MAG and burst potential provide additional value in team-based scenarios that is not captured by the 1v1 model.

#### Results: 

| Unit       | Win% (Base → Iter1 → Iter2) | Win% / Cost (Base → Iter1 → Iter2) |
|------------|------------------------------|------------------------------------|
| Ser Halden | 78.5% → 72.9% → 72.9%       | 13.08 → 9.11 → 9.11                |
| Rookwood   | 65.7% → 61.6% → 61.6%       | 9.39 → 8.80 → 8.80                 |
| Wisp       | 50.6% → 49.1% → 49.1%       | 12.65 → 12.27 → 12.27              |
| Brennan    | 46.8% → 42.0% → 42.0%       | 9.35 → 8.41 → 8.41                 |
| Pyraxis    | 23.8% → 41.5% → 41.5%       | 2.64 → 4.61 → **5.93**             |
| Sable      | 34.6% → 32.9% → 32.9%       | 6.93 → 6.58 → 6.58                 |

Iteration 2 reduced Pyraxis's cost from 9 to 7, improving his WIN%/COST from 4.61 to 5.93 while keeping his Win% at 41.5% and preserving all 15 matchup results. The roster remained stable, with the efficiency spread narrowing from 7.66 to 6.34 and the Win% spread remaining unchanged at 40.0pp. No new major outliers were introduced, and the iteration successfully reduced Pyraxis's remaining cost-efficiency imbalance without affecting combat performance.

### 4.3 Final Roster

| Unit | Final Cost | Final DEF | Final HP | Final Win% | Final WIN%/COST |
|---|---:|---:|---:|---:|---:|
| Ser Halden | 8 | 12 | — | 72.9% | 9.11 |
| Rookwood | 7 | — | — | 61.6% | 8.80 |
| Wisp | 4 | — | — | 49.1% | 12.27 |
| Brennan | 5 | — | — | 42.0% | 8.41 |
| Pyraxis | 7 | 7 | 24 | 41.5% | 5.93 |
| Sable | 5 | — | — | 32.9% | 6.58 |

All unspecified stats remain unchanged from the original roster.

### 4.4 Validation Scope**

The final roster should be considered a validated improvement within the scope of the current 1v1 combat simulator, rather than a fully validated squad-level balance solution.

Wisp's support/healing value and Sable's ranged advantage are not fully represented by the current simulation. Therefore, their remaining efficiency and Win% differences are treated as investigation points rather than confirmed balance problems.

### 5 Iterations conclusion

The two balance iterations successfully reduced the roster's main balance extremes while preserving meaningful matchup differences and unit identities. Iteration 1 addressed Halden's excessive cost efficiency and Pyraxis's low survivability, while Iteration 2 further corrected Pyraxis's remaining cost-efficiency gap through a conservative cost reduction. Across both iterations, the Win% spread decreased from 54.7pp to 40.0pp, and the WIN%/COST spread decreased from 10.44 to 6.34. No new major outliers were introduced, and matchup relationships remained meaningful. The remaining differences involving Wisp and Sable are treated as investigation points rather than confirmed balance issues, since their support and ranged value are not fully represented by the current 1v1 simulator. Overall, the roster is substantially more coherent, while further squad and encounter-level validation would be the appropriate next step before making additional balance changes.

The remaining differences involving Wisp and Sable are treated as investigation points rather than confirmed balance issues, since their support and ranged value are not fully represented by the current 1v1 simulator. Further squad- and encounter-level validation should therefore be performed before making additional balance changes.

