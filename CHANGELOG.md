# Changelog

## 2.5.1 — November 2026
- Messages between agents on the same machine never go through git: they are written straight to a local mail folder next to roam.json, with no pull, push or commit (about 5 s before, now a file write).
- Every machine keeps its own copy of every message it sends or receives, outside git. Git is only the delivery route between machines.
- Acking or handling only same-machine mail no longer triggers a git sync.
- macOS (Apple Silicon) and Linux x64 preview builds are now attached to each release. See docs/INSTALL-MAC-LINUX.md.

## 2.5.0 — November 2026
- Search stays light on big, old histories: the index reads old diaries one file at a time and no longer keeps whole files in memory. On a 4.8 GB history, building the index went from over 4 GB of RAM to 1.2 GB (78 s), and reading results for a very common word from over 3 GB to 1.5 GB.
- Showing one old session reads only that session's bytes, not the project's whole diary.
- The first search after updating rebuilds the index once.

## 2.4.9 — November 2026
- Search inside OpenCode reads the same local index as the CLI: on a 4.8 GB history, 90 s → 1–3 s for a rare word, 145 s → about 8 s for a very common one, with the same results.
- Building the index takes about a quarter of the memory.
- Fix: sessions captured since 2.4.7 no longer resume with a false "no user prompts found" warning, and search labels include their opening request again.
- Fix: `roam daemon` runs commands sent from the same machine and no longer deletes messages between two agents on one machine.
- Fix: `roam inbox --ack` no longer ends in "commit failed" on a machine that never quarantined a message.

## 2.4.8 — November 2026
- Fast search and resume: an incremental local index instead of pulling and rescanning every time (47 s → under a second for rare words on a 4.8 GB history). `--fresh` pulls first.
- macOS and Linux preview builds (CI only; no public installer yet).
- Optional extras grouped as Labs in `roam --help`.
- Fix: two voice memos made in the same millisecond no longer overwrite each other.

## 2.4.7 — November 2026
- Append-only session storage: each capture adds only its new text to git, instead of saving the whole diary again.
- Honest sync: failed saves are reported and retried, stale git locks clear themselves, and large backlogs push in batches.
- Commits stay scoped to their own files.
- Wider secret scrubbing (29 credential patterns).
- Pro features enforced consistently in the CLI, the MCP tools and the OpenCode plugin.
- OpenCode 2.x: edited files are listed again in every handoff.
