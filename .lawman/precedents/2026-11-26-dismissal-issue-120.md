---
kind: dismissal
departments:
  - dependencies
issue: 120
date: 2026-11-26
finding: .github/workflows/integration.yml::hermes-agent::unlocks
---

The finding is dismissed.

Issue: https://github.com/Akurganow/pegboard/issues/120

Title of the lead:
~~~
[Lead] dependencies: hermes-agent: the install check stands in for a skills check
~~~

The comment of the decider who closed the lead, written 2026-11-26T21:33:24Z:
~~~
Merged into #119, which now carries this finding and its recheck on `main` at 7fc5e64. Both pins sit in the same install step of `integration.yml` and the same sections of `docs/clients.md`, and both are fixed by moving the pin and replacing the weak check.
~~~
