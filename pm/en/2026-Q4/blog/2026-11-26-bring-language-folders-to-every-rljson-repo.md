<!--
@license
Copyright (c) rljson

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Bring Language Folders to Every rljson Repo

## Motivation

- This umbrella layer gives every rljson repo the whole set of topic
  layers. The topic layers now keep documentation per language:
  `doc/<lang>/` without a quarter, `pm/<lang>/<yyyy>-Q<n>/` for
  everything planned.
- The rljson guides of this layer follow the same layout, so a repo gets
  them in English, German and Farsi.

## Strategy

- Move the own guides of the layer below `dna/doc/en/`
- Add German and Farsi translations
- Point `dna/CLAUDE.md` to the new paths

## Implementation 1: The rljson guides

- `rljson-guide.md` and `for-ai/rljson-review-guide.md` moved to
  `dna/doc/en/guides/`
- New German and Farsi versions in `dna/doc/de/guides/` and
  `dna/doc/fa/guides/`, with fixed English anchors on translated headings
- `dna/CLAUDE.md` imports `doc/en/guides/rljson-guide.md` and points
  reviews to `doc/en/guides/for-ai/rljson-review-guide.md`

## What a consumer gets from the updated layers

- All generated guides under `doc/en/`, `doc/de/` and `doc/fa/`
- `/blog` writes to `pm/<lang>/<yyyy>-Q<n>/blog`, `/translate` syncs all
  languages set by `dnaLanguages`, `scripts/check-readme.js` checks
  `README.<lang>.md` for each of them
- New `/gg-review-architecture` with `doc/en/guides/architecture-guide.md`
- `/gg-ticket` derives a slug id, `/gg-commit` commits all ticket repos
  at once, `/gg-publish` runs from the workspace root with `-i <ticket>`
- `install-pnpm-guide.md` replaces `install-corepack-guide.md`
- The pm-prompts hook and its `.claude/settings.json` are no longer
  generated

## Open Points

- The README still describes dna_translate as "de and en in sync"
