# web-studio

A Claude Code plugin that walks a model through designing and building a website in five reviewed steps, so the result has a clear visual direction instead of the usual template look.

## At a glance

- **What it is.** One skill (`/web-studio`) and 34 reference files: 20 written design directions, notes on four animation and 3D libraries, colour, type and motion references, and three quality checklists.
- **My part.** I wrote the pipeline, chose the design directions and the checks, and tested it on my own site work in spring 2026.
- **What it is not.** It does not make the model a designer. It gives the model a process and a vocabulary, and it still needs a person to review every step.

## How it works

1. **Design direction.** Pick one of the 20 directions (for example `apple-minimal`, `editorial-serif`, `brutalist-pop`) or describe your own. The model writes it down before any code.
2. **Layout.** Page structure and grid, checked against the direction.
3. **Type and art.** Font pairing from the font notes, colour from the colour notes, and any generated art or SVG illustration.
4. **Motion.** Scroll and entrance animation with GSAP, Lenis, Motion or Three.js, using the patterns in `libraries/`.
5. **Polish.** Three checklists: an audit for generic AI-looking output, an accessibility check, and a performance budget.

Each step stops for your review. `--quick` skips the stops for a rough first draft.

## Install

In Claude Code:

```
/plugin marketplace add harveyjenkins03-coder/web-studio-plugin
/plugin install web-studio@web-studio-plugin
```

Then restart Claude Code or run `/reload-plugins`.

## Use

```
/web-studio            # all five steps, with a review stop after each
/web-studio --quick    # one pass, no stops
```

Asking Claude to "design a landing page with web-studio" also starts it.

## Limits

- The output is model-written code. Review it, test it, and check its accessibility before you ship it.
- Some libraries it suggests have their own licences. Check each one before you ship.
- The design directions name real studios and sites as reference points. That is for describing a style, not for copying anyone's work. See [DISCLAIMER.md](DISCLAIMER.md).

## How this was made

I wrote the pipeline and chose its contents with Claude Code's help; Claude drafted most of the reference files under my direction and I edited and tested them. This repository was re-published on 2026-11-25 as a single clean commit; the skill files are unchanged from the April 2026 release. What changed: this README, the plugin description, the disclaimer's headings and punctuation, and a new marketplace file so the install commands above work (checked with `claude plugin validate`).

## Licence

MIT. See [LICENSE](LICENSE).
