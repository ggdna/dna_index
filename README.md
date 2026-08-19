# dna_index

The DNA layer that gives every repo an `index.jsonc` describing itself.

## Guides

- `dna/doc/guides/index-guide.md` — when to create the index, how to use
  it for planning, and when to update it

## Templates

- `dna/doc/templates/index-template.jsonc` — name, summary, domain and
  interfaces of a repo, with a comment explaining each field

## Skills

- `/index` — compares the index against the code that is actually there
  and reports entries that no longer exist

## Layers

Orthogonal: this layer carries only its own topic and is combined with
other layers by the consuming repo.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-index   # TypeScript projects
dart pub add dev:dna_index         # Dart projects
helix init
```

The placed test instantiates and verifies the DNA on every test run.

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.
