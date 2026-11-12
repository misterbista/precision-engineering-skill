# Review and approval contract

## Review priorities, in order
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
- P3: optional suggestion; never block for style preference.
No claim of certainty beyond evidence; requests for evidence are not proven defects.

## Approval gates
- **Must request explicit authorization:** destructive writes or drops, schema/data migration, authentication/authorization behavior, breaking public API, secrets/IAM, infrastructure deployment, dependency upgrade with risk, changes outside agreed scope.
- **Design signoff if S2:** broad cross-module/cross-layer change, new architectural boundary, replacement of shared abstraction. If exact scope was already approved, proceed with it.
- Approval record should capture exact scope, tested fallback, risks and rollback constraints. Approval of a plan does not authorize unrelated destructive commands.

## Independent review routing
- Delegate read-only if tool supports separate agent, task is S2/S3, and independent judgment adds value.
- Supply short brief: objective, invariants, touched files, diff, tests and known risks.
- Ask for verified findings, not a score; do not blindly apply reviewer changes.
- If no capability exists, do adversarial self-review and explicitly identify it as such.
