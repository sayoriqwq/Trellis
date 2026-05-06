# Trellis SQ

This repository is `sayoriqwq`'s fork of the original
[mindfold-ai/Trellis](https://github.com/mindfold-ai/Trellis) project.

It is maintained as a personal customization and experimentation workspace for
adapting Trellis to `sayoriqwq`'s own AI-assisted development habits. The fork
keeps the Trellis workflow model, templates, agents, skills, task system, and
memory structure, but its default CLI command is `trellis-sq`.

## Scope

- Personal fork for custom Trellis behavior and local workflow changes.
- Main source package: `packages/cli`.
- Generated workflow surface: `.trellis/`, `.agents/`, `.codex/`, `.claude/`,
  `.cursor/`, `.opencode/`, `.pi/`, and related platform templates.
- The former `docs-site` and `marketplace` git submodules are intentionally not
  part of this fork's working tree.

## Command

The forked CLI exposes:

```bash
trellis-sq init -u your-name
trellis-sq update
trellis-sq uninstall
```

The internal Trellis workflow names, skill names, and generated platform entry
points still use the Trellis vocabulary unless a change explicitly says
otherwise. For example, skills such as `trellis-before-dev` and platform
commands such as `/trellis:finish-work` remain part of the local workflow
contract.

## Development

```bash
pnpm install
pnpm build
pnpm lint
pnpm typecheck
pnpm test
```

Useful package-scoped commands:

```bash
pnpm --filter trellis-sq build
pnpm --filter trellis-sq lint
pnpm --filter trellis-sq typecheck
pnpm --filter trellis-sq test
```

## Fork Notes

- Upstream project: <https://github.com/mindfold-ai/Trellis>
- Fork remote: <https://github.com/sayoriqwq/Trellis>
- Local modification log: [`change.md`](./change.md)

When syncing from upstream, treat `change.md` as the fork-local ledger. Append
new local decisions there instead of rewriting old entries.
