---
id: C:/GIT/format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/memory_procedural.md
type: memory
title: Acrobat Pdfl Sdk Procedural Memory
name: memory_procedural
description: Harness/procedural lessons rewritten from candidate-memory.md
resource: /format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/memory_procedural.md
resource_root: C:/GIT
author: brogers
tags: [format-conversion, dev.adobe.com-rst2md-project, acrobat-pdfl-sdk]
domain: content
tokens: 264
generated: {by: 'human:brogers', at: '2026-09-20T13:18:01-04:00'}
okf_version: '0.2'
memory: procedural
---
# Procedural Memory

## 1. `~/.gitignore_global` silently ignores every `tests/` directory
Line ~93 has a bare `tests/`, matching any repo. A new `tests/` folder shows as fully clean in `git status` — not even `??`. Diagnose with `git check-ignore -v <path>`; commit with `git add -f`.

## 2. MkDocs Material: `navigation.prune` + `navigation.tabs` for per-document nav isolation
`navigation.prune` alone only trims grandchildren of inactive sections — all top-level document names still render in the same sidebar (136 → 38 labels, but books still listed together). `navigation.tabs` moves top-level `nav:` sections into a top tab bar, leaving the sidebar showing only the active document's tree. Use both.

## 3. Grepping generated HTML is not proof of what a responsive theme shows
Material (and any CSS-checkbox collapsible nav) emits the FULL nav tree into the DOM for accessibility/no-JS/mobile, so a text search finds every document name regardless of visibility. Confirm nav-visibility fixes by rendering in a real browser over `http.server` (not `file://`, which some sandboxes block) and screenshotting.
