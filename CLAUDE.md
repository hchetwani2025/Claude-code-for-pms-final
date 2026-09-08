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

### The company

Rook Industries builds coordination and provisioning software for the
protective-response sector: independently-operating masked responders,
and the handlers and quartermasters who support them. Founded 2014,
headquartered at Site Aleph. 241 employees, mostly remote. Revenue is
subscription, priced per active responder.

Two products, both on a monthly release train, point releases numbered
4.x:

- **Rook Dispatch** — responder coordination: availability, proximity,
  callout routing, acceptance. Used by handlers (web console) and
  responders (mobile). This is your product.
- **Rook Supply** — gear provisioning: requisitions, maintenance, failure
  reports. Used by handlers and quartermasters. Reads the **Responder
  Availability Record**, which Dispatch writes; Supply never writes to
  it, so a change to how Dispatch calculates availability reaches Supply
  automatically.

Confidentiality: Rook never stores a responder's legal identity, only
capability tags, availability windows, and callout history. Don't design
around, or try to reconstruct, who anyone is — read Security Policy 4.1
before touching responder records.

### Your job

You are the Product Manager for Rook Dispatch, succeeding Priya
Raghunathan (departed 21 August 2026 after fourteen months, no
handover overlap). Dispatch is the flagship product — the one
responders stick around for. In one line: it ranks available
responders against an incoming incident, offers the callout to the
top of the list, and moves to the next responder on decline or
timeout.

Headline metric: **acceptance rate** (share of callout offers
accepted vs. declined or timed out), reported weekly in aggregate.
Also watched: **time-to-accept** (median seconds to acceptance) and
**coverage gap** (incidents where no available responder matched the
required capability tags).

### Where things stand

Release 4.2 shipped 12 August 2026, clean, no rollback. Its headline
change: routing now weights proximity more heavily against recent
acceptance history — a long-requested fix for responders in wide
geographies losing callouts to someone with a better acceptance record
but much farther away. The same release cut the callout offer timeout
from 90s to 60s.

Since then, acceptance is down and callout tickets are running ~3x
normal, in two roughly-even themes: responders whose phones "never go
off" (unexplained) and responders who see the offer but miss the
window before it moves on (expected — the timeout cut). Priya's read,
left in her handover note, is that this is mostly the usual August
seasonal dip plus two overlapping changes, and that it should recover
in September; she was explicit that reverting 4.2 would just trade one
unhappy group of responders for another. Nobody has yet separated the
seasonal effect from the two release changes with real numbers — that
analysis is open and yours. The team agreed to hold off on conclusions
until you'd had a week to look yourself.

Also open, left by Priya: no committed roadmap item was formally
dropped from 4.2, but some got squeezed by the timeline — confirm with
Helen which are still Q3 commitments. And there is no written
description anywhere of how routing actually decides who gets pinged;
that lives only in Wen Li's head.

**Q3 roadmap** (Helen Achebe owns; committed items against a numbered
release are locked, changes go through Product):

| Item | Surface | Target | Status |
|---|---|---|---|
| Change to who gets pinged | Dispatch | 4.2 | Shipped |
| Availability Confidence score | Dispatch | 4.2 | Committed |
| Ping timeout tuning | Dispatch | 4.2 | Shipped |
| Requisition approval chains | Supply | 4.3 | Committed |
| Handler phone app | Supply | Q4 | Exploring |
| Shared cover between responders | Dispatch | Q4 | Exploring |

### People (Dispatch)

- **Helen Achebe** — Director of Product, owns Dispatch & Supply
  roadmap. Your manager. "Good. Will give you room."
- **Marcus Oyelaran** — Engineering Manager, Dispatch. Default person
  to ask when unsure of anything; can usually pull numbers.
- **Wen Li** — Staff Engineer, built the routing/ranking logic
  (`00-rook/code/dispatch-routing/`). The only real source on how
  ranking works — ask Marcus if she's out.
- **Sofia Marino** — Product Designer, console and phone app.
- **Nadia Hoffmann** — Support Lead (Dispatch & Supply), sees ticket
  volume first. Worth a standing check-in.
- **Ravi Menon** — Data Analyst (Dispatch & Supply, Singapore), reports
  weekly on responder answer rates; go through #data.
- **Priya Raghunathan** — your predecessor, departed. Her handover note
  is `00-rook/company/notes/handoff-from-priya.docx`.

### Vocabulary (Dispatch-specific)

- **Responder** — takes callouts, not a Rook employee, no legal
  identity in our systems.
- **Handler** — manages a responder's (or small group's) availability,
  gear, readiness; the one actually using the console.
- **Callout** — a request for a responder to attend an incident; a
  **callout offer** is that request pushed to one specific responder,
  live until it's accepted, declined, or times out.
- **Routing priority** — the ranking score: proximity (travel-time),
  availability, capability match, and recent acceptance history.
  Declining or timing out lowers a responder's recent-acceptance
  component, and so their ranking, until it recovers.
- **Capability tag** — a responder's competency (e.g. flight,
  hazmat-tolerant, aquatic), matched against incident requirements.
- **Coverage gap** — an incident nobody with the right tags could take,
  distinct from low acceptance (nobody could go, vs. nobody would).
- **Responder Availability Record** — shared record Dispatch writes
  and Supply reads.
- **Mutual aid** — cross-region coverage between responders; not built,
  on the Q4 explore list as "shared cover."

### Where things live in this repo

- `00-rook/company/` — one-pagers, glossary, team roster, Priya's
  handover, the #dispatch-team Slack export.
- `00-rook/data/callout-history.csv` — weekly pings-sent vs.
  pings-taken by responder/handler, for the acceptance-rate analysis.
- `00-rook/feedback/` — 4 interviews, 25 tickets (Module 2).
- `00-rook/code/dispatch-routing/` — the actual ranking/offer code:
  `config.py` (tuning values), `routing.py` (ranks responders),
  `offer.py` (pushes offers, walks the list), `history.py`
  (acceptance score), `availability.py` (who's free, where, travel
  time). Owner: Wen Li.
