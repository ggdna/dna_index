# dna_index

The DNA layer that gives every repo an `index.md` describing itself.

## Content

- `dna/doc/en/guides/index-guide.md` — when to create and update the
  index
- `dna/doc/templates/index-template.md` — domain, goal and interfaces of a
  repo

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-index   # TypeScript projects
dart pub add dev:dna_index    # Dart projects
helix init
```

The placed test instantiates and verifies the DNA on every test run. This
layer sits on top of
[dna_base](https://github.com/ggsuite/dna_base) — everything generic comes
from there, this repo only adds its own topic.

## Development

This repo has `role: "dna"` in `dna/_dna.json`: the `dna/` folder is
authored by hand, never generated. The repo instantiates its own DNA — run
`dart test` after changes; commit first (a file the DNA would overwrite
must not carry uncommitted work).
