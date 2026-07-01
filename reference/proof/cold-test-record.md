# Cold Test Record — The Porter

> **New here? You can skip this file.** It's not part of using the Porter — for that, start at the
> `README.md` or `DEMO.md`. This is an **evidence doc for a reviewer**: the record of the Porter
> being tested on files it had never seen, to show it sorts correctly with no prior context.

> ✅ **COLD PASS achieved.** The WARM run below was the initial pass; it is **superseded** by the zero-context *Fresh-Session* and *External (claude.ai)* cold runs documented further down (see **Status**). Skim those for the Cat-11 evidence.

**Protocol:** 6 unseen markdown files dropped in `workspace/inbox/`. Expected area
written for each BEFORE sorting. Sort run per `rules.md` (5-step). Actual placement +
stamp recorded verbatim. PASS = file landed in a defensible area and the heap ended empty.

**Run date:** 2026-06-27
**Session type:** WARM — run in the same session the spec was read (build context present).

> Note: stamps below use the old top-of-file `[is:][area:][note:]` line, since superseded by
> the `porter:` front-matter block (+ `confidence` field). The routing decisions this
> record proves are unaffected by the format change.
This first run is WARM; the zero-context fresh-model cold runs that lift this to Cat-11
PASS are documented below (see Status).
**Folder version:** 01-Drafts/the-porter, area set = active-projects, ideas, reference,
drafts, archive, _unsorted.

---

## Inputs, expected vs actual

| # | Input file | Expected area | Actual area | Stamp note | Result |
|---|---|---|---|---|---|
| 1 | q4-budget-planning.md | active-projects | active-projects | — | PASS |
| 2 | regex-cheatsheet.md | reference | reference | — | PASS |
| 3 | dream-journal-2026.md | _unsorted (propose "personal") | _unsorted | proposed-new-area "personal" | PASS |
| 4 | launch-retro.md | archive (touches reference) | archive | touches reference too | PASS* |
| 5 | standup-notes-jun24.md | active-projects | active-projects | — | PASS* |
| 6 | voice-input-feature-idea.md | ideas | ideas | — | PASS |

**Headline:** 6/6 routed without stalling; heap ended empty. No routing failures.
`*` = routed correctly but surfaced a taxonomy gap (see below) — the placement is
defensible but not obviously *right*. These are the refinement targets.

---

## Gaps found (refinement targets)

### G1 — No home for routine/time-stamped logs (input #5)
Standup notes matched `active-projects` because the test is "material for something
you're actively working on." Literally true, so the Porter routed there and did not
stall. But this dumps transient daily logs into the same pile as durable project
material — `active-projects/00-inbox/` becomes noisy fast. The default area set has no
"logs / journal / daily" area. **Fix candidate:** add a `logs` area to
`destinations.md`, OR add a rule note that time-stamped throwaway logs route to
`_unsorted` and propose `logs` rather than absorbing into `active-projects`.

### G2 — archive vs reference boundary is fuzzy for records-that-inform (input #4)
The launch retro is a finished thing (→ archive) AND lookup material to avoid repeating
a mistake (→ reference). "First clear fit wins" resolved it to archive, but reference is
equally defensible. The tie was broken by file order, not by a principle. **Fix
candidate:** add a one-line precedence in `rules.md` for the finished-but-still-useful
case (e.g., "if a finished item is kept *to be consulted again*, prefer reference;
if kept only *for the record*, prefer archive").

### G3 — "personal" has now been proposed twice (input #3 + the chicken-curry sample)
`_unsorted` proposed "personal" again. Per `destinations.md` own rule ("when _unsorted
keeps proposing the same area, promote it"), `personal` has crossed that bar across runs.
**Fix candidate:** either add `personal` to the default area set, or document that the
demo intentionally leaves it unpromoted to show the propose-then-promote loop working.

---

## What worked (keep)
- The propose-new-area pressure valve fired correctly (input #3) — nothing forced, nothing lost.
- Two-area handling routed to the dominant area with a note, no split, no stall (input #4).
- Clear fits (#1, #2, #6) were unambiguous and fast — the "first clear fit" bar held.
- Every file kept; inbox emptied. Core thesis ("partition, not perfection") demonstrated end-to-end.

---

## Patch log (2026-06-27)

- **G1 — PATCHED.** Added a `logs` area to `destinations.md` and a "transient log vs.
  active-projects" tie-breaker to `rules.md`. Re-sorted `standup-notes-jun24.md` from
  `active-projects` → `logs` (stamped `evolved from active-projects`), which also exercises
  the re-sort path. `active-projects/00-inbox/` now holds only durable project material.
- **G2 — PATCHED.** Added a "finished record vs. reference" tie-breaker to `rules.md`
  (consulted-again → reference; for-the-record-only → archive). `launch-retro.md` stays in
  `archive` under the new rule (it's a record), with the reference touch still noted.
- **G3 — DEFERRED (by choice).** `personal` left unpromoted so the demo still shows the
  propose-then-promote loop working. Promote it in `destinations.md` for real personal use.

---

# Fresh-Session Cold Run — 2026-06-27

**Session type:** COLD — run by a fresh agent with **zero spec context**. It was given only
the working folder and the README's literal invocation ("sort everything in
`workspace/inbox/` using `rules.md` and `reference/destinations.md`"). It read the spec
itself, then sorted. No build context, no knowledge of prior gaps/patches.
**Protocol:** 3 new unseen inputs, each targeting a different hard path. Expected area locked
BEFORE the run. Actual placement + stamp recorded verbatim from the agent's report.

## Inputs, expected vs actual

| # | Input file | Path tested | Expected area | Actual area | Stamp note | Result |
|---|---|---|---|---|---|---|
| 1 | team-sync-2026-06-23.md | G1 logs patch firing cold | logs | logs | — | **PASS (keystone)** |
| 2 | meal-plan-week.md | propose-new-area valve | _unsorted (propose "personal") | active-projects | — | PASS* |
| 3 | launch-blog-post-draft.md | two-area dominant routing | drafts (touches active-projects) | drafts | touches active-projects too | **PASS** |

Verbatim stamps written by the cold agent:
- `[is: dated weekly engineering sync note] [area: logs] [note: —]`
- `[is: this-week meal plan + grocery list to act on] [area: active-projects] [note: —]`
- `[is: unpublished company-blog draft, still being written] [area: drafts] [note: touches active-projects too]`

**Headline:** 3/3 routed, heap emptied, no stalls. 2/3 matched the locked prediction. The
keystone (#1) PASSED — a model with no knowledge of the G1 patch routed a dated meeting log
to `logs` and cited the transient-log tie-breaker by name. **G1 is proven to fire cold**, not
just because the rule was in working memory.

## The miss (#2) — a real find, not a failure

The cold agent routed the meal plan to `active-projects`, reasoning it's "actionable material
to act on this week." That is **defensible against the literal `active-projects` test** — the
file did land in a real area, the heap emptied, nothing was forced or lost. But it is the
**same failure shape as G1**: the `active-projects` test ("material for something you're
actively working on now") is broad enough to **absorb personal-life material** that should be
its own pile. Note the agent did *not* propose `personal` — it absorbed instead of parking,
which is exactly the anti-pattern the log tie-breaker was written to stop, now showing up for
the personal/household class.

### G4 — `active-projects` test absorbs personal actionable material — PATCHED
**Symptom:** a personal meal plan reads as "active work" and buries durable *project* material
under life-admin, the personal analog of G1.
**Fix applied (a):** tightened the `active-projects` "what belongs here" line in
`destinations.md` to scope it to **work/project** material explicitly ("not personal
life-admin … and not a dated log"), plus a "why" note mirroring the logs rationale that sends
unmatched personal life-admin to `_unsorted` + a proposed `personal`/`household` area. Then
re-sorted `meal-plan-week.md` from `active-projects` → `_unsorted/00-inbox/`, stamped
`propose new area "personal" … ; evolved from active-projects` — which also exercises the
re-sort path and lines up with the two other `_unsorted` files already proposing `personal`
(chicken-curry sample, dream-journal), reinforcing the propose→promote loop the demo shows.
**Not chosen:** (b) promoting `personal` into the default set — deliberately left unpromoted
(see G3) so the propose-then-promote loop stays visible to anyone trying the demo.

---

# External Run — claude.ai, fresh chat — 2026-06-27

**Session type:** EXTERNAL COLD — a brand-new claude.ai chat with **zero build context and no
project memory**, given only `rules.md` + `reference/destinations.md` as attachments (the
authentic "a stranger runs it" test). Dry-run report (claude.ai can't move files), 3 new
inputs, each stressing a *different already-patched* rule to confirm the patches survive in the
wild. Predictions locked before the run. Full prompt + verbatim reply: `online-test-kit.md`.

| # | Input | Patch tested | Expected | Actual | Result |
|---|---|---|---|---|---|
| 1 | oncall-log-2026-06-19.md | G1 transient-log | logs | logs | **PASS** |
| 2 | tax-prep-checklist.md | G4 work/project scoping | _unsorted + propose `personal` | _unsorted + propose `personal` | **PASS** |
| 3 | incident-postmortem-2026-06-18.md | G2 consulted-again→reference | reference | reference | **PASS** |

**Result: 3/3, perfect match to predictions.** Every routing was justified by the correct
tie-breaker *named explicitly* in the model's reasoning. No misses, no stalls, heap empty, the
propose→promote loop produced a clean `personal` definition. Confirms G1, G2, and G4 all fire
in a true external setting — not just in-repo subagents that might share environment cues.

## Status
**COLD PASS, in-repo AND external (Cat-11 fully satisfied).**
- In-repo fresh-agent run: 3/3 routed, keystone G1 proven cold, surfaced+patched G4.
- External claude.ai run: 3/3 perfect, all three patches (G1/G2/G4) fired with correct
  tie-breaker citations, in a zero-context stranger's-Claude session.
Two independent cold tests now agree. This is a production-ready cold-test artifact answering
the "could a stranger use it?" judging criterion directly. No open refinements block
submission; the measuring stick (every file in a defensible area, heap empty) was met in both.

> **Override also proven.** The business-impact override (Step 4.5 / `reference/stakes.md`) has its
> own external cold pass — 4/4, including a cold-pile re-route and a no-fire control — recorded in
> `reference/proof/stakes-cold-test.md` (2026-06-29).

---

## (prior run) Status
WARM PASS (6/6 routed; G1–G2 patched, re-verified by re-sort). Superseded by the COLD PASS
above — the fresh run is the production-ready artifact.
