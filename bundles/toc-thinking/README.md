# toc-thinking

<!-- description:start -->

Applies Goldratt's Thinking Processes to software: finds the core problem behind many symptoms, resolves the conflict that sustains it, and plans the change.

<!-- description:end -->

## Install

<!-- install:start -->

### Claude Code

```
/plugin marketplace add Akurganow/pegboard
/plugin install toc-thinking@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Codex

```
codex plugin marketplace add Akurganow/pegboard --ref main
codex plugin add toc-thinking@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Oh-My-Pi

```
omp plugin marketplace add Akurganow/pegboard
omp plugin install toc-thinking@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Hermes

```
hermes plugins install Akurganow/pegboard/plugins/toc-thinking --no-enable
hermes plugins list
hermes plugins enable toc-thinking
```

Keep the `plugins/toc-thinking` suffix: without it Hermes copies the whole repository, and its two-level scan finds no package.

CI installs it on Ubuntu and macOS.

### Cursor

Cursor's documentation names no command that installs from a repository. It names three routes:

- Public marketplace: open **Customize**, find the plugin, select **Install**. A plugin appears there only after Cursor reviews a submitted repository, and this repository claims no listing.
- Team marketplace, on Teams and Enterprise plans: in **Dashboard**, **Plugins & MCPs**, **Team Marketplaces**, select **Add Marketplace**, then **Import from Repo**, and paste `https://github.com/Akurganow/pegboard`. Developers then install from **Customize**.
- Local: copy `bundles/toc-thinking` to `~/.cursor/plugins/local/toc-thinking`, then restart Cursor or run **Developer: Reload Window**.

CI does not install it.

### OpenClaw

```
openclaw plugins install toc-thinking --marketplace Akurganow/pegboard
```

OpenClaw reads this repository's `.claude-plugin/marketplace.json`. CI does not install it.

### Kiro

No install command is given. Kiro's documentation says Powers follow the Agent Plugins specification, and `plugins/toc-thinking/plugin.json` carries every field the documentation requires. The documentation does not say how Kiro finds several packages in one repository. CI does not install it.

<!-- install:end -->

## Usage

List what you observe:

```text
Deploys fail about once a week, the nightly build is flaky, and on-call
pages keep coming back after every fix. Find the core problem.
```

The `root-cause` skill reads the code, history and logs first when the session has them. It builds a
Current Reality Tree from the symptoms down to the root causes, and checks each link that carries the
conclusion by naming an effect that must also exist if the link is true. It then resolves the conflict
that keeps the problem in place with an Evaporating Cloud, tests the fix with a Future Reality Tree and
plans the change with a Prerequisite Tree and a Transition Tree. It answers in one reply, as a draft
with its assumptions marked.

## What's inside

| Path | What it is |
| :-- | :-- |
| [`skills/root-cause/SKILL.md`](skills/root-cause/SKILL.md) | the procedure |
| [`skills/root-cause/references/tools.md`](skills/root-cause/references/tools.md) | the structure of each tree and of the cloud, and what a root cause is |
| [`skills/root-cause/references/clr.md`](skills/root-cause/references/clr.md) | the eight Categories of Legitimate Reservation, with software examples |
| [`skills/root-cause/references/sources.md`](skills/root-cause/references/sources.md) | the sources and what stays unread |
| `plugin.json` in `plugins/toc-thinking/`; `.claude-plugin/`, `.codex-plugin/` and `.cursor-plugin/` manifests in `bundles/toc-thinking/` | the Agent Plugins 1.0.0 manifest in the first build, one manifest per client in the second |
| [`LICENSE`](LICENSE) | the MIT license |

The package has no script, hook, rule file or network access.

The references rest on the TOCICO Dictionary and on Dettmer's *The Logical Thinking Process*, and
`sources.md` names the public copy of each by commit.

## Boundaries

- The skill says which facts it read, which you gave and which it assumed. It does not replace a
  profiler, a debugger or a test.
- A failure often has several root causes, and the skill reports them separately when the branches do
  not meet.
- A cloud that reduces to a trade-off between two measurable parameters belongs to the `contradiction`
  skill of [`triz-thinking`](https://github.com/Akurganow/pegboard/tree/main/plugins/triz-thinking).
  `root-cause` hands over only when `contradiction` is installed.

## License

MIT. See [LICENSE](LICENSE).

## Help

See [SUPPORT.md](https://github.com/Akurganow/pegboard/blob/main/SUPPORT.md). The [pegboard marketplace](https://github.com/Akurganow/pegboard#plugins) lists the other packages.
