# memory/

Not yet exported. Five task prompts read a people/org context file at:

    ~/Library/Application Support/Claude/local-agent-mode-sessions/e98744aa-9b43-4aaf-ae88-f6611fef0ac3/b621c73a-e5d3-41e4-9703-c0eea54821b8/spaces/34ee3f9b-97f1-4bb1-931c-7dfb4a3f4826/memory/MEMORY.md

That location belongs to the Claude desktop app's own data for the source
account, so it could not be read during the export and will likely not exist
under another account.

To finish the export:

1. Copy that `MEMORY.md` (and any files it links to) into this folder.
2. Pick a stable home for it outside the app's data, e.g.
   `~/Documents/Claude/Projects/Daily Briefing/MEMORY.md`.
3. Update the path in the five prompts that reference it (see
   `local_paths_in_prompt` in each `task.yaml`).
