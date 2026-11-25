# Example

`dna_index` is a DNA layer: it ships the index guide, the `index.jsonc`
template and the `/index` skill, no library code. Declare it as a dev
dependency and instantiate it once:

```bash
dart pub add dev:dna_index    # Dart projects
pnpm add -D @ggdna/dna-index  # TypeScript projects
gg dna init
gg dna build
```

Then type `/index` in Claude Code: it creates or updates the
`index.jsonc` that describes the repo.
