# cognitive-load

<!-- description:start -->

Separates the cognitive load a task needs from the load a code base's structure adds, and names the change that removes the second.

<!-- description:end -->

## Install

<!-- install:start -->

### Claude Code

```
/plugin marketplace add Akurganow/pegboard
/plugin install cognitive-load@pegboard
```

Source: Claude Code documentation, <https://code.claude.com/docs/en/discover-plugins>. CI installs it on Ubuntu, macOS and Windows.

### Codex

```
codex plugin marketplace add Akurganow/pegboard --ref main
codex plugin add cognitive-load@pegboard
```

Source: Codex documentation, <https://developers.openai.com/plugins/build/plugins>, for `marketplace add`; Codex source, [`plugin_cmd.rs`](https://github.com/openai/codex/blob/e3e5ad28470f6a225301518c30a66e749a880164/codex-rs/cli/src/plugin_cmd.rs), for `plugin add`. CI installs it on Ubuntu, macOS and Windows.

### Oh-My-Pi

```
omp plugin marketplace add Akurganow/pegboard
omp plugin install cognitive-load@pegboard
```

Source: Oh-My-Pi documentation, [`docs/marketplace.md`](https://github.com/can1357/oh-my-pi/blob/a33cc26824e3c91edd9fa42d681f10dceb4ac2f0/docs/marketplace.md). CI installs it on Ubuntu, macOS and Windows.

### Hermes

```
hermes plugins install Akurganow/pegboard/plugins/cognitive-load --no-enable
hermes plugins list
hermes plugins enable cognitive-load
```

Keep the `plugins/cognitive-load` suffix: without it Hermes copies the whole repository, and its [two-level scan](https://github.com/NousResearch/hermes-agent/blob/a0ca7c19204e514f9590ce3b812e029b315ab9e9/website/docs/user-guide/features/plugins.md) finds no package.

Source: Hermes documentation, [`developer-guide/plugins/index.md`](https://github.com/NousResearch/hermes-agent/blob/a0ca7c19204e514f9590ce3b812e029b315ab9e9/website/docs/developer-guide/plugins/index.md), for the commands; Hermes source, [`plugins_cmd.py`](https://github.com/NousResearch/hermes-agent/blob/a0ca7c19204e514f9590ce3b812e029b315ab9e9/hermes_cli/plugins_cmd.py) (`_resolve_git_url`), for the subdirectory form and what happens without it. CI installs it on Ubuntu and macOS.

### Cursor

Cursor's documentation names no command that installs from a repository. It names three routes:

- Public marketplace: open **Customize**, find the plugin, select **Install**. A plugin appears there only after Cursor reviews a submitted repository, and this repository claims no listing.
- Team marketplace, on Teams and Enterprise plans: in **Dashboard**, **Plugins & MCPs**, **Team Marketplaces**, select **Add Marketplace**, then **Import from Repo**, and paste `https://github.com/Akurganow/pegboard`. Developers then install from **Customize**.
- Local: copy `bundles/cognitive-load` to `~/.cursor/plugins/local/cognitive-load`, then restart Cursor or run **Developer: Reload Window**.

Source: Cursor documentation, [Plugins](https://cursor.com/docs/plugins), read 2026-11-04, for the three routes; [Plugins reference](https://cursor.com/docs/reference/plugins), read 2026-11-04, for the submission and review. CI does not install it.

### OpenClaw

```
openclaw plugins install cognitive-load --marketplace Akurganow/pegboard
```

Source: OpenClaw documentation, [`docs/cli/plugins/install.md`](https://github.com/openclaw/openclaw/blob/db6ac584cf205ea9a72de7ae83a4e65199b926a4/docs/cli/plugins/install.md#L277-L283). OpenClaw reads this repository's `.claude-plugin/marketplace.json` (OpenClaw source, [`marketplace.ts`](https://github.com/openclaw/openclaw/blob/db6ac584cf205ea9a72de7ae83a4e65199b926a4/src/plugins/marketplace.ts#L35-L38)). CI does not install it.

### Kiro

No install command is given. Kiro's documentation says Powers follow the Agent Plugins specification, and `plugins/cognitive-load/plugin.json` carries every field the documentation requires. The documentation does not say how Kiro finds several packages in one repository. CI does not install it.

Source: Kiro documentation, [Create a power](https://kiro.dev/docs/powers/create) and [Installation](https://kiro.dev/docs/powers/installation), read 2026-11-04.

<!-- install:end -->

## Usage

Name the task and the place where readers struggle:

```text
New hires take weeks to fix their first bug in our billing service.
Find what makes the code hard to follow.
```

The `extraneous` skill answers in one reply. When the session holds the code and
its history, it reads them instead of asking, and reports what it had to open
and hold as its own trace of the path. For each place it names the concrete
behaviour a reader has to discover, sorts the elements into intrinsic and
extraneous, matches them to a section of Zakirullin's catalogue, and gives the
change that removes the extraneous ones, its cost and who pays it. It asks only
what the code cannot say, at the end.

## What's inside

| Path | What it is |
| :-- | :-- |
| [`skills/extraneous/SKILL.md`](skills/extraneous/SKILL.md) | the procedure |
| [`skills/extraneous/references/theory.md`](skills/extraneous/references/theory.md) | the working definitions with primary citations, and where the theory stops |
| [`skills/extraneous/references/patterns.md`](skills/extraneous/references/patterns.md) | the essay's catalogue in its own words |
| [`skills/extraneous/references/measures.md`](skills/extraneous/references/measures.md) | Cognitive Complexity, Intrinsic Complexity Points, studies of programmers, studies of language-model agents |
| [`skills/extraneous/references/sources.md`](skills/extraneous/references/sources.md) | the copy, commit and date each source was read from, and whether the full text or only the abstract was open |
| `plugin.json` in `plugins/cognitive-load/`; `.claude-plugin/`, `.codex-plugin/` and `.cursor-plugin/` manifests in `bundles/cognitive-load/` | the Agent Plugins 1.0.0 manifest in the first build, one manifest per client in the second |
| [`LICENSE`](LICENSE) | the MIT license |

The package has no script, hook, rule file or network access. The catalogue is
Artem Zakirullin's essay "Cognitive load is what matters", under CC BY 4.0.

## Boundaries

- Cognitive load theory is a theory of learning, and its effects were shown on
  instructional material. The skill applies them to code as analogies and says
  so. Its count of what a reader holds is the agent's trace of a path through
  the code, not a measurement of a human reader.
- An interface as wide as what it hides, or one change that touches many places,
  belongs to the `red-flags` skill of
  [`design-review`](https://github.com/Akurganow/pegboard/tree/main/plugins/design-review).
  A trade-off between two measured qualities belongs to `contradiction` in
  [`triz-thinking`](https://github.com/Akurganow/pegboard/tree/main/plugins/triz-thinking).
  Many complaints with one unclear cause belong to `root-cause` in
  [`toc-thinking`](https://github.com/Akurganow/pegboard/tree/main/plugins/toc-thinking).
  The skill hands over only to a skill that is installed.

## License

MIT. See [LICENSE](LICENSE).

## Help

See [SUPPORT.md](https://github.com/Akurganow/pegboard/blob/main/SUPPORT.md). The [pegboard marketplace](https://github.com/Akurganow/pegboard#plugins) lists the other packages.
