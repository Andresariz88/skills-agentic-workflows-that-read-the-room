---
name: update-github-info
description: Keep Mona's GitHub Info page current with practical updates from official GitHub sources.
engine: copilot
model: auto
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    base-branch: main
    draft: false
    max: 1
---

# Update Mona's GitHub Info

Keep `site/content/github-info.md` useful and current for developers. Changes must be proposed in a pull request for Mona to review; never write directly to `main`.

## Research

1. Read `notes/mona-notes.md` and the current `site/content/github-info.md` before drafting.
2. Use `web-fetch` to read all three source indexes:
   - https://github.blog/latest/
   - https://github.blog/changelog/
  - https://awesome-copilot.github.com/workflows/
3. Find recent, relevant GitHub Blog and Changelog updates, along with useful Awesome Copilot workflows that help developers learn or use GitHub faster. Verify each selected item's title, details, and canonical URL from its linked official source before summarizing it. Prefer items not already covered in `site/content/github-info.md`.
4. Do not invent details or dates. If a source index cannot be fetched, do not claim to have reviewed it; use only verifiable information and report the limitation in the pull request description.

## Update

- Edit only `site/content/github-info.md`.
- Preserve Mona's editorial angle and existing homepage themes.
- Maintain a `## Latest GitHub Updates` section after the editorial angle. Include at most three recent items, newest first, and remove entries that are no longer among the most useful recent updates.
- Give each item a `###` heading with the official title, one short practical summary, and a plain-text source line. For dated posts, use `Source: GitHub Blog | Month D, YYYY | https://github.blog/...` or `Source: GitHub Changelog | Month D, YYYY | https://github.blog/changelog/...`. For workflow listings, use `Source: Awesome Copilot Workflows | https://awesome-copilot.github.com/workflows/...`.
- Keep summaries concise, attribute every item to its source, and preserve valid Markdown that the site's content parser can read.
- If there are no useful new updates and the file needs no correction, leave it unchanged and do not open a pull request.

## Review

If the file changed, use the `create-pull-request` safe output to open one non-draft pull request targeting `main` for Mona to review. Include a concise summary and the official source links in the pull request description. Do not use shell, GitHub CLI, or any direct write operation to commit or push changes.