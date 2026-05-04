# Persistence Guidelines

> The CLI has no database. Persistent state is filesystem data.

## Overview

Trellis CLI stores state in user project files, not in a DB or ORM. Treat JSON,
Markdown, YAML, TOML, generated templates, and hash manifests as the persistence
surface.

The important rule is preservation: commands should update only managed files or
explicitly selected paths, and should preserve user-owned content wherever the
command contract says so.

## Persistence Surfaces

- `.trellis/.template-hashes.json`: source of truth for generated managed files.
- `.trellis/config.yaml`: package/workflow configuration.
- `.trellis/tasks/**`: task metadata, PRDs, and JSONL context files.
- `.trellis/workspace/**`: developer journals and indexes.
- Platform directories such as `.claude/`, `.codex/`, `.cursor/`,
  `.agents/skills/`, and `.github/copilot/`.
- `packages/cli/src/migrations/manifests/*.json`: versioned file manifests.

## File Access Patterns

- Use Node built-ins `fs` and `path` directly for local CLI operations.
- Use `fs.existsSync` before reading optional project files.
- Parse JSON inside `try/catch` when the file is user-controlled, returning a
  safe fallback for detection helpers.
- Prefer helpers when they already encode the contract:
  `writeFile` and `ensureDir` in `packages/cli/src/utils/file-writer.ts`,
  hash helpers in `packages/cli/src/utils/template-hash.ts`, and path constants
  in `packages/cli/src/constants/paths.ts`.

## Examples

`packages/cli/src/utils/file-writer.ts` is the canonical write path for normal
template output. It handles new files, identical content, `force`, `skip`,
`append`, and non-TTY fallback.

`packages/cli/src/commands/update.ts` defines `PROTECTED_PATHS` so update never
touches user-owned `.trellis/workspace`, `.trellis/tasks`, `.trellis/spec`,
`.trellis/.developer`, or `.trellis/.current-task`.

`packages/cli/src/utils/project-detector.ts` reads package metadata defensively:
missing or malformed `package.json`, `Cargo.toml`, `go.mod`, or `pyproject.toml`
falls through to another detector instead of crashing.

## Migration Rules

- Migrations must be idempotent. A missing file should usually become
  `skip-missing`, not a hard failure.
- Do not modify protected paths during update migrations.
- For structured config files, scrub or merge specific Trellis fields instead
  of replacing the whole file.
- Keep manifest paths POSIX-style and convert with helpers such as `toPosix`
  where needed.

## Forbidden Patterns

- Do not add a database, cache, or service dependency for CLI state unless the
  product explicitly changes architecture.
- Do not overwrite user-edited files without going through write mode,
  migration, or managed-block logic.
- Do not use ad hoc string replacement for structured JSON/TOML/YAML when a
  parser or existing scrubber helper is available.
