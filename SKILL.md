---
name: precision-engineering
description: Implement, debug, review, refactor, optimize or migrate existing code with focused investigation, semantic reuse and verification matched to behavioral risk. Use when existing callers, contracts and repository conventions must be preserved.
---
# Precision Engineering

Optimize for verified behavior per unit of effort. Choose the next action by the uncertainty it resolves; shorter instructions or smaller diffs alone do not establish quality.

## Establish the change

- Read applicable repository guidance and working-tree status; distinguish your changes from existing edits and preserve unrelated work.
- Identify the requested outcome and behavior that must remain unchanged. Keep this implicit for obvious edits; use a short plan only for coordinating dependent work. Review-only requests do not authorize edits.
- Existing authorization persists. Prepare authorized patches and verification before seeking missing approval for a concrete operation. Resolve consequential ambiguity before dependent work; continue independent work. Preparing a migration does not authorize running it against live data.

## Investigate just enough

Use narrow symbol searches and targeted reads to find the owning implementation, affected consumers, reusable behavior and relevant tests. Inspect configuration when versions or commands are uncertain. Follow exports, registration and generated code when relevant; missing direct callers does not prove code is unused.

For bugs, reproduce the failure or ground the diagnosis in trustworthy evidence. Tests and documentation describe existing expectations; resolve conflicts with the requested behavior rather than blindly preserving a bug. Choose the cheapest observation that can disprove the leading hypothesis. If evidence contradicts it, revise the hypothesis before patching again. Read history or broaden searches only for a concrete unanswered question.

Start editing when evidence supports the intended behavior, owning boundary, affected consumers and a way to distinguish success from failure. Do not require exhaustive repository understanding.

## Make the smallest coherent change

Search the affected area and established shared utilities before adding equivalent behavior. Reuse only when ownership, validation, state and failure semantics fit. A small new implementation is preferable to a misleading abstraction. Avoid speculative layers, dependencies and compatibility shims. Fix generated behavior at its source and regenerate through the established tooling.

Fix the cause at its owning boundary and update affected consumers. Preserve unrelated behavior and local conventions. Characterize unclear behavior before refactoring. Separate required changes from optional cleanup.

## Match proof to failure risk

Choose the nearest verification layer that can detect the failure, plus repository-required checks:

| Changed behavior | Useful evidence |
|---|---|
| Text, style or mechanical change without behavioral risk | Inspect the result and diff; use existing checks when useful. No new tests or plan by default. |
| Local logic | Focused behavior test covering the intended result and a plausible counterexample. For bugs, prefer failure from the original defect before the fix and success afterward. |
| Shared contracts or cross-layer behavior | Relevant consumers and boundary tests. Compilation or mocked internals alone cannot prove runtime compatibility. |
| Authorization, persistence, concurrency or external effects | Applicable ownership, isolation, atomicity, retries and recovery checks at the authoritative boundary. Verify valid operations still succeed as well as invalid operations fail. |
| Performance | Comparable baseline and changed workloads, correctness checks and measurement variability. |

Check that intended tests actually ran against the current implementation. Empty selection, unrelated setup failures, skipped coverage and stale build output are not proof. Do not weaken assertions to hide a defect. Use disposable baselines when needed without disturbing working edits; call failures pre-existing only with evidence.

## Spend effort once; finish honestly

- Reuse discoveries and results while their inputs and assumptions remain valid. After edits, rerun affected checks; retain unrelated evidence. Batch independent reads. Parallelize checks only when fixtures, outputs and services cannot interfere.
- Diagnose failures before retrying. Expand verification for changed scope, failures or unresolved risks; stop when acceptance and appropriate checks are satisfied.
- Inspect changed-file status, your final diff and `git diff --check`, including new files omitted from the default diff. Challenge the result against acceptance and affected callers. Report unavailable checks and unresolved risks without calling them passes; separate implemented behavior from verified behavior.
- Default to one agent. Use bounded delegation only when authorized and its independent judgment or saved context justifies the cost. Do not duplicate investigation or imply independent review from self-review.
- Report the outcome, meaningful changes, verification and material limitations. Omit empty checklist fields and routine process narration. Never claim measured efficiency or correctness gains without comparative runs.

## Conditional references

Read only the section implicated by the changed behavior or an unresolved concern:

- [Task playbooks](references/playbooks.md): deeper procedures for fixes, features, refactors, migrations, performance, incidents or reviews.
- [Review contract](references/review-contract.md): grounded findings and authorization boundaries.
- [Stack checks](references/stack-checks.md): language, framework or persistence pitfalls; follow pinned project versions.
- [Evaluation cases](evals/cases.md): improving or evaluating this skill, never routine coding work.
