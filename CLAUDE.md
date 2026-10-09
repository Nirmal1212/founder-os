# CLAUDE.md

This repo is a library of Claude skills (`skills/founder-os-*/SKILL.md`), not an application.

## Layout
- `skills/<name>/SKILL.md` plus `references/` (frameworks) and `assets/` (templates). Folder name must equal frontmatter `name`.
- `examples/northwind-pulse/` is a fictional end-to-end sample. Keep its IDs consistent with `context.md`.
- `scripts/validate.py` is the quality gate. `skills/INDEX.md` is generated; never edit it by hand.

## Rules
- Run `python -I scripts/validate.py --write-index` after any skill change; it must report 0 errors.
- Keep SKILL.md under about 90 lines; push detail into `references/`. Descriptions must be 1024 characters or fewer.
- Every skill except `context` follows the context protocol and has a **Depends on / Feeds** line.
- Link every file in `references/` and `assets/` from its SKILL.md.
- Sample content must be marked ILLUSTRATIVE; never present invented numbers as real data.
- Commits: Conventional Commits, feature branches off main, no AI attribution lines unless the team decides otherwise.
