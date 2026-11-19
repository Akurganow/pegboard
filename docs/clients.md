# How each client loads a package

This page says what each client reads from a package in this repository.
Install commands and install-time notes are in the [README](../README.md#install).
The reasons built on these facts are in [About this repository's design](design.md).

## Claude Code

### Manifest and fetch

- The documented manifest location is `.claude-plugin/plugin.json` under the plugin root.
- A manifest that is not valid JSON fails with `Plugin <name> has a corrupt manifest file`.
- Claude Code strips an unrecognized top-level manifest field, and the plugin loads.
  `claude plugin validate` reports the field as a warning.
- Claude Code clones a marketplace hosted in git onto the user's machine.
- A plugin starts enabled unless `defaultEnabled` is `false`.
- Users stay on their cached copy until the `version` string changes.
- Release tags take the form `<plugin-name>--v<version>`.
- The desktop app accepts marketplace and plugin names of at most 128 characters from letters, digits, `.`, `_` and `-`.
  A name starts with a letter or digit.
  Every name here meets that rule.
- The desktop app installs from configured marketplaces: the **+** button, then **Plugins**, then **Add plugin**.
- A change here reaches Claude Code users only after the plugin's next release.
  It arrives through background auto-update once a user or an admin turns that on, and otherwise when the user updates the plugin.

### Skills

- Claude Code namespaces a plugin skill by its plugin: `skills/review/` in `my-plugin` is `/my-plugin:review`.
  The bare `/review` also works unless another command already uses that name.
- Skill descriptions sit in context, and a skill's full content loads only when it is invoked.

### Always-on instructions

- A `CLAUDE.md` at the plugin root is not loaded as context.
  The manifest reference directs instructions into a skill.
- The component list names no `rules/` directory.
- For `SessionStart`, Claude Code adds plain-text stdout to the context.
  Stdout that starts with `{` and ends with `}` is parsed as JSON instead.
- `SessionStart` matchers are `startup`, `resume`, `clear`, `compact` and `fork`.
- After compaction, `SessionStart` hooks matching `compact` run, and their output joins the compacted context.
- Plain stdout and `additionalContext` are capped at 10,000 characters.
  Longer text reaches Claude as a file path and a preview.
- The Hooks page advises writing hook context as factual statements, not imperative system instructions.
  Text framed as out-of-band system commands can trigger Claude's prompt-injection defences, and Claude then shows it to the user instead.
- `SubagentStart` adds its `additionalContext` to a subagent's context before the first prompt.
  The Hooks page documents no plain-stdout route for this event.
- When the hook runs again for the same subagent, Claude Code injects its context only if the earlier copy is gone.
  Auto-compaction discards that copy, so the next run's context arrives again.
- A command hook without `args` runs in shell form: `sh -c` on macOS and Linux, Git Bash on Windows.
  Windows falls back to PowerShell when Git Bash is not installed.
  With `args`, it runs in exec form, without a shell.

### Catalogue and manifests

- The catalogue is `.claude-plugin/marketplace.json`.
  It requires `name`, `owner` and `plugins`, and each entry requires `name` and `source`.
  A relative `source` must start with `./`.
- An entry accepts `description`, `category` and `homepage`.
  When an entry and `plugin.json` both set `version`, `plugin.json` wins, and `claude plugin validate` warns if they differ.
- The Fields table of the manifest reference lists `name`, `version`, `description`, `author`, `homepage`, `repository`, `license` and `keywords`, and no `category`.
- With `--strict`, a manifest that carries `category` fails with `Field 'category' belongs in the marketplace entry (marketplace.json), not plugin.json`.
  A catalogue entry that carries Codex's `policy` or `interface` warns as an unknown field.
- `.codex-plugin/` and `.cursor-plugin/` folders beside `.claude-plugin/` raised no warning.
- `icon` is the path to an image file inside the plugin, such as `./logo.png`: "Icon for the plugin's listing in Anthropic's directory. Claude Code doesn't read it".
  In a catalogue entry `claude plugin validate` reports it as an unknown field.
- The default hooks file is `hooks/hooks.json` at the plugin root.
  A `hooks` manifest field names further files, and Claude Code merges them with the default.

### Validator

- `claude plugin validate` documents `--strict` and `--json`.
  The CLI reference does not document `--profile`.
- `--profile directory` exits 1 when the plugin directory would refuse a submission on a check the command runs.
  Older releases of Claude Code lack it.
- The directory profile reports findings with `code`, `severity`, `blocking` and `hold`.

### Windows and PowerShell

- A hook's `shell` field accepts `"bash"` or `"powershell"`.
  It defaults to `"bash"`, or to `"powershell"` on Windows when Git Bash is not installed.
- Without Git Bash, a shell-form hook with no `shell` set runs in PowerShell, where it can fail.
- `prose-discipline`'s `SubagentStart` command runs `printf`.
  No source read here says whether PowerShell has a `printf`, and no check runs the command in PowerShell.
  So the command may print nothing there, and the hook then gives a subagent no rules.
  Hosted Windows runners install Git for Windows, which brings Git Bash, so CI cannot show the gap.
  The `SessionStart` command runs `echo`, and its behaviour in PowerShell is untested too.

### Cowork

- The platform-support page lists hooks as `hooks/hooks.json`, ignored in Chat and loaded in Cowork and Claude Code.
  It names no other hooks path.
- A marketplace sync in Cowork rejected a plugin whose `hooks/hooks.json` held `commandWindows`: `Unknown hook field(s) ['commandWindows']`, because hooks "must only use fields the approval UI can display".
- The documentation does not say whether Cowork loads a hooks file that a manifest declares, or reads a file such as `hooks/codex.json` that nothing declares.

### Measured on hosted runners

- Claude Code adds this marketplace and installs every package on Ubuntu, macOS and Windows.
- `claude plugin details <name>@<marketplace>` prints a `Skills (N)` line with the bare skill names.

## Codex

### Manifest and fetch

- A portable package puts `plugin.json` at the plugin root and declares the Agent Plugins schema.
  `.codex-plugin/plugin.json` remains a compatibility fallback.
- The loader checks the root `plugin.json` first.
  A symlink there, or anything but a regular file, rejects the plugin.
- A root manifest with an `https://agent-plugins.org/schemas/` `$schema` wins.
  The vendor paths `.codex-plugin/`, `.claude-plugin/` and `.cursor-plugin/` are then never read.
- Such a package takes skills from `./skills` and MCP servers from `./mcp.json`, with no override.
- The loader drops an unknown top-level manifest field with a warning.
- The listing shows the category `Other` unless the marketplace entry supplies one.
- Adding a marketplace runs `git clone`.
- `codex plugin marketplace add` takes no name argument.
- Codex reads the marketplace name from the catalogue.
- Codex identifies the marketplace by the catalogue's top-level `name`, `pegboard` here.
- The ChatGPT desktop app can read `.claude-plugin/marketplace.json` as a legacy-compatible marketplace.

### Skills

- Codex starts with each skill's name and description, and loads the full `SKILL.md` when it uses the skill.
  Users run `/skills` or type `$` to mention one.
- Start a new session after you install a plugin, before you use its skills.
- The listing tells the model it "must use that skill" when a task clearly matches the description.
- Codex exposes a plugin skill as `<plugin>:<skill>`, with the prefix taken from the manifest `name`.

### Always-on instructions

- Hook settings go under `extensions.com.openai` in the root `plugin.json`.
  An explicit `hooks` value replaces default discovery of `hooks/hooks.json`.
- The documentation says Codex can load an enabled plugin's hooks alongside user, project and managed hooks.
- Codex skips plugin hooks until the user reviews and trusts the current hook definition.
- Codex sets `CLAUDE_PLUGIN_ROOT` for compatibility with existing plugin hooks.
- The documented command-handler fields are `timeout`, `statusMessage`, `additionalContextLimit`, `commandWindows` and `async`.
- By default, Codex saves `additionalContext` over 2,500 tokens to disk and gives the model a preview.
- Plain `SessionStart` stdout becomes model context, recorded as a developer-role message.
- An unknown top-level key in `hooks.json` fails the parse.
  The parser ignores an unknown key inside a handler.
- The loader returns no hooks for a package in Agent Plugins format, against the documentation above.
- `plugin_hooks` is a removed compatibility flag for plugin-bundled hooks.
  The config parser skips a `plugin_hooks` toggle.

### Catalogue and bundle manifest

- Codex looks for a catalogue at `.agents/plugins/marketplace.json`, then `.agents/plugins/api_marketplace.json`, `.claude-plugin/marketplace.json` and `.cursor-plugin/marketplace.json`.
  The first file found wins.
  This repository ships the first, so nothing rests on the fallbacks.
- Codex documents that each entry carries `policy.installation`, `policy.authentication` and `category`.
  The loader defaults them to `AVAILABLE` and `ON_INSTALL`, and accepts `NOT_AVAILABLE`, `INSTALLED_BY_DEFAULT` and `ON_USE`.
- An entry's `source` is a string path or an object tagged by `source`, such as `{"source": "local", "path": "./..."}`.
- An unknown key in a catalogue or an entry is not rejected.
  The top level reads `name`, `plugins` and `interface.displayName`, so `owner` and `description` are ignored.
- Codex tries `.codex-plugin/plugin.json`, then `.claude-plugin/plugin.json`, then `.cursor-plugin/plugin.json`.
  The first that exists decides, and a root Agent Plugins `plugin.json` outranks all three.
- Codex reads `.codex-plugin/plugin.json`.
- The manifest parser reads `name`, `version`, `description`, `keywords`, `skills`, `mcpServers`, `apps`, `hooks`, `interface` and `extensions`.
  It drops every other key without a message, `author`, `homepage`, `repository`, `license` and `category` among them.
- The submission documentation says to omit `$schema` from a standalone Codex compatibility manifest.
- `interface.composerIcon` and `interface.logo` take `./`-prefixed paths to square images of at least 48 by 48 px, PNG among the accepted formats.
  The same page lists `displayName`, `shortDescription`, `longDescription`, `developerName`, `category` and `capabilities` as required for the Codex format, with limits it calls the limits for public submission.
- The loader reads every `interface` field as optional or defaulted, so an `interface` with only the two icon paths loads.
  The bundles carry only the two paths, because this repository submits nothing to the Codex directory.

### Hook files, Windows and trust

- A manifest that is not in Agent Plugins format loads hooks from its declared `hooks` entries, and otherwise from the default `hooks/hooks.json`.
  A declared entry replaces the default.
  A package in Agent Plugins format loads none.
- The documentation says legacy packages can declare `hooks` directly in `.codex-plugin/plugin.json`, and that existing `.codex-plugin/plugin.json` files remain supported as a compatibility fallback.
- On Windows, Codex runs the program in `COMSPEC`, or `cmd.exe`, with `/C`.
- `commandWindows` is the optional Windows-only override of `command`.
- For `SubagentStart`, plain text on stdout is added as extra developer context for the subagent.
- Before a non-managed hook runs, Codex requires the user to review and trust its exact definition.
  Codex records trust against the hook's current hash, so changed hooks are skipped until trusted.
- For a plugin, Codex also compares a SHA-256 of every file under the installed plugin root with the one recorded at approval.
  A difference fails with `plugin contents changed; hook approval required`.
  The hash skips `__pycache__`, `.venv`, `*.pyc` and `*.egg-info`, and fails on an entry that is neither a regular file nor a directory.
- The documentation says that when a plugin update changes a bundled script, Codex requires a new review even if the hook definition stays the same.
- A release changes `version` in the manifests of the installed plugin, so its hash changes, and the user approves the hook again.

### Measured on hosted runners

- Codex adds this marketplace and every package on Ubuntu, macOS and Windows.
- `codex debug prompt-input` lists each skill as `- <plugin>:<skill>: ` followed by its description.
- CI runs the installed hook commands outside Codex, so it shows what they print and not that Codex delivers it.

## Oh-My-Pi

### Manifest and fetch

- The `agent-plugins` provider loads skills and MCP servers from packages that declare the standard.
- Skill front matter is closed to the six Agent Skills fields.
  Any other key skips the skill.
- For such a package, the `claude-plugins` provider stands down from skills and MCP.
  It still loads the other surfaces, rules included.
- The `claude-plugins` provider reads `.claude-plugin/plugin.json`, and treats a file that fails `JSON.parse` as absent.
- The marketplace fetcher clones git sources with `git`.

### Skills

- A skill keeps its bare name, with no plugin prefix.
- Providers are sorted by priority, higher first: `agent-plugins` has 75, and `claude-plugins` and `codex` have 70.
- The dedup key is the skill name, and the first item with that name wins.
- The dropped duplicate gets a `name collision` warning.
- Users invoke a skill with `/skill:<name>`.

### Always-on instructions

- The `claude-plugins` provider contributes rules from marketplace plugins.
- It reads `rules/*.md` and `rules/*.mdc` directly under the plugin root.
- A rule with `alwaysApply: true` has its full content injected into the system prompt.
- A rule with `condition`, `astCondition` or `question` is a TTSR rule, and leaves the always-apply bucket.
- A TTSR match aborts the response and retries it with the rule injected.
- Rules deduplicate by name, and the first wins.
- A rule without `agents:` applies to every agent, subagents included.
- Plugin hooks are files under `hooks/pre/` and `hooks/post/`.
  A Claude-style `hooks/hooks.json` has no reader.

### Catalogue

- Oh-My-Pi looks for `.omp-plugin/marketplace.json` first, then `.claude-plugin/marketplace.json`.
- A catalogue requires `name`, `owner.name` and `plugins`.
  An invalid entry is logged and skipped.
- An entry requires `name` and `source`, and a string `source` must start with `./`.
  `description`, `version`, `author`, `homepage`, `repository`, `license`, `keywords`, `category` and `tags` are optional.
  Extra fields are preserved, and nothing warns on an unknown entry key.
- `--plugin-dir <dir>` adds a local plugin directory to discovery.
- A plugin identifier is `name@marketplace-name`, and the marketplace half is the catalogue's `name` field.

### Measured on hosted runners

- Oh-My-Pi adds this marketplace and installs every package on Ubuntu, macOS and Windows.
- `omp read skill://<skill>:raw` resolves each skill by its bare name and prints `name: <skill>`.

## Hermes

### Manifest and fetch

- Hermes loads a supported subset of an Agent Plugins package: root `plugin.json`, `skills/*/SKILL.md` and root `mcp.json`.
- `plugin.json` must be a regular file inside the plugin root, with the exact 1.0.0 `$schema`.
- The loader reads skills and MCP servers, and nothing else: no `hooks/`, no `rules/`.
- Discovery skips `.claude-plugin` and other vendor manifest directories.
- `hermes plugins install` resolves the identifier to a git URL and clones that repository with depth one.
- An identifier of the form `owner/repo/subdir` resolves to that GitHub repository and a subdirectory.
- The desktop app turns a `hermes://plugin/install?repo=owner/repo` link into a `plugins.manage` install request with that identifier.
- The server hands that request to `dashboard_install_plugin`.
  It and `hermes plugins install` both call `_install_plugin_core`, so the link takes the same identifiers.
- The desktop's own repository probe also reads `owner/repo` with an optional subdirectory.
- On Windows, `install.ps1` clones a branch and then checks out the pinned commit.
- Hermes reads no per-repository catalogue.
  It installs a package by identifier, and its community index is `NousResearch/hermes-plugin-index`.
- Installed with `--no-enable`, a package stays disabled until `hermes plugins enable <name>` runs.
- In the desktop app, a `hermes://plugin/install?repo=owner/repo` link installs a plugin after a confirmation dialog.
  An agent-plugin install from that link goes through the same install-time security scanning as `hermes plugins install`.
- Hermes scans a package when it installs it.
  A `caution` verdict shows the findings and asks `Install anyway? [y/N]`.
  A `dangerous` verdict blocks the install, and `--force` does not override it.

### Skills

- A package skill has the qualified name `agent-plugin-<slug>-<hash>:<skill>`.
- The hash is the first eight hex digits of the SHA-256 of the key.
  For a package directly under a plugins root, the key is `plugin.json`'s `name`.
- Hermes leaves plugin skills out of the system prompt's `<available_skills>` index.
- The agent's `skills_list` tool shows the qualified name.
- A package skill gets no slash command, because Hermes builds slash commands from skill directories only.
  The agent loads a package skill with the `skill_view` tool and its qualified name.
- Neither `hermes plugins show`, `hermes plugins list --json` nor `hermes skills list` prints a portable package's skill names.
  `hermes plugins show` prints name, version, description, `Status`, `Source`, `Key`, `Emits` and `Listens`.
- `hermes plugins list --json` carries `name`, `status`, `version`, `description`, `source` and `removed`.
  `hermes skills list` reads skill directories only.
  The `skills_list` tool adds plugin skills after that scan.

### Always-on instructions

- `skills.auto_load` in `config.yaml` loads the listed skills in full at the start of every new session.
  `--ignore-rules` skips it.
- The documentation calls each entry a skill name.
  A qualified plugin name resolves too: the lookup sends any name containing `:` to the plugin registry.
- An auto-loaded skill sits in the stable part of the system prompt.
- Hermes wraps it with a note to "Treat its instructions as active guidance for the duration of this session".
- A native plugin can add a system-prompt section.
  A native plugin needs `plugin.yaml` and an `__init__.py` with a `register(ctx)` function.

### Measured on hosted runners

- Hermes installs on Ubuntu and macOS, and every package installs and is enabled.
  `hermes plugins show <name>` prints `Key: <name>` and `Status: enabled` for each package.
- `hermes plugins validate` prints `✓ security scan — safe` for every package.
- On Windows, the installer clones a branch before it checks out the pinned commit, and the checkout can fail with `Your local changes to the following files would be overwritten by checkout`.
- The integration matrix excludes Hermes on the windows-latest runner.

## Cursor

CI installs nothing into Cursor, so these facts rest on its documentation alone.

### Manifest and catalogue

- Every Cursor plugin requires `.cursor-plugin/plugin.json`.
  `name` is required, in lowercase kebab-case.
  Optional fields include `description`, `version`, `author` with `name` and `email`, `homepage`, `repository`, `license`, `keywords`, `logo`, `rules`, `skills`, `hooks` and `mcpServers`.
- `logo` is a relative path to a logo file in the repository, shown as `assets/logo.svg`, or an absolute URL.
- The reference documents no `category` and no `$schema` for this manifest, and no `url` in `author`.
  It does not say what Cursor does with an unknown manifest key.
- Cursor's template validator checks the manifest `name`, that an entry name equals its manifest `name`, and that path fields are safe relative paths that exist.
  It has no check for unknown fields.
- A repository with several plugins places `.cursor-plugin/marketplace.json` at its root.
  It requires `name`, `owner` and `plugins`, and an entry requires `name` and `source`.
- Cursor merges the plugin folder's `.cursor-plugin/plugin.json` into the entry, and the manifest's values take precedence.
- The documentation shows `source` as a bare folder name.
  Cursor's template repository writes `./plugins/<name>`, and its guide calls `source` the path from the repository root to the plugin folder.
  The documentation does not say whether the parser accepts the `./` prefix.

### Components

- Default discovery reads `skills/`, `rules/` (`.md`, `.mdc` and `.markdown` files), `agents/`, `commands/`, `hooks/hooks.json` and `mcp.json`.
  A manifest field for a component replaces discovery of that component.
- A rule with `alwaysApply: true` applies to all files, and `false` makes it available on request.
  That is how `prose-discipline` reaches Cursor.
- Discovery parses `hooks/hooks.json` for hook event names.
  Claude Code's file sits at that path in the bundle.
  The documentation does not say whether Cursor accepts that file, and nothing here ran it.
- Cursor loads a root Agent Plugins `plugin.json` for skills and MCP servers only.
  Rules and hooks need `.cursor-plugin/plugin.json`.

### Install routes

- Public marketplace: open **Customize**, find the plugin, and select **Install** with a project or user scope.
  A plugin appears there after submission and review by the Cursor team.
- Team marketplace, on Teams and Enterprise plans: **Dashboard**, **Plugins & MCPs**, **Team Marketplaces**, **Add Marketplace**, **Import from Repo**, then the repository URL.
  Import accepts GitHub, GitLab, Bitbucket and Azure DevOps URLs.
  Developers install from **Customize**.
- Cursor's Plugins page does not say which catalogue file **Import from Repo** reads.
  The reference names `.cursor-plugin/marketplace.json` for a multi-plugin repository, and no page mentions `.claude-plugin/marketplace.json`.
- Local: put either plugin format in `~/.cursor/plugins/local`, then restart Cursor or run **Developer: Reload Window**.
  On Enterprise, **Allow Local Plugin Imports** is off by default.
- The pages document no `cursor` command that installs a plugin.
  The CLI's API-key route for automation reads `CURSOR_API_KEY`.

## OpenClaw

CI installs nothing into OpenClaw, so these facts rest on its documentation and source alone.

- OpenClaw reads `.claude-plugin/marketplace.json`, then `marketplace.json` at the marketplace root.
- For a marketplace on GitHub or git, a plugin entry must stay inside the cloned repository, and OpenClaw accepts relative path sources.
- The documented install command from a GitHub repository is `openclaw plugins install <plugin-name> --marketplace <owner/repo>`.
  `openclaw plugins marketplace list <source>` lists the entries.
- Of `.codex-plugin/plugin.json`, `.cursor-plugin/plugin.json` and `.claude-plugin/plugin.json`, the first that exists sets the bundle format.
  A root `plugin.json` counts only when none of them exists.
  The documentation lists the markers in that order and says a client marker beats a root `plugin.json`, and the source fixes the order among the three.
- `hooks/hooks.json` of a Claude bundle is "detected but not executed".
- A Codex manifest's `hooks` value is read as a list of hook-root directories, each holding child directories with `HOOK.md` and a handler.
  A path that is a file, such as `./hooks/codex.json`, loads no entries, and the hooks capability is reported unavailable.
- No bundle format reads a plugin-root `rules/` directory.
  A Cursor bundle's `.cursor/rules/` is detect-only.
  The documentation never mentions a root `rules/`, and the only `rules` lookup in the manifest reader is for `.cursor/rules`.
- A bundle's skill roots load as normal OpenClaw skills, in every bundle format.
  A Codex bundle lists `skills/` as content.
- So `prose-discipline` gets its skills from OpenClaw, and no hook or rule.

## Kiro

Kiro is closed source, and CI installs nothing into Kiro, so these facts rest on its documentation alone.

- Powers follow the Agent Plugins specification.
  Kiro supports the Agent Plugins format (`plugin.json`) and the legacy `POWER.md` format.
- A power requires `$schema`, `name`, `version`, `description`, `author` with at least `name`, and `keywords`.
  `plugins/<name>/plugin.json` carries all six.
- Kiro documents the components `skills/` and `mcp.json`, and mentions no hooks and no rules.
- A power can live at the root of a repository or in a folder, and one repository can hold several powers, each in its own folder.
  The pages do not say how Kiro finds the folders, how deep it looks, or whether it reads a catalogue file.
- GitHub import is a flow in the Powers panel: **Add Custom Power**, **Import power from GitHub**, a repository URL, **Install**.
  The pages document no command for it.
- `/powers install <name|path>` and `kiro-cli powers install <name|path>` install a power from an existing directory, or else by an exact name in the powers catalog.
- This repository states no Kiro import command, because the pages leave the several-packages case open.

## Anthropic plugin directory

- The portal's Validate runs every directory check.
  A finding labelled "Blocks" stops a submission until it is fixed, and one "Held for a reviewer" still lets the plugin be submitted.
- The portal's Validate wants a square PNG or JPEG, 512 to 2048 px a side and under 2 MB, at `.claude-plugin/icon.png` or named by `icon`, and accepts no SVG or WebP.
  The file "may become the listing icon only once: the first time the plugin is saved or submitted in the developer portal".
- With `icon` set in `.claude-plugin/plugin.json`, Validate warns "Field from another tool's manifest": "The plugin directory reads 'icon' for the listing; Claude Code itself ignores it at load time."
  So the bundles keep the file at `.claude-plugin/icon.png` and set no `icon`.
- The plugin folder "can be the repository root or a subfolder".
- A repository with several plugins is submitted one plugin folder at a time.
  With a plugin path set, "the directory reads and scans only that folder".
- The rule for hook commands: "In the command of a hook or an MCP server, write each path in full from `${CLAUDE_PLUGIN_ROOT}`, with no other variable, command substitution, wildcard, or inline program such as `python3 -c`". The result if you do not: "Blocks for another variable, a command substitution, a wildcard, or an inline program".
- A companion row asks to keep launchers and package installs out of each script that a hook runs, and a hook that runs a non-shell file from the plugin is held for a reviewer.
- Validate blocks a command hook from an organization that is not Verified.
  The finding is "Hooks of type `command` accepted only from Verified organizations", and its text says the rule covers hooks of every type.
  It names `bundles/prose-discipline/hooks/hooks.json`, whose two commands are a literal `echo` and a literal `printf`.
- Validate also blocks `bundles/prose-discipline/rules/prose-discipline.mdc`, under "Files outside the allowed list accepted only from Verified organizations".
  The list it gives is Markdown, text, JSON, YAML, and PNG, JPEG, GIF, WebP and ICO images.
- `claude plugin validate --profile directory` reports no finding for the same two files.
- The checklist states neither Verified-only rule, and no page read says how an organization becomes Verified.
  The pages read were the checklist, Submit your plugin, Publish to the directory, Plugin structure and testing, Plugin feature support across platforms and Connector verification.
- The validator is not published.
