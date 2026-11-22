# Precision Engineering

A portable Agent Skills package for building new projects and features, and changing or reviewing existing code. It starts with one question. **What must be true for this change to be correct?** Use the answer to find where the behavior belongs, reuse the existing method or pattern whenever it meets the requirement, and choose a check that could expose a mistake.

The depth of investigation and verification follows the behavior at risk. A local label change may need only inspection and a focused check. A shared validation change may need checks through several callers, including a caller whose existing behavior must hold.

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

`$precision-engineering Fix duplicate invoice submission when two requests for the same provider and invoice arrive at once. Submissions for distinct invoices must still succeed.`

## Evaluate changes to this skill

[The manual evaluation guide](evals/README.md) gives exact prompts, fixture setup, and scoring criteria for comparing skill instructions ON and OFF or comparing revisions. [The case catalog](evals/cases.md) lists additional scenarios.

## Background research (November 2026)

Public user reports identify practical failure modes, not controlled proof of savings:

| Source | Practice |
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
