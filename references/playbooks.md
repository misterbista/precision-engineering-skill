# Task playbooks (load only relevant section)

Use the relevant section to choose checks that can expose a task-specific failure.

## Bug fix
1. Reproduce the observable failure or capture trustworthy incident evidence.
2. Trace from symptom to first incorrect state transition; test hypotheses, don't guess.
3. Where practical, show the regression test fails on the original behavior and passes after the fix. An import, setup or unrelated assertion failure does not establish a regression test.
4. Repair at the owning boundary within scope; if the producer cannot be changed, handle the failure at the nearest owned boundary and disclose the limitation. Inspect sibling paths sharing the faulty rule, not unrelated opportunities for cleanup.
5. Run targeted and adjacent regression tests; confirm the original reproduction is fixed and a nearby valid case still works. Check test selection and skipped-test output.

Before a reproduction or check can mutate external state, verify its effective target and isolation; a disposable checkout can still inherit live credentials, service endpoints or shared fixtures. Use a safe target within authorization, or report the blocked check.

## New feature
1. Define user-visible outcome and negative/edge cases.
2. Locate similar feature, route, API and tests; reuse established patterns.
3. Trace UI → API → validation/authorization → persistence → events/side effects as relevant.
4. Implement one working vertical slice; avoid broad scaffolding.
5. Verify acceptance end-to-end and failures, not merely compilation.

## UI

- Inspect consumers of the shared component for behavior, accessible states, and styling conventions. Read the component API for the resolved version. An old call site can document usage while relying on a deprecated property.
- Exercise the requested interaction and verify that existing consumers still render and behave as expected. Verify keyboard interaction and accessible labeling when the change affects them.

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
1. Choose the metric that represents the problem. Capture a repeatable workload and enough baseline runs to see variability. Include latency distribution, throughput, allocations, responsiveness, or resource use as relevant.
2. Locate the bottleneck with measurements. Check whether an algorithm, query, data layout, or I/O change addresses it directly. If caching fits the measured workload, account for invalidation, consistency, and memory limits.
3. Control meaningful variables for before-and-after runs and check behavior under the same conditions. Measure costs that may have moved, such as memory or the first uncached request.
4. Report the workload, environment, observed change, and tradeoffs. Treat changes within run-to-run noise as inconclusive and keep production claims within the measured scope.

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
