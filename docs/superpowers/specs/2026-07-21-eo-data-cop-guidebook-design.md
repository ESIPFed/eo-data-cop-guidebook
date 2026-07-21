# Design: eo-data-cop-guidebook

Date: 2026-07-21

## Purpose

Stand up a GitHub repository, `ESIPFed/eo-data-cop-guidebook`, that acts as a
web book (via Quarto + GitHub Pages) for the guide: *"Guidebook for creating
and sustaining Earth observing data focused communities of practice."*

The book must be easy for both non-technical community members (small edits
via the GitHub web UI) and technical contributors (standard fork/branch/PR
workflow) to contribute to.

## Repository metadata

- **Name:** `eo-data-cop-guidebook`
- **Org:** `ESIPFed`
- **Description:** "Guidebook for creating and sustaining Earth observing
  data focused communities of practice."
- **License:** CC BY 4.0 (content license — this is a guidebook, not
  software)
- **Site title:** "Guidebook for Earth Observation Data Communities of
  Practice"

## Repo structure

```
eo-data-cop-guidebook/
├── _quarto.yml              # book config: title, parts/chapters, theme, output
├── index.md                 # book landing page / preface
├── LICENSE                  # CC BY 4.0
├── README.md                # what this is, link to live site, how to contribute
├── CONTRIBUTING.md          # dual-path: web-edit quick fixes + full git/PR workflow
├── .github/
│   ├── workflows/
│   │   └── publish.yml      # quarto render + deploy to gh-pages on push to main
│   ├── ISSUE_TEMPLATE/
│   │   └── propose-chapter.md
│   └── PULL_REQUEST_TEMPLATE.md
├── chapters/
│   ├── getting-started/
│   │   ├── designing-your-community.md
│   │   ├── governance.md
│   │   ├── recruiting-members.md
│   │   └── welcome-inaugural-meeting.md
│   ├── sustaining-momentum/
│   │   ├── running-meetings.md
│   │   ├── communication.md
│   │   ├── engaging-member-participation.md
│   │   └── working-asynchronously.md
│   └── measuring-success/
│       ├── longevity-assessment.md
│       ├── cooperative-research-outcomes.md
│       └── attendance-metrics.md
└── .gitignore                # Quarto build artifacts (_book/, .quarto/)
```

Chapter files are plain `.md`, not `.qmd`: no code execution is needed for
this content, and `.md` renders as readable markdown directly in GitHub's
file viewer — important for non-technical contributors browsing or editing
on github.com. `.qmd` files show as raw text in GitHub's viewer.

On-disk layout mirrors the book's three parts as physical folders
(`chapters/getting-started/`, `chapters/sustaining-momentum/`,
`chapters/measuring-success/`) so contributors can navigate straight to the
right section without needing to understand `_quarto.yml`.

Starter content for each chapter is a **bare stub**: a title heading plus a
one-line "content coming soon" placeholder. No outline or scaffolding beyond
that — the community fills in real content via PRs.

## `_quarto.yml`

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

`repo-actions: [edit, issue]` puts an "Edit this page" link (opens GitHub's
web editor directly on that file) and a "Report an issue" link on every
rendered chapter — a direct fit for the dual-path contribution model.

## Deployment

`.github/workflows/publish.yml` runs on every push to `main`: installs
Quarto, renders the book, and publishes the `_book/` output to the
`gh-pages` branch via `quarto-dev/quarto-actions/publish`. GitHub Pages is
then configured (one-time, manual repo setting, done after the repo exists
on GitHub) to serve from the `gh-pages` branch.

Effect: merging a PR, or editing a file directly in the browser and
committing straight to `main`, triggers a live site rebuild. No contributor
needs Quarto installed locally.

## Contribution workflow

`CONTRIBUTING.md` documents two paths, most-common first:

1. **Quick fix (no git needed):** click "Edit this page" on the live site,
   edit the markdown in GitHub's web editor, submit — GitHub auto-creates a
   fork + PR.
2. **New chapter or larger change:** clone the repo, branch, add/edit files
   under `chapters/<part>/`, optionally `quarto preview` locally, open a PR.

It also documents: where new chapters go (which `part`, plus the one-line
addition needed in `_quarto.yml`), the bare-stub convention (a title +
placeholder is a valid PR), and a short style note (plain markdown, no code
chunks, headings start at `#`).

`.github/PULL_REQUEST_TEMPLATE.md`: short checklist (what changed, which
chapter/part, "renders locally" or "N/A — edited via web").

`.github/ISSUE_TEMPLATE/propose-chapter.md`: for proposing a new chapter or
restructuring — the book's outline itself should be community-proposable.

`README.md`: purpose paragraph (the repo description text), link to the
live Pages site, pointer to `CONTRIBUTING.md`.

## Validation

No traditional test suite. The meaningful check is "does the book render" —
the publish workflow itself is the validation (a PR that breaks
`_quarto.yml` or introduces a rendering error fails the Action). A local
`quarto render` will be run against the initial scaffold before handoff, if
Quarto is available in this environment, to confirm it builds cleanly.

## Out of scope / explicitly deferred

- Actually creating the GitHub repo under `ESIPFed` and pushing — this
  session prepares the full scaffold locally (git-initialized, committed);
  someone with `ESIPFed` org permissions creates the remote repo and pushes,
  then enables GitHub Pages (serve from `gh-pages` branch) in repo settings.
- Real chapter content — stubs only.
- Custom branding/theming beyond Quarto's built-in `cosmo` theme.
