# Tasks — Signal (AI Task Intelligence)

Status legend: `[x]` done · `[ ]` open

## Phase 1 — Core build (complete, this delivery)

- [x] Three-column task board (To do / In progress / Done)
- [x] Quick-add input with AI-assisted parsing (title, due date, priority)
- [x] Graceful fallback when no API key is set or AI parsing is off
- [x] Task move / delete actions
- [x] `localStorage` persistence for tasks and API key
- [x] Analytics view: totals, completion rate, overdue count, priority
      and status breakdowns
- [x] AI-generated executive briefing from live task data
- [x] Copy-to-clipboard for the briefing
- [x] Settings view for API key management and data reset
- [x] Responsive layout down to mobile width
- [x] REQUIREMENTS.md and TASKS.md written
- [x] Deployable as a static file with no build step

## Phase 2 — Before wider rollout (backlog, not started)

- [ ] Move the Anthropic API key server-side (thin proxy) so the app
      can be shared with people who shouldn't hold their own key
- [ ] Add due-date reminders (browser notification or daily digest)
- [ ] Add task editing (currently: delete and re-add)
- [ ] Add CSV / JSON export of the raw task list, separate from the
      prose briefing
- [ ] Add a weekly (not just point-in-time) briefing that compares
      against the prior week's snapshot

## Phase 3 — Team use (backlog, larger effort)

- [ ] Shared/synced task list across users (needs a real backend +
      auth — this is the point where the single-file architecture is
      outgrown)
- [ ] Per-person task ownership and filtering
- [ ] Slack/Teams delivery of the generated briefing on a schedule
- [ ] Role-based briefing tone (e.g. shorter variant for leadership,
      detailed variant for the working team)

## How to pick this back up

Everything lives in one file, `index.html` — CSS in the `<style>`
block, logic in the `<script>` block, organized by section comments
(`Quick add`, `Board rendering`, `Analytics`, `Briefing`, `Settings`).
There's no build step: edit, save, refresh the browser.
