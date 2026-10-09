---
id: C:/GIT/format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/release_notes.md
type: reference
title: acrobat-pdfl-sdk change list
name: acrobat-pdfl-sdk-change-list
description: ''
resource: /format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/release_notes.md
resource_root: C:/GIT
author: brogers
tags: [format-conversion, dev.adobe.com-rst2md-project, acrobat-pdfl-sdk]
domain: content
tokens: 302
generated: {by: 'human:brogers', at: '2026-08-15T22:50:04-04:00'}
okf_version: '0.2'
---
# Release Notes

## Changes

### 08-27
- Populated src/pages/guides with the full converted SDK documentation (15 doc directories, 105 markdown pages) from rst2md_converter's output_md/source.
- Replaced src/pages/pdfl/index.md with an exact RST-to-Markdown conversion of the PDFL Documentation_PDFL_Acrobat_SDK repo's docbuild/pdfl/index.rst (including its shared documentation/sdkcompare includes), not a summary. Added src/pages/pdfl/releasenotes18.md, releasenotes21.md, releasenotes21.0.0.7.md, and releasenotes25.0.md (converted from that repo's four release-notes RST files) and turned pdfl/releasenotes.md into a landing page linking to them.
- Populated src/pages/acrobat with an exact RST-to-Markdown conversion of the same repo's docbuild/acrobatsdk (index, getting started, choose-a-technology, release notes, 64-bit Windows dev guide), replacing the two placeholder pages and adding gettingstarted.md, choose.md, and 64bitdev.md plus their referenced images.
- Copied the PDFL SDK's ReadMe PDFs and .docx files (v18.0.5, v21.0.0, template1) from docbuild/pdfl into src/pages/pdfl.

## Future
