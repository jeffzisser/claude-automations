# Restoring on another Claude account

These steps are written so that Claude on the new account can carry them out.
Open a session there with this repo attached and say: "Follow RESTORE.md."

## Before you start

1. On the **old** account, pause all seven tasks so nothing runs twice.
2. On the **new** account, connect the connectors listed in the README table.
   On an organization account, some custom connectors may need admin approval.
3. `myintervals` is a local MCP server on the Mac, used by the two timesheet
   tasks and the gmail cleanup. It must be configured in the desktop app that
   the new account is signed in to.
4. Open the Claude desktop app on the Mac under the new account, so tasks that
   need the computer can be bound to it.
5. Resolve the memory file path (`memory/README.md`) and update the prompts.

## For each folder under `tasks/`

Create one scheduled task using `task.yaml` and `prompt.md`:

- **Name:** `name`
- **Schedule:** `schedule`, exactly as written (it carries its own time zone)
- **Prompt:** the full contents of `prompt.md`, unchanged
- **Needs the computer:** yes when `requires_local_computer` is true
- **Folders:** each entry under `folders`. Confirm the folder exists first.
- **Approval:** `approval: "auto"` means runs go ahead without waiting.
  Claude cannot request this when creating a task; after creation, switch the
  task to automatic approval in its settings if the organization allows it.

Create them paused or check the first run of each by hand before leaving them
unattended. Several of them send Slack messages, change Gmail and write
timesheet entries.

## Skills

For each folder under `skills/`, ask Claude to "add this as a skill" and save
the proposal it shows. Skills do not migrate between accounts on their own.

## After restoring

- Run each task once and compare its output with the last file it wrote under
  `~/Documents/Claude/Projects/`.
- Delete the paused tasks on the old account once the new ones are confirmed.
