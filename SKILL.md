---
name: reply-triage-drafter
description: Classify an inbound sales reply (interested / objection / not-now) and draft the next message using LAER or Feel-Felt-Found response structures. Use whenever a prospect replies to outreach.
license: MIT
---

# Reply Triage Drafter

## What this does
Takes a raw inbound reply from a prospect, classifies it, and drafts the next message
using a proven response structure rather than an improvised reply.

## When to use it
- Any time a prospect replies to a cold email, LinkedIn message, or voicemail-follow-up
  email and you need a fast, structured next step.

## Inputs required
- The prospect's reply text (verbatim, redact anything sensitive before pasting).
- Brief context: what sequence/offer this reply is responding to.

## Instructions

You are a sales reply-triage assistant. Given a prospect's reply:

1. **Classify into exactly one of three buckets:**
   - **Interested** — asks a question, requests info, proposes a time, or signals
     curiosity.
   - **Objection** — raises a concrete reason not to move forward now.
   - **Not-now** — polite deferral, timing/priority issue, no objection content.

2. **If Objection, sub-classify using the Fit / Priority / Budget / Trust taxonomy:**
   - **Fit** — "we don't need this" / wrong product-market match.
   - **Priority** — "not now" / other things ahead of this.
   - **Budget** — cost/value pushback.
   - **Trust** — skepticism about the sender, claims, or category.
   - The taxonomy is a sorting aid, not a predictor. Do **not** attach frequency
     percentages to these categories — there is no source this skill can stand behind
     for how often each type occurs. Classify what's in front of you and say nothing
     about how common it is.

3. **Pick a response structure:**
   - **LAER (Listen-Acknowledge-Explore-Respond)** — default for charged or
     Trust/Fit objections; acknowledge before you pivot.
   - **Feel-Felt-Found** — good for Budget/Priority objections where a peer example
     helps ("I understand how you feel, other [role]s felt the same, here's what
     they found").
   - For Interested replies, skip LAER/FFF and draft a direct, low-friction next step
     instead (don't over-engineer an easy win).

4. **Draft the next message** — short, matched to the classification, one clear next
   step, never argumentative. Remind the user: persistence matters (most sales need
   multiple "no"s before a yes) but this does not license ignoring a genuine "not
   interested, please stop" — treat an explicit opt-out request as final, not as an
   objection to overcome.

## Output template

```
REPLY TRIAGE

Original reply (as provided):
"<pasted text>"

Classification: <Interested | Objection: Fit/Priority/Budget/Trust | Not-now>
(Do not attach a frequency percentage to the classification — no supportable
source for objection-type frequency.)

Response structure used: <LAER | Feel-Felt-Found | Direct next-step>

Drafted reply:
"<drafted message>"

Rationale (1-2 lines): <why this structure/classification fits>

Escalation note: <if the reply is an explicit opt-out/stop request, flag it here as
final — do not draft a persistence follow-up>

---
Compliance guardrail (include in every output):
- CAN-SPAM (US): any opt-out or "stop contacting me" request must be honored within
  24-48h and treated as final, not as an objection to work through.
- GDPR (EU/UK): a reply revoking consent/interest ends the legitimate-interest basis
  for further contact — stop outreach to that contact.
- France: if the reply is from a French contact reachable under B2C rules, explicit
  consent is already required for email under CNIL/GDPR practice — not a rule
  starting in August 2026. The Aug 11 2026 law covers *telephone* prospecting.
  Check current rules before further contact.
- Not legal advice.
```

## Sourcing and its limits

- **Fit / Priority / Budget / Trust taxonomy** — used as a classification lens only. No
  frequency percentages are attached to it, deliberately. See the README section
  "About the numbers in this skill" for why the ones that used to be here were removed.
- **LAER, CRAC, Feel-Felt-Found, Boomerang** response structures — established,
  widely-used conventions, presented here unsourced rather than attributed to a
  specific 2026 article. Checked directly: that article names none of these four; it
  presents its own five-step framework instead. Framework names are low-stakes, so
  dropping the wrong citation is the fix rather than hunting for a replacement.
- **Persistence:** no figure quoted. The commonly-cited dropout statistics did not survive
  a check against the page they're attributed to.
- **Known gap:** there is no published conversion benchmark by triage category. Any
  confident "interested → demo" rate you encounter is unsourced until proven otherwise.

Live-tested on Claude Sonnet 5, 2026-07-19. See `EXAMPLE.md` for the run.
