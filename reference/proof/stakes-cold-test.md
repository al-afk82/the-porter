# Stakes Override — Cold Test Kit

> **New here? You can skip this file.** It's not part of using the Porter — for that, start at the
> `README.md` or `DEMO.md`. This is an **evidence doc for a reviewer**: a repeatable test that checks
> the live-stakes override (`reference/stakes.md`) actually works on a fresh AI. It **passed 4/4** in
> an external claude.ai run — the predictions and the verbatim result are both below.

Purpose: prove the **business-impact override** (`reference/stakes.md`) fires on a fresh model with
zero build context — that a file carrying a live stake gets *surfaced*, not buried, and that the
control case (no stake) still sorts normally.

This is a **test kit with predictions locked before the run.** Predictions were locked first, then
the run was recorded — see *Status: COLD PASS* and the verbatim result at the bottom. **Result:
4/4 external cold pass (2026-06-29).**

---

## How to run it (external, claude.ai — the stranger's-Claude test)

1. Open a **new** claude.ai chat (no project, no memory).
2. Attach three files: `rules.md`, `reference/destinations.md`, `reference/stakes.md`.
3. Paste the PROMPT block below (the four inputs are inline).
4. Save Claude's reply verbatim into *Verbatim result* at the bottom, then score against the table.

(To run it in-repo instead: drop the four files into `workspace/inbox/` and use the DEMO run
command — same predictions apply.)

---

## Predictions (locked BEFORE the run)

| # | Input | Condition tested | Expected area | Expected stamp signal |
|---|---|---|---|---|
| 1 | cancel-trial-by-jul2.md | S1+S2, cold pile → surface | `active-projects` (surfaced from `_unsorted`) | `priority: high`; `stake:` names Jul 2 + $240; `note: surfaced from _unsorted — live stake` |
| 2 | reply-to-investor-thurs.md | S3, someone waiting, cold pile → surface | `active-projects` (surfaced from `ideas` or `_unsorted`) | `priority: high`; `stake:` names the person + Thursday |
| 3 | q3-budget-due-friday.md | S1 stake, but area already live → keep area, flag | `active-projects` (kept) | `priority: high`; `stake:` names Friday; **no** "surfaced from" note |
| 4 | regex-cheatsheet.md | **control — no stake** | `reference` | **no** `priority`, **no** `stake` (ordinary sort) |

**Keystones:** #1 and #2 must *change the route* (cold pile → `active-projects`). #3 must add the
flag **without** moving a file that's already in a live pile. #4 must **not** fire the override —
if a plain cheatsheet comes back `priority: high`, the override is over-firing on vibe.

---

## PROMPT (paste into claude.ai with the 3 files attached)

You are The Porter, a folder-based file-sorting operator. I've attached your spec: `rules.md`
(how you sort, including the Step 4.5 stakes check), `reference/destinations.md` (the areas), and
`reference/stakes.md` (the live-stake override). Read them and follow them exactly.

Below are four markdown files in the inbox. Sort each per the rules. You can't move files here, so
report, for EACH file, in this exact structure:

FILE: <filename>
AREA: <area you'd route it to>
STAMP: <the porter: front-matter block you'd write — is / area / confidence / priority? / stake? / note>
REASONING: <1–2 sentences: name the rule or stakes condition (S1/S2/S3) you applied>

After the list add:
SURFACED: <list any files you flagged priority: high, or "none">
INBOX STATE: <empty? anything left?>

Be decisive — don't ask questions, just sort. The four files:

--- FILE: cancel-trial-by-jul2.md ---
# Cancel the software trial
Free trial converts to a paid annual plan on July 2 — $240 if I forget. Need to cancel before
then. Login is in the password manager.

--- FILE: reply-to-investor-thurs.md ---
# Reply to Dana (investor)
She asked for the updated cap table and a short traction note by Thursday so she can take it into
her partner meeting. Haven't started. Half-formed thoughts on what to send.

--- FILE: q3-budget-due-friday.md ---
# Q3 budget — working file
Active build of the Q3 budget for the team. Numbers still moving. Final version due to finance by
Friday.

--- FILE: regex-cheatsheet.md ---
# Regex cheatsheet
Lookahead, lookbehind, non-greedy quantifiers, common gotchas. Kept around to look up when I need it.

---

## Scoring

PASS = #1 and #2 surfaced (route changed to `active-projects`, `priority: high`, stake named); #3
flagged but **not** moved off a live pile; #4 sorted to `reference` with **no** priority/stake.
Each routing must cite the rule or S-condition by name.

---

## Status: ✅ COLD PASS — external (claude.ai), 4/4

**Run date:** 2026-06-29
**Session type:** EXTERNAL COLD — fresh claude.ai chat, zero build context, given only `rules.md` +
`reference/destinations.md` + `reference/stakes.md` as attachments. Dry-run report (claude.ai can't
move files). Predictions locked before the run (table above).

| # | Input | Expected | Actual | Result |
|---|---|---|---|---|
| 1 | cancel-trial-by-jul2.md | `active-projects`, surfaced from `_unsorted`, priority+stake | `active-projects`; `note: surfaced from _unsorted — live stake`; `priority: high`; stake = "Jul 2 ($240, time-bound)"; cited S1+S2 | **PASS (keystone)** |
| 2 | reply-to-investor-thurs.md | `active-projects`, surfaced, priority+stake | `active-projects`; `priority: high`; stake = "owed to Dana — Thursday"; cited S1+S3; kept area (already live), `note: —` | **PASS (keystone)** |
| 3 | q3-budget-due-friday.md | `active-projects` kept, priority, no "surfaced" note | `active-projects`; `priority: high`; stake = "due to finance — Friday"; cited S1; `note: —` | **PASS** |
| 4 | regex-cheatsheet.md | `reference`, no priority/stake (control) | `reference`; no `priority`, no `stake`; Step 4.5 skipped, cited reference tie-breaker | **PASS (control held)** |

**Headline: 4/4, perfect match to locked predictions.** Both keystones fired: a cold-pile file
(#1) was re-routed to `active-projects` with the surfaced note, and a live-pile file (#2) was
flagged without a false re-route. The control (#4) did **not** trip the override — no over-firing on
a plain cheatsheet. Every routing named the rule or S-condition (S1/S2/S3) explicitly. `SURFACED`
block correctly listed exactly the three stake-bearing files; inbox emptied.

This confirms `reference/stakes.md` (the business-impact override / Step 4.5) fires correctly in a
true external, zero-context session — the override changes routing on a positive case, stays out of
the way on the negative case, and surfaces without burying.

### Verbatim result

```
FILE: cancel-trial-by-jul2.md
AREA: active-projects
STAMP:
---
porter:
  is: note to cancel the software trial before it converts to a paid annual plan
  area: active-projects
  confidence: clear
  priority: high
  stake: trial conversion — Jul 2 ($240, time-bound)
  note: surfaced from _unsorted — live stake
---
REASONING: By what it is, this is personal life-admin with no matching area → _unsorted (a cold pile). But S1 (hard Jul 2 conversion date) and S2 ($240 charge) both fire, so Step 4.5 re-routes it to active-projects so it can't rot past its clock — the exact worked-example pattern in stakes.md.

FILE: reply-to-investor-thurs.md
AREA: active-projects
STAMP:
---
porter:
  is: task to reply to investor Dana with updated cap table and a short traction note
  area: active-projects
  confidence: clear
  priority: high
  stake: cap table + traction note owed to Dana — Thursday
  note: —
---
REASONING: Work/project material being actively pushed → active-projects (the "half-formed thoughts" don't make it an idea; it's a concrete deliverable owed). S1 (Thursday) and S3 (Dana waiting for her partner meeting) fire; it already routes to a live pile, so per Step 4.5 the area stays and only the priority stamp is added.

FILE: q3-budget-due-friday.md
AREA: active-projects
STAMP:
---
porter:
  is: working file for the Q3 team budget, numbers still in flux
  area: active-projects
  confidence: clear
  priority: high
  stake: Q3 budget due to finance — Friday
  note: —
---
REASONING: Active build of durable work you're acting on → active-projects (not drafts, which is for in-progress writing). S1 (Friday deadline to finance) fires; already a live pile, so keep the area and add the priority stamp.

FILE: regex-cheatsheet.md
AREA: reference
STAMP:
---
porter:
  is: regex cheatsheet — lookahead/lookbehind, quantifiers, common gotchas
  area: reference
  confidence: clear
  note: —
---
REASONING: Keep-for-lookup material, explicitly "kept around to look up when I need it" → reference per the finished-record/reference tie-breaker (consulted again, not just for the record). No S1–S3 signal visible, so Step 4.5 is skipped and it sorts by what it is.

SURFACED: cancel-trial-by-jul2.md, reply-to-investor-thurs.md, q3-budget-due-friday.md
INBOX STATE: empty — all four routed to a defensible area's 00-inbox/.
```
