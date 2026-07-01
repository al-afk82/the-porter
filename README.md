# The Porter

[Live Webpage](the-porter.html)

A folder-based operator that reads a heap of markdown files and drops each one into the **`00-inbox/` of the right area** — fast. It turns one paralyzing mountain of files into a handful of labeled, climbable piles. It **keeps everything**; the piles are folders.

Its job is **partition, not perfection.** The output isn't a clean desk — it's an *organized mess:* each file staged in the right area's inbox, sorted *enough* that the real cleaning, when you do it, is easy. **Five labeled hills are climbable; one mountain isn't.**

> Problem & full philosophy: `brief.md` · `identity.md`

**In one line of lineage:** it's **PARA's just-in-time organizing, automated by an LLM at the inbox moment, with GTD's mandatory "clarify each item" step deliberately refused.** Not a new theory — a considered variant of well-evidenced ideas (Malone 1983; Whittaker & Hirschberg 2001; Bergman 2013). See `identity.md` → *Declared lineage*.

---

## Try it — three ways

Every option below runs **the Porter's real rules** (`rules.md` + `reference/destinations.md`) — nothing is faked or typed in by hand. The point isn't "will an AI follow instructions" (it always will); it's *does the folder do the work?* So each rung loads the actual files.

### 1. Run it in claude.ai — the real rules, online (start here)

The honest "could a stranger use the folder?" test: Claude reasons from *the actual files*, not from a prompt you typed.

1. **Download the repo** (green **Code → Download ZIP**, then unzip). To test online you need **only two files** from it: `rules.md` and `reference/destinations.md`.
2. **Start a new claude.ai chat and attach just those two files.** That's everything the sort needs — you don't upload the rest of the repo. *(No attach button? Copy the full contents of both files and paste them in — same effect.)*
3. **Paste this, then your note** (or any file from `workspace/inbox/`):

```
You are the Porter. Using ONLY the attached rules.md and destinations.md, sort the
note below.

NOTE TO SORT:

# Onboarding Guide (draft)

First pass at the new-user onboarding doc. Still rough.
- Welcome screen → what the product does in one line (need a better line)
- Step 1: connect your data source (screenshots TODO)
- Step 2: first sort run — show the "before/after" piles
- FAQ section: half-written, come back to this

Goal is to have something shippable by the launch. Not there yet.
```

*(That's a sample note — swap in your own, or any file from `workspace/inbox/`.)*

**You get back the pile, the reasoning, and the stamp.** This note *mentions* a launch
(pulls toward `active-projects`), but what it **is** is a draft in progress — so that's its home:

> **Route →** `drafts/00-inbox/`
> **Reason:** in-progress writing being worked toward launch — a draft, not a project plan or a finished record.
> ```yaml
> porter:
>   is: first-pass draft of the new-user onboarding guide
>   area: drafts
>   confidence: clear
>   note: touches active-projects too (tied to the launch)
> ```

claude.ai can't move files, so this is a **dry-run preview** — Claude decides where each file *would* go. It's the same setup as the cold-test in `reference/proof/`. To actually move and stamp files, use option 2. More worked cases are in `examples.md`.

### 2. Run it for real — move & stamp your files

Needs an AI that can **edit files on your computer** — *Claude Code in VS Code.*

1. **Open this folder** in VS Code with Claude Code.
2. **Set your areas.** Open `reference/destinations.md` — the one file you edit. Point each area at a real folder of yours, *or* leave the example paths to try it on the built-in `workspace/areas/` first. Each area is just a **name + a one-line "what belongs here" + a folder path.**
3. **Drop your markdown files** into `workspace/inbox/`. *(Just trying it? Six sample files are already there — each one a call a keyword sorter would botch. Skip to step 4.)*
4. **Paste this prompt** to Claude:

```
You are the Porter. Sort every file in workspace/inbox/ using rules.md and
reference/destinations.md.
```

It reads each file, moves it to the right pile, and stamps *why* — so you can override any call in a second. It **sorts; it doesn't clean.** Deciding what to *do* with a file happens later, one pile at a time, by you.

### 3. See it instantly — no AI, no download

No claude.ai account handy? **[Open the intake bench in your browser](the-porter-doc-to-md.html)** (or open `the-porter-doc-to-md.html` from the repo locally) — type or paste a note (or pick a sample), and hit **Route it →**. The page runs the Porter's rules and tie-breakers right in the page and shows the pile, the reasoning, and the stamp — a self-contained preview (the live, judgment-based sort still happens in Claude, options 1 and 2).

---

## The structure

```
the-porter/
├── CLAUDE.md                  boot file — who the Porter is + load order (start here if you're Claude)
├── brief.md · identity.md · rules.md · examples.md   the spec
├── DEMO.md                    run it in 2 minutes — paste-ready test + pass criteria
├── the-porter.html           the landing page — problem, point of view, how it sorts, proof
├── the-porter-doc-to-md.html the intake bench — convert docs→md + routing demo (browser, no install)
├── reference/
│   ├── destinations.md        the area map — YOU edit this (area → folder whose 00-inbox receives the file)
│   ├── stakes.md              the one override — surface a file with a live deadline, don't bury it
│   └── proof/                 reviewer evidence — cold-test records (skippable if you're just using it)
└── workspace/
    ├── inbox/                  drop the unsorted heap here
    └── areas/                  destination areas (example set — repoint to your real folders)
        ├── active-projects/00-inbox/
        ├── ideas/00-inbox/
        ├── reference/00-inbox/
        ├── drafts/00-inbox/
        ├── logs/00-inbox/      time-stamped, transient entries (standup/meeting notes, journals)
        ├── archive/00-inbox/
        └── _unsorted/00-inbox/ no clear fit lands here + a new area is proposed
```

---

## The intake bench (companion web tool)

The intake bench ([open it live](the-porter-doc-to-md.html), or `the-porter-doc-to-md.html` from the repo) is a self-contained, browser-only front door — **no install, nothing uploaded.** It does two jobs:

- **Converts docs to markdown.** Drop a `.pdf`, `.docx`, `.xlsx`, `.csv`, `.pptx`, `.html`, or an image (OCR) and get clean `.md` with a metadata header — this is how non-markdown files become Porter-ready input.
- **Shows the sort, live.** Type or paste a note (or pick a sample) and hit **Route it →**: the file converts to `.md`, gets its `porter:` stamp, and lands in the right area's `00-inbox/` in a folder tree, with the reasoning shown. Every converted file also gets its own **Route** button that runs the same sort.

The in-browser router is a **deterministic preview** — it mirrors the Porter's rules and tie-breakers so you can *see* the sort happen offline. The live, judgment-based sort runs in **Claude** (the real engine, which handles the ambiguous cases rules alone can't). The bench is the front door; Claude does the thinking.

> Because most source material isn't markdown yet, the bench doubles as the **intake door
> to an md-based OS**: it makes non-markdown documents Porter-ready, then shows the
> same sort. A convenience at the threshold — not a second product.

> **Open:** [the landing page](the-porter.html) → [the intake bench](the-porter-doc-to-md.html) in any browser.

---

## The five-step sort (and the one override)

1. **Read it fast** — skim what it *is* and what it's *about*. No deep-reading.
2. **Match it to an area** (from `destinations.md`) — first clear fit wins.
3. **No clear fit?** Route to `_unsorted/00-inbox/` and **propose a new area** — never force, never discard.
4. **Touches two areas?** Route to the dominant one, note the other. Don't split.
5. **Move it and stamp it.**

**The one override — live stakes.** Between matching and moving, the Porter checks for a *live stake*: a deadline, a money/legal consequence, or someone waiting on the file. If one fires, the file gets `priority: high` — and if it would land in a cold pile (`archive`/`ideas`/`_unsorted`), it's routed to `active-projects` instead, so the thing with a clock on it can't rot unseen. This is the **one** time stakes override the by-what-it-is sort. *(See `reference/stakes.md`.)*

Stamp written into the file's **YAML front-matter** (merged in, never injected above existing front-matter — the body is never touched):
```yaml
---
porter:
  is: <what the file is>
  area: <area name>
  confidence: <clear | low>
  priority: <high>            # optional — only when a live stake fires (reference/stakes.md)
  stake: <what + when>        # optional — names the stake; present only with priority
  note: <proposed-new-area | touches X too | evolved from Y | surfaced from Z — live stake | —>
---
```

---

## How it decides which area (this is judgment, not bucketing)

The sort *looks* mechanical — five steps — but each file gets a real call a keyword sorter would
get wrong. Three of those calls are where the judgment lives:

**1. It rejects the surface match.** A dated standup note *looks like* active-project work — it's
literally about active work — so a keyword sorter dumps it in `active-projects` and buries your
real projects under daily noise. The Porter refuses the obvious read and routes it to `logs`.
Same move with a meal plan: it *looks* actionable, but it's personal life-admin, so it doesn't
land in `active-projects` either. It reads what a file *is*, not what it superficially resembles.

**2. It refuses to force a fit — and says so.** When nothing fits, a lesser sorter jams the file
into the nearest bucket to avoid looking unsure. The Porter parks it in `_unsorted/` *and
proposes a new area* — a name plus a one-line "what belongs here." "I don't have a home for this
yet" is a first-class, honest output, not a failure.

**3. It commits to one home.** A file that spans two areas doesn't get split, copied, or handed
back with "where should this go?" The Porter routes it to the area it's *most* about, notes the
other, and moves on. It decides.

That's why it's a porter and not a search box: it makes the fast, repetitive judgment call for
you — and shows its reasoning in the stamp, so you can override any call in a second.

## Worked example

**Input** — `workspace/inbox/q3-launch-notes.md`: scattered notes about the Q3 product launch you're actively running.

**Sort:**
- Read fast → it's working notes for an active launch.
- Match → `active-projects` (clear fit).
- Move → `workspace/areas/active-projects/00-inbox/q3-launch-notes.md`, stamped in front-matter:
```yaml
---
porter:
  is: working notes for the Q3 launch
  area: active-projects
  confidence: clear
  note: —
---
```

More cases — a no-fit that proposes a new area, a two-area file, and a file that *evolved* between areas — are in `examples.md`.

---

## What it does NOT do

- ❌ Discard or delete anything — every file lands in some area's inbox.
- ❌ Deep-read, summarize, or rewrite — fast skim only.
- ❌ Decide what to *do* with a file (act/keep/toss) — that's the later, per-area cleaning.
- ❌ Clean the destination inboxes — it fills them; each area cleans its own.

---

## Running it on your own system (and how it's shown here)

The logic is generic; **your specifics live in `reference/destinations.md`.** As shipped, that map points to the **example areas** in `workspace/areas/`, so anyone can drop files in and watch them route — self-contained, no dependency on your folders. To run it on your real OS, repoint each area's path at your actual subfolder; the file then lands in that folder's `00-inbox/`. Wiring to your live folders is a deliberate config step, kept out of scope so the **sorting logic** is the focus.

---

Built by Alec Webb.
