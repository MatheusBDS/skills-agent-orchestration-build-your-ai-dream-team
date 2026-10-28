# Agent team

I will use GitHub Copilot CLI in a Codespace to orchestrate the custom agent team building Mona's Project Pulse dashboard.

| Agent | Target model | Responsibility | Definition |
|---|---|---|---|
| Orchestrator | Claude Opus 5.5 (copilot) | Coordinates the Planner, Designer, and Coder; assigns work by phase and file scope, integrates the results, and reports the outcome. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 5.5 (copilot) | Researches the repository and requirements, then creates an implementation plan with steps, ownership, dependencies, parallel work, risks, and validation expectations. | `.github/agents/planner.agent.md` |
| Designer | Gemini 3.7 Flash (copilot) | Guides the dashboard's usability, accessibility, information hierarchy, responsive layout, and visual design, including polished project cards and status/priority treatments. | `.github/agents/designer.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements and validates the assigned dashboard code and support files, including `.vscode/launch.json` when assigned. | `.github/agents/coder.agent.md` |
