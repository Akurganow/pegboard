# Examples: calibration corpus

One before and after pair per rule. When you report a finding, name the closest pair. The "before" specimens quote bad patterns, which the core rules exempt.

## Review comment

Before: "I think it might perhaps be slightly better if we didn't perform this database query inside the loop because it could lead to some performance degradation."

After: `issue (blocking):` This query runs inside the loop and issues one query per row on a 10k-row page. Fetch the IDs first and query once with `WHERE id IN (...)`.

## Change description

Before: "In this PR, we have spent significant effort revamping the authentication module."

After, in the template's own fields. **Summary:** Replaces the custom OAuth handler with the provider adapter, because the handler deadlocked the refresh timer (#1421). **Test plan:** `npm test auth/` passes.

Session narrative. Before: "Verification: an independent agent reviewed the change and returned PASS." After: "Verification: `npm test auth/` passes."

## Error message

For a developer. Before: "Oops! Something went wrong while attempting to establish a connection." After: "Connection to Postgres failed: authentication rejected for user `app`. Verify `DB_PASSWORD` in `.env` and retry."

For an end user. Before: "Error E-4012: token validation failed." After: "We could not sign you in because the sign-in link has expired. Request a new link."

## Code comments

Before: `// This function handles the validation of the user payload.` and `// should work for most cases`. After: delete both, and add the missing case to the test.

## Sentences

Too short. Before: "Certificate expired. Gateway rejected calls. Error rate up." After: "The gateway rejected calls because its TLS certificate expired, and the error rate rose."

Noun stack. Before: "the service cluster event bus message priority handler". After: "the handler that sets event priority on the service cluster's event bus".

## Progress update, final report, brief, unverified claim

Progress. Before: "Still working on this! Looked at a bunch of stuff in the billing module." After: "The refund step fails for the one sample account with a partial refund, so I am reading the refund handler next."

Final report. Before: "First I looked at the queue and the worker logs. The memory thing turned out to matter." After: "Nightly imports failed because the importer ran out of memory: it needs 2 GB and the container limit was 1.5 GB. Raising the limit to 4 GB on the test cluster let a full import finish. You decide by Friday whether to change the live limit. The change has not run on the live cluster."

Brief. Before: "Look into why test_ledger_close is flaky and fix it." After: "Find the cause of the failure of `test_ledger_close` in billing-core. We ruled out the database fixtures. Do not change production code. You are done when you can state the cause and give a command that makes the test fail."

Unverified. Before: "This should work now." After: "`cargo test -p ledger` passes. I did not run it against the live database."

## Shortening that keeps every fact

Before: "Hi team, a heads-up on the search outage: at about 09:20 UTC alerts fired for slow queries, and we found that a full disk on the index node caused them. We freed the space, and as of 09:41 UTC latency is normal. Thanks for hanging in there!"

After: "A full disk on the index node slowed search queries, which alerts flagged at about 09:20 UTC. We freed the space, and latency has been normal since 09:41 UTC."

Cuts: "Hi team", "a heads-up on the search outage:", "we found that", "Thanks for hanging in there!". Dropping a fact, as in "Search is fixed.", is a `major` finding.
