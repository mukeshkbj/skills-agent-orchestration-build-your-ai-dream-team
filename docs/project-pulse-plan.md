# Project Pulse Implementation Plan

## Summary & Goal

Build **Project Pulse**, a lightweight static dashboard that helps Mona's team and contributors quickly understand active projects, owners, current status, recent activity, and priority levels.

## Specialist Responsibilities

- **Designer**: Defines the visual hierarchy, accessible color contrast, responsive grid, status badge treatment, and polished card styling (`.dashboard`, `.project-card`, `border-radius`, `box-shadow`) in `app/styles.css`.
- **Coder**: Creates the structured project dataset in `app/project-data.json`, builds the semantic markup and card rendering logic in `app/index.html`, and configures the VS Code launch configuration in `.vscode/launch.json`.

## Implementation Phases & File Assignments

### Phase 1: Contract & Parallel Foundation
1. **Project Dataset (`app/project-data.json`)** — Assigned to **Coder**
   - Define a top-level `"projects"` array where each item includes `name`, `owner`, `status`, `recentActivity`, and `priority`.
2. **Dashboard Styling (`app/styles.css`)** — Assigned to **Designer**
   - Implement `.dashboard` container layout, `.project-card` rules with `border-radius` and `box-shadow`, status/priority badges, and responsive breakpoints.
3. **VS Code Launch Configuration (`.vscode/launch.json`)** — Assigned to **Coder**
   - Create strict JSON (no comments) with configuration `"Run Project Pulse Dashboard"` serving `${workspaceFolder}/app` via `python3 -m http.server 5500` and `serverReadyAction` opening `http://localhost:%s/index.html`.

### Phase 2: Sequential Dashboard Integration
4. **Dashboard Markup & Rendering (`app/index.html`)** — Assigned to **Coder**
   - Set page `<title>` and heading to `"Project Pulse"`.
   - Link `styles.css` and load `project-data.json` (with inline fallback cards so `project-card`, `status`, `recentActivity`, and `priority` appear both in static markup and dynamic rendering).

## Dependencies

- `app/index.html` has dependencies on the CSS class contract in `app/styles.css` (`.dashboard`, `.project-card`) and the JSON schema in `app/project-data.json` (`projects` array with `name`, `owner`, `status`, `recentActivity`, `priority`).
- `.vscode/launch.json` depends on `app/index.html` existing in the `app/` directory at runtime to open the dashboard instead of a directory listing.

## Parallel Work Decisions

- **Parallel work**: `app/styles.css` (**Designer**), `app/project-data.json` (**Coder**), and `.vscode/launch.json` (**Coder**) have non-overlapping file scopes and can be created in parallel once the class names and JSON schema are fixed.
- **Sequential work**: `app/index.html` (**Coder**) runs after the schema and class hooks are locked so markup and fetch logic match both `app/styles.css` and `app/project-data.json`.

## Edge Cases to Handle

- Empty or failed `fetch('project-data.json')` requests: provide accessible fallback status messaging and pre-rendered `.project-card` markup.
- Long project descriptions or activity strings: wrap text cleanly inside `.project-card` without breaking grid alignment on narrow viewports.

## Validation Expectations

- Verify `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json` exist.
- Validate `app/project-data.json` and `.vscode/launch.json` with `python3 -m json.tool`.
- Confirm `app/index.html` references `styles.css` and `project-data.json`, uses title `Project Pulse`, and renders `.project-card` elements displaying `status`, `recentActivity`, and `priority`.
- Confirm `app/styles.css` defines `.dashboard` and `.project-card` with `border-radius` and `box-shadow`.
- Serve `app/` on port 5500 and verify `http://localhost:5500/index.html` renders the Project Pulse cards.
