# Pattern Threshold

A pattern qualifies for a new rule proposal when:

1. The same rule ID has fired 3 or more times
2. All 3 instances have response set to "accepted"
3. The excerpts share a recognisable common pattern

If response is "overridden" on any instance — the rule fired incorrectly. Do not propose. Flag the existing rule for review instead.

If response is null — the user did not respond. Do not count toward the threshold.
