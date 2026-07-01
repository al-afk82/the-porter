# Examples — The Porter

Five worked sorts. Each shows a fast read, the area chosen, and the stamp. The stamp is written into the file's **YAML front-matter** (merged into existing front-matter, never injected above it — the body is never mutated). The Porter keeps every file — the only question is *which area's `00-inbox/`.*

> **New here? Start with Example 0** — it's a copy-paste you can run in any browser chat right now, no install.

---

## Example 0 — Try it in your browser (no setup)

The quickest way to *see* the Porter work. In a **claude.ai** chat, attach two files from this repo — `rules.md` and `reference/destinations.md` — then paste the prompt below. It **previews** the sort *from the real rules*, not a hardcoded list (the actual file move happens in Claude Code — see the README *Run it for real* section). *(No attach button? Paste the full contents of both files first, then the prompt.)*

**Paste this:**

```
You are the Porter. Using ONLY the attached rules.md and destinations.md, sort the
note below. Report the area, the reasoning, and the `porter:` stamp you would write —
fill every field with a real value, and don't rewrite the note.

NOTE TO SORT:

# Onboarding Guide (draft)

First pass at the new-user onboarding doc. Still rough.
- Welcome screen → what the product does in one line (need a better line)
- Step 1: connect your data source (screenshots TODO)
- Step 2: first sort run — show the "before/after" piles
- FAQ section: half-written, come back to this

Goal is to have something shippable by the launch. Not there yet.
```

**What comes back** — a filled-in result card. The note *mentions* a launch (pulls toward `active-projects`), but what it **is** is a draft in progress, so that's the home; the launch is noted as the secondary:

> **Route →** `drafts/00-inbox/`
> **Reason:** it's what the doc *is* (a draft being written), not what it's *for* (the launch).

**Stamp:**
```yaml
---
porter:
  is: first-pass draft of the new-user onboarding guide
  area: drafts
  confidence: clear
  note: touches active-projects too (tied to the launch)
---
```

> **If you see blank fields** (`is:` with nothing after it), the chat echoed the template instead of doing the sort — re-paste and add a line at the end: *"Replace every placeholder with your actual decision."*

To try the trickier calls, swap the note for any file in [`workspace/inbox/`](workspace/inbox/) — `standup-notes-jun24.md` (looks active, is a **log**) or `chicken-curry-recipe.md` (looks actionable, is **personal** → `_unsorted` + a proposed area).

---

## Example 1 — Clear fit → route it

**Input file:** `q3-launch-notes.md` — scattered notes for the Q3 product launch you're actively running.

- **Read fast:** working notes for an active launch.
- **Match:** `active-projects` — a clear fit.
- **Route:** `active-projects/00-inbox/`.

**Stamp:**
```yaml
---
porter:
  is: working notes for the Q3 launch
  area: active-projects
  confidence: clear
  note: —
---
```

---

## Example 2 — No clear fit → park and propose (don't force)

**Input file:** `interview-prep-questions.md` — a list of questions to ask candidates, but you have no "hiring" area defined.

- **Read fast:** hiring/interview material.
- **Match:** nothing in the area set is a clear home. Do **not** jam it into `reference` or `active-projects`.
- **Route:** `_unsorted/00-inbox/`, and **propose a new area.**

**Stamp:**
```yaml
---
porter:
  is: interview questions for candidate screening
  area: _unsorted
  confidence: low
  note: proposed-new-area "hiring" — recruiting/interview material
---
```

*"hiring" is only **proposed** — it isn't a real area, and the Porter won't route to it, until you add it to `destinations.md`. If it keeps getting proposed across runs, that's your signal to accept it and re-run.*

---

## Example 3 — Touches two areas → route to the dominant one

**Input file:** `pricing-rewrite.md` — a draft of a new pricing page that also captures a half-formed idea about usage-based tiers.

- **Read fast:** mostly a piece of writing in progress; secondarily an idea.
- **Match:** it's *most* a draft → `drafts`. Note the idea; don't split the file.
- **Route:** `drafts/00-inbox/`.

**Stamp:**
```yaml
---
porter:
  is: draft of the new pricing page
  area: drafts
  confidence: clear
  note: touches ideas too (usage-based tiers)
---
```

---

## Example 4 — Evolution → re-sort to its new area

**Input file:** `side-tool-concept.md` — last month it was a loose idea in `ideas`; you've now started building it.

- **Read fast (re-run):** no longer a someday-maybe — it's active work.
- **Match:** `active-projects` now fits better than `ideas`.
- **Route:** move from `ideas/00-inbox/` to `active-projects/00-inbox/`.

**Stamp:**
```yaml
---
porter:
  is: build notes for the side tool
  area: active-projects
  confidence: clear
  note: evolved from ideas
---
```

---

## What these show

- **Everything is kept** — even the no-fit file (Example 2) lands somewhere; nothing is discarded.
- **It never forces a bad home** — no-fit → `_unsorted` + a proposed area, not a wrong pile.
- **Speed over precision** — a two-area file goes to its dominant home with a note (Example 3), not a split or a stall.
- **Files are allowed to move** — re-sorting as things evolve is normal (Example 4), not a failure.