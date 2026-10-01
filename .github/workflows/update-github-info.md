---
name: update-github-info
description: Propose concise, source-backed updates to the GitHub Info content page.
strict: true
engine: copilot
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
  copilot-requests: write
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - api.github.com
    - awesome-copilot.github.com
  # hosted-web:
  #   allowed:
  #     - github.blog
  #     - github.com
  #   max-uses: 2
tools:
  edit:
  web-fetch:
  github:
    mode: gh-proxy
    toolsets: [pull_requests, repos]
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: false
    allowed-files:
      - site/content/github-info.md
  noop:
---

<!-- # Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md` first. Use the web-fetch tool to fetch these sources:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Identify recent items from the sources that offer practical value to developers and fit the site's existing editorial angle. Verify every proposed factual claim against the fetched sources. Keep summaries short and practical, and include a clear source link for each update. Preserve the existing page's structure and themes; change only `site/content/github-info.md`.

Before editing, check open pull requests for an unfinished update to this page. If one exists, do not create a competing proposal; call `noop` with a short reason so Mona can review the existing PR.

If there is no useful, verified update, make no changes and call `noop` with a short reason. Otherwise, edit the page and use the configured `create-pull-request` safe output to open one non-draft PR for Mona to review. Summarize the update and its official sources in the PR description. Do not push changes or write directly to the base branch. -->

# Update GitHub Info
 
Read these repository files first:
 
- `notes/mona-notes.md`
- `site/content/github-info.md`
 
## Check for an existing update
 
Before researching updates, check open pull requests.
 
If an open pull request already modifies:
 
`site/content/github-info.md`
 
do not create a competing proposal.
 
Use the configured `noop` safe output with a short explanation.

## Research
 
Find recent GitHub developments relevant to developers.
 
Preferred discovery sources:
 
- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/
 
Use these sources when accessible.
 
If an index page cannot be fetched, use other accessible official GitHub
sources to discover and verify candidate updates.
 
Acceptable authoritative sources include:
 
- individual articles on github.blog
- GitHub changelog articles
- official GitHub repositories
- GitHub API repository data
- official GitHub documentation
 
Do not require an index page itself to be successfully fetched in order
to use an individual official article.
 
Never invent or infer an update from commit messages alone.
 
Only update the page when the factual claims can be verified from an
official GitHub source.
 
<!-- ## Research
 
Look for recent GitHub developments that provide practical value to
developers and fit the existing editorial angle of
`site/content/github-info.md`.
 
Prefer official GitHub sources.
 
Research these sources:
 
- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/
 
If a source cannot be read directly with `web-fetch`, do not repeatedly
retry the same URL.
 
Instead:
 
1. Follow relevant links discovered from the source.
2. Use GitHub repository/API information when the content is hosted on GitHub.
3. Use another official GitHub source containing the same factual information.
4. Skip an item if it cannot be verified from an official source.
 
A failure to read one source must not terminate the research if other
official sources remain available. -->
 
## Editorial requirements
 
Identify recent items that:
 
- offer practical value to developers;
- fit the site's existing themes;
- are supported by an official source;
- are not already covered by the page.
 
Verify every factual claim before adding it.
 
Keep each update short and practical.
 
Include a clear official source URL for each update.
 
Preserve the page's existing structure and themes.
 
Change only:
 
`site/content/github-info.md`
 
## Required final action
 
Finish by invoking exactly one safe output.
 
### Existing PR
 
If an open PR already updates the page, invoke `noop`.
 
### No useful update
 
If, after checking the available official sources, there is no useful
and verified update, invoke `noop` with a short explanation.
 
### Update available
 
If one or more useful verified updates are available:
 
1. Edit `site/content/github-info.md`.
2. Review the resulting diff.
3. Do not modify any other file.
4. Invoke the configured `create-pull-request` safe output.
5. Create exactly one non-draft pull request.
6. Summarize the changes in the PR description.
7. Include the official source URLs in the PR description.
 
Do not finish after editing the file without invoking either
`create-pull-request` or `noop`.
 
Do not push changes directly to the base branch.
Show less
The key improvement

The most important change isn't actually YAML. It's this instruction:

Plain Text
If a source cannot be read directly with web-fetch, do not repeatedly
retry the same URL.
 
Instead:
 
1. Follow relevant links discovered from the source.
2. Use GitHub repository/API information when the content is hosted on GitHub.
3. Use another official GitHub source containing the same factual information.
4. Skip an item if it cannot be verified from an official source.
 
A failure to read one source must not terminate the research if other
official sources remain available.