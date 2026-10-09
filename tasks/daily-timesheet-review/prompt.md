You are producing a daily timesheet review for Jeff (jeff.zisser@gmail.com). The goal is to suggest MyIntervals time entries for **yesterday** based on his Google Calendar, the project's classification rules, and current priorities. **Do NOT log time to MyIntervals during this run.** Logging happens later, in a chat where Jeff replies to the review with corrections or approval.

# Step 1 — Determine the target date

The target date is **yesterday in America/Chicago**. If yesterday was a weekend (Saturday or Sunday) or a US federal holiday, produce a single brief note ("No review — weekend/holiday") and stop. Federal holidays include New Year's Day, MLK Day, Presidents' Day, Memorial Day, Juneteenth, Independence Day, Labor Day, Columbus Day, Veterans Day, Thanksgiving, and Christmas.

# Step 2 — Load the rules

Read `timetracking-rules.md` from the XPS Time Tracking project knowledge. If not accessible there, fall back to reading `/Users/jzisser/Documents/Claude/Projects/XPS Time Tracking/timetracking-rules.md`.

The rules file defines: priority projects, workday window (7AM–6PM CT), rounding (round up to 0.5h, min entry 0.5h), classification by event title, tiebreakers for overlaps (seniority first — Dan Rashke and Tom Torre, then Jeff-organized, smaller, required, project-specific), gap-fill logic (never auto-fill, always ask), all-day "OOO"-titled event handling (propose 8h pto and exclude inside meetings), exclusions, judgment-call events (including `needsAction` — include tentatively, flag for confirmation), and sanity checks.

**The rules file is authoritative.** If it conflicts with anything in this prompt, the rules file wins. If the rules file is missing from both locations, output a single note saying so and stop.

# Step 3 — Load supporting context

Call each of these and stop with a brief error note if any fails:

1. `myintervals:list_activities` — verify alias names are still valid
2. `myintervals:list_time` with `date=<target date YYYY-MM-DD>` — detect entries already logged manually for the target date (must not propose duplicates)
3. `myintervals:list_time` with `datebegin=<Monday of current week YYYY-MM-DD>` and `dateend=<day before target date YYYY-MM-DD>` — week-to-date hours and priority allocation. If target date is Monday, this step returns empty (no week-to-date data).
4. `google-calendar:list_events` for the target date:
   - `startTime`: midnight target date in America/Chicago (e.g., `2026-05-22T00:00:00-05:00`)
   - `endTime`: midnight day-after target date
   - `orderBy`: `startTime`
   - `pageSize`: 250
   - `timeZone`: `America/Chicago`

When parsing calendar events, trust the UTC offset in each `dateTime` field over the `timeZone` label, because Google Calendar may mix labels (events scheduled in NY may appear with NY label but the dateTime is normalized to the requested timezone).

# Step 4 — Apply exclusions

Drop events matching the rules file's exclusion list:
- Declined events (`responseStatus: declined`)
- Personal events with `transparency: transparent`
- Events outside the 7AM–6PM CT workday window unless clearly work
- Events under 10 minutes with no adjacent block
- Standing "HOLD" blocks unless work clearly happened (flag if unclear)

# Step 5 — Build the entry list

For each remaining event:
1. **All-day OOO check first.** If an all-day or full-workday-window event titled "OOO" or "Jeff OOO" (or similar) is present and covers the 7AM–6PM window, propose a single 8.0h `pto` entry for the day and **exclude all other events that fall inside the OOO block**, even if `responseStatus: accepted`. Skip steps 5.2–5.6 for that day and go straight to step 7. If only part of the day is OOO, propose `pto` for that portion and process the rest of the day normally.
2. Apply classification rules from the rules file to assign an alias.
3. Round duration up to the nearest 0.5h (minimum entry 0.5h).
4. Merge contiguous same-alias blocks into single entries.
5. Resolve overlapping events using rules-file tiebreakers (seniority → Jeff-organized → smaller → required → project-specific). Log the winner, note the conflict for the review output.
6. Flag events needing judgment (multi-hour optional, `responseStatus: needsAction`, OOO partial, half-attended, etc.). For `needsAction`: include the event tentatively per the normal rules but ALWAYS list it in the "Items needing your input" section.

# Step 6 — Identify gaps and fill questions

Find unaccounted time in the 7AM–6PM CT window. **Never auto-fill gaps.** For each gap (including before-first-meeting, between-meeting, and after-last-meeting time), surface it in the review with a suggested allocation:
- Default suggestion: split between `soc2` and `xps1`, weighted toward whichever is behind weekly target. If week-to-date is empty, split 50/50.
- Lunch hour (typically around 12:00–13:00) — flag and ask whether to leave unbilled or absorb.

If proposed entries from steps 5.2–5.6 total less than 6h on a non-PTO day, the gap-fill question applies to the full unaccounted portion.

# Step 7 — Sanity checks

Before producing the review:
- Day total between 6 and 12 hours (unless PTO)
- All aliases used exist in `list_activities` output
- PTO entries non-billable
- No conflict with already-logged entries (from step 3.2) — if entries exist, do not propose duplicates; show the existing entries and offer to add/correct
- Weekly total trending toward 45–50h
- Priority allocation roughly on target

# Step 8 — Format and deliver

Produce a markdown review with this structure:

```
# Daily timesheet review — [Day, Date]

**Day total:** X.X hours (target 6–12h)
**Week-to-date:** X.X hours (target 45–50h)
**Priority allocation week-to-date:** soc2 X.Xh, xps1 X.Xh, other X.Xh
**Existing entries for [date]:** [none / list]

## Proposed entries

| Time (CT) | Event/Block | Hours | Alias | Notes |
|---|---|---|---|---|
| ... | ... | ... | ... | ... |

## Items needing your input

- [conflicts, judgment calls, gap-fill questions, needsAction flags]

## Ready to log on approval

[concise summary list of proposed entries with alias and hours]

---

Reply in this project with corrections or "approve" to log everything as proposed. Reply "skip" to dismiss the review.
```

For quiet days (no gaps, conflicts, or judgment calls), use the compact format from the project task definition.

**Deliver the review two ways:**
1. Output the markdown as the chat message for this scheduled run (this is the primary delivery)
2. Save a copy to `/Users/jzisser/Documents/Claude/Projects/XPS Time Tracking/reviews/YYYY-MM-DD.md` using the target date for the filename (create the `reviews/` directory if it doesn't exist)

# Step 9 — End

Do not log time. Do not modify or delete any existing time entries. End the task after delivering the review. Jeff will open the review in a chat within this project and reply with corrections or "approve" to trigger logging via a separate chat session.

# Error handling

- Calendar fetch fails → brief note saying so; stop.
- MyIntervals fetch fails → brief note saying so; stop.
- Rules file missing from both locations → note that the rules file wasn't found; stop.
- Tool returns unexpected schema → surface the issue rather than retrying blindly.
- File save fails → still deliver the markdown inline; mention the save failure.
