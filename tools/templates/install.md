### Claude Code

```
/plugin marketplace add Akurganow/pegboard
/plugin install {{name}}@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Codex

```
codex plugin marketplace add Akurganow/pegboard --ref main
codex plugin add {{name}}@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Oh-My-Pi

```
omp plugin marketplace add Akurganow/pegboard
omp plugin install {{name}}@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Hermes

```
hermes plugins install Akurganow/pegboard/plugins/{{name}} --no-enable
hermes plugins list
hermes plugins enable {{name}}
```

Keep the `plugins/{{name}}` suffix: without it Hermes copies the whole repository, and its two-level scan finds no package.

CI installs it on Ubuntu and macOS.

### Cursor

Cursor's documentation names no command that installs from a repository. It names three routes:

- Public marketplace: open **Customize**, find the plugin, select **Install**. A plugin appears there only after Cursor reviews a submitted repository, and this repository claims no listing.
- Team marketplace, on Teams and Enterprise plans: in **Dashboard**, **Plugins & MCPs**, **Team Marketplaces**, select **Add Marketplace**, then **Import from Repo**, and paste `https://github.com/Akurganow/pegboard`. Developers then install from **Customize**.
- Local: copy `bundles/{{name}}` to `~/.cursor/plugins/local/{{name}}`, then restart Cursor or run **Developer: Reload Window**.

CI does not install it.

### OpenClaw

```
openclaw plugins install {{name}} --marketplace Akurganow/pegboard
```

OpenClaw reads this repository's `.claude-plugin/marketplace.json`. CI does not install it.

### Kiro

No install command is given. Kiro's documentation says Powers follow the Agent Plugins specification, and `plugins/{{name}}/plugin.json` carries every field the documentation requires. The documentation does not say how Kiro finds several packages in one repository. CI does not install it.
