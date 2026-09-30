---
name: update-github-info
description: Propose concise, source-backed updates to the GitHub Info content page.
strict: true
engine: claude
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
network:
  allowed:
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
    toolsets: [pull_requests]
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: false
    allowed-files:
      - site/content/github-info.md
  noop:
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md` first. Use the web-fetch tool to fetch these sources:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Identify recent items from the sources that offer practical value to developers and fit the site's existing editorial angle. Verify every proposed factual claim against the fetched sources. Keep summaries short and practical, and include a clear source link for each update. Preserve the existing page's structure and themes; change only `site/content/github-info.md`.

Before editing, check open pull requests for an unfinished update to this page. If one exists, do not create a competing proposal; call `noop` with a short reason so Mona can review the existing PR.

If there is no useful, verified update, make no changes and call `noop` with a short reason. Otherwise, edit the page and use the configured `create-pull-request` safe output to open one non-draft PR for Mona to review. Summarize the update and its official sources in the PR description. Do not push changes or write directly to the base branch.