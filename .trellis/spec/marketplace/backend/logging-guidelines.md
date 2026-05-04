# Logging Guidelines

> Marketplace has no runtime logger.

## Overview

Marketplace is static content. Logging is limited to validation commands, CLI
fetcher errors when Trellis consumes the registry, and review notes.

## Rules

- Do not add scripts whose only purpose is ad hoc logging.
- Keep troubleshooting and prerequisites in README or skill docs.
- If adding validation scripts later, make their output concise and
  machine-actionable enough for CI.

## Examples

- `marketplace/README.md` documents manual installation and `npx skills add`
  usage instead of relying on runtime output.
- `marketplace/skills/cc-codex-spec-bootstrap/SKILL.md` includes quick-check
  commands for required tools.
- CLI-side registry errors are classified in
  `packages/cli/src/utils/template-fetcher.ts`, not in marketplace content.

## Forbidden Patterns

- Do not add permanent debug output to example code in templates.
- Do not introduce a service logger or telemetry dependency.
- Do not hide validation requirements in comments only.
