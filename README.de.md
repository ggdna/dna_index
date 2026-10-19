# dna_index

[English](README.md) | Deutsch

Gibt einem Repo eine index.jsonc, die es für die Planung beschreibt, mit einem
Guide, einem Template und einem Skill, der sie aktuell hält.

## Motivation

Die Planung eines Tickets beginnt mit der Frage, welche Repos es betrifft.
Jedes Repo dafür zu lesen kostet Zeit und Tokens. Diese Schicht gibt jedem Repo
eine kurze Selbstbeschreibung in Stichworten — Name, Zusammenfassung, Domäne,
die Repos, die es nutzt, und die Repos, die es nutzen —, sodass Entwickler oder
Agenten zuerst die Index-Dateien lesen und dann die Repos auswählen, die das
Ticket braucht. Der Guide hält den Index aktuell, indem er ihn vor jedem
Publish aktualisieren lässt.

## Verwendung

Als Dev-Dependency eintragen und einmal initialisieren:

```bash
pnpm add -D @ggdna/dna-index   # TypeScript projects
dart pub add dev:dna_index     # Dart projects
helix init
```

`helix init` legt einen Test ab, der die DNA bei jedem Testlauf instanziiert
und prüft. Er kopiert den Guide nach `doc/guides/`, das Template nach
`doc/templates/` und den Skill nach `.claude/skills/index/`.

Tippe `/index` in Claude Code, um `index.jsonc` im Wurzelverzeichnis des Repos
aus dem Template anzulegen oder eine vorhandene mit dem Code abzugleichen und
zu aktualisieren. Der Skill zeigt den Diff, bevor etwas committet wird.

## Guides

- `dna/doc/guides/index-guide.md` — wann `index.jsonc` angelegt wird, wie die
  Index-Dateien bei der Planung eines Tickets helfen und dass der Index vor
  jedem Publish aktualisiert wird, in Stichworten statt in Sätzen

## Templates

- `dna/doc/templates/index-template.jsonc` — die Felder von `index.jsonc`:
  Name, Zusammenfassung, Domäne und die Schnittstellen zu anderen Repos, mit
  einem Kommentar zu jedem Feld

## Skills

- `/index` — meldet eine fehlende `index.jsonc`, Einträge, die es im Code
  nicht mehr gibt, und fehlende Schnittstellen und schreibt dann den Index;
  folgt dem Index-Guide

## Umfang

Die Schicht legt nur den Index fest und hält ihn aktuell. Sie schreibt den
Index nicht von selbst, liefert dem nutzenden Repo keine `index.jsonc` und
überlässt den Ticket-Ablauf, der die Index-Dateien liest, anderen Schichten wie
[dna_gg](https://github.com/ggsuite/dna_gg).

## Schichten

Die Schicht ist orthogonal: `dna/_dna.json` nennt keine Eltern-Schichten. Sie
trägt nur ihr eigenes Thema und wird vom nutzenden Repo mit anderen Schichten
kombiniert.

## Variablen

- `dnaCopyrightHolder` — der Rechteinhaber im Copyright-Kopf jeder abgelegten
  Datei. `mustOverride` in `dna/_dna.json` zwingt jedes Repo und jede Schicht,
  die diese Schicht einbindet, ihn in der eigenen `dna/_vars.json` zu setzen;
  ein Umbrella wie dna_ggdna setzt ihn einmal für seine Organisation

## Entwicklung

Der Ordner `dna/` ist handgeschriebene Quelle und wird nie generiert. Das Repo
instanziiert seine eigene DNA — nach Änderungen `dart test` laufen lassen;
vorher committen, denn eine Datei, die die DNA überschreiben würde, darf keine
uncommittete Arbeit enthalten.

Bearbeite die Dateien unter `dna/`, nie ihre Kopien in `doc/` und `.claude/`:
Der Test überschreibt sie.

## Lizenz

MIT — siehe [LICENSE](LICENSE).
