# Trellis CLI Frontend Guidelines

> The `trellis-sq` package currently has no runtime frontend.

## Overview

`packages/cli` is a command-line package. It does not render React components,
ship browser state, or own a web application. Frontend-related guidance here is
therefore mostly boundary guidance: do not invent UI patterns inside the CLI.

The only frontend-adjacent assets are generated templates, Markdown/MDX content,
and an existing TypeScript config with `jsx: "react-jsx"` for compatibility.

## Guidelines Index

| Guide | Description | Status |
|-------|-------------|--------|
| [Directory Structure](./directory-structure.md) | Frontend-adjacent assets and boundaries | Filled |
| [Component Guidelines](./component-guidelines.md) | No runtime components; generated content rules | Filled |
| [Hook Guidelines](./hook-guidelines.md) | No React hooks; plain function patterns | Filled |
| [State Management](./state-management.md) | CLI module state and persisted file state | Filled |
| [Quality Guidelines](./quality-guidelines.md) | Template/content quality checks | Filled |
| [Type Safety](./type-safety.md) | Strict TypeScript rules that apply if UI code is added | Filled |

## Pre-Development Checklist

- If a change is for CLI behavior, read the backend specs first.
- If a change edits templates under `packages/cli/src/templates/`, inspect the
  matching configurator and tests.
- If a change adds a real UI, treat that as a new architectural decision and
  create package-specific frontend specs for that UI.

## Core Rules Summary

- Do not add React runtime code to `packages/cli` for CLI prompts.
- Use `inquirer` for interactive terminal prompts, following existing command
  patterns.
- Keep template content as generated assets, not as executable frontend modules.
- Use TypeScript types and explicit return values for template render helpers.

**Language**: All documentation should be written in English.
