# Contributing

## Add a skill
1. Create `skills/founder-os-<role>/SKILL.md` with frontmatter `name` (equal to the folder) and `description` (1024 characters or fewer).
2. Write the description as: role, what it produces, "Use this skill whenever..." trigger phrases, then a "Not for:" line naming neighbouring skills.
3. Body structure: persona intro, **Depends on / Feeds** line, context protocol, steps or modes, delivery format, quality bar ("what makes this senior rather than junior").
4. Put frameworks in `references/` and templates in `assets/`; link each from SKILL.md.
5. Add the skill to a group in `scripts/validate.py` (`GROUPS`) and run `python -I scripts/validate.py --write-index`.
6. If it joins the product chain, extend the sample in `examples/northwind-pulse/`.

## Quality bar
Opinionated guidance, explicit modes, checkpoints between stages, and unhappy paths called out. No invented statistics.

## Workflow
Branch from main as `feature/<topic>`, use Conventional Commits (`feat:`, `fix:`, `docs:`), update `CHANGELOG.md`, and keep `validate.py` clean.
