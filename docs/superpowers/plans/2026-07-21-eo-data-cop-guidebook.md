# eo-data-cop-guidebook Scaffold Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Scaffold the full `eo-data-cop-guidebook` repository locally as a working, renderable Quarto book, ready for someone with `ESIPFed` GitHub org permissions to push and enable Pages.

**Architecture:** A Quarto `book` project at the repo root. Chapter content lives under `chapters/<part>/` as plain `.md` files, referenced from `_quarto.yml`. GitHub Actions renders and publishes to the `gh-pages` branch on every push to `main`. Contribution docs/templates support both a no-git web-edit path and a standard fork/branch/PR path.

**Tech Stack:** Quarto CLI (1.6.40, confirmed installed locally), GitHub Actions (`quarto-dev/quarto-actions`), plain Markdown, YAML.

## Global Constraints

- Repo name: `eo-data-cop-guidebook`. Org: `ESIPFed`. Description: "Guidebook for creating and sustaining Earth observing data focused communities of practice."
- License: CC BY 4.0 (content license, not a software license).
- Site title: "Guidebook for Earth Observation Data Communities of Practice".
- Chapter files are plain `.md`, never `.qmd` — no code execution needed, and `.md` renders in GitHub's file viewer for non-technical contributors.
- On-disk layout mirrors book parts as physical folders under `chapters/`.
- Starter content per chapter is a bare stub: title heading + one-line "content coming soon" placeholder. No outlines, no real content.
- This task does NOT create the remote GitHub repo or push. It produces a git-initialized local scaffold with commits per task. Repo creation/push/Pages setup is a manual handoff step for someone with `ESIPFed` org permissions.
- Working directory for all tasks: `/Users/afriesz/eo-data-cop-guidebook` (already `git init`'d, with one existing commit for the design spec).

---

### Task 1: Root repo metadata files

**Files:**
- Create: `.gitignore`
- Create: `LICENSE`
- Create: `README.md`

**Interfaces:**
- Consumes: none
- Produces: none consumed by other tasks (these are terminal, standalone files)

- [ ] **Step 1: Create `.gitignore`**

```
/.quarto/
/_book/
.DS_Store
```

- [ ] **Step 2: Create `LICENSE`**

```
Creative Commons Attribution 4.0 International License

This work is licensed under a Creative Commons Attribution 4.0
International License. To view a copy of this license, visit
http://creativecommons.org/licenses/by/4.0/ or send a letter to
Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

You are free to:

  Share — copy and redistribute the material in any medium or format
  Adapt — remix, transform, and build upon the material

  for any purpose, even commercially.

Under the following terms:

  Attribution — You must give appropriate credit, provide a link to the
  license, and indicate if changes were made. You may do so in any
  reasonable manner, but not in any way that suggests the licensor
  endorses you or your use.

  No additional restrictions — You may not apply legal terms or
  technological measures that legally restrict others from doing
  anything the license permits.
```

- [ ] **Step 3: Create `README.md`**

```markdown
# EO Data CoP Guidebook

Guidebook for creating and sustaining Earth observing data focused
communities of practice.

**Read it live:** https://esipfed.github.io/eo-data-cop-guidebook/

This is a [Quarto](https://quarto.org) book. Chapters live under
`chapters/`, grouped by part (Getting Started, Sustaining Momentum,
Measuring Success).

## Contributing

Found something to fix, or want to write a chapter? See
[CONTRIBUTING.md](CONTRIBUTING.md) — small edits can be made directly in
your browser, no git required.

## License

Content is licensed [CC BY 4.0](LICENSE).
```

- [ ] **Step 4: Verify files exist with expected content**

Run: `ls -la /Users/afriesz/eo-data-cop-guidebook/.gitignore /Users/afriesz/eo-data-cop-guidebook/LICENSE /Users/afriesz/eo-data-cop-guidebook/README.md`
Expected: all three paths listed, no "No such file" errors

- [ ] **Step 5: Commit**

```bash
git add .gitignore LICENSE README.md
git commit -m "Add repo metadata: gitignore, CC BY 4.0 license, README"
```

---

### Task 2: Contribution workflow files

**Files:**
- Create: `CONTRIBUTING.md`
- Create: `.github/PULL_REQUEST_TEMPLATE.md`
- Create: `.github/ISSUE_TEMPLATE/propose-chapter.md`

**Interfaces:**
- Consumes: none
- Produces: `CONTRIBUTING.md` is linked from chapter stub files in Task 3 via a relative path `../../CONTRIBUTING.md`

- [ ] **Step 1: Create `CONTRIBUTING.md`**

```markdown
# Contributing

There are two ways to contribute, depending on the size of the change.

## Quick fix (no git required)

For a typo, a small wording change, or filling in a stub chapter with a
paragraph or two:

1. Go to the live site: https://esipfed.github.io/eo-data-cop-guidebook/
2. Open the page you want to change and click **Edit this page** (in the
   right-hand margin, or at the bottom of the page).
3. GitHub opens its web editor. Make your change.
4. Scroll down, add a short description of what you changed, and click
   **Propose changes**. GitHub creates a fork and a pull request for you
   automatically.
5. That's it — a maintainer will review and merge.

## New chapter or larger change

For adding a new chapter, restructuring, or anything touching multiple
files:

1. Clone the repo and create a branch:
   ```bash
   git clone https://github.com/ESIPFed/eo-data-cop-guidebook.git
   cd eo-data-cop-guidebook
   git checkout -b my-change
   ```
2. Add or edit files under `chapters/<part>/`, where `<part>` is one of
   `getting-started`, `sustaining-momentum`, or `measuring-success`.
3. **If you added a new chapter file**, add it to `_quarto.yml` under the
   matching `part:` entry so it shows up in the book.
4. (Optional) Preview your changes locally:
   ```bash
   quarto preview
   ```
5. Commit, push, and open a pull request.

## Chapter conventions

- Files are plain Markdown (`.md`), not `.qmd` — no code chunks, no
  executable content.
- Start each chapter with a single `#` top-level heading matching the
  chapter title.
- A stub chapter (title + "content coming soon") is a completely valid
  starting point for a PR — you don't need to finish the whole chapter in
  one pass.

## Proposing changes to the book's outline

If you want to propose a new chapter, a new part, or a restructuring of
the existing outline before writing content, open an issue using the
"Propose a new chapter or restructuring" template.
```

- [ ] **Step 2: Create `.github/PULL_REQUEST_TEMPLATE.md`**

```markdown
## What changed?

<!-- Briefly describe the change -->

## Which chapter/part does this affect?

<!-- e.g. Getting Started > Governance, or "new chapter", or "site config" -->

## Checklist

- [ ] I previewed this change (either `quarto preview` locally, or
      GitHub's file preview for a single-file web edit)
- [ ] If I added a new chapter, I added it to `_quarto.yml` under the
      correct `part`
- [ ] N/A — this was a small text edit made directly on github.com
```

- [ ] **Step 3: Create `.github/ISSUE_TEMPLATE/propose-chapter.md`**

```markdown
---
name: Propose a new chapter or restructuring
about: Suggest a new chapter, a new part, or a change to the guidebook's outline
title: "[Proposal] "
labels: proposal
---

## What are you proposing?

<!-- New chapter, new part, rename/merge/split existing chapters, reorder, etc. -->

## Where would it fit?

<!-- Which part (Getting Started / Sustaining Momentum / Measuring Success), or is this a new part? -->

## Why does the guidebook need this?

<!-- What gap does this fill for communities of practice? -->
```

- [ ] **Step 4: Verify files exist**

Run: `find /Users/afriesz/eo-data-cop-guidebook -maxdepth 3 -name "CONTRIBUTING.md" -o -maxdepth 3 -name "PULL_REQUEST_TEMPLATE.md" -o -name "propose-chapter.md"`
Expected: three matching paths printed

- [ ] **Step 5: Commit**

```bash
git add CONTRIBUTING.md .github/PULL_REQUEST_TEMPLATE.md .github/ISSUE_TEMPLATE/propose-chapter.md
git commit -m "Add contribution guide, PR template, and chapter-proposal issue template"
```

---

### Task 3: Chapter stub files

**Files:**
- Create: `chapters/getting-started/designing-your-community.md`
- Create: `chapters/getting-started/governance.md`
- Create: `chapters/getting-started/recruiting-members.md`
- Create: `chapters/getting-started/welcome-inaugural-meeting.md`
- Create: `chapters/sustaining-momentum/running-meetings.md`
- Create: `chapters/sustaining-momentum/communication.md`
- Create: `chapters/sustaining-momentum/engaging-member-participation.md`
- Create: `chapters/sustaining-momentum/working-asynchronously.md`
- Create: `chapters/measuring-success/longevity-assessment.md`
- Create: `chapters/measuring-success/cooperative-research-outcomes.md`
- Create: `chapters/measuring-success/attendance-metrics.md`

**Interfaces:**
- Consumes: `CONTRIBUTING.md` (Task 2) via relative link `../../CONTRIBUTING.md`
- Produces: these exact 11 paths are referenced verbatim in `_quarto.yml` in Task 4

- [ ] **Step 1: Create the four "Getting Started" chapter stubs**

`chapters/getting-started/designing-your-community.md`:
```markdown
# Designing Your Community

_Content coming soon. [Contribute this chapter](../../CONTRIBUTING.md)._
```

`chapters/getting-started/governance.md`:
```markdown
# Governance

_Content coming soon. [Contribute this chapter](../../CONTRIBUTING.md)._
```

`chapters/getting-started/recruiting-members.md`:
```markdown
# Recruiting Members

_Content coming soon. [Contribute this chapter](../../CONTRIBUTING.md)._
```

`chapters/getting-started/welcome-inaugural-meeting.md`:
```markdown
# Welcome / Inaugural Meeting

_Content coming soon. [Contribute this chapter](../../CONTRIBUTING.md)._
```

- [ ] **Step 2: Create the four "Sustaining Momentum" chapter stubs**

`chapters/sustaining-momentum/running-meetings.md`:
```markdown
# Running Meetings

_Content coming soon. [Contribute this chapter](../../CONTRIBUTING.md)._
```

`chapters/sustaining-momentum/communication.md`:
```markdown
# Communication

_Content coming soon. [Contribute this chapter](../../CONTRIBUTING.md)._
```

`chapters/sustaining-momentum/engaging-member-participation.md`:
```markdown
# Engaging Members' Participation Through Interesting Meeting Topics

_Content coming soon. [Contribute this chapter](../../CONTRIBUTING.md)._
```

`chapters/sustaining-momentum/working-asynchronously.md`:
```markdown
# Working Asynchronously Between Meetings

_Content coming soon. [Contribute this chapter](../../CONTRIBUTING.md)._
```

- [ ] **Step 3: Create the three "Measuring Success" chapter stubs**

`chapters/measuring-success/longevity-assessment.md`:
```markdown
# Longevity Assessment (Has the Goal Been Met?)

_Content coming soon. [Contribute this chapter](../../CONTRIBUTING.md)._
```

`chapters/measuring-success/cooperative-research-outcomes.md`:
```markdown
# Cooperative Research Outcomes

_Content coming soon. [Contribute this chapter](../../CONTRIBUTING.md)._
```

`chapters/measuring-success/attendance-metrics.md`:
```markdown
# Attendance Metrics

_Content coming soon. [Contribute this chapter](../../CONTRIBUTING.md)._
```

- [ ] **Step 4: Verify all 11 files exist**

Run: `find /Users/afriesz/eo-data-cop-guidebook/chapters -name "*.md" | sort | wc -l`
Expected: `11`

- [ ] **Step 5: Commit**

```bash
git add chapters/
git commit -m "Add chapter stubs for all 11 chapters across 3 parts"
```

---

### Task 4: Quarto book config, landing page, and render validation

**Files:**
- Create: `index.md`
- Create: `_quarto.yml`

**Interfaces:**
- Consumes: exact chapter paths produced in Task 3; `README.md` description text from Task 1
- Produces: a renderable Quarto book (`_book/` output, gitignored) — validated in this task and re-validated in Task 6

- [ ] **Step 1: Create `index.md`**

```markdown
# Preface {.unnumbered}

This guidebook collects practical guidance for creating and sustaining
Earth observing data focused communities of practice — from the first
conversation about starting one, through keeping it healthy, to knowing
when its goal has been met.

It's a living, community-maintained document. See
[Contributing](CONTRIBUTING.md) if you'd like to add or improve a
chapter.
```

- [ ] **Step 2: Create `_quarto.yml`**

```yaml
project:
  type: book

book:
  title: "Guidebook for Earth Observation Data Communities of Practice"
  repo-url: https://github.com/ESIPFed/eo-data-cop-guidebook
  repo-actions: [edit, issue]
  page-footer:
    left: "Licensed CC BY 4.0"
  chapters:
    - index.md
    - part: "Getting Started"
      chapters:
        - chapters/getting-started/designing-your-community.md
        - chapters/getting-started/governance.md
        - chapters/getting-started/recruiting-members.md
        - chapters/getting-started/welcome-inaugural-meeting.md
    - part: "Sustaining Momentum"
      chapters:
        - chapters/sustaining-momentum/running-meetings.md
        - chapters/sustaining-momentum/communication.md
        - chapters/sustaining-momentum/engaging-member-participation.md
        - chapters/sustaining-momentum/working-asynchronously.md
    - part: "Measuring Success"
      chapters:
        - chapters/measuring-success/longevity-assessment.md
        - chapters/measuring-success/cooperative-research-outcomes.md
        - chapters/measuring-success/attendance-metrics.md

format:
  html:
    theme: cosmo
    toc: true
```

- [ ] **Step 3: Validate `_quarto.yml` YAML syntax**

Run: `ruby -ryaml -e "YAML.load_file('/Users/afriesz/eo-data-cop-guidebook/_quarto.yml'); puts 'valid yaml'"`
Expected: `valid yaml`

- [ ] **Step 4: Render the book**

Run: `cd /Users/afriesz/eo-data-cop-guidebook && quarto render`
Expected: exits 0, output ends with something like `Output created: _book/index.html`, no ERROR lines

- [ ] **Step 5: Spot-check rendered output**

Run: `ls /Users/afriesz/eo-data-cop-guidebook/_book/*.html | wc -l`
Expected: `12` (index + 11 chapters, each producing one `.html` file at the top of `_book/`)

- [ ] **Step 6: Commit**

```bash
git add index.md _quarto.yml
git commit -m "Add Quarto book config and landing page"
```

Note: `_book/` and `.quarto/` are excluded by `.gitignore` from Task 1 and should NOT be staged.

---

### Task 5: GitHub Actions publish workflow

**Files:**
- Create: `.github/workflows/publish.yml`

**Interfaces:**
- Consumes: none (references `_quarto.yml` from Task 4 only at CI runtime, not at authoring time)
- Produces: none consumed by other tasks in this plan (this is the deployment mechanism, exercised after the repo is pushed — outside this plan's scope)

- [ ] **Step 1: Create `.github/workflows/publish.yml`**

```yaml
on:
  push:
    branches: main

name: Quarto Publish

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2

      - name: Render and Publish
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

- [ ] **Step 2: Validate YAML syntax**

Run: `ruby -ryaml -e "YAML.load_file('/Users/afriesz/eo-data-cop-guidebook/.github/workflows/publish.yml'); puts 'valid yaml'"`
Expected: `valid yaml`

- [ ] **Step 3: Commit**

```bash
git add .github/workflows/publish.yml
git commit -m "Add GitHub Actions workflow to publish the book to gh-pages"
```

---

### Task 6: Final full validation

**Files:**
- None created or modified — this task only validates the completed scaffold.

**Interfaces:**
- Consumes: the entire scaffold produced by Tasks 1-5
- Produces: nothing further consumes this; it's the plan's final gate

- [ ] **Step 1: Clean rebuild of the book**

Run: `cd /Users/afriesz/eo-data-cop-guidebook && rm -rf _book .quarto && quarto render`
Expected: exits 0, no ERROR lines, ends with output for `_book/index.html`

- [ ] **Step 2: Confirm working tree is clean aside from gitignored build output**

Run: `cd /Users/afriesz/eo-data-cop-guidebook && git status --porcelain`
Expected: empty output (nothing to commit; `_book/` and `.quarto/` are gitignored so they won't appear)

- [ ] **Step 3: Confirm full commit history**

Run: `cd /Users/afriesz/eo-data-cop-guidebook && git log --oneline`
Expected: 6 commits, one per task in this plan, plus the earlier design-spec commit (7 total)

- [ ] **Step 4: Print handoff instructions**

No command to run — report the following to the user as the final output of this plan, since actually creating the remote repo and pushing is explicitly out of scope (requires `ESIPFed` org permissions this session doesn't have):

```
Local scaffold is complete and committed. To go live:

1. Create the repo (requires ESIPFed org admin/write access):
   gh repo create ESIPFed/eo-data-cop-guidebook --public \
     --description "Guidebook for creating and sustaining Earth observing data focused communities of practice." \
     --source=/Users/afriesz/eo-data-cop-guidebook --remote=origin

2. Push:
   cd /Users/afriesz/eo-data-cop-guidebook
   git push -u origin main

3. Enable GitHub Pages:
   In repo Settings > Pages, set Source to "Deploy from a branch",
   branch "gh-pages", folder "/ (root)". (The gh-pages branch is
   created automatically the first time the publish workflow runs
   after step 2.)

4. Confirm the Actions tab shows the "Quarto Publish" workflow
   succeeding, then visit https://esipfed.github.io/eo-data-cop-guidebook/
```

---

## Self-Review Notes

- **Spec coverage:** every section of the design spec (repo metadata, repo structure, `_quarto.yml`, deployment workflow, contribution workflow, license, validation, out-of-scope items) maps to a task above.
- **Placeholder scan:** no TBD/TODO markers; every step shows complete file content or an exact command with expected output.
- **Type/name consistency:** chapter file paths in Task 3 match verbatim what's referenced in `_quarto.yml` (Task 4); the `../../CONTRIBUTING.md` relative link in Task 3 matches `CONTRIBUTING.md`'s actual location (repo root) from Task 2.
