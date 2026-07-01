# Destinations — the area map (you edit this)

This is the Porter's only configuration: the set of **areas** a file can be routed to, and the **folder path** whose `00-inbox/` receives the file. The sort *logic* (in `rules.md`) never changes; this file is where you point it at *your* world.

Each area has a **name**, a one-line **"what belongs here"** test, and a **path**.

> **What an area's `00-inbox/` is.** The Porter's job ends the moment a file lands there.
> That inbox is the **handoff point into that area's own system** — it's where that area's
> own routing picks the file up. The Porter delivers raw material to the right front door;
> what happens inside the area is that area's job, not the Porter's.

---

## How to use this file

- **For the demo (as shipped):** the paths point to the example areas in `workspace/areas/`, so anyone can run the Porter self-contained.
- **For your real OS:** repoint each `path` to your actual subfolder. The file lands in that folder's `00-inbox/`. Add, rename, or remove areas freely — the Porter sorts into whatever is listed here and proposes new ones when a file fits none.

---

## Areas

> These are **sensible defaults** — common file-system categories most knowledge workers already use. Keep them, rename them, or repoint each `path` to your own folders.

| Area | What belongs here (the test) | Path (its `00-inbox/` receives the file) |
|---|---|---|
| `active-projects` | **Work/project** material you're actively pushing forward now — not personal life-admin (meals, errands, home) and not a dated log | `workspace/areas/active-projects/00-inbox/` |
| `ideas` | Half-formed ideas, someday-maybe, not yet acted on | `workspace/areas/ideas/00-inbox/` |
| `reference` | Keep-for-lookup material; not active, but worth having | `workspace/areas/reference/00-inbox/` |
| `drafts` | In-progress writing — essays, posts, docs being worked | `workspace/areas/drafts/00-inbox/` |
| `logs` | Time-stamped, transient entries — standup/meeting notes, daily logs, journals | `workspace/areas/logs/00-inbox/` |
| `archive` | Finished or superseded; kept for the record | `workspace/areas/archive/00-inbox/` |
| `_unsorted` | **Catch-all.** No clear area fits → file lands here and the Porter proposes a new area. | `workspace/areas/_unsorted/00-inbox/` |

> **Why `logs` is its own area:** without it, time-stamped throwaway entries (a daily
> standup, a meeting note) match `active-projects` on a technicality — they *are* about
> active work — and quietly bury durable project material under transient noise. Keeping
> logs in their own pile is what stops a hill from becoming a mountain again. See the
> log tie-breaker in `rules.md`.
>
> **Why `active-projects` is scoped to *work/project*:** an actionable personal file (a meal
> plan, an errand list) also reads as "something you're working on now," so it gets absorbed
> into `active-projects` and buries the real project work — the same trap as logs. So
> `active-projects` is **work/project** material only. Personal life-admin with no matching
> area should be **parked in `_unsorted` with a proposed `personal`/`household` area**, not
> forced into `active-projects`.

---

## Rules for a good area set

- **Few, distinct piles.** Five clear areas beat fifteen fuzzy ones — the point is climbable hills, not a new mountain of folders.
- **Soft cap ~10 areas.** Past that, the set is sprawling — merge overlapping areas back down rather than keep adding. A heap of thin areas is the original mountain reformed one level up.
- **Each test is a one-liner you can apply in seconds.** If you can't tell in a glance whether a file belongs, the test is too vague.
- **Always keep `_unsorted`.** It is the pressure valve that lets the Porter stay fast and honest — nothing gets forced, nothing gets lost.
- **A proposed area isn't real until you add it here.** The Porter *proposes*; you *ratify*. A proposed area's files sit in `_unsorted/` and the Porter won't route to it until you add it to this file. When `_unsorted` keeps proposing the same area, that's your signal to promote it and re-run.
