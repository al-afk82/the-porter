# Postmortem — Checkout Outage, 2026-06-18

Status: RESOLVED. Writing this up so we don't repeat it next quarter.

## What happened
Checkout was down for 22 minutes after a bad config push removed a required env var.

## Root cause
No validation on the config pipeline; the missing var only failed at request time.

## What we're keeping for next time
- Add a config schema check in CI (ticket filed).
- The rollback took too long because nobody knew the runbook — link it in the on-call doc.
- Re-read this before the next big config change.
