# Project Pulse implementation plan

## Goal

Build a lightweight, polished static Project Pulse dashboard that helps contributors quickly scan active projects, ownership, current status, recent activity, priority or risk, and a concise contributor-friendly summary. Show multiple projects as readable, accessible cards with responsive layout and clear status and priority treatments.

The project data will live in a top-level `projects` array in `app/project-data.json`. Each project will include `name`, `owner`, `status`, `recentActivity`, `priority`, and `summary`. The dashboard will render those fields from the data rather than duplicating project content in the HTML.

## Responsibilities

- **Planner** — define this implementation sequence, file ownership, dependencies, parallel work, and validation expectations.
- **Orchestrator** — share the interface contract below, delegate work by file scope, integrate the deliverables, and verify the working dashboard.
- **Designer** — own the visual and accessibility direction and implement the responsive styles in `app/styles.css`. Use `.dashboard` and `.project-card` hooks, readable spacing and contrast, and distinct but legible status and priority treatments.
- **Coder** — implement the semantic page and data rendering in `app/index.html`, provide representative project records in `app/project-data.json`, and configure `.vscode/launch.json` for a reliable preview. Ensure the markup and rendered cards follow the shared design and data contracts.

## Interface contract

Before parallel implementation starts, agree on the card markup hooks and fields: `.dashboard` is the dashboard layout container; each `.project-card` contains the project's name, owner, status, recent activity, priority, and contributor-friendly summary. Use semantic headings and suitable labels for status and priority so these remain understandable without color. The HTML must reference `styles.css` and load `project-data.json` to render the cards.

## Ordered phases, file assignments, and dependencies

1. **Agree on contracts — Orchestrator**
   - Confirm the `projects` array and all six project fields, the card content, and CSS hooks in the interface contract above.
   - This is a prerequisite for the parallel work: it prevents mismatched data fields and styles.

2. **Build independent assets in parallel**
   - **Designer — `app/styles.css`:** create polished, responsive styling for the agreed dashboard and project-card hooks, with visible status badges, clear priority treatment, accessible contrast, and readable spacing.
   - **Coder — `app/project-data.json`:** add a valid top-level `projects` array with realistic sample records containing `name`, `owner`, `status`, `recentActivity`, `priority`, and `summary`.
   - **Coder — `.vscode/launch.json`:** add strict JSON for the **Run Project Pulse Dashboard** launch configuration. Serve with `python3 -m http.server 5500`, set `cwd` to `${workspaceFolder}/app`, and use `serverReadyAction` to open `http://localhost:%s/index.html`. The URL must target the app page, not the server root or a directory listing.
   - These files have distinct ownership and can be produced concurrently after the interface contract is fixed. The stylesheet and sample data do not depend on one another; the launch configuration is also independent of the UI implementation.

3. **Implement and integrate the page — Coder**
   - **File: `app/index.html`.** Create the Project Pulse page, reference `styles.css`, load `project-data.json`, and render one `.project-card` per project with every agreed field visible. Keep the structure semantic and accessible.
   - This phase depends on the stylesheet hooks and data schema from Phase 2. Integrate their results without changing the agreed contract; handle a data-loading failure with a clear message rather than silently showing an empty dashboard.

4. **Review and validate — Orchestrator with Designer and Coder**
   - Review all four assigned files together, resolve integration issues with the owning agent, and check the rendered dashboard and launch behavior before handoff.
   - Do not start the page integration until its data and styling contracts are available. If the agreed contract must change, communicate the change to both owners before they revise their files.

## Parallel and sequential work decisions

- **Parallel:** Once the interface contract is set, Designer can implement `app/styles.css` while Coder prepares `app/project-data.json` and `.vscode/launch.json`. These assignments do not overlap and their outputs are independent.
- **Sequential:** Coder builds `app/index.html` after the stylesheet hooks and JSON schema are agreed and available, because the page must connect both. The final integrated review follows all implementation work.
- Keep each file with its named owner; Orchestrator coordinates integration rather than making conflicting edits.

## Validation expectations

- Parse `app/project-data.json` and `.vscode/launch.json` as JSON (for example, with `python3 -m json.tool`); launch configuration JSON must contain no comments.
- Confirm the data has a top-level `projects` array and every record has `name`, `owner`, `status`, `recentActivity`, `priority`, and `summary`.
- Inspect `app/index.html` for the exact **Project Pulse** title, references to `styles.css` and `project-data.json`, semantic accessible content, and rendered `.project-card` elements that display all project fields.
- Confirm `app/styles.css` includes `.dashboard` and `.project-card`, polished card styling, visible status and priority distinctions, readable contrast and spacing, and responsive behavior.
- Confirm `.vscode/launch.json` has the **Run Project Pulse Dashboard** configuration, runs `python3 -m http.server 5500` from `${workspaceFolder}/app`, and opens `http://localhost:%s/index.html` rather than the directory root.
- Run the launch configuration and verify the browser shows the Project Pulse dashboard with populated cards, not a directory listing. Check that the layout remains usable at narrow viewport widths and that project details remain understandable without relying on color alone.
