# Project Pulse implementation plan

## Goal

Build a lightweight static dashboard that helps contributors scan Mona's projects, owners, status, recent activity, and priority. Keep content in JSON and render it as responsive, accessible project cards.

## File ownership

| File | Owner | Responsibilities |
|---|---|---|
| `app/index.html` | Coder | Create the semantic page structure, exact page title and visible heading “Project Pulse”; reference `styles.css` and load `project-data.json`; render multiple project cards with each required field. |
| `app/styles.css` | Coder, guided by Designer | Implement the visual system, responsive layout, and polished status/priority treatments. Include `.dashboard` and `.project-card` selectors, clear focus states, and readable contrast and spacing. |
| `app/project-data.json` | Coder | Provide representative project records under a top-level `projects` array. Every record must include `name`, `owner`, `status`, `recentActivity`, and `priority`. |
| `.vscode/launch.json` | Coder | Add strict, comment-free JSON configuration named `Run Project Pulse Dashboard`; run `python3 -m http.server 5500` with `app/` as the working directory and open `http://localhost:%s/index.html`. |

## Roles and coordination

- **Designer:** Define the card layout, information hierarchy, status and priority visual language, responsive behavior, and accessibility requirements. Share concise implementation guidance before styling is finalized; review the resulting UI against those decisions.
- **Coder:** Implement all four assigned files, integrate JSON-driven rendering with the page, and resolve integration issues. Keep the dashboard static, with no unnecessary framework or build step.
- **Orchestrator:** Coordinate the handoff, ensure the plan is followed, and run the validation checklist before considering the work complete.

## Dependencies and parallelism

1. Designer first defines the visual and accessibility direction; this guides `app/styles.css` and the card structure in `app/index.html`.
2. Coder can create the sample data in `app/project-data.json` in parallel with Designer's work because the required schema is fixed. The HTML renderer and data must agree on field names.
3. After the design handoff and sample data are available, Coder completes `app/index.html` and `app/styles.css`. These are coordinated work: page classes and structure must match the stylesheet.
4. Coder can create `.vscode/launch.json` independently of the UI implementation. Final browser validation depends on all app files and the launch configuration being complete.

## Implementation phases

1. **Design and data:** Designer specifies the visual/accessibility direction; Coder prepares representative JSON records using the required schema.
2. **Build the dashboard:** Coder builds the semantic page, renders multiple data-backed cards, and applies the responsive design and status/priority treatments.
3. **Configure launch:** Coder adds the strict JSON launch configuration with the exact name, command, `app/` working directory, and page URL.
4. **Integrate and verify:** Orchestrator checks file integration and acceptance criteria; Coder fixes any issues and the team confirms the page in a browser.

## Validation expectations

- Parse `app/project-data.json` as JSON; confirm the top-level `projects` value is an array and each project has all five required fields.
- Confirm `app/index.html` has the exact title “Project Pulse,” references the stylesheet and JSON data, and renders multiple `.project-card` elements showing status, recent activity, and priority.
- Confirm `app/styles.css` includes `.dashboard` and `.project-card`, polished card treatment, readable contrast, visible keyboard focus, and layouts that work on narrow and wide screens.
- Parse `.vscode/launch.json` as strict JSON. Confirm the configuration name is exact, the command is `python3 -m http.server 5500`, its working directory is `app/`, and its server-ready URL is `http://localhost:%s/index.html`.
- Launch the configuration and verify the browser displays the dashboard at `index.html`, not a directory listing; check cards and key information at desktop and mobile widths.
