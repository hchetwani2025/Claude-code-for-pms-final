---
name: review-checklist-skills
description: Review and score a product brief (one-pager, proposal, spec) out of 8 against four fixed checks before it goes any further — named owner, success measure, scope consistency, and problem-before-fix. Use when the user asks to review, check, score, vet, or gate a brief, or runs /review-checklist-skills with a file path or pasted text.
argument-hint: <path to brief, several paths, or a folder>
---

# Review checklist

Run the same four checks on a brief, every time, score them against the
same eight criteria, and report them in the same format. This is a gate,
not an edit: judge the brief as written.

## Input

- `$ARGUMENTS` is a file path, several paths, or a folder. For a folder,
  review every brief in it.
- If the user pasted the brief text instead, review that.
- If there is no brief, ask for one. Do not guess which file they mean.
- Read the whole brief before you score any criterion.
- Do not edit the brief. Do not rewrite it for the user.

## Scoring

Each check has two criteria. Each criterion scores **1** (met) or **0**
(not met). There is no half point: if you are unsure, score 0 and say what
is missing.

- Each check scores 0, 1, or 2: **2 = Pass**, **1 = Partial**,
  **0 = Fail**.
- The brief scores out of **8**.
- Back every criterion with a short quote from the brief, or write
  "not in the brief". Judge only what the brief says — do not fill gaps
  from other files or from what you think the author meant.
- Where a criterion says "needs 1a" (or similar), it scores 0 when that
  first criterion scores 0.

## The four checks and their criteria

### 1. Owner named

- **1a. A named owner.** The brief names a person or a named team for the
  work. An author line, a byline, an addressee ("To: Helen"), or a
  department header ("Product, Dispatch") does not count. People who only
  give input or an estimate do not count.
- **1b. The ownership is firm.** Needs 1a. The owner is accountable for
  decisions now — not "TBD", "exploring", "not yet staffed", "whoever
  picks it up", and not only the team that builds it.

### 2. Success measure

- **2a. A measurable signal tied to the problem.** The brief commits to
  one signal that measures the outcome the problem describes. A list of
  options not yet chosen, or an activity measure ("feature shipped",
  "people use it"), does not count.
- **2b. A baseline or a target.** Needs 2a. The signal has a starting
  number or a number to reach.

### 3. Scope holds

- **3a. Scope is stated.** The brief says what the work is, and what it
  is not (a scope section, an in/out list, or "that's the whole ask").
- **3b. The end matches the start.** Needs 3a. Compare the opening
  (problem and proposal) with the closing (scope, next steps, open
  questions). Score 0 if the closing adds work after the core ask, drops
  a need the problem raised, or contradicts the stated scope. List each
  addition, drop, or conflict by name.

### 4. Problem before fix

- **4a. The problem comes first.** A problem statement appears before the
  proposal.
- **4b. The problem stands on its own.** It says who hurts and how, in
  terms that do not depend on the fix — not "we lack <the solution>".

## Verdict bands

| Score | Verdict | Meaning |
|---|---|---|
| 8/8 | **Ready** | All four checks pass. It can move on. |
| 5–7 | **Not ready — small fixes** | The author can fix it in the brief. |
| 0–4 | **Not ready — rework** | Something basic is missing. Send it back. |

Only 8/8 is Ready. A score of 7 is still a gate stop.

## Result emoji

Put one emoji line directly under the score line of each brief:

- **8/8:** `🎉🎊✨ 🎊🎉✨ 🎉🎊✨` (confetti)
- **Below 8:** `😞`

Use these exact strings, so every run looks the same. In the summary table
for several briefs, put the same emoji at the start of the Verdict cell
(`🎉` for 8/8, `😞` for lower).

## Output format

Use exactly this layout for each brief. Keep it short.

```
## <Brief title> — <file name>

**Score: <n>/8 — <verdict>**
<confetti line if 8/8, else 😞>

| Check | Criteria met | Score | Evidence |
|---|---|---|---|
| Owner named | 1a ✓/✗ · 1b ✓/✗ | <0–2> Pass/Partial/Fail | "<quote>" or not in the brief |
| Success measure | 2a ✓/✗ · 2b ✓/✗ | <0–2> Pass/Partial/Fail | "<quote>" |
| Scope holds | 3a ✓/✗ · 3b ✓/✗ | <0–2> Pass/Partial/Fail | "<quote from start>" vs "<quote from end>" |
| Problem before fix | 4a ✓/✗ · 4b ✓/✗ | <0–2> Pass/Partial/Fail | <section order + quote> |

**To fix before it moves on**
- <one line per criterion scored 0: the criterion ID, what is missing, and
  the question the author must answer>
```

If the score is 8/8, write "Nothing to fix." under the fix heading.

When you review more than one brief, put a summary table first — one row
per brief, one column per check with its 0–2 score, the total out of 8,
and the verdict — then the detail for each brief in the same order.

## Do not

- Add checks or criteria beyond these eight. Other issues (tone, length,
  feasibility) go in one optional line at the end, headed "Outside the
  checklist", and only when they are serious. They never change the score.
- Give a point because the idea is good, or hold one back because the idea
  is weak. The checklist scores the brief, not the idea.
- Grade on a curve across several briefs. Each brief stands alone.
