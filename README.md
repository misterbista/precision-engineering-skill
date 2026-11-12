# Precision Engineering v1

A portable Agent Skills package optimized for Codex, not a clone of pstack. It adds a single reusable evidence-first/reuse-first engineering workflow and opt-in references.

The core workflow applies across languages. Optional checks cover C#, PHP, Go, TypeScript, Java, Python, Rust, Kotlin and Swift; separate framework/runtime sections cover .NET, Laravel, React and Spring/JPA. Combine relevant sections, such as PHP + Laravel or TypeScript + React, with SQL and distributed systems checks where needed. These are engineering checklists, not stack-selection recommendations or exhaustive language coverage. Project versions, tooling and repository conventions determine which checks apply.

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
Follow repository code style and existing test commands. Reuse existing implementations before introducing new symbols. Never modify unrelated user changes. Treat auth, data, contracts, and infra as high-risk: request explicit approval before risky changes. Never claim tests pass without running them. Apply the `precision-engineering` skill for nontrivial implementation, bug fixes, refactors, migrations and reviews.
```

Do not paste the full skill into AGENTS.md; that duplicates context. Keep repo-specific file locations, test commands, and architectural constraints in AGENTS.md.

## Example

`$precision-engineering Fix duplicate invoice submission for the same provider. Trace existing transaction and ownership logic, reuse it, propose a bounded patch, add a concurrent duplicate regression test, and show the diff and actual verification results.`

## Sources consulted (2026-11-12)
- Poteto pstack: https://github.com/cursor/plugins/tree/main/pstack
- phthomas pstack: https://github.com/phthomas/pstack
- Superpowers: https://github.com/obra/superpowers
- Everything Claude Code: https://github.com/affaan-m/ECC
- Codex skill evals: https://developers.openai.com/blog/eval-skills
- Codex skills guidance: https://learn.chatgpt.com/docs/build-skills
- Agent Skills specification: https://agentskills.io/specification
- OpenAI instruction minimization: https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra
