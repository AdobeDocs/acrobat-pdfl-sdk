
# Documentation

## Doc status

- This repo contains the source markdown for PDFL and Acrobat SDK guides published to developer.adobe.com. RST is deprecated and cannot be used since the new source has thousands of changes (including bug fixes).
- The old site at https://opensource.adobe.com/dc-acrobat-sdk-docs/ redirects here.
- Only API References continue to live at https://github.com/adobe/dc-acrobat-sdk-docs

## Information about using this platfrom

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

## Links


Deployment docs: https://developer-stage.adobe.com/dev-docs-reference/getting-started/dev-docs/
Staging: https://developer-stage.adobe.com/acrobat-pdfl-sdk/
Production: 


# ADP deployment gotchas

Devsite content and deploy issues that took 2+ turns to resolve.

1. **Local preview needs three servers.** Run `npm run dev` in this repo (port 3003), `..\adp-devsite` (3000/3001), and `..\devsite-runtime-connector` (3002). Open http://localhost:3000/acrobat-pdfl-sdk/. If a page returns HTTP 500, it is usually an MDX parse error in that page.

2. **Angle brackets and braces break MDX.** Bare `<word>`, `<<...>>`, `{...}` in prose, a lone `<` or `>` in table cells, and placeholders like `<insert bullet >` fail to parse. Locally the page returns 500; on deploy the upload fails. Wrap them in backticks.

3. **Leftover RST directives break pages.** Remove or convert lines like `.. raw:: html` and the anchor HTML inside them. Keep only `<a id="..."></a>` anchors.

4. **Check MDX before pushing.** Parse every page with the connector's chain: remark-parse + frontmatter + remark-mdx + remarkGfmNoLink + remark-gridtables. A deploy that fails on parse errors costs a full round trip.

5. **No extra dots in filenames.** `releasenotes25.0.md` returns 404 through routing. Use hyphens, e.g. `releasenotes25-0.md`, and update `config.md` and any links to it.

6. **No underscores in filenames.** ADP turns `_` into `-` in URLs, so the deploy reports "File not found" for `annotation_apis.md`. Use hyphens, e.g. `annotation-apis.md`.

7. **Very large pages time out on deploy.** The html2md backend has a 10 s limit and returns 504 for big files. A ~773 KB page still timed out; at ~520 KB it passed. Split large pages by `##` section into separate files.

8. **When splitting a page, keep links working.** Move each section's `<a id>` anchors with it. Rewrite `#anchor` links in all files to `./newfile.md#anchor`, including links from other folders. Add links to the new pages in the section's `index.md` and at the top of the original page.

9. **Deploy flow.** A push to `main` auto-deploys only the changed files to prod (`deploy.yml`). Staging (`stage.yml`) only runs manually. The first deploy, or a fix after earlier failures, needs a full deploy: `gh workflow run deploy.yml -f env=prod -f deployAll=true`. Then cancel the duplicate run the push triggered. Only `.md` and `.json` files are uploaded. To find failures, run `gh run view <id> --log-failed` and filter for `x-error:`.

10. **A successful deploy can still 404 on developer.adobe.com.** Check the AEM origin first: `https://main--adp-devsite--adobedocs.aem.live/<path>/`. If that returns 200, the content is published, and the ADP team needs to route the `/<path>` prefix on developer.adobe.com. The site is never on github.io.
