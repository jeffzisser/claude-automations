---
name: pr-to-asana
description: "Create an Asana task in Platform Operations from a GitHub pull request, or reconcile an existing task against its PR, and link the two. Use when Jeff names a PR and asks for a task, asks to file/track/link a PR in Asana, or asks whether a PR and its task still agree. Covers the xformative and xps-management GitHub orgs. Do not use for filing backlog items that have no PR behind them."
---

# PR to Asana task

Jeff Zisser (Chief Architect / CISO / Compliance Officer at Xformative) files platform work in
Asana against pull requests. The task and the PR are two views of one piece of work; they are
linked in both directions and they must not disagree.

## Locations

**Asana** — workspace `700151736839330`, project **Platform Operations** `1213005514655412`.
Not "Platform Engineering," which is the *team* (`1213005514655408`).

Sections: Backlog `1213005628097851` · To do `1213005628097848` · In progress
`1213005628944074` · Done `1213005628944071` · Canceled `1213005514655413`

Custom fields: **PLAT1** `1213005628093859` (text, workflow-assigned — never set it) ·
**Item Priority** `1214754024811346` (enum: Critical `1214754024811347`, High
`1214754024811348`, Medium `1214754024811349`, Low `1214754024811350`)

**GitHub** — platform infrastructure lives in the **`xps-management`** org
(`platform-infrastructure`, `platform-docs`, `platform-access-control`,
`github-platform-config`, `management-compliance`). Application repos live in **`xformative`**.
Both orgs exist; guessing wrong wastes a whole exchange. Search across both before concluding a
repo or PR does not exist.

## Task structure

Every Platform Operations task follows the same shape. Match it exactly — plain text in `notes`,
not HTML, not Markdown.

```
Priority: Medium

DESCRIPTION
Prose. What the change does, then why it is needed. Name the concrete
blocker or defect, not a category.

---
ACCEPTANCE CRITERIA
1. Numbered. Verifiable. Each one a thing someone could check.

DONE WHEN
1. Numbered. The completion condition, not a restatement of the criteria.

NOTES
Open questions, deliberate exclusions, priority justification, related
tickets.

DOCS
Doc paths this ticket writes or updates.
```

`SOURCE` replaces `DOCS` when the item came out of a review or meeting. Both are optional; the
first four blocks are not.

House conventions worth preserving:

- **The priority line is repeated in the notes** even though Item Priority is a real field.
- **Justify a High or Critical against the operating model** (`docs/01-foundation/operating-model.md`)
  and invite correction: "Priority set to High — … Correct me if that's overweighted."
- **Name what is deliberately out of scope.** Tasks here routinely say "not fixed here, file
  separately" or "explicitly out of scope for this ticket."
- **Leave open questions open.** "Open question, not yet decided:" is normal and preferred over
  a guess presented as a decision.
- Emoji priority prefixes (🔴 🟠 🟡) appear on some names. They are inconsistent across the
  project — follow whatever Jeff has used most recently rather than introducing them.

## Workflow

1. **Find the PR.** `search_pull_requests` with `repo:owner/name <term>`. Read the body and, when
   the description is thin, the diff.

2. **Check for an existing task** before creating one. `search_tasks` on distinctive terms from
   the PR. A null result does not prove absence — `search_objects` with `resource_type=task` in
   particular returns nothing for repo-name queries even when a task exists.

3. **Reconcile PR and task content.** These are two views of one change, so they must agree on
   scope, on what was deliberately excluded, and on what remains unapplied. Where they differ,
   ask which one is right rather than silently propagating one into the other — the PR body is
   usually more current on mechanics, the task on priority and follow-ups.

4. **Draft, then create.** Show Jeff the draft before creating unless he has already approved
   the content. Section by state: open PR awaiting review or apply → In progress; merged and
   applied → Done; not started → Backlog or To do.

5. **Retrieve PLAT1.** Poll `get_task` after creation. It is assigned by an Asana workflow rule,
   sometimes within seconds and sometimes not for several minutes. If it is still null after two
   polls, hand Jeff the task URL and say the ID has not landed yet rather than waiting further.

6. **Link both directions.**
   - Asana → PR: a `PR` block in the notes holding the PR URL.
   - PR → Asana: the task permalink on its own line under `### Description` in the PR body. A
     GitHub Action picks the URL up from there and creates the link. A comment is the fallback
     when the body cannot be edited.

## Access limits

The GitHub MCP integration authenticates as `jeffzisser`. Read tools are confirmed; write tools
(`add_issue_comment`, `create_pull_request_review`) are not.

**`xps-management` has OAuth App access restrictions enabled.** The search API works against it,
but every REST call — `get_file_contents`, `pull_request_read`, anything that posts — returns
403. In practice: PRs in that org can be found and read through search, and the PR-side half of
the link has to be done by Jeff by hand until the app is approved for the org
(Settings → Third-party Access). Say so plainly and hand him the exact text to paste; do not
report the link as complete when only the Asana half landed.

If the GitHub server returns a device-authorization code instead of results, that is its own
auth flow. Give Jeff the code and the URL and stop — it is his to complete, not something to
work around.

## Asana connectivity

`get_me` succeeds even when other Asana tools are blocked behind per-tool approval prompts. Use
it to check connectivity before concluding the integration is down.
