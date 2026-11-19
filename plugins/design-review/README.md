# design-review

<!-- description:start -->

Reviews a software design for complexity with the red flags and principles of Ousterhout's A Philosophy of Software Design, each finding cited by chapter.

<!-- description:end -->

## Install

<!-- install:start -->

### Claude Code

```
/plugin marketplace add Akurganow/pegboard
/plugin install design-review@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Codex

```
codex plugin marketplace add Akurganow/pegboard --ref main
codex plugin add design-review@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Oh-My-Pi

```
omp plugin marketplace add Akurganow/pegboard
omp plugin install design-review@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Hermes

```
hermes plugins install Akurganow/pegboard/plugins/design-review --no-enable
hermes plugins list
hermes plugins enable design-review
```

Keep the `plugins/design-review` suffix: without it Hermes copies the whole repository, and its two-level scan finds no package.

CI installs it on Ubuntu and macOS.

### Cursor

Cursor's documentation names no command that installs from a repository. It names three routes:

- Public marketplace: open **Customize**, find the plugin, select **Install**. A plugin appears there only after Cursor reviews a submitted repository, and this repository claims no listing.
- Team marketplace, on Teams and Enterprise plans: in **Dashboard**, **Plugins & MCPs**, **Team Marketplaces**, select **Add Marketplace**, then **Import from Repo**, and paste `https://github.com/Akurganow/pegboard`. Developers then install from **Customize**.
- Local: copy `bundles/design-review` to `~/.cursor/plugins/local/design-review`, then restart Cursor or run **Developer: Reload Window**.

CI does not install it.

### OpenClaw

```
openclaw plugins install design-review --marketplace Akurganow/pegboard
```

OpenClaw reads this repository's `.claude-plugin/marketplace.json`. CI does not install it.

### Kiro

No install command is given. Kiro's documentation says Powers follow the Agent Plugins specification, and `plugins/design-review/plugin.json` carries every field the documentation requires. The documentation does not say how Kiro finds several packages in one repository. CI does not install it.

<!-- install:end -->

## Usage

Describe the design, or paste it:

```text
Review the design of our storage module. Callers must call open, configure
and start in that order before every read, and three services wrap it.
```

When the session has the repository, the `red-flags` skill reads the callers
and the change history itself and asks you only for what the code cannot say.
It answers in one reply: a verdict on your question, then findings ranked by
how often each part is touched and what touching it costs. Each finding gives
the place, the flag or principle with its chapter or section, the cause, the
change and what the change costs. At most three questions come at the end.

## What's inside

| Path | What it is |
| :-- | :-- |
| [`skills/red-flags/SKILL.md`](skills/red-flags/SKILL.md) | the procedure, the fourteen red flags and the sixteen principles with their sections |
| [`skills/red-flags/references/red-flags.md`](skills/red-flags/references/red-flags.md) | what to look for under each red flag |
| [`skills/red-flags/references/complexity.md`](skills/red-flags/references/complexity.md) | the definition of complexity, its weighting, and the studies on change history |
| [`skills/red-flags/references/principles.md`](skills/red-flags/references/principles.md) | depth, the limit of general-purpose modules, pulling complexity down |
| [`skills/red-flags/references/decisions.md`](skills/red-flags/references/decisions.md) | the criteria for together or apart, errors, design it twice, comments and names |
| [`skills/red-flags/references/positions.md`](skills/red-flags/references/positions.md) | where the book takes a side, the other side, and the evidence on TDD and method length |
| [`skills/red-flags/references/sources.md`](skills/red-flags/references/sources.md) | where each text was read, its kind and date, and what was not read |
| `plugin.json` in `plugins/design-review/`; `.claude-plugin/`, `.codex-plugin/` and `.cursor-plugin/` manifests in `bundles/design-review/` | the Agent Plugins 1.0.0 manifest in the first build, one manifest per client in the second |
| [`LICENSE`](LICENSE) | the MIT license |

The package has no script, hook, rule file or network access.

The book is under copyright. `sources.md` records the author's published
extract of the second edition and two public translation repositories that
carry the English, each named by commit, and no bought copy of either edition.
Chapter quotations are a few sentences at most.

## Boundaries

- The review weighs one quality: complexity in the book's sense.
- For method length, comments and test-driven development, a finding carries
  Robert Martin's reply from his written discussion with Ousterhout. The
  book's other positions carry no reply, because `positions.md` quotes no text
  of the other side for them.
- The weights come from version history when the repository is at hand. The
  skill says this is its proxy for the book's time spent, and `complexity.md`
  records that no study read tests change frequency times complexity as a
  ranking.
- A trade-off between two measured qualities belongs to the `contradiction`
  skill of [`triz-thinking`](https://github.com/Akurganow/pegboard/tree/main/plugins/triz-thinking). Many symptoms with
  one unclear cause belong to `root-cause` in
  [`toc-thinking`](https://github.com/Akurganow/pegboard/tree/main/plugins/toc-thinking). What a reader cannot hold
  in their head belongs to `extraneous` in
  [`cognitive-load`](https://github.com/Akurganow/pegboard/tree/main/plugins/cognitive-load). The skill offers a hand-over
  only to a skill that is installed.

## License

MIT. See [LICENSE](LICENSE).

## Help

See [SUPPORT.md](https://github.com/Akurganow/pegboard/blob/main/SUPPORT.md). The [pegboard marketplace](https://github.com/Akurganow/pegboard#plugins) lists the other packages.
