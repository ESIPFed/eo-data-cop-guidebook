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
