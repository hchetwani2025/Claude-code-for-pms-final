---
name: review-checklist
description: Review a product brief (one-pager, proposal, spec) against four fixed checks before it goes any further — named owner, success measure, scope consistency, and problem-before-fix. Use when the user asks to review, check, vet, or gate a brief, or runs /review-checklist with a file path or pasted text.
argument-hint: <path to brief, several paths, or a folder>
---

# Review checklist

Run the same four checks on a brief, every time, and report them in the
same format. This is a gate, not an edit: judge the brief as written.

## Input

- `$ARGUMENTS` is a file path, several paths, or a folder. For a folder,
  review every brief in it.
- If the user pasted the brief text instead, review that.
- If there is no brief, ask for one. Do not guess which file they mean.
- Read the whole brief before you judge any check.
- Do not edit the brief. Do not rewrite it for the user.

## The four checks

Give each check one verdict: **Pass**, **Partial**, or **Fail**.
Back every verdict with a short quote from the brief, or say "not in the
brief" when the evidence is absent. Judge only what the brief says — do not
fill gaps from other files or from what you think the author meant.

### 1. Names who owns it

- **Pass** — a named person or a named team is accountable for the work.
- **Partial** — ownership is vague or conditional ("TBD", "someone on
  Supply", "exploring, not staffed"), or it names who builds but not who
  decides.
- **Fail** — no owner anywhere. A byline, author line, or department
  header ("Product, Dispatch") is not an owner.

### 2. Says how we'll know it worked

- **Pass** — a measurable signal that ties back to the stated problem,
  with a baseline or a target.
- **Partial** — a signal exists but has no baseline or target, is hard to
  measure, or measures activity ("feature shipped", "people use it") and
  not the outcome.
- **Fail** — no success measure at all.

### 3. Scope at the end matches scope at the start

Compare what the opening (problem and proposal) says the work is with what
the closing (scope, next steps, open questions, "and while we're at it")
says it is.

- **Pass** — the same work from start to end.
- **Partial** — small drift: one extra item added late, or a need raised in
  the problem that the scope later excludes without saying so.
- **Fail** — the brief grows (several additions after the core ask), or it
  shrinks so that the stated problem is no longer solved, or there is no
  scope statement to compare against.

List each addition or dropped item by name.

### 4. Explains the problem before it proposes a fix

- **Pass** — a problem section comes before the proposal, and it describes
  who hurts and how, in terms that do not depend on the fix.
- **Partial** — the problem exists but comes after the proposal, or it is
  written as "we lack <the solution>".
- **Fail** — no problem statement; the brief opens with and only argues
  for a solution.

## Output format

Use exactly this layout for each brief. Keep it short.

```
## <Brief title> — <file name>

**Verdict: Ready | Not ready** (<n>/4 pass)

| Check | Result | Evidence |
|---|---|---|
| Owner named | Pass/Partial/Fail | "<quote>" or not in the brief |
| Success measure | Pass/Partial/Fail | "<quote>" |
| Scope holds | Pass/Partial/Fail | "<quote from start>" vs "<quote from end>" |
| Problem before fix | Pass/Partial/Fail | <section order + quote> |

**To fix before it moves on**
- <one line per Partial or Fail: what is missing, and the question the
  author must answer>
```

Rules for the verdict:

- **Ready** only when all four checks pass.
- Any Partial or Fail makes it **Not ready**.
- If all four pass, write "Nothing to fix." under the fix heading.

When you review more than one brief, put a summary table first — one row
per brief, one column per check, plus the verdict — then the detail for
each brief in the same order.

## Do not

- Add checks beyond these four. Other issues (tone, length, feasibility)
  go in one optional line at the end, headed "Outside the checklist", and
  only when they are serious.
- Soften a verdict because the idea is good, or harden it because the idea
  is weak. The checklist judges the brief, not the idea.
- Grade on a curve across several briefs. Each brief stands alone.
