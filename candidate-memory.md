---
id: C:/GIT/format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/candidate-memory.md
type: memory
title: Acrobat Pdfl Sdk
name: candidate-memory
description: 'Rule: In `rst2md_converter/input_rst/**.rst`, if a bare caption line sits directly above a grid table''s `+---+` top border with no blank line between them, docutils merges the caption and the entire table into one giant paragraph instead of a `table` node — no parse error/warning is emitted. The rendered markdown then shows the raw RST table syntax as prose (garbled, with smart-quote substitution turning `--` into en/em dashes), with no GFM separator row. Fixed in `1rst2md.py`''s `_fix_rst_grid_tables` by inserting a blank line whenever a grid-table delimiter line immediately follows a non-blank line.'
resource: /format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/candidate-memory.md
resource_root: C:/GIT
author: brogers
tags: [format-conversion, dev.adobe.com-rst2md-project, acrobat-pdfl-sdk]
domain: content
tokens: 3963
generated: {by: 'human:brogers', at: '2026-08-15T22:50:04-04:00'}
okf_version: '0.2'
memory: procedural
---
## 1. 2026-08-27 — Project: RST grid-table caption glued to border breaks docutils parsing

Rule: In `rst2md_converter/input_rst/**.rst`, if a bare caption line sits directly above a grid table's `+---+` top border with no blank line between them, docutils merges the caption and the entire table into one giant paragraph instead of a `table` node — no parse error/warning is emitted. The rendered markdown then shows the raw RST table syntax as prose (garbled, with smart-quote substitution turning `--` into en/em dashes), with no GFM separator row. Fixed in `1rst2md.py`'s `_fix_rst_grid_tables` by inserting a blank line whenever a grid-table delimiter line immediately follows a non-blank line.

Rationale: This is invisible from source inspection alone — the RST looks superficially fine, docutils gives no error, and the resulting broken markdown looks like a renderer bug rather than a source formatting defect. Wasted significant effort before tracing it to a missing blank line via direct docutils.publish_doctree inspection.

## 2. 2026-08-27 — Project: output_md/source in rst2md_converter mixes generated and static-asset files

Rule: `rst2md_converter/output_md/source/` contains both pipeline-generated `.md`/`.json` files and hand-maintained static assets (`css/`, `js/`, `images/`, `.claude/settings.local.json`) checked into git. None of `python/1rst2md.py`, `2rename-files.py`, `3create-yaml-toc.py`, or `5clean-markdown.py` recreate those static assets. If you `git rm`/`git clean` that directory to fix stale duplicate-case `.md` files (a real recurring problem — `2rename-files.py` isn't idempotent and errors with `FileExistsError` if rerun after a previous successful rename), you must `git checkout HEAD -- <asset paths>` afterward to restore the static assets before treating the regeneration as done.

Rationale: Wiping and regenerating output_md/source silently deletes real hand-maintained assets that no script replaces, which would break the built MkDocs site (missing CSS/JS/images) if not caught before committing.

Update: the `2rename-files.py` non-idempotency described above is now fixed — `1rst2md.py` writes already-normalized (lowercase) filenames directly via a new `normalize_filename`/`build_output_path_map` step, and `2rename-files.py` was gutted to only delete `toc.md`/`toc.rst` stubs. Rerunning the pipeline twice with no cleanup between runs no longer crashes or duplicates files.

## 3. 2026-08-27 — Harness: user's global ~/.gitignore_global silently ignores all "tests/" directories

Rule: `~/.gitignore_global` (line 93) has a bare `tests/` rule that matches a directory named `tests` anywhere in any repo. A `tests/` folder created in `rst2md_converter/` (or any other repo) will show as fully clean in `git status`/`git add` with no untracked-file indication at all — not even `??` — making it easy to believe files were never created or were already committed when they're actually just invisible to git. Check with `git check-ignore -v <path>` when a newly created file/dir mysteriously doesn't show up in `git status`. To commit such a directory, use `git add -f`.

Rationale: This is not visible from the repo's own `.gitignore` and cost real effort to diagnose (looked like a git bug or a lost test suite) — the diagnostic command (`git check-ignore -v`) is the fast path next time.

## 4. 2026-08-27 — Project: rst2md_converter's 5clean-markdown.py silently broke almost all internal links

Rule: `output_md/source/**` pages depend on `<a id="..."></a>` anchors emitted deliberately by `1rst2md.py` for internal cross-references. A prior version of `5clean-markdown.py::clean_text` called `remove_html_anchors()` unconditionally, stripping every standalone anchor tag as a "cleanup" step — after `1rst2md.py` had already validated those same links successfully. This single step was responsible for ~2000 of ~2069 total missing-anchor/target issues. Diagnosed by comparing `validate_internal_links()` output at each pipeline stage (right after `1rst2md.py` vs. after the full pipeline) rather than assuming the renderer itself was at fault.

Rationale: The bug hid in a "cleanup" pass that looked purely cosmetic (dead-code-removal-style regex sub), not in the renderer where broken links would naturally be suspected. Bisecting pipeline stage-by-stage with the converter's own `validate_internal_links()` is the fast diagnostic path for any future "links don't work" report in this project.

## 5. 2026-08-27 — Project: rst2md_converter's `_rewrite_refuri_to_md` must resolve through docname_to_output before naive suffix-swap

Rule: `input_rst/**.rst` contains literal explicit hyperlinks (e.g. `` `Access DOM <Access_DOM.html>`__ ``) that reference a sibling doc's original RST filename/case directly — these bypass Sphinx's `:doc:`/`:ref:` resolution entirely, so Sphinx leaves `refuri` as the literal text. Once `1rst2md.py` started writing normalized (lowercase-dash) output filenames (see entry 2), a naive `.html`→`.md` suffix swap on these literal refuris pointed at files that no longer exist. Fix: resolve `base` (stripped of `.html`/`.rst`/`.md`, joined with the current docname's directory via `posixpath.normpath`) against `docname_to_output` FIRST, before any naive suffix rewriting.

Rationale: This is a footgun specific to converting a doc set that mixes Sphinx-role cross-references with literal hand-authored relative hyperlinks (common in docs migrated from FrameMaker/RoboHelp) — any future renderer change to output filenames must re-verify this resolution path, since literal hyperlinks won't show up as Sphinx warnings.

## 6. 2026-08-27 — Reference: MkDocs Material `navigation.prune` scopes sidebar nav to the current document

Rule: When an MkDocs site's `nav:` groups multiple independent "documents" (e.g. one per top-level source directory, each with its own conceptual TOC), the Material theme's default sidebar renders the ENTIRE site's nav tree (all documents' full chapter lists) in the raw HTML on every page. Adding `navigation.prune` to `theme.features` in `mkdocs.yml` prunes other documents down to just their top-level link, leaving only the current document's own chapter tree expanded. Verified in `rst2md_converter/output_md/mkdocs.yml`: dropped from 136 to 38 sidebar nav labels on a sample page.

Rationale: Not obvious that this is a "feature flag" fix rather than a `nav:` structure or CSS problem — worth checking `navigation.prune` first for any "the sidebar shows too much" complaint on a Material site with a multi-document `nav:`.

Update: `navigation.prune` alone was NOT sufficient — it only trims grandchildren of inactive top-level sections; the top-level document/book NAMES themselves still all render together in the same left sidebar (confirmed the user still saw "all books in every book toc" after this fix alone). The actual fix for full per-document isolation is `navigation.tabs`, which moves top-level `nav:` sections into a separate top tab bar, leaving the left sidebar to show only the active document's own tree. Use both together.

## 7. 2026-08-27 — Project: rst2md_converter's custom MkDocs theme overrides had broken asset paths on nested pages

Rule: `output_md/overrides/main.html` and `overrides/partials/nav.html` referenced `js/extra.js`, `js/animations.js`, and `config.extra.productname` (image path) as literal site-root-relative strings instead of running them through MkDocs' `{{ ... | url }}` Jinja filter (or `{{ base_url }}/...`). With `use_directory_urls: false`, pages live in nested directories (e.g. `pdfmark/pdfmark-syntax.html`), so the literal paths resolved to e.g. `pdfmark/js/extra.js` (404) instead of the real site-root path. Every nested page silently lost its logo image and the two custom JS files, with 404s only visible in the browser console (not in `mkdocs build` output). Fixed by wrapping both in `| url`.

Rationale: `mkdocs build` gives no warning for this class of bug — it only surfaces as browser console 404s on pages below the site root. When custom theme overrides (`overrides/*.html`) reference any static asset, always run it through `| url` and verify via an actual rendered page (not just `mkdocs build` exit code), ideally checking a page 2+ directories deep, not just the site root index.

## 9. 2026-08-27 — Project: rst2md_converter's filename normalization (entry 2) makes nav labels unrecoverable from filenames

Rule: `normalize_filename()` (in both `1rst2md.py` and `3create-yaml-toc.py`) only replaces non-alphanumeric characters with `-` — it does NOT split camelCase, so an original RST filename like `Snippet_SnippetRunnerCookbook.rst` normalizes to `snippet-snippetrunnercookbook.md`, permanently losing the word boundary inside `SnippetRunnerCookbook`. Any nav-title generator that derives a page's label from its filename (mkdocs' own default title-from-slug fallback, or a naive `.replace('-', ' ').title()`) can NEVER recover "Snippet Runner Cookbook" from that filename — the information is gone. Fixed by making `3create-yaml-toc.py` read each page's actual `# H1` heading (`extract_h1_title`) instead of deriving titles from filenames at all.

Rationale: This is a direct, non-obvious consequence of the entry-2 normalization fix — anyone touching filename normalization in this project must remember that downstream nav/title generation can no longer rely on filenames looking human-readable, and must read real content (H1) instead.

## 8. 2026-08-27 — Harness: raw generated-HTML grep is not proof of what a Material (or any CSS-responsive) theme visually shows

Rule: For MkDocs Material (and similar CSS-checkbox-driven collapsible nav themes), the built HTML always contains the FULL site nav tree somewhere in the DOM (for accessibility/no-JS/mobile-drawer support) — grepping the raw HTML for nav labels will show all documents' names regardless of whether they're actually visible to a user. Only rendering the page in a real browser (e.g. via `playwright-cli` served over `http.server`, not `file://` which some sandboxes block) and screenshotting/inspecting it reveals the true visible state.

## 10. 2026-08-27 — Project: rst2md_converter's "missing_anchor" links mostly point to real headings under a dead legacy ID, not lost content

Rule: `input_rst/**.rst` contains many literal explicit hyperlinks migrated from an older FrameMaker/RoboHelp doc set, e.g. `` `Annotations (ANN) <pdfmark_Basic.html#50454556_26704>`__ ``, where the numeric fragment (`50454556_26704`) never exists as a real anchor anywhere in the RST — but the heading the link is supposed to reach (`Annotations (ANN)`, via `.. _Annotations (ANN):`) does exist with matching text. To check whether a given `missing_anchor` entry is truly unfixable vs. just pointing at a dead ID, grep `input_rst/**/*.rst` for the numeric ID first (confirms it's never defined) then grep for the link's visible text as a heading (confirms whether a real target exists). Fixed systematically in `1rst2md.py`: section headings now always emit a real anchor (`_render_section` no longer gates that on `STRIP_ANCHORS`), and a new post-process pass (`fix_stale_literal_anchor_links`) rewrites any link whose fragment doesn't match a real anchor in the target file to the anchor of the heading whose text matches the link text. This cut remaining anchor issues from 271 to 94 — the 94 left are genuine orphans (e.g. `AutErcNotToThisFieldType`, referenced only as a link, never defined as a heading anywhere in this repo — likely lives in a separate error-codes manual not migrated here).

Rationale: Don't assume a `missing_anchor` report means the content is gone — check the RST source directly (numeric ID search + link-text-as-heading search) before writing it off, since most of these were mechanically fixable once the actual pattern (dead legacy ID, real heading) was identified.

## 11. 2026-08-27 — Project: rst2md_converter's markdown link regex must exclude newlines (fenced code blocks contain literal '[' ']')

Rule: `pdfmark/*.rst` files contain PostScript code examples with literal, unbalanced-looking `[`/`]` array syntax (e.g. `[ /Rect [xll yll xur yur] /Subtype name /ANN pdfmark`) inside fenced code blocks. A markdown link regex like `\[([^\]]*)\]\(([^)]+)\)` has no `\n` exclusion, so `[^\]]*` can match across many lines from a stray `[` inside a code block all the way to the next real `]...(...)`  link syntax later in the document, silently corrupting which text gets matched as the "link" and sometimes causing a real link right after the swallowed span to be skipped by `re.sub`'s scan position. Fix: exclude `\n` from both capture groups (`\[([^\]\n]*)\]\(([^)\n]*)\)`) since every link this renderer emits is always single-line anyway. Found via `python/6suggest-anchor-fixes.py`'s output showing a multi-hundred-line "link text" for a pdfmark-logical.md entry.

Rationale: Any future regex written against this project's generated markdown that scans for `[...](...)`  link syntax must add the `\n` exclusion — pdfmark's code blocks are the one place in this corpus where it silently breaks, and the failure mode (wrong/swallowed matches) doesn't throw an error, so it's easy to ship unnoticed.

## 12. 2026-08-27 — Project: rst2md_converter's manual content-review fixes are keyed by (docname, legacy_fragment), not by text position

Rule: `python/7apply-anchor-review.py` applies a human-reviewed curation pass (fix or strip specific broken links) on top of the automated fixes. It's keyed by `(current_docname, legacy_numeric_fragment)` tuples rather than line numbers or exact surrounding text, because those legacy FrameMaker-era fragment IDs (e.g. `50532372_95231`) are unique and stable across any regeneration of `output_md/source` from `input_rst`, whereas line positions shift constantly. This is the pattern to follow for any future one-off, human-reviewed content fix in this pipeline: key it by a stable identifier already present in the source, add it as a new numbered `pythonN...py` post-process step (after `5clean-markdown.py`), and rerun it after every regeneration rather than hand-editing the generated `.md` (which regeneration would silently discard).

Rationale: Generated files in `output_md/source` are always overwritten by `1rst2md.py`; only `input_rst/**.rst` and the `python/*.py` pipeline scripts are durable. A curated content fix that isn't expressed as pipeline code disappears the next time someone regenerates.

Rationale: Wasted a diagnostic pass concluding "the fix didn't work" purely from a text-based HTML search before actually rendering the page — this class of theme requires visual/rendered verification, not text search, when confirming a nav-visibility fix.

## 13. 2026-08-27 — Project: docbuild's top-level manuals (e.g. pdfl/) are siblings of shared/, not children of library/ — and RST comment nodes leaked text

Rule: The upstream `Adobe-Print/Documentation_PDFL_Acrobat_SDK` repo's `docbuild/` root has `library/` (which maps to this project's `input_rst/`), `pdfl/`, and `shared/` (containing `documentation.rst`/`sdkcompare.rst`, `.. include::`-d by both `library/index.rst` and `pdfl/index.rst` via a relative `../shared/...` path) all as siblings. To convert `pdfl/` through this pipeline with its includes resolving, it had to be added as `input_rst/pdfl/` with `input_rst/shared/` alongside it (sibling, matching the include's `../shared` relative path) — putting `shared/` one level higher (next to `input_rst/` itself, which is where `library/index.rst`'s own already-broken include silently points) would not have worked for `pdfl/`. Separately, converting `pdfl/releasenotes25.0.rst` surfaced a real converter bug: an RST comment line with no `::` (e.g. `.. setup:`) had no case in `render_node()`, so it fell through to the generic child-renderer and its text leaked into the output, glued onto the next heading's anchor (`setup:<a id="getting-started">`). Fixed by adding an explicit `if name == "comment": return ""` case in `1rst2md.py`.

Rationale: When migrating a new top-level manual from this source repo (not one of the existing `library/` sub-guides), check `docbuild/`'s actual directory nesting before placing the new content under `input_rst/`, since `../shared` will resolve relative to wherever you put it, not to where an existing sibling doc's identical-looking include happens to already point. Also: any newly-migrated RST tree should be spot-checked for text glued onto anchors — it's the signature of an unhandled docutils node type falling through to the generic renderer.
