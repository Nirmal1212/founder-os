# Changelog

## [Unreleased]
### Changed
- Renamed the project to founder-os and and dropped the `nirmal-ai-` skill prefix (plugin namespacing gives `/founder-os:pm`).
- `pm`, `architect` and `design-artifacts` now follow the context read-then-write protocol.
- Added **Depends on / Feeds** lines and "Not for:" boundaries to descriptions to reduce trigger overlap.
- Normalized line endings to LF.

### Fixed
- Removed the reference to a nonexistent `codegen` skill from `metrics`.
- Linked the orphaned persona template from `research`.
- Shortened the `architect` description to stay within the 1024-character limit.

### Added
- Claude Code plugin and marketplace manifests in `.claude-plugin/` (install via `/plugin`).
- README, CLAUDE.md, CONTRIBUTING.md, generated `skills/INDEX.md`.
- `scripts/validate.py` quality gate.
- `examples/northwind-pulse/`: a fictional end-to-end sample.

## [0.1.0]
- Initial 14 skills.
