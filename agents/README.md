# agents/ — the judges

Each folder here is one judge, a lens the reasoning layer reads content through. A judge is a
folder, not a process. See `REASON.md` at the repo root for how they are used and why there is no
coordinator.

## The shape of a judge

Every judge folder is the same three parts, so once you read one you can read them all.

`ABOUT.md` is what the judge is, in one read. `CONTRACT.md` is the exact verdict it returns.
`reference/` holds the standard it judges against, as plain markdown you edit to change its behaviour.

## The judges in this slice

`constraints` checks the hard rules that must never break. `antipatterns` matches known mistakes.
`voice` checks writing against how you actually write. `quality` checks whether the output is good
enough. `identity` checks that anything speaking as you stays on who you are.

## The verdict

Every judge returns the same five fields, defined in `reference/verdict-schema.json`, `agent`,
`status`, `rule`, `excerpt`, `severity`. A flag always carries the exact excerpt it fired on.
Evidence, not a score.

## Imported from Keel

These standards came from the Keel drift system, where they ran as live agents behind a coordinator.
Here they are folders only. Where an `ABOUT.md` or `CONTRACT.md` still mentions "the coordinator,"
read it as the harness in `REASON.md`.
