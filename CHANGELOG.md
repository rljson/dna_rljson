# Changelog

## Unreleased

### Changed

- Lift the `mustOverride` duty for `dnaCopyrightHolder`, `dnaCompany`,
  `dnaGitOrg`, `dnaGitOrgUrl` and `dnaJiraPrefix`: a repo takes the rljson
  values from this layer instead of repeating them in its own
  `dna/_vars.json` (format version 2)
- Ship `scripts/functions/colors.js` and `run-command.js`, which the repos'
  own scripts import and the upgraded layers no longer place

## 0.3.0 - 2026-10-29

### Changed

- Move to dna-gg 1.x: the `/gg-*` skills, the development guide, the hooks
- Publish to npm only (`publish_to: none`)

## 0.2.0 - 2026-09-07

## 0.1.1 - 2026-08-20

### Fixed

- README: name the layers the table actually lists, wrap the prose the
way every other README in the family does, and state the license
holder the way the engine renders it.

## 0.1.0 - 2026-08-20

- First release. The rljson umbrella: every topic layer in one dependency, replacing the script that copied doc, scripts and settings out of template-project.
