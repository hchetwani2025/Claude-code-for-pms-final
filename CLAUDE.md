# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

You are the new Product Manager for **Rook Dispatch**. You started this Monday. Priya Raghunathan, the previous PM, left 21 August after 14 months on Dispatch alone. This section is built from Rook's own documents in `00-rook/company/`.

### The products

Rook sells two connected surfaces, subscription-priced per active responder:

- **Rook Dispatch** (yours) — responder coordination. An incident enters the console, Dispatch ranks available responders, sends a callout offer to the top-ranked responder's phone, and moves to the next responder on a decline or timeout. Handlers use the web console; responders use mobile. Current release: **4.2**.
- **Rook Supply** — gear provisioning. Handlers raise requisitions, quartermasters approve and fulfill, issued items carry a maintenance schedule. Supply reads Dispatch's **Responder Availability Record** to schedule maintenance around callout load; it does not write to that record.

Releases ship monthly on a 4.x train. Routing configuration ships with the release — a handler cannot tune it at runtime.

### The people

| Name | Role | Owns | Notes |
|---|---|---|---|
| Helen Achebe | Director of Product | Roadmap and commitments | Chicago. Your manager. |
| Marcus Oyelaran | Engineering Manager, Dispatch | The Dispatch engineering team | Chicago. Start here when unsure of anything. |
| Wen Li | Staff Engineer, Dispatch | Routing logic — she built it | Berlin. No document explains routing fully; ask her. |
| Sofia Marino | Product Designer, Dispatch | Console and phone app | Chicago |
| Nadia Hoffmann | Support Lead, Dispatch & Supply | Ticket volume and themes | Berlin. Worth a standing 15 minutes. |
| Ravi Menon | Data Analyst, Dispatch & Supply | Weekly acceptance-rate numbers | Singapore. Requests go through `#data`. |

### Vocabulary you need on day one

- **Callout** — a request for a responder to attend an incident; the unit of work in Dispatch.
- **Callout offer** — one callout presented to one responder's phone, awaiting accept or decline.
- **Decline** vs. **timeout** — a decline is an active refusal; a timeout is an expired, unanswered offer. Both move the callout to the next responder, but they are recorded separately.
- **Routing priority** — the score ranking available responders for a callout. Inputs: proximity (travel-time estimate), current availability, capability-tag match, and recent-acceptance history. A decline or timeout lowers that responder's recent-acceptance component, and so their routing priority, until it recovers.
- **Acceptance rate** — share of callout offers accepted. Dispatch's headline metric, reported weekly in aggregate.
- **Time-to-accept** and **coverage gap** — secondary metrics: median seconds to accept; incidents with no responder matching the required capability tags.
- **Capability tag** — a responder's labeled competency (flight, structural-entry, hazmat-tolerant, cold-weather, aquatic, crowd-management, de-escalation), matched against incident requirements.
- **Responder Availability Record** — written by Dispatch, read by Supply for maintenance scheduling.
- **Cover identity** — a responder's public persona. Rook holds no mapping to a legal identity, by contract, not policy. Never design a feature that assumes such a mapping exists, and never try to work out who a responder is.

### Where things stand

4.2 (released 12 August) is the live issue. It reweighted routing toward proximity and away from recent-acceptance history — a long-standing ask from responders working wide geographies — and separately cut the callout timeout from 90 to 60 seconds. Since then, acceptance is down and complaint volume is roughly 3x normal, split about two-thirds "phone never rings" to one-third "gone before I could answer." The timeout cut plausibly explains the second theme; the first is unexplained. Priya's read, and Engineering's working assumption, is that this is mostly seasonal (August is soft every year) with the timeout change layered on top — not proof the reweight itself is broken. Nobody has reverted anything, and Priya's handover explicitly warns against making 4.2 reversal the default conversation: the reweight was asked for, and undoing it just moves the complaints to a different group of responders. Your first real task is to get real numbers (ask Ravi) and separate the two effects before anyone concludes anything.

Other open items from the handover:
- No committed Q3 item was formally dropped when 4.2's timeline compressed, but Priya flags this needs a real conversation with Helen: confirm what's still committed.
- There is no written description of how routing ranks responders — only Wen's head. Writing that down is on you.
- The Q3 roadmap (owner: Helen) lists 4.2 items as done/committed; Supply's requisition approval chains target 4.3; handler phone app and shared cover between responders are Q4-exploring, not committed.

### Reference material in this repo

`00-rook/company/` holds the source documents above plus release history and the Q3 roadmap. `00-rook/feedback/` holds four interviews and 25 tickets (Module 2). `00-rook/data/callout-history.csv` is the weekly pings-sent/pings-taken export by responder and handler (Module 3). `00-rook/code/dispatch-routing/` is the actual routing code — owner Wen Li, ask Marcus if she's out (Module 4).

### Brief review habit (Module 6)

- My brief gate is the `review-checklist-skills` skill (`.claude/skills/review-checklist-skills/`). It scores a brief out of 8: owner, success measure, scope holds, problem before fix, two yes/no criteria each. Only 8/8 is Ready. 1b/2b/3b need their "a"; 4b does not. It also writes an animated HTML report to `scratch/review-checklist/` (gitignored). Skill names must use hyphens, not underscores.
- My Module 5 brief ("Quiet responders", `05-super-speed/brief.md` plus one-pager exports and prototypes) is only on branch `claude/admiring-davinci-v1wwxv`, not on `main`. It scored 3/8: no named owner, no chosen success measure, and "I'm ready" conflicts with its own "doesn't touch scoring" scope.
- `Mel_brief.md` ("A way back": score decay/recovery) came in as an upload and is not in the repo. It scored 6/8; the only gap is a named, accountable owner.
- Baseline scores for `06-sidekicks/briefs/`: Bulk Callout 4, Handler Phone App 5, Requisition Approval Chains 7, Routing Override Audit Log 5. None is Ready.
- The routine "Review checklist runner" runs the skill on `06-sidekicks/briefs/` every Monday 09:00 UTC in a fresh session (push + email when done). It pulls the skill from branch `claude/magical-heisenberg-9xkpa5`, so skill changes must be pushed there. My time zone is not confirmed.
