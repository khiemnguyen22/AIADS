# AIADS

AIADS (AI Agent Development Stack) is a reusable set of role-based agent definitions for bringing a consistent, hand-off-driven software development workflow to projects. It is designed to be added to a consuming repository as a Git submodule under `.github/`, keeping the shared agent setup versioned separately from the project code.

## What's included

- [`agents/orchestrator-agent.agent.md`](./agents/orchestrator-agent.agent.md) — clarifies and breaks down requests, defines acceptance criteria, and hands implementation briefs to the developer.
- [`agents/developer-agent.agent.md`](./agents/developer-agent.agent.md) — implements assigned programming tasks and reports focused validation.
- [`agents/code-reviewer-agent.agent.md`](./agents/code-reviewer-agent.agent.md) — reviews changes for correctness, regression risk, quality, and acceptance-criteria coverage.
- [`agents/qa-agent.agent.md`](./agents/qa-agent.agent.md) — adds and runs focused tests, probes edge cases, and routes failures back for fixes.
- [`agents/documentation-agent.agent.md`](./agents/documentation-agent.agent.md) — documents verified features and code changes.
- [`documentation/`](./documentation/) — the documentation home and guidance for projects adopting this stack.

## Standard workflow

1. **Orchestrator → Developer:** break down the request into an actionable brief with context, proposed solution, acceptance criteria, and validation suggestions.
2. **Developer → Code reviewer:** implement the task, run focused checks, and summarize the changes.
3. **Code reviewer → Developer or QA:** send actionable findings back for fixes, or move reviewed changes to QA.
4. **QA → Developer or Documentation:** return defects and test failures for fixes, or hand off verified work for documentation.
5. **Documentation:** update the appropriate project documentation based on the implementation and QA results.

Each transition is defined as a hand-off in the agent's frontmatter. Start with the orchestrator, then use its hand-off actions to move through the workflow.

## Add AIADS to a project

Add this repository itself as the consuming project's `.github/` directory:

```sh
git submodule add <AIADS-repository-url> .github
git submodule update --init --recursive
```

The `.github` destination must not already contain files when adding the submodule. If the consuming project already has GitHub configuration there, move or merge those files into the AIADS repository before adding it as the submodule. Commit the submodule reference in the consuming project so teammates receive the same AIADS version. To update it later, check out the desired revision in `.github` and commit the updated submodule reference.

The agent definitions are kept together in this repository's [`agents/`](./agents/) directory. With AIADS mounted at `.github`, they are available at `.github/agents/`, which is VS Code's native workspace custom-agent location.

## Adopting the documentation directory

Use [`documentation/README.md`](./documentation/README.md) as the starting point for maintaining project documentation. Keep documentation accurate to the implementation, update existing pages where appropriate, and add focused pages for distinct topics.
