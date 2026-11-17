---
name: update-github-info
description: Review official GitHub Blog and Changelog updates and propose useful changes to the GitHub Info page.
intent: Keep the GitHub Info page useful and current with concise, practical guidance backed by official GitHub sources.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
engine:
  id: copilot
  copilot-sdk: true
tools:
  bash: false
  cli-proxy: false
  edit: true
  web-fetch: {}
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    reviewers: [mona]
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current `site/content/github-info.md` before
making any changes. Fetch both official sources:

- https://github.blog/latest/
- https://github.blog/changelog/

Identify recent, relevant updates that help developers learn GitHub faster.
Only make factual, useful changes supported by those sources; include a link to
the source for every new item. Keep summaries short and practical, preserve the
page's existing editorial direction, and avoid duplicating content already
there. Edit only `site/content/github-info.md`.

If there is no worthwhile new information, either source cannot be reviewed, or
the page needs no change, do not create a pull request; call `noop` with a brief
reason. Otherwise, use the configured `create-pull-request` safe output to open
a non-draft pull request requesting Mona's review. Never write directly to the
default branch or use another mechanism to publish changes.
