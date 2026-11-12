# Task playbooks (load only relevant section)

## Bug fix
1. Reproduce the observable failure or capture trustworthy incident evidence.
2. Trace from symptom to first incorrect state transition; test hypotheses, don't guess.
3. Add a regression test that fails for the right reason, where practical.
4. Repair at the owning boundary, not a downstream symptom; review sibling paths.
5. Run targeted and adjacent regression tests; confirm the original reproduction is fixed.

## New feature
1. Define user-visible outcome and negative/edge cases.
2. Locate similar feature, route, API and tests; reuse established patterns.
3. Trace UI → API → validation/authorization → persistence → events/side effects as relevant.
4. Implement one working vertical slice; avoid broad scaffolding.
5. Verify acceptance end-to-end and failures, not merely compilation.

## Refactor
1. Identify measurable problem and invariant behavior.
2. Characterize behavior first; separate mechanical moves from semantic changes.
3. Update all callers, preserve external contracts; remove dead code.
4. Compare tests and observable outputs before and after; inspect scope creep.

## Migration
1. Inventory consumers and contracts, compatibility/deployment order, ownership and rollback feasibility.
2. Gate before schema/data changes or breaking API transitions.
3. Use expand → migrate/dual-read if justified → contract, rather than destructive one-step deployment.
4. Validate forward and backward compatibility, partial failures, data verification and retries.
5. Never claim rollback possible if destructive migration makes it impossible.

## Performance
1. Establish baseline and workload, variability, SLO and resources.
2. Profile bottleneck before choosing optimization. Explain algorithmic and operational tradeoffs.
3. Change one variable at a time; test correctness as well as speed.
4. Compare repeatable before/after runs including latency distributions and resource usage.
5. Revert/no-ship if improvement is noise or regression elsewhere.

## Incident / distributed concurrency
1. Capture reproducible timeline, ownership, message IDs and state transitions.
2. Identify at-least-once delivery, idempotency, ordering, race and timeout boundaries.
3. Verify atomic state changes and retry behavior under injected faults.
4. Avoid treating a lock as sufficient unless its scope and process boundaries are proven.

## Code review only
1. No edits unless separately requested.
2. Read requirements, actual diff, affected callers and tests.
3. Return only actionable findings with severity, path:line, failure scenario and evidence.
4. Separate demonstrated bug from plausible risk or stylistic preference.
5. If no findings, state what was checked and limitations; don't invent issues.
