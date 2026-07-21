# Reply Triage Drafter

A free Claude skill that classifies an inbound sales reply and drafts the next message
using a named response structure instead of an improvised one.

Paste a prospect's reply plus one line of context. Get back a classification, the
structure chosen, a drafted response, and the reasoning — in about thirty seconds.

MIT licensed. Works in Claude Code, or by copy-paste into any Claude session.

---

## Install

**Claude Code —** copy `SKILL.md` into your project:

```bash
mkdir -p .claude/skills/reply-triage-drafter
curl -o .claude/skills/reply-triage-drafter/SKILL.md \
  https://raw.githubusercontent.com/cursedplum/claude-reply-triage/main/SKILL.md
```

Claude Code picks it up automatically.

**Anywhere else —** open [`SKILL.md`](SKILL.md), copy the *Instructions* and *Output
template* sections into a prompt along with the prospect's reply, and send. Nothing in it
is Claude-specific, though that's where it's been tested.

See [`EXAMPLE.md`](EXAMPLE.md) for a full run.

---

## What it does

1. **Classifies** the reply as *Interested*, *Objection*, or *Not-now*.
2. **Sub-classifies objections** as Fit, Priority, Budget, or Trust.
3. **Picks a response structure** — LAER for charged Trust/Fit objections,
   Feel-Felt-Found for Budget/Priority, a direct next step for interested replies.
4. **Drafts the message**, with the reasoning stated so you can disagree with it.
5. **Flags explicit opt-outs as final** rather than as objections to overcome.

That last one is deliberate. A reply-handling tool that treats "stop contacting me" as a
persistence opportunity is a liability, not a feature — so the skill escalates it and
refuses to draft a follow-up.

---

## ⚠️ About the numbers in this skill — read this part

**This skill quotes no objection-frequency statistics, and that's deliberate.**

An earlier draft did. It carried a "48% budget / 32% timing / 20% competitor" split,
attributed to a vendor blog, wrapped in a prominent caveat about it being unreplicated
proprietary data. Before publishing I opened that page to check the wording of the caveat.

**The split isn't on it.** What the page actually reports — citing Gong's analysis of 300
million cold calls, not its own data — is 49.5% dismissive brush-offs and 42.6%
situational concerns, which merges budget and timing into one bucket and so can't produce
the taxonomy that split was supposed to support.

I had been careful about that number's *epistemic status* for weeks without ever checking
whether the source contained it. Labelling something "vendor data, treat with caution"
says how much to trust a figure. It says nothing about whether the figure is real.

Three other statistics from the same page came apart on the same read, including one that
meant the **opposite** of what I'd written: the page says 44% of reps *do* follow up after
a first "no"; I had it as 44% *quitting*.

All of them are gone. Nothing was swapped for a substitute that happened to fit.

**What's left:** the taxonomy itself, as a classification lens — which is what it's good
for and never depended on the percentages. The skill sorts what's in front of you. It
won't tell you how common your objection is, because I can't currently support a claim
about that.

**The gap I can't fill either:** there is no published conversion benchmark by triage
category. Nobody reliably reports "interested → demo" rates. If you see that quoted with
confidence, ask where it came from.

If you have better-sourced objection-frequency data, please open an issue. I'd rather cite
yours than nothing — but I'd rather cite nothing than something I haven't opened.

Other sourcing: LAER, CRAC, Feel-Felt-Found, and Boomerang are established, widely-used
response structures, carried here unsourced. An earlier draft attributed them to a 2026
Cognism article; that article was opened directly and names none of the four — it
presents its own five-step framework instead. Re-attributing four names to whichever
real originator coined each isn't worth the research cost for a low-stakes framework
label, so they're presented as general convention rather than tied to a source that
doesn't actually cover them.

---

## Tested, not just written

Run on Claude Sonnet 5, 2026-07-19, via `claude -p`, against the current skill — the one
with the objection-frequency figure removed.

Given a Priority objection with a budget history buried in it — a fictional VP of RevOps
saying a similar project "stalled out because leadership didn't want to commit budget
mid-year" and that now isn't the right time — the skill classified it as
**Objection: Priority**, naming the mid-year budget freeze as the mechanism behind the
timing objection rather than mis-reading it as a Budget objection, chose Feel-Felt-Found
over LAER, drafted a full reply, and did **not** escalate it as an opt-out. It emitted no
frequency percentage anywhere in the output — nothing attached to the taxonomy, the
reasoning notes, the rationale, or the draft. Passed first run, no fixes.

The full run — including the drafted message body, not an excerpt — is in
[`EXAMPLE.md`](EXAMPLE.md).

---

## Compliance

Every output ends with a guardrail footer: CAN-SPAM opt-out handling (24–48h, final),
GDPR legitimate-interest revocation, and a note on France.

**On France, since most write-ups get this wrong:** B2C email prospecting in France
**already** requires explicit consent under existing CNIL/GDPR practice. It is not a new
rule starting in August 2026. The 11 August 2026 law that gets cited in this context
covers *telephone* prospecting — cold calls to personal numbers become opt-in, replacing
the Bloctel opt-out register. Reading it as an email deadline gets your exposure
backwards: there is no grace period to plan around, because the email requirement is
already in force.

**This is guidance, not legal advice.** Confirm current requirements with counsel before
sending at scale.

---

## Where this came from

This is one of five skills from **Outreach Engine**, a paid pack covering prospect
research, cold-email sequencing, follow-up cadence planning, reply triage, and discovery
calls — each built from dated 2025–26 sources and live-tested before shipping.

This one is free, MIT, and standalone. It's a fair sample of how the rest are built: if
you don't like this, don't buy those. The other four skills are in
[Outreach Engine](https://cursedplum.gumroad.com/l/outreach-engine) on Gumroad. The
benchmark research behind the whole pack is published free at
[cursedplum.substack.com](https://cursedplum.substack.com).

## License

MIT — see [`LICENSE`](LICENSE). Use it commercially, fork it, ship it inside your own
tooling. No attribution required, though it's welcome.
