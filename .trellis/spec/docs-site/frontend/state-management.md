# State Management

> Docs-site state is navigation config, route/version selection, and small DOM
> interaction state.

## Overview

There is no app-level client state library. State belongs in Mintlify config,
URLs, or local DOM behavior.

## Navigation State

`docs-site/docs.json` owns:

- language selection: English and Chinese
- version selection: `RC` and `Release`
- navigation groups and page ordering
- redirects from old URLs
- navbar links and global anchors

When moving or adding pages, update this file deliberately.

## Interaction State

`docs-site/terminal-demo.js` keeps local state for:

- visible terminal lines
- progress dots
- timeline fill
- description timers
- manual vs autoplay mode

That state is scoped to `.td-wrap` and should not leak to the rest of the page.

## Examples

- `docs-site/docs.json` marks the RC version as default for both English and
  Chinese navigation.
- `docs-site/terminal-demo.js` stores timer IDs on `wrap._descTimers` and clears
  them before scheduling new description transitions.
- `docs-site/styles.css` uses CSS animation delays as declarative state for the
  terminal demo timeline.

## Forbidden Patterns

- Do not add Redux, Zustand, React Context, or another app state library.
- Do not store docs navigation in multiple unsynchronized config files.
- Do not let custom demo state affect unrelated Mintlify pages.
