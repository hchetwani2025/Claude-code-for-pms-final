# 05 · Super Speed — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. You've spent three sessions finding out what went
wrong: the two piles of feedback that didn't agree, the numbers that
hid four people inside an average, and the code that settled it —
the shorter timeout is what did it.

At the end of the session, ask Claude Code to save the prompts you
wrote yourself below — not the starter prompt. The closing slide has
the exact prompt to paste. By Module 6 this file is a prompt library
built from your own questions.

---

## Prompts I wrote this session

### 1. Find what the brief is missing
Using Kip and Meteor Mite, walk me through what's still missing from
the brief before this could actually get built. The note says this
shouldn't just be a setting we quietly flip.

### 2. Cut it for a director
Make it succinct — executive director level audience — more
pictographic.

### 3. Change the container, keep the content
Turn this into PowerPoint, but one pager. / Convert to PDF.

### 4. Make it real, not described
Take the brief you just wrote and build me a working prototype, an
actual screen I can click through, not a description of one. Save it
as 05-super-speed/prototype.html, a single file I can just open in my
browser. Show me where this would actually happen, and make at least
one thing on it respond when I click it.

### 5. Save the artefact exactly as it stands
Save the brief exactly as it stands now as 05-super-speed/brief.md.
Show me the file when it's done.

### 6. Ask for the next prompts
Suggest more prompts to polish the prototype — easy, intuitive and
clean.

---

## Polish prompts (run against prototype.html)

**Make it cleaner**

- Strip the prototype to one idea per screen. On Kip's console, hide
  the "Why?" details until clicked and make the offer count the only
  large number. On Mite's phone, cut the explanation box to two
  sentences. Nothing else changes.
- Give the console and phone the same spacing scale and the same
  three type sizes. Right now they look like two different products —
  make them read as one.
- Add a 200ms transition when the "Why?" panel opens and when
  "I'm ready" changes state, so clicks feel like they did something.
  No other animation.
- Make it work at 375px wide without horizontal scroll. Stack Kip's
  two cards vertically on narrow screens.

**Make it more real**

- Add the offer itself. Give Mite's phone a second screen: a live
  callout offer with a 60-second countdown that visibly runs out,
  then flips to the "missed window" state. That's the moment the
  brief is about — show it happening.
- Add a small 10-week sparkline under "Offers this week" on each
  console card, using the real numbers from
  00-rook/data/callout-history.csv. Kip should see the drop, not just
  read the number.
- Show Mite's phone in a normal week too — 11 offers, mostly
  accepted. Add a toggle so I can flip between the good week and the
  bad week and see what actually changes on screen.
- Give the console a dark and light theme toggle. Kip's interview
  asks for dark mode; keep dark as the default and make sure the
  amber "Why" note still reads on both.

**Close the gaps the brief names**

- Build the unsympathetic case. Add a third coverage card for a
  responder with 4 real declines and 0 missed windows. Make the card
  honest without making it accusatory, and show me the wording.
- Give Kip a lever. After "Why?" expands, add one action — "Check in
  with Mite" or "Flag to Marcus" — and make it respond when clicked.
  Then tell me which one you'd ship and why.
- Define what "I'm ready" actually does. After tapping, show a
  cooldown ("available again in 4h") and a one-line note on how it
  moves ranking. If you can't say what it does, say so on the screen.
- Show the same console for a handler with 30 responders, not 2. Turn
  the cards into a sortable list where "quiet for reasons that aren't
  declines" floats to the top.
- Rewrite every label on both screens using words that appear in the
  tickets in 00-rook/feedback/tickets/. Then list what you changed
  and why.

**After any of the above**

- What did you assume that isn't in the brief?
