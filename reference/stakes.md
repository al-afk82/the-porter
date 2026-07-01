# Stakes — the business-impact override (you edit the conditions)

The Porter normally routes a file by **what it is**. This file is the one deliberate exception:
a narrow, named override that changes routing when a file carries a **live external stake** — an
observable real-world consequence with a *clock, a cost, or a person* attached.

The point is **not** to judge what *matters to you* — that's yours. It's to make sure a file with
a **deadline on it can't die in a cold pile** — the "tidy graveyard" failure this system openly
owns (see `identity.md` → *The known risk*). Stakes don't change *what* you do with a file; they
change *whether it stays visible long enough for you to do it.*

---

## When the override fires (observable conditions only)

It fires only when one of these is visible on a fast read — never on vibe, importance, or what the
file is "about":

| # | Condition (observable) | Signals that trip it |
|---|---|---|
| S1 | **Live deadline / time-bound obligation** in the near future | "due", "by Friday", a dated filing, an RSVP, an event date, an expiring window |
| S2 | **Money / legal / compliance consequence** | taxes, an invoice owed, a contract, a payment, a regulatory or legal matter |
| S3 | **Someone else is waiting** — a commitment to a person | "they need this by", a reply owed, a promised deliverable, a blocked teammate |

If none is visibly present, the override does **not** fire — sort normally by what the file is.

---

## What firing changes (this is a routing change, not a label)

When any condition fires:

1. **Stamp `priority: high`** and name the stake: `stake: <what + when>`.
2. **Surface it in the run summary** under a `⚠ Surfaced — live stakes, don't let these sit`
   block, listed before the ordinary one-line-per-file summary.
3. **If the by-what-it-is area is a *cold pile* (`archive`, `ideas`, `_unsorted`) — re-route to
   `active-projects/00-inbox/` instead**, stamped `note: surfaced from <area> — live stake`. A file
   with a clock on it may not rest in a pile you rarely open.
   *If the file already routes to a live pile (`active-projects`, `drafts`, `logs`), keep that area
   — just add the priority stamp and surface it.*

**Worked example.** `cancel-insurance-by-jun30.md` reads as life-admin with no matching area →
by-what-it-is that's `_unsorted` (propose `personal`). But S1 fires (a hard cancellation date), and
`_unsorted` is a cold pile — so it is surfaced to `active-projects/00-inbox/`:

```yaml
---
porter:
  is: note to cancel the insurance policy before the Jun 30 renewal
  area: active-projects
  confidence: clear
  priority: high
  stake: cancellation deadline — Jun 30 (money + time-bound)
  note: surfaced from _unsorted — live stake
---
```

---

## What the override does NOT do

- It does **not** decide what you should *do* with the file (act / keep / toss) — still yours.
- It does **not** fire on importance-by-vibe — only the observable S1–S3 signals trip it.
- It does **not** escalate beyond surfacing — there is no "urgent" tier, no notification, no action
  taken on your behalf. It moves the file to a pile you'll see and flags it. That's the whole move.

---

## Why this is the right override for a *sorter*

A pure "keep everything, clean later" sorter has exactly one real failure mode: *later* never comes,
and a clock-bearing file rots in a pile past its deadline. This override is the precise mitigation —
the **only** stakes-based exception, kept observable and narrow on purpose so it *strengthens* the
sort instead of turning the Porter into a decider. Sorting is still not deciding. The Porter just
refuses to let the things with a clock on them get buried.
