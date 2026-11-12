# Task playbooks (load only relevant section)

Use the matching procedure to resolve a task-specific risk; it does not add a second mandatory workflow. Select checks that could reveal a defect in the changed behavior.

## Bug fix
1. Reproduce the observable failure or capture trustworthy incident evidence.
2. Trace from symptom to first incorrect state transition; test hypotheses, don't guess.
3. Where practical, show the regression test fails on the original behavior and passes after the fix. An import, setup or unrelated assertion failure does not establish a regression test.
4. Repair at the owning boundary, not a downstream symptom; review sibling paths.
5. Run targeted and adjacent regression tests; confirm the original reproduction is fixed and a nearby valid case still works. Check test selection and skipped-test output.

## New feature
1. Define user-visible outcome and negative/edge cases.
2. Locate similar feature, route, API and tests; reuse established patterns.
3. Trace UI → API → validation/authorization → persistence → events/side effects as relevant.
4. Implement one working vertical slice; avoid broad scaffolding.
5. Verify acceptance end-to-end and failures, not merely compilation.

## Refactor
1. Identify the requested structural improvement and invariant behavior.
2. Characterize behavior first; separate mechanical moves from semantic changes.
3. Update all callers, preserve external contracts; remove dead code.
4. Compare tests and observable outputs before and after; inspect scope creep.

## Migration
1. Inventory consumers and contracts, compatibility/deployment order, ownership and rollback feasibility.
2. Distinguish preparing a migration from executing it; confirm missing authorization before live data changes or breaking transitions.
3. Match deployment order to actual consumers. Use expand → migrate → contract when old and new versions must coexist; add dual reads/writes only when necessary and specify their removal condition.
4. Validate forward and backward compatibility, partial failures, data verification and retries.
5. Never claim rollback possible if destructive migration makes it impossible.

## Performance
1. Establish baseline and workload, variability, SLO and resources.
2. Profile bottleneck before choosing optimization. Explain algorithmic and operational tradeoffs.
3. Change one variable at a time; test correctness as well as speed.
4. Compare repeatable before/after runs including latency distributions and resource usage.
5. Do not claim an improvement within measurement noise. Revise or remove your unsupported optimization, preserving unrelated work; disclose deliberate tradeoffs.

## Incident / distributed concurrency
1. Capture reproducible timeline, ownership, message IDs and state transitions.
2. Identify at-least-once delivery, idempotency, ordering, race and timeout boundaries.
3. Verify atomic state changes and retry behavior under injected faults.
4. Avoid treating a lock as sufficient unless its scope and process boundaries are proven.
5. Exercise the actual storage/process boundary where relevant; sequential calls and mocked writes do not demonstrate race safety. Prefer controlled interleavings over timing-dependent sleeps.

## Code review only
1. No edits unless separately requested.
2. Read requirements, actual diff, affected callers and tests.
3. Return only actionable findings with severity, path:line, failure scenario and evidence.
4. Separate demonstrated bug from plausible risk or stylistic preference.
5. If no findings, state what was checked and limitations; don't invent issues.
