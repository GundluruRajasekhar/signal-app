# Requirements — Signal (AI Task Intelligence)

## 1. Purpose

Signal is a single-page task management tool that solves a specific
productivity gap: individuals and small teams track work in scattered
places (chat threads, sticky notes, email), and reporting status upward
to management means manually rewriting that scattered work into a
coherent update. Signal keeps the task board and the status report in
one place, and uses AI to do both the data entry and the reporting.

## 2. Problem statement

- Task capture is slow because structured forms (title, priority, due
  date) are more friction than typing a sentence.
- Status updates to management are a recurring manual writing task,
  usually done by looking back over a messy list and translating it.
- Most lightweight task tools either have no reporting feature, or
  require a paid SaaS backend to get one.

## 3. Goals

1. Let a user add a task by typing a plain sentence; AI extracts title,
   due date, and priority.
2. Provide a three-column board (To do / In progress / Done) to move
   work through a lifecycle.
3. Surface completion rate, overdue count, and priority/status
   breakdowns without a separate analytics tool.
4. Generate a short, plain-English status briefing from the live task
   list, in a format suitable for forwarding to management as-is.
5. Run entirely client-side: no backend, no server cost, deployable as
   a static file.

## 4. Non-goals

- Multi-user collaboration or shared/synced task lists (out of scope
  for v1 — see Tasks.md backlog for a possible future phase).
- Notifications, reminders, or calendar integration.
- Authentication or access control (this is a single-user local tool).

## 5. Functional requirements

| ID | Requirement |
|----|-------------|
| FR-1 | User can add a task via free-text quick-add input. |
| FR-2 | When AI parsing is enabled and an API key is set, the app extracts `title`, `due_date`, and `priority` from the input via the Claude API. |
| FR-3 | When AI parsing is disabled or unavailable, the raw text is saved as the task title with medium priority and no due date. |
| FR-4 | Tasks can be moved between To do / In progress / Done. |
| FR-5 | Tasks can be deleted. |
| FR-6 | Tasks persist across browser sessions via `localStorage`. |
| FR-7 | Analytics view shows: total tasks, completed count, overdue count, completion rate, and breakdowns by priority and status. |
| FR-8 | Briefing view generates a prose status summary from the current task list via the Claude API. |
| FR-9 | Generated briefing can be copied to the clipboard in one click. |
| FR-10 | User can set and persist their own Anthropic API key locally; the app functions (minus AI features) without one. |
| FR-11 | User can clear all locally stored task data. |

## 6. Non-functional requirements

- **Zero backend.** Single HTML file; deployable to GitHub Pages,
  Netlify, or any static host with no build step.
- **Data locality.** All task data and the API key stay in the
  browser's `localStorage`; nothing is sent to any server except
  direct, user-initiated calls to `api.anthropic.com`.
- **Graceful degradation.** Every core feature (add, move, delete
  tasks, view analytics) works with zero configuration and no API key;
  AI parsing and briefing generation are additive, not required.
- **Responsive.** Usable down to a single-column mobile layout.
- **No external runtime dependencies.** No build tools, no npm
  packages — just HTML, CSS, and vanilla JS, plus two Google Fonts
  loaded over CDN.

## 7. Security considerations

- The Anthropic API key is stored in browser `localStorage` and used
  directly from client-side JavaScript. This is acceptable for
  personal or small-team use where the user controls their own
  browser and key, but **this is not a pattern for public multi-user
  deployment** — anyone with access to the browser or its dev tools
  can read the stored key. A production version for a wider audience
  would need a thin backend to hold the key server-side (see Tasks.md
  backlog).

## 8. Success criteria

- A user can go from an empty board to a management-ready briefing in
  under two minutes with no setup beyond pasting an API key.
- The app requires no installation step for a viewer — opening the
  deployed URL is the entire onboarding.
