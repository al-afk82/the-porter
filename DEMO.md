# DEMO — run the Porter in 2 minutes

The fastest way to watch the Porter make a real call. Two ways: a **no-install browser preview**,
or the **real move-and-stamp** in Claude Code. Both run the actual rules — nothing is faked.

---

## Option A — browser preview (no install, 30 seconds)

1. Open `the-porter-doc-to-md.html` in any browser.
2. Paste the test note below (or pick a sample chip) and hit **Route it →**.
3. You get the pile, the reasoning, and the `porter:` stamp — offline, nothing uploaded.

This is a deterministic preview of the sort. The live, judgment-based sort runs in Claude
(Option B), which handles the ambiguous calls rules alone can't.

---

## Option B — the real thing (Claude Code, move + stamp)

1. Open this folder in VS Code with Claude Code.
2. Paste this run command:

```
Sort every file in workspace/inbox/ using rules.md, reference/destinations.md, and
reference/stakes.md. For each file: pick the best-fit area by what it is, apply the stakes
check, MOVE it into that area's 00-inbox/, and stamp it in YAML front-matter. Give me a one-line
summary per file, with any live-stake files listed first. Never delete anything.
```

3. The Porter reads each file, moves it to the right pile, stamps *why*, and surfaces anything
   carrying a live deadline. Override any call in one edit — the stamp tells you the reasoning.

---

## Quick Test — paste this, check the result

A single note that proves the part that's hard: the **stakes override**. This note *looks* like
life-admin with no home — a keyword sorter dumps it in a catch-all, where it rots past its date.

**Paste-ready input** (`workspace/inbox/cancel-trial-by-jul2.md`):

```markdown
# Cancel the software trial

Free trial converts to a paid annual plan on July 2 — $240 if I forget.
Need to cancel before then. Login is in the password manager.
```

**Expected decision (written before you run it):**

> **Route →** `active-projects/00-inbox/` — *surfaced from `_unsorted`.*
> By what it is, this is personal life-admin with no matching area → it would park in `_unsorted`
> and propose a `personal` area. But a hard date + a dollar cost trips the stakes override (S1 +
> S2), and `_unsorted` is a cold pile — so it's surfaced to `active-projects` instead, where you'll
> actually see it before July 2.

**Expected stamp:**

```yaml
---
porter:
  is: reminder to cancel the software trial before it auto-converts to a paid plan
  area: active-projects
  confidence: clear
  priority: high
  stake: trial auto-converts July 2 — $240 (time-bound + money)
  note: surfaced from _unsorted — live stake
---
```

### Passing criteria (5)

- [ ] The file **moved** into `active-projects/00-inbox/` (not `_unsorted`, not a catch-all).
- [ ] Stamp has `priority: high` and a `stake:` line naming both the date and the cost.
- [ ] `note:` records it was **surfaced from `_unsorted`** (the override changed the route).
- [ ] The note's *body* is untouched — only front-matter was added.
- [ ] The run summary lists this file **first**, under a surfaced / live-stakes heading.

If all five hold, the override works: the thing with a clock on it didn't get buried.

---

## Proof on file

This DEMO shows one case. The full cold-test evidence — in-repo fresh-agent run **and** an external
claude.ai stranger's-session run, predictions locked before each run, verbatim outputs — is in:

- `reference/proof/cold-test-record.md` — the core sort, COLD PASS (in-repo + external)
- `reference/proof/online-test-kit.md` — the exact claude.ai prompt + inputs, reproducible
- `reference/proof/stakes-cold-test.md` — the stakes-override test kit (predictions locked; run it yourself to confirm)
