# claude-automations

Source of truth for Jeff's Claude scheduled tasks and custom skills, kept
outside any one Claude account so they can be recreated after an account move.

Exported 2026-10-09 from the personal Claude account. Keep this repo private:
the prompts contain work context, colleague names and internal identifiers.

## Layout

| Path | What it is |
|---|---|
| `tasks/<task>/prompt.md` | The task's prompt, verbatim |
| `tasks/<task>/task.yaml` | Name, schedule, folder, approval setting, connectors, local paths |
| `skills/<skill>/SKILL.md` | Custom skills, verbatim |
| `memory/` | Placeholder for the people/org context file (not yet exported) |
| `RESTORE.md` | How to recreate everything on another account |

## Tasks

| Task | Schedule (America/Chicago) | Connected folder | Connectors the prompt uses |
|---|---|---|---|
| [Daily gmail cleanup](tasks/daily-gmail-cleanup) | Weekdays 5:30 am | Daily Briefing | Gmail, Slack, Google Calendar, HubSpot, myintervals |
| [Daily briefing](tasks/daily-briefing) | Weekdays 6:00 am | Daily Briefing | Gmail, Slack, Google Calendar, Asana |
| [Workstream pm check](tasks/workstream-pm-check) | Weekdays 6:30 am | none attached (prompt writes to Workstream PM) | Slack, Google Calendar, Google Drive, Asana |
| [Daily timesheet review](tasks/daily-timesheet-review) | Weekdays 2:00 pm | XPS Time Tracking | Gmail, Google Calendar, myintervals |
| [Weekly timesheet completion](tasks/weekly-timesheet-completion) | Thu and Fri 4:00 pm | XPS Time Tracking | Gmail, Google Calendar, myintervals |
| [Weekly activity rollup](tasks/weekly-activity-rollup) | Fri 3:00 pm | Daily Briefing | Slack |
| [Quarterly self review](tasks/quarterly-self-review) | 1st of Jan, Apr, Jul, Oct, 8:00 am | Daily Briefing | Slack |

The "connectors the prompt uses" column is a keyword match against each
prompt, so treat it as a starting point. `task.yaml` also lists every
connector that was attached on the source account.

## What is not in this repo

- **Run history.** Past runs are sessions owned by the source account and
  cannot be exported.
- **Working data.** The tasks keep their own record in files on the Mac under
  `~/Documents/Claude/Projects/` (`Daily Briefing/activity-ledger.json`,
  `Daily Briefing/accomplishments-log.md`, `XPS Time Tracking/reviews/`,
  `XPS Time Tracking/timetracking-rules.md`, `Workstream PM/`). Those folders
  are independent of the Claude account. Back them up separately if wanted.
- **The memory file.** See `memory/README.md`.
- **Connector sign-ins.** These never transfer; reconnect on the new account.
- **Tasks stored only in the desktop app**, if any. This export covers the
  account's cloud scheduled tasks.

## Known issues to fix before or during a move

1. Five prompts hard-code a `MEMORY.md` path inside the desktop app's data for
   the source account. See `memory/README.md`.
2. All prompts use absolute paths under `/Users/jzisser/`. They work on the
   same Mac and break on another machine or username.
3. `Workstream pm check` has no folder attached and its approval setting is
   the default (asks before acting), unlike the other six (automatic), yet its
   prompt writes to `Workstream PM/`.
4. `skills/daily-briefing` is an older version of the `tasks/daily-briefing`
   prompt (no activity-tracking loop). The task prompt is the current one.

## Keeping this current

When a task's prompt or schedule changes in Claude, ask Claude to "re-export
my scheduled tasks to claude-automations" and commit the diff.
