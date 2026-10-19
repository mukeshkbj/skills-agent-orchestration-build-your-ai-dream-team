# Project Pulse Agent Team

Mona's team uses four custom agents defined in `.github/agents/` to plan, design, build, and validate the **Project Pulse** dashboard.

## Custom Agents

| Agent | Definition File | Assigned Model | Responsibility |
| --- | --- | --- | --- |
| **Orchestrator** | `.github/agents/orchestrator.agent.md` | Claude Opus 5.5 (copilot) | Coordinates the request, parses plans into phases, delegates isolated file scopes to specialists, verifies the integrated dashboard, and reports the final outcome. |
| **Planner** | `.github/agents/planner.agent.md` | Claude Opus 5.5 (copilot) | Researches the repository, identifies dependencies and edge cases, and produces an ordered implementation plan with explicit file ownership and validation criteria. |
| **Designer** | `.github/agents/designer.agent.md` | Gemini 3.7 Flash (copilot) | Owns UI/UX direction, accessibility, information hierarchy, responsive card layout, status badges, and visual styling in `app/styles.css`. |
| **Coder** | `.github/agents/coder.agent.md` | GPT-5.5 (copilot) | Implements deterministic HTML, JavaScript, and JSON data in `app/index.html` and `app/project-data.json`, plus the runnable VS Code launch configuration in `.vscode/launch.json`. |

## How the Team Collaborates on Project Pulse

1. **Planning**: The **Orchestrator** delegates to the **Planner** (`.github/agents/planner.agent.md`, running on Opus 5.5) to create `docs/project-pulse-plan.md` covering phases, file assignments, dependencies, parallel execution choices, and validation expectations.
2. **Parallel Design & Data/Config**: Where file scopes do not overlap, the **Orchestrator** assigns `app/styles.css` to the **Designer** (`.github/agents/designer.agent.md`, running on Gemini 3.7 Flash) and assigns `app/project-data.json` and `.vscode/launch.json` to the **Coder** (`.github/agents/coder.agent.md`, running on GPT-5.5).
3. **Sequential Dashboard Assembly**: The **Coder** builds `app/index.html` using the agreed data schema (`name`, `owner`, `status`, `recentActivity`, `priority`) and CSS hooks (`.dashboard`, `.project-card`).
4. **Validation & Handoff**: The **Orchestrator** verifies the integrated **Project Pulse** dashboard files and launch configuration and writes `docs/final-handoff.md`.
