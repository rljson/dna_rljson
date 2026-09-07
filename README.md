# dna_rljson

The DNA of every rljson repo: one dependency that pulls in the whole set
of topic layers.

Add this one layer and a repo gets the README structure, the guides, the
translations, the index, the blog format, the install guides, the VS Code
settings, the clean code and test conventions, and the gg workflow. It
takes over from copying doc, scripts and settings out of
`template-project` with `update-dna.js`: the engine merges the layers and
instantiates them on every test run, and it reports what it changed
instead of overwriting silently.

## Layers

| Layer                                                     | What it brings                                                 |
| --------------------------------------------------------- | -------------------------------------------------------------- |
| [dna_readme](https://github.com/ggdna/dna_readme)         | README structure and templates                                 |
| [dna_guides](https://github.com/ggdna/dna_guides)         | developer and AI guides                                        |
| [dna_translate](https://github.com/ggdna/dna_translate)   | multi-language docs, de and en in sync                         |
| [dna_index](https://github.com/ggdna/dna_index)           | index and navigation files                                     |
| [dna_blog](https://github.com/ggdna/dna_blog)             | blog format, templates, layout                                 |
| [dna_install](https://github.com/ggdna/dna_install)       | install guides: editor, node, Azure, tooling                   |
| [dna_clean_code](https://github.com/ggdna/dna_clean_code) | how code is written and tested, incl. the TypeScript specifics |
| [dna_gg](https://github.com/ggdna/dna_gg)                 | the gg workflow: ticket, commit, push, publish                 |

This layer carries no files of its own — it exists to compose the ones
above. Everything an rljson repo sees comes from them.

## Layers left out on purpose

- [dna_vscode](https://github.com/ggdna/dna_vscode) — the rljson repos
  carry their own `.vscode` settings, with the ESLint and Dart
  configuration their developers work with every day. Taking the layer
  would replace that, and change how people work, for no gain.
- [dna_scripts](https://github.com/ggdna/dna_scripts) — the repos keep
  their own workflow scripts. `dna_gg` no longer pulls this layer in; the
  only script that comes along is `delete-feature-branch.js`, the one
  `dna_gg` calls itself from `/cleanup`.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file,
  set to `rljson` here

  Substitution is case-adaptive: a `dnaCopyrightHolder` reference renders
  the value in camelCase, so the header reads `Copyright (c) rljson`. To
  carry a capitalized name into the header, reference it in Pascal form.

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @rljson/dna-rljson   # TypeScript projects
dart pub add dev:dna_rljson      # Dart projects
gg dna init
```

The placed test instantiates and verifies the DNA on every test run.

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.
