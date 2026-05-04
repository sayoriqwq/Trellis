# Hook Guidelines

> No React hooks. Custom browser behavior uses plain JavaScript.

## Overview

Docs-site does not define React components or React hooks. The only custom
browser behavior found in the repo is `terminal-demo.js`, loaded by `docs.json`.

## JavaScript Pattern

`docs-site/terminal-demo.js` follows a defensive DOM pattern:

- Find elements with `querySelector` / `querySelectorAll`.
- Check whether optional elements exist before using them.
- Use `MutationObserver` to initialize after Mintlify renders content.
- Store local control state on the wrapper element, such as `_descTimers`.
- Use event listeners for animation and click behavior.

## Rules

- Keep custom JS framework-free unless docs-site intentionally adopts a
  framework.
- Prefix feature-specific classes and query only within the feature wrapper.
- Guard every optional DOM query.
- Avoid global variables unless they are namespaced or scoped to an initializer.

## Examples

- `docs-site/terminal-demo.js` initializes only when `.td-wrap` exists and
  `wrap.dataset.init` is not set.
- `docs-site/terminal-demo.js` checks `if (body)` before adding scroll behavior.
- `docs-site/styles.css` defines matching `.td-*` classes for the script.

## Forbidden Patterns

- Do not add React `useEffect`, `useState`, or custom hooks to MDX.
- Do not assume Mintlify has rendered custom elements before the script runs.
- Do not attach broad event listeners without scoping to the feature wrapper.
