# dna_index

English | [Deutsch](README.de.md)

Gives a repo an index.jsonc that describes it for planning, with a guide, a
template and a skill that keeps it current.

## Motivation

Planning a ticket starts with the question which repos it touches. Reading
every repo to answer it costs time and tokens. This layer gives every repo a
short, keyword-style description of itself — name, summary, domain, the repos
it uses and the repos that use it — so a developer or an agent reads the index
files first and then picks the repos the ticket needs. The guide keeps the
index current by updating it before every publish.

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-index   # TypeScript projects
dart pub add dev:dna_index     # Dart projects
helix init
```

`helix init` places a test that instantiates and verifies the DNA on every
test run. It copies the guide to `doc/guides/`, the template to
`doc/templates/` and the skill to `.claude/skills/index/`.

Type `/index` in Claude Code to create `index.jsonc` in the repo root from the
template, or to compare an existing one against the code and update it. The
skill shows the diff before anything is committed.

## Guides

- `dna/doc/guides/index-guide.md` — when to create `index.jsonc`, how to use
  the index files for planning a ticket, and that it is updated before each
  publish, in keywords instead of sentences

## Templates

- `dna/doc/templates/index-template.jsonc` — the fields of `index.jsonc`:
  name, summary, domain and the interfaces to other repos, with a comment
  explaining each field

## Skills

- `/index` — reports a missing `index.jsonc`, entries that no longer exist in
  the code and interfaces that are missing, then writes the index; follows the
  index guide

## Scope

The layer only defines the index and keeps it current. It does not write the
index on its own, ships no `index.jsonc` for the consuming repo, and leaves the
ticket workflow that reads the index files to other layers such as
[dna_gg](https://github.com/ggsuite/dna_gg).

## Layers

The layer is orthogonal: `dna/_dna.json` lists no parent layers. It carries
only its own topic and is combined with other layers by the consuming repo.

## Variables

- `dnaCopyrightHolder` — the holder named in the copyright header of every
  placed file. `mustOverride` in `dna/_dna.json` forces every repo or layer
  that lists this layer to set it in its own `dna/_vars.json`; an umbrella
  such as dna_ggdna sets it once for its organization

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a file
the DNA would overwrite must not carry uncommitted work.

Edit the files below `dna/`, never their copies in `doc/` and `.claude/`: the
test overwrites them.

## License

MIT — see [LICENSE](LICENSE).
