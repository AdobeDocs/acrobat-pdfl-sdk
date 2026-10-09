---
id: C:/GIT/format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/memory_workspace.md
type: memory
title: Acrobat Pdfl Sdk Workspace Memory
name: memory_workspace
description: Project-specific implementation lessons rewritten from candidate-memory.md
resource: /format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/memory_workspace.md
resource_root: C:/GIT
author: brogers
tags: [format-conversion, dev.adobe.com-rst2md-project, acrobat-pdfl-sdk]
domain: content
tokens: 1239
generated: {by: 'human:brogers', at: '2026-09-20T13:17:51-04:00'}
okf_version: '0.2'
memory: project
---
# Workspace Memory

## 1. A caption glued to a grid-table border silently breaks docutils
With no blank line between a caption and a `+---+` top border, docutils merges caption and whole table into one paragraph — no error, no warning; the markdown then shows raw RST as prose with smart-quote damage. Fixed in `1rst2md.py`'s `_fix_rst_grid_tables` (insert a blank line whenever a grid-table delimiter follows a non-blank line).

## 2. `output_md/source/` mixes generated files with committed static assets
`css/`, `js/`, `images/`, `.claude/settings.local.json` are hand-maintained and recreated by no script. If you `git rm`/`git clean` that directory, `git checkout HEAD -- <asset paths>` afterwards. (The old `2rename-files.py` non-idempotency that motivated such cleanups is fixed: `1rst2md.py` now writes normalized lowercase filenames directly via `normalize_filename`/`build_output_path_map`, and `2rename-files.py` only deletes `toc.md`/`toc.rst` stubs.)

## 3. `5clean-markdown.py` once stripped every internal-link anchor
`clean_text` called `remove_html_anchors()` unconditionally, removing the `<a id="..."></a>` anchors `1rst2md.py` emits for cross-references — ~2000 of ~2069 missing-anchor issues. Diagnostic path for any "links don't work" report: run `validate_internal_links()` after each pipeline stage and bisect, rather than suspecting the renderer.

## 4. `_rewrite_refuri_to_md` must resolve through `docname_to_output` first
`input_rst/**.rst` has literal explicit hyperlinks (`` `Access DOM <Access_DOM.html>`__ ``) that bypass Sphinx resolution, so `refuri` stays literal. Since output filenames are now normalized, a naive `.html`→`.md` swap points at nonexistent files. Strip the suffix, join with the current docname's directory via `posixpath.normpath`, and look up `docname_to_output` before any suffix rewriting. Literal hyperlinks raise no Sphinx warning, so re-verify this path after any output-filename change.

## 5. Theme overrides must run asset paths through `| url`
`output_md/overrides/main.html` and `partials/nav.html` referenced `js/extra.js`, `js/animations.js` and the logo image as site-root-relative literals. With `use_directory_urls: false`, nested pages resolved them to e.g. `pdfmark/js/extra.js` → 404, visible only in the browser console, never in `mkdocs build`. Verify on a page 2+ directories deep.

## 6. `normalize_filename()` destroys camelCase word boundaries
It only replaces non-alphanumerics with `-`, so `Snippet_SnippetRunnerCookbook.rst` → `snippet-snippetrunnercookbook.md` and "Snippet Runner Cookbook" is unrecoverable from the filename. `3create-yaml-toc.py` therefore reads each page's real `# H1` (`extract_h1_title`) instead of deriving titles from filenames.

## 7. Most `missing_anchor` links point at dead legacy IDs, not lost content
Links like `` `Annotations (ANN) <pdfmark_Basic.html#50454556_26704>`__ `` carry FrameMaker-era numeric fragments that exist nowhere, while the heading they target does exist. Check: grep the numeric id (confirm undefined), then grep the link text as a heading. Fixed systematically — `_render_section` always emits an anchor, and `fix_stale_literal_anchor_links` rewrites fragments to the heading whose text matches the link text (271 → 94 issues). The remaining 94 are genuine orphans (e.g. `AutErcNotToThisFieldType`, likely in an unmigrated error-codes manual).

## 8. The markdown-link regex must exclude newlines
`pdfmark/*.rst` code blocks contain literal unbalanced `[`/`]` (PostScript arrays), so `\[([^\]]*)\]\(([^)]+)\)` matches across hundreds of lines from a stray `[` to the next real link, corrupting matches and skipping the following link. Use `\[([^\]\n]*)\]\(([^)\n]*)\)` — every emitted link is single-line.

## 9. Curated content fixes are keyed by `(docname, legacy_fragment)`
`python/7apply-anchor-review.py` keys human-reviewed fixes on stable legacy numeric fragment ids, not line numbers or surrounding text, because positions shift on every regeneration. Express any one-off content fix as a new numbered `pythonN...py` post-process step after `5clean-markdown.py` — hand-edits to generated `.md` are discarded on the next run. Only `input_rst/**.rst` and `python/*.py` are durable.

## 10. Upstream `docbuild/` has `library/`, `pdfl/` and `shared/` as siblings
`shared/` (holding `documentation.rst`/`sdkcompare.rst`) is `.. include::`-d as `../shared/...` by both `library/index.rst` and `pdfl/index.rst`, so converting `pdfl/` required `input_rst/pdfl/` with `input_rst/shared/` alongside it — not one level up. Check the real nesting before placing a new manual. Also found there: an RST comment with no `::` (`.. setup:`) had no case in `render_node()` and leaked its text onto the next heading's anchor; fixed with an explicit `if name == "comment": return ""`. Spot-check any newly migrated tree for text glued to anchors — that's the signature of an unhandled node type.
