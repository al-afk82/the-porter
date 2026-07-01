# Online Test Kit — The Porter (claude.ai run)

> **New here? You can skip this file.** It's not part of using the Porter — for that, start at the
> `README.md` or `DEMO.md`. This is an **evidence doc for a reviewer**: the exact prompt and inputs
> used to run the Porter in a clean claude.ai chat, so anyone can reproduce the "could a stranger
> use it?" test.

Purpose: prove a stranger can run The Porter in a clean Claude.ai chat with zero build
context — the real "could a stranger use it?" test. This is a **dry-run report** (Claude.ai
can't move files), so it outputs the routing + stamp + reasoning per file instead of moving.

## How to run it
1. Open a **new** chat at claude.ai (no project context, fresh).
2. **Attach two files** from this folder: `rules.md` and `reference/destinations.md`.
3. Paste the PROMPT block below (it contains the 3 test inputs inline).
4. Save Claude's reply into "Verbatim result" at the bottom, then score against the
   predictions table.

## Predictions (locked BEFORE the run)
| # | Input | Path tested | Expected area | Expected stamp note |
|---|---|---|---|---|
| 1 | oncall-log-2026-06-19.md | G1 logs patch (online) | logs | — |
| 2 | tax-prep-checklist.md | G4 personal patch (online) | _unsorted | propose new area "personal" |
| 3 | incident-postmortem-2026-06-18.md | G2 record-vs-reference tie-breaker | reference | (consulted-again; touches archive) |

PASS = each file lands in a defensible area, stamps are well-formed, and the heap "empties."
Keystones: #1 must NOT go to active-projects; #2 must park+propose (not absorb); #3 should
prefer reference over archive (kept to consult before the next incident).

---

## PROMPT (paste this into claude.ai, with rules.md + destinations.md attached)

You are The Porter, a folder-based file-sorting operator. I've attached your two spec files:
`rules.md` (how you sort) and `destinations.md` (the areas you can route to). Read them and
follow them exactly.

Below are three markdown files sitting in the inbox. Sort each one per rules.md. You can't move
files here, so instead report, for EACH file, in this exact structure:

FILE: <filename>
AREA: <area you'd route it to>
STAMP: <the `porter:` front-matter block you'd write, per rules.md (is / area / confidence / note)>
REASONING: <1-2 sentences: why that area, naming the rule/tie-breaker you applied>

After the list, add:
INBOX STATE: <would it be empty? anything left?>
NEW AREAS PROPOSED: <any new areas you proposed + their one-line "what belongs here", or "none">

Be decisive — don't ask questions, just sort. Here are the three files:

--- FILE: oncall-log-2026-06-19.md ---
# On-Call Log — 2026-06-19

Shift: Fri 18:00 - Sat 06:00. Quiet-ish night.

- 19:42 — pager: elevated 5xx on checkout. Auto-recovered in 4 min, no action needed. Noted.
- 23:10 — disk warning on db-replica-2, cleared old WAL segments, back to normal.
- 02:30 — false alarm, flapping healthcheck on worker-7. Acked, no fix.
- 05:50 — handed off to Dev, nothing open.

Carryover: file a ticket for the worker-7 healthcheck flap (low priority).

--- FILE: tax-prep-checklist.md ---
# Tax Prep Checklist

Stuff to gather before the accountant appointment.

- [ ] W-2 from employer
- [ ] 1099s (the brokerage one is usually late)
- [ ] mortgage interest statement
- [ ] charitable donation receipts
- [ ] last year's return for reference
- [ ] HSA contribution summary

Appointment is in a few weeks — don't leave this to the last day again.

--- FILE: incident-postmortem-2026-06-18.md ---
# Postmortem — Checkout Outage, 2026-06-18

Status: RESOLVED. Writing this up so we don't repeat it next quarter.

## What happened
Checkout was down for 22 minutes after a bad config push removed a required env var.

## Root cause
No validation on the config pipeline; the missing var only failed at request time.

## What we're keeping for next time
- Add a config schema check in CI (ticket filed).
- The rollback took too long because nobody knew the runbook — link it in the on-call doc.
- Re-read this before the next big config change.

---

## Verbatim result (claude.ai, fresh chat, rules.md + destinations.md attached, 2026-06-27)

> Note: this run predates the 2026-06-27 stamp change — its stamps use the old top-of-file
> `[is:][area:][note:]` line, since superseded by the `porter:` front-matter block (+ a
> `confidence` field). The routing decisions and tie-breakers it proves are unaffected.

FILE: oncall-log-2026-06-19.md
AREA: logs
STAMP: [is: on-call shift log for 2026-06-19, mostly quiet] [area: logs] [note: —]
REASONING: It's a dated, time-stamped record of a single shift — exactly the log vs.
active-projects tie-breaker: it reads as active work but is kept as a record of a moment, so
it routes to logs, not active-projects. The carryover ticket doesn't change its nature.

FILE: tax-prep-checklist.md
AREA: _unsorted
STAMP: [is: tax-prep document checklist for an accountant appointment] [area: _unsorted] [note: proposed-new-area: personal]
REASONING: Actionable "now" work, but personal life-admin, not work/project — and
active-projects is explicitly scoped to work/project only. Per Step 3 and the destinations
scoping note, parked in _unsorted and proposed a personal area rather than forcing it.

FILE: incident-postmortem-2026-06-18.md
AREA: reference
STAMP: [is: resolved postmortem of the checkout config-push outage] [area: reference] [note: —]
REASONING: Finished item, so it hits the finished-record vs. reference tie-breaker — and it's
explicitly written to be reread ("so we don't repeat it next quarter," "Re-read this before
the next big config change"), the consulted-again test for reference over archive.

INBOX STATE: Empty — all three routed, nothing left, nothing discarded.
NEW AREAS PROPOSED: personal — personal life-admin (taxes, errands, home, appointments,
health) that you act on but that isn't tied to a work project.

## Score
**3/3 — perfect match to locked predictions.** All three NEW patches fired correctly in a
clean, zero-context claude.ai session and each was justified by the correct tie-breaker named
explicitly:
- #1 → logs (G1 transient-log tie-breaker) — did NOT default to active-projects.
- #2 → _unsorted + proposed `personal` (G4 work/project scoping) — parked, did NOT absorb.
- #3 → reference (G2 consulted-again over archive) — correct tie resolution.
The propose→promote loop produced a clean `personal` definition. No misses, no stalls, heap
empty. This is an external Cat-11 PASS — strangers' Claude, no build context, runs the spec
as written.
