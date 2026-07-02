# Reason — the Porter's reasoning layer

> The Porter sorts. This layer reasons. It reads a piece of content and judges it against
> the standards held in `agents/`, then returns a verdict. There is no coordinator. Routing is
> a step you read, not a service you run. Plain folders, plain prompts, direct model calls.

This is the Porter grown up. The sort puts each file in the right area. This layer answers the
next question: given the standards you care about, does this content hold, and where does it fail.

---

## Folders over agents

Each judge lives in `agents/<name>/` as a folder, not as a running process. A judge is three
things on disk. `ABOUT.md` says what it is. `CONTRACT.md` says the exact verdict it returns.
`reference/` holds the standard it judges against, as plain markdown you can read and edit. Change
the standard by changing the folder. Nothing is buried in code.

The five judges in this slice are `constraints`, `antipatterns`, `voice`, `quality`, and
`identity`. Each one is a lens on the same content.

---

## The five layers

This layer is built on Jake's method, the same five layers the rest of the folder uses.

Identity is `agents/<name>/ABOUT.md`, what each judge is. Routing is the step below, which judges
apply to this input. The stage contract is `agents/<name>/CONTRACT.md` and the shared verdict shape
in `agents/reference/verdict-schema.json`. Reference material is each `agents/<name>/reference/`
folder, the standard itself. Working artifacts are the verdicts this layer writes out.

---

## No coordinator

Keel ran these as live agents held together by a coordinator that fired them and gathered verdicts.
That is the agent and framework layer Jake says to stop building on, and it is where the crash loops
came from. Here there is no coordinator and no live fan out. One harness, meaning one reasoning pass
driven from these files, reads routing, loads the folders that apply, and reasons. Where an imported
`ABOUT.md` or `CONTRACT.md` still says "the coordinator," read that as this harness.

---

## The flow

Give the harness a piece of content, a sorted file, a draft, an exchange, anything.

First, route. Decide which judges apply. Constraints and antipatterns apply to almost anything.
Voice and quality apply to writing meant to be read. Identity applies to anything speaking as you or
for you. Loading a judge that does not fit only adds noise, so pick the lenses that fit the content.

Second, reason. Load the `reference/` folders of the judges that apply and read the content against
them in one pass. For each judge return one verdict in the shape in `agents/reference/verdict-schema.json`,
the five fields `agent`, `status`, `rule`, `excerpt`, `severity`. Return the highest severity hit per
judge, one verdict each. A clean judge returns `status: clean` with the other fields null.

Third, verify. This is the one pass that stays separate. Do not let the reasoning that produced a
finding also bless it. Take each `violation` and check that the rule actually applies to this exact
content before it counts. A constraint about outreach copy does not fire on a technical note.
Relevance must be confirmed. Only verified violations are real. This separation is deliberate, a
single pass judging its own work talks itself into a verdict.

---

## What it writes

A short report, one line per judge, verified violations first, each naming the rule and quoting the
exact excerpt it fired on. Evidence, never a confidence number. The content itself is never edited.
Like the sort, this layer surfaces and records, it does not act for you.

---

## This slice, and what is next

This is the first slice, the five knowledge judges reasoned over in one pass, plus the separate
verify pass. It reuses the standards already on disk, nothing new was written. The judgment agents
that earn an independent view, the alignment check and the gap analysis, are not here yet, and the
loggers and the record are a later layer. Build order lives in the branch, not on main.
