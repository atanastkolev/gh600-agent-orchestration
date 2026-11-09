# Agent team

I am using GitHub Copilot CLI in a Codespace to orchestrate the work of building Mona's Project Pulse dashboard. The custom agents below coordinate through the Orchestrator.

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 5.5 (copilot) | Breaks the request into phases, delegates to specialists with explicit file scopes, runs work in parallel only when scopes don't overlap, verifies the integrated result, and reports back. Does not implement. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 5.5 (copilot) | Researches the repo and docs, then returns an implementation plan with steps, file assignments, dependencies, edge cases, and validation expectations. Writes no code. | `.github/agents/planner.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements code and logic within its assigned files, plus runnable-app support such as `.vscode/launch.json` (cwd `${workspaceFolder}/app`, opens `index.html`). Validates before reporting. | `.github/agents/coder.agent.md` |
| Designer | Gemini 3.7 Flash (copilot) | Handles UI/UX, accessibility, and visual design: project cards, status badges, priority treatment, responsive layout, and CSS hooks like `.dashboard` and `.project-card`. | `.github/agents/designer.agent.md` |

## Workflow

1. Orchestrator asks Planner for a plan.
2. Orchestrator splits the plan into phases with non-overlapping file scopes.
3. Coder and Designer execute their assigned scopes.
4. Orchestrator verifies the result and reports.

No agent stages, commits, or pushes; I control all git operations through Copilot CLI prompts.
