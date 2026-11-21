---
name: precision-engineering
description: Build new projects and features, or debug, review, refactor, optimize, or migrate existing code. Use established implementations and patterns, preserve caller contracts, and verify observable behavior.
---

# Precision Engineering

Ask **what must be true for this change to be correct?** Identify the outcome the user wants, the behavior affected callers rely on, and what evidence would establish both. Let those answers set the scope of the work.

## Find where the behavior is decided

Start at the entry point people or systems actually use. Check repository guidance and the working tree before editing. Follow the path to the code, data, or configuration that decides the outcome. Read affected callers and nearby tests where they can establish the contract or reveal an exception. Check how a guarantee is enforced before relying on it.

For a new project without local conventions, use standard library facilities and follow the chosen framework's conventions where applicable. Build the smallest end-to-end version that meets a real requirement, and verify it through its intended entry point. Add abstractions only when a concrete requirement calls for them.

## Change the owning boundary

Fix a shared rule at its source when it is wrong for every caller. When callers have different requirements, put each policy where that requirement is known. If the source is outside your control, handle invalid input or failure at the nearest boundary you own.

**Reuse is required.** Before introducing a method, helper, wrapper, abstraction, or pattern, check the owning code and comparable callers for an existing solution. Call an existing method directly when it satisfies the contract and fits the dependency direction. Extend the owning implementation in place when it can cover the new requirement and preserve the behavior other callers rely on. Follow established local patterns for any necessary new code. Introduce a new method or pattern only when the existing options cannot safely meet the requirement.

Keep the patch as small as the complete behavioral change allows and preserve unrelated edits.

For example, if an import rejects a blank field, check where that field may be blank. If only imports permit it, handle the policy at the import boundary and verify that a caller requiring a value still rejects a blank one.

## Choose a check that could prove you wrong

Exercise the changed behavior through an existing entry point and cover a plausible regression. For a bug, verify the failing case and an adjacent case that should still work. For a refactor, compare observable behavior. For a migration, exercise representative existing data and realistic interruption or retry paths. Establish a comparable baseline before claiming a performance gain.

Run focused and repository-required checks against the final change. Confirm the intended checks actually ran and passed. Before any check with external effects, confirm the effective target is authorized and isolated where needed.

## Stop once the evidence is sufficient

Keep investigating while an unresolved question could change the fix or the verification it needs. In a review, report actionable findings with the affected behavior, the conditions that trigger it, and the supporting evidence. Finish with the outcome, the checks you actually ran, and any material gap in verification.
