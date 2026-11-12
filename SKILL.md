---
name: precision-engineering
description: Evidence-first, reuse-first software engineering workflow for Codex when implementing, fixing, reviewing, refactoring, optimizing or migrating existing code across languages and frameworks. Selects rigor by risk, maps existing behavior and data flow, minimizes new abstractions, approval-gates risky changes and verifies behavior. Includes optional language, framework, database and distributed systems checks.
---
# Precision Engineering v1

## Objective
Maximize verified correctness and maintainability per unit of agent usage. Preserve repository conventions, existing behavior and user control. No process theater: apply only steps that materially reduce task risk. This is a workflow, not permission to bypass user approval or tool limitations.

## Non-negotiable rules
1. **Evidence before edits.** Inspect actual code, tests, callers and relevant history; distinguish observations from assumptions.
2. **Reuse before creation.** Search for equivalent types, methods, components, hooks, queries, validators, abstractions and test fixtures before adding any. Prefer reuse, then extension, then composition; create new symbols only when a clearly documented boundary requires them. Do not force reuse of a semantically wrong abstraction.
3. **Minimal sufficient diff.** Fix the underlying cause, preserve unrelated behavior, match local style, and avoid speculative redesign, dependencies, reformatting, new layers and compatibility shims without a real caller.
4. **No silent risky changes.** Require explicit approval before schema/data migrations, auth/permissions/security semantics, public contract breaking changes, destructive operations, infrastructure changes, dependency upgrades, or expanding beyond approved scope. User approval cannot be inferred from the existence of this skill.
5. **Prove claims.** Report commands executed and results. Never equate a passing unit test with production correctness. If a check cannot run, say so and explain residual risk.
6. **Protect existing work.** Check git status first. Never reset, overwrite, delete or revert unrelated user changes. Use worktrees only when beneficial and available, never presume they are required.
7. **No fabricated capabilities.** Delegation, model routing, tool calls and CI execution occur only where actually available. Never claim an independent review if the same agent performed it.

## Route by risk, not by number of words
- **S0 / tiny:** local, easily reversible, no behavior or contract risk. Inspect target + neighbors, patch, run focused check, inspect diff. No plan ceremony.
- **S1 / normal:** localized bug or feature. Reproduce or define acceptance, discover existing patterns, write brief plan, implement bounded slice, run focused tests plus relevant regression checks.
- **S2 / substantial:** cross-file or cross-layer changes, concurrency/performance or medium-risk data flows. Trace caller→boundary→state→storage→side effects, enumerate failure paths, present an approval checkpoint for the proposed design/scope, implement in slices, verify at boundaries, request a fresh review when available.
- **S3 / critical:** security, payment, data loss, auth, schema/migration, external contracts, distributed consistency. Stop at an approval gate before modifying behavior; add explicit rollback/recovery and failure-injection considerations, independent review if available, plus end-to-end validation. Never reduce these gates to save tokens.
Escalate if evidence reveals higher risk. Do not downgrade merely because the requested diff is small.

## Operating loop
**0. Frame (short).** State desired outcome, observable acceptance criteria, constraints, non-goals, and risk tier. For S0, keep this implicit unless useful. Ask only about genuine blockers; otherwise make a safe assumption and label it.

**1. Discover (read-only).** Inspect repo guidance, `git status --short`, target files, tests and nearby conventions. Search narrowly with symbols and call sites before opening large files. Establish baseline where feasible. Stop exploring when you can explain what runs, where state lives and what the narrowest change is.

Identify the affected language, framework, runtime, pinned versions and verification commands from manifests, lockfiles, build configuration and CI. Apply only relevant language, framework and cross-cutting checks from the stack reference; a listed stack is not a recommendation to adopt it. For an unlisted stack, use the core workflow, repository conventions and official documentation for the project's version. Do not install tools, upgrade dependencies or introduce frameworks just to satisfy a checklist.

**2. Model the change.** For S1+, record: (a) current vs expected behavior; (b) causal path and affected callers; (c) reuse candidates and why chosen/rejected; (d) invariants/failure modes; (e) smallest patch and tests. For S2/S3 explicitly include request/data flow, authorization/tenant boundaries, concurrency, retries/idempotency and rollback as relevant.

**3. Gate.** S0: implement. S1: proceed if bounded and user authorized the task. S2: pause for design/scope approval if the change is architectural or broad. S3: require explicit approval for any risky change. If the user already approved the precise scope, do not ask twice. Do not turn a simple fix into a prolonged interview.

**4. Implement one vertical slice.** Prefer a failing regression test for confirmed bugs and important invariants; use characterization tests if legacy behavior is unclear. Keep production changes minimal. Change callers when necessary; delete superseded code when safe. Do not create a new service/hook/interface just to avoid touching established code.

**5. Verify proportionally.** Run targeted tests first; then compile/typecheck/lint and relevant integration or contract tests. For concurrency, test racing/interleavings; for SQL, test transaction and tenant scoping; for UI, test loading/error/empty states and accessible behavior; for performance, measure baseline and repeat under comparable conditions. Inspect `git diff --check`, `git diff --stat`, `git diff`, and unintended file changes. A failed check requires diagnosis, not repeated blind reruns.

**6. Adversarial review.** Critique the changed code against acceptance, existing conventions and newly introduced defects: authorization, boundaries, nullability, timeouts, concurrency, retry/idempotency, resource lifecycle, query semantics, migration safety, unnecessary symbols, hidden behavior and regression coverage. On S2/S3 prefer an independent, read-only reviewer if supported and worth the cost. Reviewer must cite exact evidence; reject speculative recommendations without evidence.

**7. Report.** Provide concise summary: outcome; files/symbols changed; reuse decisions; verification command + result; risks/untested paths; and any requested approval. State `verified`, `partially verified`, or `not verified` accurately. No self-congratulatory score and no assertions of perfection.

## Usage policy
- Default to **one implementation agent**. Use a subagent only for an independent, bounded question whose saved context or judgment clearly exceeds orchestration cost. Never spawn subagents reflexively or to summarize files the parent has already read.
- Use a separate reviewer on S2/S3 if supported; not on every trivial edit. Reviewer receives scope, diffs, invariants and tests—not a full session transcript. Do not delegate overlapping writes to different agents.
- Route tool/model capability opportunistically, never hardcode presumed model names or require a custom router. If routing is unavailable, operate inline and report it.
- Use `rg -n`/targeted ranges; avoid dumping the repo, entire logs or repeated full files. Capture short evidence notes, path:line references and command results. Prefer deterministic tools to LLM judgment for formatting, test pass/fail and API checks.
- Stop when acceptance and appropriate verification are met; do not generate optional improvements without user request.
- Avoid raw token-budget quotas that incentivize incomplete verification. Track cost and defects over several comparable tasks instead.

## Approval request contract (only when needed)
`Goal | Evidence | Reuse decision | Proposed files/contracts | Invariants + failure modes | Tests | Risk / rollback | Explicit approval requested`
No implementation of gated behavior until approved. Read-only investigation and plan drafting are allowed.

## Completion contract
`Outcome | Change footprint | Reused vs new symbols | Checks (pass/fail/not run) | Remaining risk | Diff scope confirmation`

## Optional focused references
- For task-specific checklists, read [references/playbooks.md](references/playbooks.md) **only** for the relevant task type.
- For review criteria and approval gates, read [references/review-contract.md](references/review-contract.md) on S2/S3 or review tasks.
- For language, framework/runtime, database or distributed systems concerns, select only applicable sections of [references/stack-checks.md](references/stack-checks.md). Combine checks when needed, such as PHP + Laravel or TypeScript + React.
- For evaluations, read [evals/cases.md](evals/cases.md) when testing or improving this skill, not during normal coding work.
