# Accessibility Quick Audit

Paste an HTML snippet or a full page's source and get a real client-side accessibility audit. The tool parses your HTML safely (it never executes it) and reports concrete WCAG-aligned issues with a severity, the offending element, the relevant success criterion, and a one-line fix. Everything runs in your browser with no external dependencies and works offline.

## Live demo

https://0xelitesystem.github.io/accessibility-quick-audit/

## Features

The audit covers these check categories, each mapped to a WCAG success criterion where one applies:

- **Images** (1.1.1): missing `alt` attribute (error), `alt` that is a filename or a generic word like "image" (warning), decorative `alt=""` noted for review (info).
- **Form controls** (1.3.1, 4.1.2): inputs, selects, and textareas with no associated label via `for`/`id`, a wrapping `<label>`, `aria-label`, or `aria-labelledby` (error); inputs missing a `type` (info); image inputs and buttons with no accessible name (error).
- **Headings** (1.3.1, 2.4.6): no `<h1>` on a full page (warning), multiple `<h1>` (info), skipped heading levels such as h2 to h4 (warning).
- **Landmarks and structure** (1.3.1, 2.4.2, 3.1.1): missing `<main>`, missing `lang` on `<html>`, missing or empty `<title>`, and multiple `<nav>` landmarks where one is unlabelled (warning).
- **Links** (2.4.4): empty link text or icon-only links with no accessible name (error); generic text like "click here" or "read more" (info).
- **ARIA** (1.3.1, 2.4.3, 4.1.2): invalid or nonexistent `role` values (error); `aria-*` attributes referencing an id that does not exist (error); redundant roles on native elements (info); positive `tabindex` (warning).
- **Tables** (1.3.1): data tables missing `<th>` header cells (warning) or `<th>` cells missing `scope` (info).
- **Media** (1.2.2): `<video>` and `<audio>` with no captions `<track>` (warning).
- **Color contrast** (1.4.3): when an element has both an inline `color` and `background-color`, the tool computes the WCAG contrast ratio and flags anything below 4.5:1 for normal text (warning).

Findings are grouped and sorted by severity, and you can toggle each severity on or off. A rough heuristic score (0 to 100) summarizes the result. A "load example" button fills the textarea with a deliberately flawed sample so the tool demonstrates itself.

## How it works

The pasted HTML is parsed with the browser's built-in `DOMParser` into an off-DOM document. The tool inspects that parsed tree only. It never injects the HTML into the live page and never evaluates any scripts, so pasting a page is safe. Each check walks the parsed tree, applies a heuristic tied to a WCAG success criterion, and records a finding with a truncated, escaped snippet of the element and a concrete fix. The color contrast check implements the WCAG relative-luminance formula and computes the ratio between the two lightness values.

## What it is not

This is a static heuristic linter, not a full WCAG conformance audit. It checks structure and markup patterns that can be detected from source alone. It cannot judge whether alt text is actually meaningful, whether reading order makes sense, whether focus is visible, whether contrast holds for text styled by external CSS, or whether an interaction works with a keyboard. It does not replace manual testing, real keyboard navigation, or a screen reader. A clean report here does not mean a page is accessible. Treat it as a fast first pass that surfaces the obvious, machine-detectable problems.

## Privacy

The HTML you paste is processed entirely in your browser and is never sent to any server. There are no analytics, no tracking, and no network requests. You can verify this by viewing the page source or by opening your browser's developer tools and watching the network tab while you run an audit.

## License

MIT. Copyright 0xelitesystem 2026.
