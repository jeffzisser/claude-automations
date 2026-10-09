You are producing Jeff Zisser's WEEKLY ACTIVITY ROLLUP from the daily-briefing activity ledger. This is a status/accomplishments summary, not a task list.

CONTEXT
- Jeff is Chief Architect, CISO, and Compliance Officer at Xformative. His domains: architecture, security, compliance.
- Source of truth: /Users/jzisser/Documents/Claude/Projects/Daily Briefing/activity-ledger.json (schema in briefing-process-v2.md, same folder). Each activity has: title, domain, source, source_links, status (open/done), first_surfaced, last_surfaced, completed_on.
- Check the memory index at /Users/jzisser/Library/Application Support/Claude/local-agent-mode-sessions/e98744aa-9b43-4aaf-ae88-f6611fef0ac3/b621c73a-e5d3-41e4-9703-c0eea54821b8/spaces/34ee3f9b-97f1-4bb1-931c-7dfb4a3f4826/memory/MEMORY.md for people/project context.

WHAT TO DO
1. Read activity-ledger.json. Define "this week" = Monday through today.
2. Bucket activities by domain (architecture / security / compliance / other). Within each domain split into:
   - Completed this week (status done, completed_on within this week)
   - Still in flight (status open) — include age (days since first_surfaced)
3. Append a dated section to a running log at /Users/jzisser/Documents/Claude/Projects/Daily Briefing/accomplishments-log.md (create it if missing, newest section at top under a top heading). The section header is the week range (e.g. "Week of Mon 6/8–Fri 6/12"). Under it, the by-domain breakdown with one concise line per activity and its source link(s). This file is the cumulative record the quarterly self-review reads — never overwrite prior weeks, only prepend the new week.
4. Post a SHORT Slack DM to Jeff (slack_send_message, channel_id U09A9HW3D47): "*Weekly rollup — <week range>*" then a 3–6 line summary: counts (X completed, Y in flight) and the 2–3 most significant accomplishments by domain. Link the accomplishments-log.md path at the end. Keep it under ~1500 chars. If Slack fails, just ensure the markdown file is written.
5. If the ledger has no activity this week, write a one-line "quiet week" entry to the log and send a one-line Slack note. Never skip silently.

Be concise and outcome-focused — this is the raw material for performance reviews, so phrase completed items as accomplishments ("Delivered…", "Closed…", "Approved…"), not as chores.
