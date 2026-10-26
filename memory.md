# ADP devsite memory

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
