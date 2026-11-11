# triz-thinking

<!-- description:start -->

Resolves software trade-offs with TRIZ: the contradiction matrix and 40 inventive principles, the separation principles, and ARIZ-85C walked part by part.

<!-- description:end -->

## Install

<!-- install:start -->

### Claude Code

```
/plugin marketplace add Akurganow/pegboard
/plugin install triz-thinking@pegboard
```

Source: Claude Code documentation, <https://code.claude.com/docs/en/discover-plugins>. CI installs it on Ubuntu, macOS and Windows.

### Codex

```
codex plugin marketplace add Akurganow/pegboard --ref main
codex plugin add triz-thinking@pegboard
```

Source: Codex documentation, <https://developers.openai.com/plugins/build/plugins>, for `marketplace add`; Codex source, [`plugin_cmd.rs`](https://github.com/openai/codex/blob/e3e5ad28470f6a225301518c30a66e749a880164/codex-rs/cli/src/plugin_cmd.rs), for `plugin add`. CI installs it on Ubuntu, macOS and Windows.

### Oh-My-Pi

```
omp plugin marketplace add Akurganow/pegboard
omp plugin install triz-thinking@pegboard
```

Source: Oh-My-Pi documentation, [`docs/marketplace.md`](https://github.com/can1357/oh-my-pi/blob/a33cc26824e3c91edd9fa42d681f10dceb4ac2f0/docs/marketplace.md). CI installs it on Ubuntu, macOS and Windows.

### Hermes

```
hermes plugins install Akurganow/pegboard/plugins/triz-thinking --no-enable
hermes plugins list
hermes plugins enable triz-thinking
```

Keep the `plugins/triz-thinking` suffix: without it Hermes copies the whole repository, and its [two-level scan](https://github.com/NousResearch/hermes-agent/blob/a0ca7c19204e514f9590ce3b812e029b315ab9e9/website/docs/user-guide/features/plugins.md) finds no package.

Source: Hermes documentation, [`developer-guide/plugins/index.md`](https://github.com/NousResearch/hermes-agent/blob/a0ca7c19204e514f9590ce3b812e029b315ab9e9/website/docs/developer-guide/plugins/index.md), for the commands; Hermes source, [`plugins_cmd.py`](https://github.com/NousResearch/hermes-agent/blob/a0ca7c19204e514f9590ce3b812e029b315ab9e9/hermes_cli/plugins_cmd.py) (`_resolve_git_url`), for the subdirectory form and what happens without it. CI installs it on Ubuntu and macOS.

### Cursor

Cursor's documentation names no command that installs from a repository. It names three routes:

- Public marketplace: open **Customize**, find the plugin, select **Install**. A plugin appears there only after Cursor reviews a submitted repository, and this repository claims no listing.
- Team marketplace, on Teams and Enterprise plans: in **Dashboard**, **Plugins & MCPs**, **Team Marketplaces**, select **Add Marketplace**, then **Import from Repo**, and paste `https://github.com/Akurganow/pegboard`. Developers then install from **Customize**.
- Local: copy `bundles/triz-thinking` to `~/.cursor/plugins/local/triz-thinking`, then restart Cursor or run **Developer: Reload Window**.

Source: Cursor documentation, [Plugins](https://cursor.com/docs/plugins), read 2026-11-04, for the three routes; [Plugins reference](https://cursor.com/docs/reference/plugins), read 2026-11-04, for the submission and review. CI does not install it.

### OpenClaw

```
openclaw plugins install triz-thinking --marketplace Akurganow/pegboard
```

Source: OpenClaw documentation, [`docs/cli/plugins/install.md`](https://github.com/openclaw/openclaw/blob/db6ac584cf205ea9a72de7ae83a4e65199b926a4/docs/cli/plugins/install.md#L277-L283). OpenClaw reads this repository's `.claude-plugin/marketplace.json` (OpenClaw source, [`marketplace.ts`](https://github.com/openclaw/openclaw/blob/db6ac584cf205ea9a72de7ae83a4e65199b926a4/src/plugins/marketplace.ts#L35-L38)). CI does not install it.

### Kiro

No install command is given. Kiro's documentation says Powers follow the Agent Plugins specification, and `plugins/triz-thinking/plugin.json` carries every field the documentation requires. The documentation does not say how Kiro finds several packages in one repository. CI does not install it.

Source: Kiro documentation, [Create a power](https://kiro.dev/docs/powers/create) and [Installation](https://kiro.dev/docs/powers/installation), read 2026-11-04.

<!-- install:end -->

## Usage

Describe the trade-off in your own words:

```text
A longer cache lifetime takes load off the database but serves stale reads.
Find a way out that is not a compromise.
```

The `contradiction` skill reads your code and history when the session has
them. It states the contradiction and the ideal final result, maps both sides
to two or three of Altshuller's 39 parameters, reads each pair's cell of the
contradiction matrix, and writes what each principle in the cell would mean
in your system. The reply leads with the strongest direction, stated as a
change to a named part of your system.

A problem that has outlasted earlier fixes, or whose tensions feed each
other, goes to the `ariz` skill. It walks ARIZ-85C: Parts 1 to 3 compactly in
the first reply, then directions from Parts 4 and 5, with assumed facts
marked. A restated technical contradiction goes back to `contradiction`.

## What's inside

| Path | What it is |
| :-- | :-- |
| [`skills/contradiction/SKILL.md`](skills/contradiction/SKILL.md) | the matrix route |
| [`skills/contradiction/references/parameters.md`](skills/contradiction/references/parameters.md) | the 39 parameters, each with a reading for software |
| [`skills/contradiction/references/principles.md`](skills/contradiction/references/principles.md) | the 40 principles with a reading for software and, where one exists, the analogy of Rea or Fulbright; `ariz` reads it too |
| [`skills/contradiction/references/matrix/`](skills/contradiction/references/matrix/) | the classic matrix as 39 files, `01.md` to `39.md`, one per improving parameter, and `provenance.md` |
| [`skills/contradiction/references/sources.md`](skills/contradiction/references/sources.md) | where each reference of both skills was read, and what was not read |
| [`skills/ariz/SKILL.md`](skills/ariz/SKILL.md) | the ARIZ-85C walk, for a problem that has outlasted earlier fixes |
| [`skills/ariz/references/ariz-85c.md`](skills/ariz/references/ariz-85c.md) | the nine parts and forty steps of ARIZ-85C, with the formulas quoted and a software gloss |
| `plugin.json` in `plugins/triz-thinking/`; `.claude-plugin/`, `.codex-plugin/` and `.cursor-plugin/` manifests in `bundles/triz-thinking/` | the Agent Plugins 1.0.0 manifest in the first build, one manifest per client in the second |
| [`LICENSE`](LICENSE) | the MIT license |

The package has no script, hook, rule file or network access. A lookup is
one file read, such as `matrix/09.md`.

The matrix is the classic 39-by-39 table with 1,248 non-empty cells, settled
by majority from several public transcriptions. [The Altshuller Foundation's
page](https://www.altshuller.ru/triz/technique2.asp) of the table, read on
2026-11-11, presents itself as Appendix 1 of the 1973 edition of «Алгоритм изобретения». The 1973 print was not read.
`matrix/provenance.md` lists every reading of each disputed cell.

## Boundaries

- The matrix, the principles and ARIZ give directions, not guarantees. Your
  knowledge of your system decides which direction survives.
- A problem with no trade-off in it is not a TRIZ problem. Both skills say so.
- The software readings of the parameters and principles are this package's
  own, except the analogies marked with their author. `sources.md` reports
  finding no published mapping of the parameters to software, no study of the
  classic matrix on software problems, and no published software reading of
  the 76 standard solutions. The package carries ARIZ-85C's table of typical
  transformations, not the standard solutions or the pointer to physical
  effects.
- A tangle of symptoms with no trade-off in sight belongs to the `root-cause`
  skill of [`toc-thinking`](https://github.com/Akurganow/pegboard/tree/main/plugins/toc-thinking).
  Both skills hand over only when it is installed.

## License

MIT. See [LICENSE](LICENSE).

## Help

See [SUPPORT.md](https://github.com/Akurganow/pegboard/blob/main/SUPPORT.md). The [pegboard marketplace](https://github.com/Akurganow/pegboard#plugins) lists the other packages.
