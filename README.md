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


Source docs for developer.adobe.com. As of 10/8/26, the md here is copied to https://github.com/Adobe-Print/Documentation_PDFL_Acrobat_SDK_2026.git. It has 2k content fixes and md. RST should no longer be used. 

Please see the [ADP Developer Site Documentation](https://developer-stage.adobe.com/dev-docs-reference/).
notes: 

- Getting started: https://developer-stage.adobe.com/dev-docs-reference/getting-started/dev-docs/#
-  Questions & Support: #adobe-developer-website

Notes: 

- Need to login in with external gh acct. Won't see the right UI otherwise. 
- Make sure for the first deployment to click on "Force deploy all files"

## Release process

1. Create branch without  /  in name; edit + preview locally.
2. Commit + push branch.
3. GitHub Actions → Staging → Run workflow → select branch. First deployment: check Force deploy all files.
4. Review staging site.
5. Open PR → review → merge into  main .
6. Merge triggers automatic production deployment; check Actions succeeds, then check live site.

Staging = manual. Production after merge/push to  main  = automatic.
