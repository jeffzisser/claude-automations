You are producing Jeff Zisser's QUARTERLY SELF-REVIEW as a Word document, drawn from his accumulated activity record.

CONTEXT
- Jeff is Chief Architect, CISO, and Compliance Officer at Xformative; reports to CEO Tom Torre; peer to CTO Dan Piltch. Domains: architecture, security, compliance.
- Sources (read both):
  1. /Users/jzisser/Documents/Claude/Projects/Daily Briefing/activity-ledger.json — structured activities with domain/status/dates/links (schema in briefing-process-v2.md).
  2. /Users/jzisser/Documents/Claude/Projects/Daily Briefing/accomplishments-log.md — weekly narrative rollups.
- Check the memory index at /Users/jzisser/Library/Application Support/Claude/local-agent-mode-sessions/e98744aa-9b43-4aaf-ae88-f6611fef0ac3/b621c73a-e5d3-41e4-9703-c0eea54821b8/spaces/34ee3f9b-97f1-4bb1-931c-7dfb4a3f4826/memory/MEMORY.md for people/org context.

THE QUARTER
- "Prior quarter" = the three months ending the day before this run (e.g. a 1 July run covers Apr–Jun). State the exact date range at the top.

WHAT TO DO
1. Read both sources. Collect every activity whose completed_on (done) or activity within first_surfaced..last_surfaced (in flight) falls in the quarter.
2. Build the document content FIRST (facts before formatting): organize by Jeff's three domains — Architecture, Security, Compliance (plus a short "Other / cross-functional" if needed). For each domain: a 2–4 sentence narrative of what was accomplished, then a bulleted list of concrete completed items (phrased as accomplishments) with dates, then a short "In progress / carried forward" list. Add an opening "Summary" with headline metrics (totals completed by domain) and a closing "Themes & focus for next quarter" drawn from what stayed open.
3. ONLY AFTER the content is assembled, read the docx skill at /var/folders/hz/klsdk2g17pg9724mg8fmz08r0000gq/T/claude-hostloop-plugins/59c9bf290d6d36bd/skills/docx/SKILL.md and build a clean, professional Word document. Title: "Quarterly Self-Review — <Qx YYYY> — Jeff Zisser". Save to /Users/jzisser/Documents/Claude/Projects/Daily Briefing/self-review-<YYYY>-Q<x>.docx.
4. Post a short Slack DM to Jeff (slack_send_message, channel_id U09A9HW3D47) noting the review is ready and where it is. If Slack fails, ensure the docx is saved.

Tone: factual, evidence-backed, achievement-oriented. Include source links where useful as evidence. This is a self-review Jeff will edit, so completeness and accurate dates matter more than brevity.
