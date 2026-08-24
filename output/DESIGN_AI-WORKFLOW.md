# Hollow Crown — AI Design Workflow

## 1. Objective

The objective of the AI-assisted workflow was to use AI for evidence-based
balance analysis and hypothesis generation while keeping simulation results
and designer judgment as the final validation.

The workflow followed:

**Measure → Diagnose → Cross-check → Hypothesize → Simulate → Analyze → Iterate → Verify**

The AI was not treated as an authority on balance. AI-generated conclusions
and balance proposals were treated as hypotheses that required validation
through the existing combat simulator.

---

## 2. AI Tools

### ChatGPT

Used for:

* Understanding the existing combat rules and roster.
* Interpreting simulator results.
* Identifying potential outliers.
* Prompting.
* Structuring the balance report and design documentation.

### Claude

Used for:

* Understanding the existing combat rules and roster.
* Interpreting simulator results.
* Identifying potential outliers.
* Generating hypotheses about why certain units over- or under-performed.
* Proposing candidate cost/stat changes.
* Challenging balancing assumptions.
* Identifying edge cases and possible misleading metrics.
* Processing and validatinh baseline and iteration simulations.

### AI Tool Rationale

Both tools were used as complementary analysis assistants.

ChatGPT was generally more exploratory and useful for broad system analysis
and structuring the investigation. Claude was generally more concise and
useful for cross-checking relationships between unit statistics, matchups,
and simulation results.

AI outputs were compared against the repository and simulator data before
being accepted as evidence.

---

## 3. AI-Assisted Design Process

### Step 1 — Baseline Diagnosis

**Objective**

Establish an evidence-based understanding of the initial roster balance
before making any changes.

**AI was asked to:**

- Inspect the combat simulator and roster.
- Explain the combat rules and available metrics.
- Analyze baseline Win% and WIN%/COST.
- Identify major balance outliers.
- Separate facts, conclusions, and hypotheses.
- Identify limitations of the 1v1 model.
- Avoid proposing balance changes.

**Result**

A baseline diagnosis identifying the main outliers and the questions that
must be answered before modifying the roster.

---

### Step 2 — Pairwise Matchup Analysis

**Objective**

Generate more detailed evidence about how individual units perform against
each other.

**AI was asked to:**

- Extend the existing simulator with reusable matchup functionality.
- Preserve all existing combat rules and baseline behavior.
- Simulate every unique unit pairing.
- Generate a matchup matrix and per-matchup statistics.
- Repeat the analysis using multiple seeds.


<details>
<summary>PROMPT IN STEP 2 </summary>

///
I am continuing the balance investigation of the Hollow Crown roster.
The baseline simulation is already working and must remain unchanged.
I now need to add a pairwise matchup analysis to the existing simulator.
### Goal
For every unique pair of units in the current roster, simulate them against each other and generate a matchup matrix.
Use the existing combat rules exactly as they are.
Do NOT:
* change unit stats
* change unit costs
* change combat formulas
* change RNG behavior
* add movement or positioning
* add team combat
* make any balance changes
### Simulation
Use:
* 5,000 trials per matchup
* seed 42
* the same initialization and combat logic used by the baseline
Each unique pair should be evaluated once, with the results reported for both units.
### Output
Generate a matrix like:
| Unit     | Halden | Rookwood | Brennan | Sable | Wisp | Pyraxis |
| -------- | -----: | -------: | ------: | ----: | ---: | ------: |
| Halden   |      — |        ? |       ? |     ? |    ? |       ? |
| Rookwood |      ? |        — |       ? |     ? |    ? |       ? |
| Brennan  |      ? |        ? |       — |     ? |    ? |       ? |
| Sable    |      ? |        ? |       ? |     — |    ? |       ? |
| Wisp     |      ? |        ? |       ? |     ? |    — |       ? |
| Pyraxis  |      ? |        ? |       ? |     ? |    ? |       — |
For each matchup, also report:
* Unit A
* Unit B
* Unit A Win%
* Unit B Win%
* Average rounds
If the existing simulator already exposes damage/follow-up/crit information without modifying combat rules, include those metrics as well.
### Implementation
Prefer adding reusable matchup functions to the existing simulator rather than duplicating combat logic.
Before making changes, inspect the existing code and explain briefly where the matchup functionality should be added.
Then implement it.
Do not interpret the results or recommend balance changes yet.
After implementation, show me:
1. What files were changed.
2. What functions were added or modified.
3. How to run the matchup simulation.
4. A sample of the generated output.
///

</details>


**Result**

A reproducible matchup dataset showing Win%, average rounds, and available
combat metrics for every pair.

---

### Step 3 — Matchup Diagnosis

**Objective**

Identify the likely mechanical causes behind the baseline outliers.

**AI was asked to investigate:**

- Halden's physical-matchup dominance and DEF.
- Pyraxis's low survivability and SPD.
- Rookwood's follow-up potential.
- Sable's matchup dependence and unmodeled ranged value.
- Wisp's apparent cost efficiency and unmodeled support value.

Findings were classified as:

- Strong evidence
- Moderate evidence
- Hypothesis requiring further testing

<details>
<summary>PROMPT IN STEP 3 </summary>
///
Analyze the matchup results we just generated.
Do not propose balance changes yet.
The purpose of this analysis is to identify the likely causes behind the baseline outliers.
Focus on these questions:
Halden

Is Halden broadly dominant across the roster or only against specific units?
Which matchups contribute most to his ~78.5% baseline win rate?
Do the results support the hypothesis that his DEF 12 and the minimum-damage rule are the main cause of his overperformance?
Pyraxis

Is Pyraxis broadly weak or mainly weak against specific opponents?
Does his MAG 18 produce meaningful offensive advantages in any matchup?
How much do low SPD and low DEF appear to contribute to his losses?
Rookwood

Are his wins broadly distributed?
Is there evidence that SPD/follow-up mechanics contribute disproportionately to his performance?
Sable

Is her low win rate consistent across matchups?
Are there matchups where she performs reasonably well?
Could the current 1v1 model be underrepresenting her ranged role?
Wisp

Is her performance broadly average?
Does her low cost create unusually strong efficiency?
Does the 1v1 data provide enough evidence to consider changing her cost?
Finally, classify each finding as:

Strong evidence
Moderate evidence
Hypothesis requiring further testing
Do not recommend stat or cost changes yet.
End with the 3 most important investigations that should happen next.
///

</details>

**Result**

A mechanic-based diagnosis supported by matchup evidence, with clear
uncertainties and priorities for further investigation.

---

### Step 4 — Targeted Balance Iteration

**Objective**

Convert the strongest findings into a small number of testable balance
changes.

**AI was asked to:**

- Propose 2–3 targeted approaches.
- Prioritize the major outliers.
- Preserve unit identity and meaningful matchups.
- Explain the expected impact and possible side effects.
- Avoid unnecessary changes to Wisp, Sable, or the combat rules.

Candidate changes were then implemented and simulated rather than accepted
solely based on AI recommendations.

<details>
<summary>PROMPT IN STEP 4 </summary>

///
We now have enough evidence from the baseline and matchup analysis to begin the first balance iteration.
I do NOT want more general diagnostics at this stage.
Based on the baseline and matchup findings, propose a small number of targeted balance changes.

**Key findings:**
Ser Halden
Cost: 6
Baseline Win%: ~78.5%
Dominates Rookwood, Brennan, and Sable (99–100% win rate).
His DEF 12 combined with the minimum-damage floor makes him extremely resistant to physical attacks.
He is strongly countered by Wisp (13.9% win rate), mainly because Wisp attacks RES and can double him.
His dominance is therefore primarily physical-matchup driven rather than universal.

Pyraxis
Cost: 9
Baseline Win%: ~23.7%.
Loses against every unit in the matchup matrix.
MAG 18 produces meaningful damage and is not a dead stat.
However, DEF 4, HP 20, and SPD 5 make him extremely fragile.
Rookwood and Sable double him.
His offensive power does not convert into enough wins.

Rookwood
Cost: 7
Baseline Win%: ~65.3%.
Wins broadly against most units except Halden.
SPD 16 contributes to several follow-up attacks, but SKL/LCK also contribute significantly.

Wisp
Cost: 4
Baseline Win%: ~50.9%.
Very high apparent cost efficiency.
Highly matchup-dependent.
Her healing/support value is not represented in the current 1v1 model.
Do not treat her current efficiency as sufficient evidence for a cost increase.

Sable
Cost: 5
Baseline Win%: ~34.8%.
Strong against Wisp and Pyraxis but weak against physical frontliners.
Her range 2 is not represented in the 1v1 simulator.
Design objective
The goal is NOT to make every unit have approximately 50% win rate.
The goal is to:
remove the clear auto-include/trap-pick extremes,
preserve meaningful matchup differences,
preserve unit identity,
keep the cost curve meaningful,
avoid broad stat normalization,
and use the smallest targeted changes that address the identified causes.
Task
Propose 2–3 possible first-iteration balance approaches.
For each approach provide:

- Exact proposed changes.
- Which problem each change addresses.
- Why the change targets the identified cause rather than just the symptom.
- Expected impact on the relevant matchups.
- Possible unintended consequences.
- Which option you recommend and why.
- Prioritize targeted changes to Halden and Pyraxis.
- Do not edit any files yet. I want to review the proposed changes first.
///

</details>


**Result**

three small, evidence-based balance iterations targeting the identified causes
rather than broadly normalizing the roster.

---

### Step 5 — Verification and Iteration Review

**Objective**

Determine whether the proposed changes actually improved roster cohesion
without creating new problems.

**AI was used to:**

- Compare baseline, Iteration 1, and Iteration 2 results.
- Analyze changes in Win% and WIN%/COST.
- Check whether important matchup relationships were preserved.
- Identify remaining outliers.
- Determine whether additional iteration was justified.

<details>
<summary>PROMPT IN STEP 5 </summary>

///
I am ready to implement Balance Iteration 2.
Use the Iteration 1 roster as the starting point.
## Iteration 2 — Approved Change option 1
Modify ONLY Pyraxis:
- Cost: 9 → 7
- HP: 24 → 24
- DEF: 7 → 7
- SPD: 5 → 5
- All other Pyraxis stats unchanged.
Do not modify any other unit.
Do not modify:
- combat rules
- simulator logic
- formulas
- trial methodology
- seeds
Do not overwrite the original roster or Iteration 1 CSV.
Create a separate CSV for Iteration 2, for example:
roster_iteration_2.csv
## Validation
Run the simulator using the Iteration 2 roster with the same methodology used previously:
- 2000 trials
- seed 42
- seed 7
Report:
1. Win% for every unit.
2. WIN%/COST for every unit.
3. Baseline → Iteration 1 → Iteration 2 comparison.
4. Change in Pyraxis's Win%.
5. Change in Pyraxis's WIN%/COST.
6. Overall Win% and WIN%/COST spread.
7. Whether a new major outlier appears.
Then re-run the matchup analysis and verify that Pyraxis's combat matchups remain unchanged, since only deployment cost was modified.
Pay particular attention to:
- Pyraxis vs Halden
- Pyraxis vs Rookwood
- Pyraxis vs Brennan
- Pyraxis vs Sable
- Pyraxis vs Wisp
## Important
This is a controlled balance iteration.
Do NOT make any additional balance changes based on the results.
Do NOT start Iteration 3.
Do NOT modify the combat rules.
At the end, provide a concise summary of:
- files created,
- files modified,
- Iteration 2 results,
- whether Pyraxis remains an efficiency outlier,
- and whether the iteration introduced any new balance concern.
///

</details>

**Result**

A validated iteration with measurable improvement and documented remaining
limitations.

---

## 4. AI Verification

AI recommendations were treated as hypotheses rather than conclusions.

For example, the proposed Pyraxis cost reduction from 9 → 7 was not accepted
because it appeared reasonable. It was simulated and evaluated using the
resulting Win% and WIN%/COST data.

The change improved Pyraxis's WIN%/COST from **4.61 → 5.93** while keeping
his Win% at **41.5%** and preserving the tested matchup structure.

This verification step ensured that AI confidence did not replace measurable
simulation evidence.

---

## 5. AI Error / Misleading Recommendation

One important lesson from the workflow was that an AI-generated balance recommendation can sound reasonable while still being incorrect under the actual combat model.

A concrete example occurred when evaluating the role of **Wisp** as a potential trap pick.

The initial temptation was to interpret low performance primarily through its win rate. However, the definition of a trap pick should not simply be:

> "The unit with the lowest win rate."

A trap pick is better understood as a unit whose opportunity cost is poor: the player spends resources on it but receives insufficient battlefield value compared with realistic alternatives.

This distinction required checking the simulator results, cost efficiency, and matchup behavior rather than assigning the label based on a single metric.

Similarly, the analysis of **Ser Halden** showed why raw win rate alone is insufficient. His `DEF = 12` creates a strong defensive floor against the physical attackers represented in the roster, while his `ATK = 16` allows him to defeat their defenses efficiently. The simulator results supported the conclusion that his strength was not simply a statistical anomaly but was reinforced by the structure of the combat formula.

## 6. Key Design Decisions

### Ser Halden

Cost increased from **6 → 8**.

The change targeted excessive cost efficiency while preserving his high
defensive identity and vulnerability to magic-based attacks.

### Pyraxis

DEF increased from **4 → 7** and HP from **20 → 24**.

These changes targeted survivability rather than MAG, allowing Pyraxis to
better convert his existing offensive power into wins.

His cost was subsequently reduced from **9 → 7** after Iteration 1 showed
that his combat performance had improved but his cost efficiency remained
an outlier.

### Wisp

No cost change was made.

Her 1v1 efficiency appeared high, but the simulator does not fully represent
her support/healing value. The evidence was therefore considered insufficient
for an immediate cost adjustment.

### Sable

No immediate balance change was made.

Her ranged advantage is not fully represented by the current 1v1 model, so
her lower Win% was treated as an investigation point rather than definitive
evidence of underpowering.

---

## 6. Scaling the Workflow

For a larger roster, the same human-in-the-loop structure could be automated:

1. Run standardized simulations across multiple seeds and trial counts.
2. Generate Win%, WIN%/COST, matchup spreads, and outlier reports.
3. Use AI to classify likely causes and generate balance hypotheses.
4. Automatically simulate candidate changes.
5. Reject changes that create new major outliers.
6. Present the strongest candidates for designer review.
7. Store each iteration's inputs, hypotheses, changes, and results.

This allows AI to handle repetitive analysis while keeping simulation as the
validation layer and the designer as the final decision-maker.

---

## 7. Key Principle

> **AI proposes; simulation verifies; the designer decides.**
