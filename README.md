# Precision Engineering

A portable Agent Skills package for improving existing code with focused investigation, semantic reuse and verification matched to behavioral risk. The core skill loads for engineering work; supporting references and evaluation guidance are read only when needed.

The skill favors first-principles reasoning: understand the surrounding domain behavior before editing, make the smallest cohesive fix and justify each addition against a concrete requirement or contract. Prefer editing the existing path over parallel mechanisms or broad rewrites; small diffs must still preserve correctness and readability. Fix invalid state at its source, trust enforced internal contracts, validate untrusted input at entry, and preserve local code style. Database origin alone does not guarantee non-null values or a matching row. Redundant consumer guards, silent defaults and speculative abstractions are not substitutes for correctness. Use non-deprecated APIs compatible with pinned versions, and prefer deterministic tooling over speculative reading when it can answer the question.

For Codex usage efficiency, keep investigation targeted, reuse valid evidence, load references only for concrete concerns, default to one agent, and stop once acceptance and risk-appropriate checks are satisfied—even on higher-capability models. The skill does not change Codex usage limits; shorter instructions alone do not prove lower total usage. Preserve correctness checks rather than imposing arbitrary tool or token caps.

Verification follows behavioral effect, not file extension or diff size: instructions, configuration and CI can change behavior or authority. Before checks with external effects, verify effective targets and isolation; disposable files do not isolate inherited credentials or service endpoints.

The core workflow applies across languages without bundled stack checklists. Derive stack-specific decisions and checks from the affected project's pinned versions, source, configuration and existing tests; consult version-matched official documentation only for unresolved questions.

## Install on macOS / Codex

Copy this directory to `~/.agents/skills/precision-engineering/` (a currently documented Codex user skill location):

```bash
mkdir -p ~/.agents/skills
cp -R precision-engineering ~/.agents/skills/
```

Restart Codex if the new skill does not appear. You can invoke `$precision-engineering` in your coding task or let Codex match its description. This package does not install external models, a router, agents, plugins, or permissions. It only adds instruction files.

Repo-level alternative: place in `<repo>/.agents/skills/precision-engineering/` and commit if shared.

## Suggested tiny root AGENTS.md (manual, optional)

```md
Follow repository code style and existing test commands. Reuse existing implementations before introducing new symbols. Never modify unrelated user changes. Verify auth, data, contracts, and infra changes proportionally to risk; confirm missing authorization before destructive or live operations. Never claim tests pass without running them. Apply the `precision-engineering` skill for nontrivial implementation, bug fixes, refactors, migrations and reviews.
```

Do not paste the full skill into AGENTS.md; that duplicates context. Keep repo-specific file locations, test commands, and architectural constraints in AGENTS.md.

## Example

`$precision-engineering Fix duplicate invoice submission for the same provider. Trace existing transaction and ownership logic, reuse it, propose a bounded patch, add a concurrent duplicate regression test, and show the diff and actual verification results.`

## Evaluate changes to this skill

[Evaluation guidance](evals/cases.md) describes comparison scenarios and scoring criteria. Measuring the skill's effect requires separate coding-agent runs with the same tasks, model and settings. Executable fixtures and test tooling are not bundled.

## Usage-efficiency research (November 2026)

Public user reports identify practical failure modes, not controlled proof of savings:

| Source | Incorporated practice |
|---|---|
| [User reporting RTK use with Codex](https://github.com/openai/codex/issues/19001) | Bound tool output and inspect relevant summaries; preserve full failure evidence. No wrapper dependency or claimed savings percentage. |
| [Oversized observations and repeated retries](https://github.com/openai/codex/issues/48792) | Narrow reads, retain findings and reassess failed approaches instead of repeating unchanged observations. |
| [Compaction visibility and lost constraints](https://github.com/openai/codex/issues/21468) | Compact handoffs preserve invariants, decisions, changed files and actual verification state. |
| [Official best practices](https://learn.chatgpt.com/guides/best-practices) | One chat per coherent outcome; preserve continuity while iterating on the same problem. |
| [Official skills guidance](https://learn.chatgpt.com/docs/build-skills) | Progressive disclosure: keep the core focused and load supporting material only when needed. |

These sources were checked on 2026-11-15. User reports are anecdotal and version-specific; their advertised savings are not this skill's measured results. We do not adopt automatic session resets, blanket lower-reasoning settings or output filters that conceal failures. No Codex configuration or external tools are installed by these instructions.

## Earlier sources consulted (2026-11-12)
- Poteto pstack: https://github.com/cursor/plugins/tree/main/pstack
- phthomas pstack: https://github.com/phthomas/pstack
- Superpowers: https://github.com/obra/superpowers
- Everything Claude Code: https://github.com/affaan-m/ECC
- Codex skill evals: https://developers.openai.com/blog/eval-skills
- Codex skills guidance: https://learn.chatgpt.com/docs/build-skills
- Agent Skills specification: https://agentskills.io/specification
- OpenAI instruction minimization: https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra
