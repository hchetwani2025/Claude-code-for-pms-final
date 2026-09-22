# Quiet responders: what we'd build instead of a number

**To:** Helen Achebe
**Re:** the 4.2 "phone never rings" pattern — before any code ships

## The question nobody answered

Two days after 4.2 shipped, Marcus asked in `#dispatch-team`:

> "was that meant to apply to responders who've been turning jobs down too, or
> only everyone else? the config doesn't distinguish between them as far as I
> can tell... not saying it's wrong, just want to know if it was a decision or
> if it just fell out that way."

Wen was on PTO. Nobody answered it. Three weeks later Nadia had a number for
it: ticket volume up roughly 3x, split about two-thirds "phone never goes off"
to one-third "gone before I could answer." The second theme is the shorter
callout timeout — Nadia said so herself, the same day. The first theme is
Marcus's question, unanswered.

## Who this is for

Meteor Mite, one of Kip's two responders. Kip's other responder, The Gale, is
having the opposite week — same city, same desk, same three monitors. Kip has
been telling Mite to hang in there, because nothing on the console explains
why one coverage card is dead quiet while the other doesn't stop.

The callout-history export backs up what Kip is watching happen. Week of 3
Aug: Dispatch sent Mite 11 callout offers, Mite accepted 8. Week of 31 Aug:
Dispatch sent Mite 1. Over the same four weeks, Gale went from 13 offers to
21. Mite's acceptance didn't collapse first — the offers did. Mite did not
become unreliable. Dispatch stopped asking.

This is the mechanism the glossary already names: routing priority factors in
recent acceptance history, and "declining or timing out lowers the
recent-acceptance component... until the component recovers." Nothing in
Dispatch's data distinguishes a timeout from a decline once it's scored —
that's Marcus's question, still open. A callout timeout cut from 90 seconds
to 60 means more timeouts. Each one costs Mite exactly what an active decline
would. Miss the window twice in a bad week and every subsequent callout ranks
Mite lower — asked less, so fewer chances to recover, so ranked lower again.

## What changes for Mite once this exists

Right now: silence. Mite doesn't know the offers stopped because of a
90-second decision made three release cycles ago about how fast someone
needs to reach for their phone. Mite just knows the phone stopped ringing,
and has started asking Kip if something's broken.

With this built, Mite's app shows a plain account instead: offers this week
against their usual, and a breakdown of accepted / declined / missed-window.
When most of the drop is missed-window, it says so, and names the timeout as
the reason — not "you've been unreliable," because Mite hasn't been. One
action, "I'm ready," lets Mite refresh their own standing directly, instead
of waiting on a callout that isn't coming to prove they're still in.

On Kip's side, the coverage card carries the same line Mite sees: offers this
week vs. usual, and why, when it's dropped. Kip stops guessing whether Mite
went quiet by choice and can tell Mite the actual answer instead of "hang in
there."

## What this deliberately doesn't do

- **Doesn't answer Marcus's question in code.** Whether a timeout should cost
  a responder the same as a decline, and whether the recent-acceptance
  component should ease back on its own, is Wen's call to scope — this is
  what the person on the other end of that call should see once she's made
  it, not a substitute for making it.
- **Doesn't touch the proximity reweight.** Priya's handover is explicit that
  4.2's reweight was a long-standing, deliberate ask and reverting it just
  moves the complaint to a different group of responders. This doesn't
  reopen that.
- **Doesn't assume any mapping to who Mite actually is.** Cover identity
  stays exactly what the glossary says it is: a public-facing persona Rook
  holds no legal mapping to. Everything above is built on the offer/accept/
  decline/timeout record, nothing else.
- **Doesn't close the ticket.** Ravi still has to separate how much of the
  3x is 4.2 and how much is the seasonal softness Priya flagged before
  anyone treats this as solved.

## What I need

Fifteen minutes with Sofia to turn this into two real screens, and a check
with Nadia that "missed window" reads the way responders actually talk about
it — before Wen scopes the change underneath.

*A rough clickable version of both screens is attached: the console view Kip
would see, and the phone screen Mite would see.*
