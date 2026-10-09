---
id: C:/GIT/format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/README.md
type: project-readme
title: acrobat-pdfl-sdk readme
name: acrobat-pdfl-sdk-readme
description: SDK files in RST format ready for conversion to MD.
resource: /format_conversion/dev.adobe.com_rst2md_project/acrobat-pdfl-sdk/README.md
resource_root: C:/GIT
author: brogers
tags: [project, repo, RST, markdown, formats, format conversion, ADP]
domain: content
tokens: 216
generated: {by: 'human:brogers', at: '2026-08-21T23:28:30-04:00'}
okf_version: '0.2'
timestamp: 2026-08-16 02:50:04+00:00
---
# Documentation

This is the source that should go into ADP devsite. As of 10/8/26, the md here is copied to https://github.com/Adobe-Print/Documentation_PDFL_Acrobat_SDK_2026.git. It has 2k content fixes and md. RST should no longer be used. 


Please xxx see the [ADP Developer Site Documentation](https://developer-stage.adobe.com/dev-docs-reference/).
notes: 

- https://developer-stage.adobe.com/dev-docs-reference/getting-started/dev-docs/#
 
-  Questions & Support: #adobe-developer-website

need to login in with external gh acct. Won't see the right UI otherwise. 

make sure for the frist deployment to click on "Force deploy all files"

delete unneeded files

what happens if dirs left empty? 

create manual toc? 

"devsitepaths.json" means something not set up. 

do i need to modify Action yml? when? 

dd Metadata (title, keywords, description etc) for awesome Search/SEO results, include Analytics for reporting, check Accessibility (run AXE) and test all links on Stage before going live. Best Practices can be found on this wiki. Please reach out if you have any questions.


  ┌─────────┬─────────────┬─────────────────────────────────────────────────────────────────────────────────────────┐
  │ Commit  │    Date     │                                          What                                           │
  ├─────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────┤
  │ e28ccf0 │ 2026-08-27  │ "Final conversion of rst to markdown. Fixed 2000 links…": 137 files, 84,960 lines added │
  ├─────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────┤
  │ 36f9573 │ today 21:04 │ "convert to md and 2000 content fixes": 112 files, 1,669 lines added                    │
  ├─────────┼─────────────┼─────────────────────────────────────────────────────────────────────────────────────────┤
  │ bab12d8 │ today 21:04 │ merge of origin/main                                                                    │
  └─────────┴─────────────┴─────────────────────────────────────────────────────────────────────────────────────────┘

  Local main is 3 ahead and 0 behind origin/main, with a clean working tree. GitHub is still at 495ba19 from 2026-05-28.

  On the size: this repo holds 134 .md files under src/pages/, not 2000+. The rst sources I found are about the same count (142 in Documentation_PDFL_Acrobat_SDK_2026, 136 in
  rst2md_converter/input_rst). The "2000" in your commit messages refers to links and content fixes; the 85k lines could plausibly be 2000+ printed pages.

  Other copies of conversion work in sibling folders, all older:
  - rst2md_converter/output_md: 125 md files, last commit 2026-03-27 (Adobe-DMe-Help-Content/rst2md_converter). It has uncommitted deletions in output_md.
  - Documentation_PDFL_Acrobat_SDK_2026: first conversion, 2026-01-28 (Adobe-Print/...), still mostly rst.

  To publish, git push origin main would be a clean fast-forward. I haven't pushed because it goes straight to main on a public AdobeDocs repo; say the word and I'll do it, or I can
  put it on a branch for a PR instead.


  ## Todo

    The 43 unresolved link targets
  - PDFs not in the repo (19): seven ../pdfstandards/*.pdf references, each linked from both acrobat/index.md and pdfl/index.md, plus two PDFL ReadMe PDFs,
    acrobatsdk_pluginguide.pdf and CreatedPRC.pdf.
  - API reference not migrated (12): API_References/Acrobat_API_Reference/index.md (3) and API_References/PRCReference/3D_API_Reference/index.md (9, all from
    plugins-a3d-api.md).
  - Old RST-era filenames (8): Overview_GettingStarted.md, Overview_UsageRights.md, Plugins_Introduction.md, JS_API_acrojspreface.md, Faq.md, Samples_Tools.md,
    ./snippet/index.md.
  - Template placeholders (4): support/… links in config.md.
  - One malformed external link: www.verity.com with no https://, in plugins-extendedapi.md.

  The two RST leftovers
  - guides/jsapiref/js-api-acrojs.md:9939 has a raw .. raw:: html directive.
  - guides/jsapiref/media.md:575 has a broken :ref: role.