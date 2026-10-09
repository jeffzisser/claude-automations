You are producing the weekly timesheet completion review for Jeff (jeff.zisser@gmail.com). Goal: ensure his MyIntervals timesheet for THIS WEEK (Monday–Friday in America/Chicago) is complete and ready to submit by 10 AM Monday morning. Do NOT log, modify, or delete any time entries. Do NOT submit the timesheet. The review is informational.

# Step 0 — Decide whether this run is FINAL or PROGRESS

1. Determine today's day of week in America/Chicago.
2. Compute the target week's Monday and Friday dates (America/Chicago).
3. Fetch Friday's calendar via `google-calendar:list_events` (startTime: midnight Friday CT, endTime: midnight Saturday CT, timeZone: America/Chicago). Look for an all-day or full-workday-window event titled "OOO" or "Jeff OOO" (or similar). Also check for US federal holidays on Friday.
4. Decide:
   - **THURSDAY + Friday is OOO/holiday:** produce FINAL REVIEW now. Treat Friday as 8.0h `pto`.
   - **THURSDAY + Friday is a normal workday:** produce a PROGRESS SNAPSHOT. Note the FINAL runs tomorrow.
   - **FRIDAY + today is OOO/holiday:** SKIP. Output one line: "Friday OOO — final was produced Thursday." Stop.
   - **FRIDAY + today is a normal workday:** produce FINAL REVIEW now.

# Step 1 — Load rules and context

1. Read `/Users/jzisser/Documents/Claude/Projects/XPS Time Tracking/timetracking-rules.md`. If missing, output a note and stop.
2. Call `myintervals:weekly_summary` with `week_offset=0` for per-day totals and submission status.
3. Call `myintervals:list_time` with `datebegin=<Mon YYYY-MM-DD>` and `dateend=<Fri YYYY-MM-DD>` for entry details.
4. Call `myintervals:list_activities` to verify aliases used.

# Step 2 — Per-day completeness check

For each weekday Mon–Fri:
- Sum logged hours for that day.
- If day total < 6h AND not PTO: call `google-calendar:list_events` for that day (timezone America/Chicago) and identify uncovered calendar meetings + workday-window gaps.
- If day has an all-day OOO event but no matching `pto` entry: flag.
- If day has zero entries and is a normal workday: flag as a **MISSED DAILY** — the daily review for that day was either never produced or never approved/logged. Capture the date for inline catch-up in Step 2.5.

# Step 2.5 — Inline catch-up daily review (for MISSED DAILY days)

For each prior weekday this week (strictly before today) flagged as MISSED DAILY in Step 2, produce a full daily-review-style block inline as part of this run's output. Use the same classification logic the daily timesheet review task uses (see `/Users/jzisser/Documents/Claude/Projects/XPS Time Tracking/timetracking-rules.md`):

1. Apply exclusion rules (declined events, transparent personal events, sub-10-minute fragments, HOLD blocks).
2. Classify each remaining event to an alias.
3. Round each entry up to nearest 0.5h, merge contiguous same-alias blocks, resolve overlaps with the tiebreakers in the rules file (flag conflicts).
4. Identify unaccounted workday-window gaps and mark them ⚠️ confirm — do not auto-fill.
5. Surface multi-hour optional / tentative / needsAction events as judgment items.

Today's date (the run date) is excluded from catch-up — its daily review will run tomorrow morning per the normal schedule.

# Step 3 — Weekly metrics

- Total logged hours vs 45–50h target
- Priority allocation: `soc2`, `xps1`, other — flag if soc2 or xps1 are well below the priority lean (soc2 should not lag dramatically behind xps1 per current priorities)
- Submission status from `weekly_summary` (open / submitted / approved)
- Compute MyIntervals submission URL: `https://tcbenterprise.timetask.com/time/index/384448/{year}/{ISOweek}/93445/`
  - Use the Monday of the target week to compute the ISO week number and year

# Step 4 — Format

For FINAL REVIEW:

```
# Weekly timesheet review — Week of {Mon Mon-DD} – {Fri Mon-DD}

**Total logged:** X.X hours (target 45–50h)
**Priority allocation:** soc2 X.Xh, xps1 X.Xh, other X.Xh
**Submission status:** {open/submitted/approved}
**Submit URL:** {URL}

## Daily totals

| Day | Date | Hours | Status |
|---|---|---|---|
| Mon | YYYY-MM-DD | X.X | ✅ or ⚠️ description |
| Tue | ... | ... | ... |
| Wed | ... | ... | ... |
| Thu | ... | ... | ... |
| Fri | ... | ... | ... |

## Catch-up daily reviews

(Only include this section if Step 2.5 produced any blocks. One subsection per MISSED DAILY date, in chronological order. Each subsection follows the daily review format: proposed entries table, items needing input, ready-to-log summary. End each subsection with: "Reply with corrections or 'approve {date}' to log this day's entries.")

## Action items before Monday 10 AM

- [Concrete punch list: missing entries, under-logged days, calendar items not yet logged, misclassifications, PTO confirmations needed]

## Ready to submit

- [Days/aliases that look complete]

---

Submit via the URL above once any action items are resolved.
```

For PROGRESS SNAPSHOT (Thursday, normal Friday ahead):

```
# Weekly timesheet snapshot — Week of {Mon} – {Fri} (Thursday preview)

**Mon–Thu logged so far:** X.X hours (target ~36h by EOD Thursday for a 45h week)
**Priority allocation MTD:** soc2 X.Xh, xps1 X.Xh, other X.Xh

## Daily totals (Mon–Thu)

[table]

## Catch-up daily reviews

(Only include this section if Step 2.5 produced any blocks. One subsection per MISSED DAILY date, in chronological order. Each subsection follows the daily review format: proposed entries table, items needing input, ready-to-log summary. End each subsection with: "Reply with corrections or 'approve {date}' to log this day's entries.")

## Heads-up for Friday's final

- [Any issues already visible: missing days, big gaps, misclassifications]

The final weekly review runs Friday at 4 PM CT.
```

# Step 5 — Deliver

1. Output the markdown as the chat message for this scheduled run.
2. Save a copy to `/Users/jzisser/Documents/Claude/Projects/XPS Time Tracking/reviews/weekly-{Friday-date YYYY-MM-DD}.md` for FINAL, or `reviews/weekly-{Friday-date}-preview.md` for SNAPSHOT. Create the `reviews/` directory if it doesn't exist.

# Error handling

- Calendar/MyIntervals fetch failure → brief note, stop.
- Rules file missing → note, stop.
- Save failure → still deliver inline, mention save failure.

# What this task explicitly does NOT do

- Does not log, modify, or delete time entries
- Does not submit the timesheet
- Does not auto-fix misclassifications
- Does not skip a normal Friday run
