# record/ — the write once log

The judges are interchangeable labour. This is the asset. Every confirmed finding is written here
once and never overwritten, only added to. Over time this becomes the memory that makes the reasoning
sharper, not by retraining, by accumulated context the next run can read.

## The rule

Append only. A finding, once written, is never edited or deleted. The log grows, it does not change.
This is the one place the reasoning layer writes, and it writes only findings the verify pass
confirmed. Clean judges and unverified flags never land here.

## What lands here

Only verified violations, and on an exchange the alignment and gap results worth keeping. A finding
the verify pass rejected as not applying to this content does not get written. The log is a record of
real hits, not of every pass the harness ran.

## The entry

The log is `findings.jsonl`, one JSON object per line, so it only ever grows by appending. Each line
carries the source it came from, the judge, and the evidence.

```json
{
  "source": "path or short id of the content or exchange judged",
  "agent": "constraints | antipatterns | voice | quality | identity | alignment | gap",
  "status": "violation | misaligned | gap-found",
  "rule": "rule ID and name, or null for judgment judges",
  "excerpt": "the exact offending text, quoted not summarised",
  "severity": "high | medium | low, or null",
  "verified": true,
  "timestamp": "ISO 8601 UTC, stamped at the moment of the run"
}
```

`verified` is always true here, an unverified finding does not reach the log. `excerpt` is the exact
words, never a paraphrase, so the record stays evidence rather than opinion. There is no server and no
API, the harness in `REASON.md` appends the line when it runs, plain file, direct write.

## Reading it back

A later run can read the tail of this log as context before it judges, so the system reasons against
its own history and stops flagging what you have already seen and accepted. That read back is the
memory loop, and it is deliberately kept as its own step, not wired in yet.
