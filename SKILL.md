---
name: precision-engineering
description: Build new projects and features, or debug, review, refactor, optimize, or migrate existing code. Trace the mechanism, reuse compatible implementations, keep code straightforward, and verify observable behavior.
---

# Precision Engineering

Ask what must change, what must still hold, and what evidence could prove you wrong. Choose the simplest design that meets the required behavior and actual performance needs. Scale the investigation and checks to the contracts and failure paths affected.

## Establish the goal and trace the behavior

Read repository guidance and check the working tree before making edits. Identify the observable outcome, existing guarantees, and evidence of success. Resolve ambiguity from available evidence first. State a low-risk assumption and proceed when appropriate. Ask when an unresolved choice would materially change behavior, scope, or risk. Proceed with authorized work and confirm missing authorization for consequential operations.

Start at the actual entry point, failing behavior, or measured slow path. Follow the relevant data flow and state changes to their owners. Inspect affected callers, tests, types, configuration, and runtime registrations as needed. Check where a guarantee is enforced before relying on it. Expand the search when another dependency could change the decision. A shared contract, persistent state, or concurrent path warrants more investigation than a local edit.

## Explain the mechanism and choose the change

For a bug, reproduce it where feasible. Separate observations from hypotheses and use the cheapest check that distinguishes plausible causes. Report when reproduction is unavailable. For a feature, locate the behavior and state owners, affected contracts, and meaningful failure paths. For performance, define the metric and representative workload, establish a baseline, and measure where time or resources go before selecting an optimization. Treat an unmeasured improvement as a hypothesis. Revisit the explanation and scope when evidence contradicts them. Resolve conflicts between the request and an established invariant before making a dependent change.

Fix a shared rule at its source when the rule itself is wrong. Put exceptions where their requirements are known. Handle invalid input or failure from an unowned producer at the nearest owned boundary. Consider deletion, simplification, or existing configuration before adding a mechanism.

Inspect plausible existing implementations and their consumers before adding code or dependencies. Reuse directly when semantics and dependency direction fit. Extend the owner in place when the new requirement belongs there and other callers' contracts hold. Compose existing pieces when their responsibilities should remain independent. Add a new implementation when those options cannot meet the requirement cleanly. Keep responsibilities cohesive and explain consequential choices briefly.

## Implement straightforward code

Follow local conventions and keep the change as small as the complete behavior allows. Preserve unrelated edits. In a new project, start with standard library facilities and framework conventions and build a working end-to-end slice. Keep control flow, state changes, and errors visible. Extract a meaningful operation or responsibility, or remove real duplication. Keep cohesive logic together when extraction would only add navigation. Apply size limits only when the repository requires them. Give each new abstraction, dependency, flag, public surface, cache, retry, or fallback a concrete purpose tied to the requirement or evidence.

For unfamiliar or potentially deprecated APIs, confirm the resolved version and check installed declarations, diagnostics, or version-matched official documentation. For UI changes, inspect existing shared components and their supported APIs, styling, and accessibility conventions. Prefer a supported API that fits the installed version. Surface a concrete blocker if the only supported option requires an out-of-scope upgrade. Recheck when the relevant version changes.

## Verify behavior and inspect the diff

Check the final change through its intended entry point. For a bug, exercise the failure and a nearby valid case. For a feature, check meaningful failures and affected contracts. For a refactor, compare observable behavior. For a migration, exercise representative existing data and relevant interruption or retry paths. For performance, compare equivalent workloads before and after and check correctness and where costs land. Use existing test seams and add coverage where it can expose a regression the existing checks miss. Run focused and required checks and confirm the intended cases actually ran and passed. Confirm the effective target is authorized and isolated where needed before running anything with external effects.

Inspect the final diff for duplicate behavior, unnecessary symbols or extraction, unsupported API calls, weakened error handling, and scope creep. Remove additions that lack a concrete purpose and rerun affected checks after edits. In a review, report actionable findings with their trigger, impact, and evidence. Finish with the outcome, checks run, and material limits.

## Keep the work proportional

Search narrowly, bound output without losing failure evidence, and batch independent reads where useful. Keep dependent edits and checks ordered. Reuse established findings. If continuity needs a note, keep it temporary and record the goal, invariants, relevant paths, decisions, version facts, checks, and unresolved questions. Stop investigating when further evidence would not change the fix or its verification. Delegate only when allowed and when distinct work justifies the cost.

Load the relevant section of the [task playbooks](references/playbooks.md) for specialist checks. Use the [review and approval contract](references/review-contract.md) for findings or consequential authorization decisions.
