# Review and approval contract

## Review priorities
Inspect the affected behavior and its consumers. Use these priorities where applicable; do not audit unrelated subsystems or generate a finding for every category.

1. Wrong behavior vs acceptance, missing negative or edge case.
2. Authorization, tenant isolation, secret handling, injection and insecure defaults.
3. Persistence consistency, transaction boundary, partial writes, retries/idempotency and data loss.
4. Race conditions, cancellation, resource lifecycle and timeouts.
5. Compatibility and dependent callers: API/schema/message/serialization contracts.
6. Reuse accuracy: duplicate methods/components/hooks/services; wrong ownership; unnecessary abstractions.
7. Tests that assert mocks but not observable behavior; inadequate failure coverage.
8. Unrelated edits and style divergence.

## Finding format
`[P0|P1|P2|P3] path:line — issue; concrete trigger; consequence; minimal fix or missing proof`
- P0: immediate security/data-loss or consistently broken critical flow.
- P1: significant production incorrectness or high-likelihood regression.
- P2: bounded defect or material maintainability hazard with demonstrated impact.
- P3: low-impact, concrete defect.
Trace each finding to an affected caller or reachable state. Separate unverified risks and requested suggestions from defects; style preferences are not blockers. No claim of certainty beyond evidence; requests for evidence are not proven defects.

## Authorization boundaries
- Honor existing authorization for the requested scope; high risk alone does not require asking again.
- Resolve consequential ambiguity before dependent work. Prepare authorized patches and verification before asking for approval of a concrete operation.
- Confirm missing authorization before destructive execution, live schema/data migration, deployment, breaking external transitions or work outside the agreed scope. Approval to prepare a migration does not authorize running it against production.
- State the exact operation, evidence, risks and recovery limitations when approval is needed; do not claim a tested fallback unless tested.

## Independent review routing
- Delegate read-only only when authorized, supported and independent judgment adds enough value to justify the cost. Risk labels alone do not require delegation.
- Supply short brief: objective, invariants, touched files, diff, tests and known risks.
- Ask for verified findings, not a score; do not blindly apply reviewer changes.
- If no capability exists, do adversarial self-review and explicitly identify it as such.
