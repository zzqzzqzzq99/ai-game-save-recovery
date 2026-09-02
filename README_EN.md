# AI Game Save Recovery Playbook

English | [简体中文](README.md)

**Recover overwritten or corrupted single-player game saves with a local AI agent—using evidence, not guesswork.**

> Preserve first. Reconstruct the timeline. Test candidates safely. Write only with approval.

This is an incident-recovery method, not another save manager and not a save editor.

## The idea in 30 seconds

After a cloud overwrite, players often relaunch the game, toggle sync, and copy files at random. Those actions may destroy the last recoverable versions.

A safer workflow is:

1. Quit the game and launcher immediately.
2. Let a local AI agent inventory save files, rotating backups, indexes, and sync logs in read-only mode.
3. Reconstruct which device wrote, uploaded, or downloaded each candidate version.
4. Preserve and test candidates before replacing the smallest possible set of files—with explicit player approval.

The useful insight is not a complicated command. It is treating an AI agent as an incident investigator and careful operator, rather than asking it to blindly edit a save.

## What this can help with

- Steam Cloud or another sync service overwrote newer local progress.
- A crash, update, or mod change left a save corrupted.
- A game kept rotating backups, temporary files, indexes, or logs but has no recovery UI.
- Character and world slots became mismatched.
- A local configuration or data bug can be investigated from files and logs.

## What this does not cover

- Competitive multiplayer, leaderboards, trading, online economies, or anti-cheat systems
- Server-authoritative data or another player's files or shared world
- DRM, access-control, encryption, or signature bypass
- Fabricating online achievements or records
- Blind write attempts when no rollback copy exists

A game marketed as “single-player” may still use online services. Stop if a change could affect another player, a shared service, or an online record.

## The six-phase protocol

1. **Freeze** — Quit processes and pause sync before more writes occur.
2. **Snapshot** — Copy relevant saves, caches, indexes, and logs; record hashes.
3. **Discover** — Search bounded, game-related locations for candidate versions.
4. **Reconstruct** — Build a timeline from user memory, session logs, sync events, metadata, and file relationships.
5. **Validate** — Parse copies when possible; otherwise test one candidate at a time offline.
6. **Restore** — Make another safety backup, replace the minimum file set, verify in game, and only then reconsider cloud sync.

Read the [full protocol](docs/protocol.md). The [agent task template](templates/agent-task.md) separates read-only investigation from write authorization.

## Evidence hierarchy

From strongest to weakest:

1. Repeatable in-game state
2. Explicit game or launcher events for exit, upload, download, and version changes
3. Internal save metadata and slot/index relationships
4. Hashes, sizes, timestamps, and rotation order
5. Player memory of time, level, quest, or location
6. A guess based only on a filename or “latest modified” timestamp

The agent should label facts, inferences, and unknowns separately.

## Case study

The [Enshrouded Steam Cloud overwrite case](cases/enshrouded-cloud-overwrite.md) is based on a real recovery: a lower-level character state from another computer overwrote newer local progress. Account identifiers, usernames, absolute paths, IP addresses, hashes, raw logs, and save files are excluded.

## Privacy and safety

- Search confirmed game-related paths first; do not start with an unbounded full-disk scan.
- Keep original saves and logs local by default.
- Run generated commands in read-only or preview mode first.
- Require separate approval for overwrite, rename, deletion, upload, download, or sync.
- Publish only fictional, public, or thoroughly de-identified cases.

## Relationship to save managers

Tools such as [Ludusavi](https://github.com/mtkennerly/ludusavi), [OpenSave](https://github.com/Liquid-co/OpenSave), and other save managers are valuable for prevention and versioned backups. This playbook focuses on investigation after an incident, including cases where no backup tool was installed beforehand. See the [upstream assessment](docs/upstream-assessment.md).

## Contributing

Reproducible failure cases are as valuable as successful recoveries. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before sharing a case. Never submit real saves, full logs, account IDs, personal paths, tokens, or another person's data.

## License and status

The text, process, templates, and de-identified case study are licensed under [CC BY 4.0](LICENSE).

`v0.1-draft`: the method and first case study are complete, but there is no external reproduction report yet. The project does not claim universal compatibility with every game, launcher, or save format.

Enshrouded and Steam are names or trademarks of their respective owners. This independent community project is not affiliated with, sponsored by, or endorsed by the game's developer or publisher, Valve, or Steam.
