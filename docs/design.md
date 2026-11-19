# About this repository's design

This page explains why the repository and its packages are built the way they are.
The client facts behind each reason are in [How each client loads a package](clients.md).

## One source for every copy

Clients read the same facts from different files.
Claude Code documents one manifest path, `.claude-plugin/plugin.json` ([Claude Code](clients.md#claude-code)).
Codex reads `.codex-plugin/plugin.json` and a catalogue at `.agents/plugins/marketplace.json` ([Codex](clients.md#codex)).
Cursor loads rules and hooks from a plugin that has `.cursor-plugin/plugin.json` ([Cursor](clients.md#cursor)).
Codex shows the category `Other` unless the catalogue entry supplies one ([Codex](clients.md#codex)).
Claude Code documents `category` on a catalogue entry and not in the manifest ([Claude Code](clients.md#claude-code)).
So one package has three client manifests and four catalogues, and each repeats a description.
Every package README repeats the install commands, and every build carries its own `LICENSE`.
A package installs alone, and Agent Plugins 1.0.0 §4.1 keeps every path it supplies inside its root.
So each build carries its own copy, not a path to a root file.

A copy kept by hand drifts from its source, and nothing notices until a reader does.
So each package has one hand-written source, `src/<name>/`, and its `source.json` is the only source of the package's metadata.
No client reads `src/`, and no catalogue points into it.
A client manifest could not hold the metadata, because that client would load the source.
`tools/build.sh` writes `bundles/<name>/`, `plugins/<name>/` and the four catalogues from `src/`.
`tools/regenerate.sh` fills the README regions and tables of contents first, with ready-made tools such as `jq` and `doctoc`, and then runs the builder.
The builder is a separate script because the release job runs it alone, and that job has `jq` and no Node.js, which `doctoc` needs.
CI runs `tools/regenerate.sh` and fails when the tree then differs from the commit.
The failure message names the command that repairs it.
For each pull request commit that changes `src/` or a file the builder shares, CI also runs the builder on that commit alone.
cocogitto counts a package's builds toward its release, so builds that land in a later commit would leave the earlier commit with nothing to release.

Three alternatives lost.
One command per kind of copy leaves a contributor to remember which command follows which edit.
A CI job that commits the copies back would put changes on `main` that no pull request showed.
Keeping the source in `plugins/<name>/` would let a client read hand-written files, and the Hermes install command reads that path.

## Two builds from one source

`bundles/<name>/` holds a manifest folder per client and no root `plugin.json`.
`plugins/<name>/` holds a root `plugin.json` in Agent Plugins 1.0.0 format and nothing vendor-specific.
Every package gets both, including those without hooks, so the catalogues and the documentation carry no per-package case.
The builder branches on one package only: it writes the hooks and the rule of `prose-discipline`.

Codex is the reason for two.
It looks for a root `plugin.json` in Agent Plugins format before any manifest folder, and a package in that format loads no hooks ([Codex](clients.md#codex)).
`prose-discipline` needs Codex hooks, so its bundle has no such manifest.
Hermes needs the opposite: it loads a package only from a root `plugin.json` with the exact 1.0.0 `$schema`, and it skips `.claude-plugin` and other vendor folders ([Hermes](clients.md#hermes)).
A bundle therefore cannot serve Hermes, and the Agent Plugins build cannot serve Codex's hooks.
Kiro's documentation says Powers follow the Agent Plugins specification, and `plugins/<name>/plugin.json` carries the fields it requires ([Kiro](clients.md#kiro)).

Each client picks one manifest folder and ignores the rest.
Claude Code and Oh-My-Pi read `.claude-plugin/plugin.json`, Cursor reads `.cursor-plugin/plugin.json`, and Codex and OpenClaw prefer `.codex-plugin/plugin.json` ([Claude Code](clients.md#claude-code), [Oh-My-Pi](clients.md#oh-my-pi), [Cursor](clients.md#cursor), [Codex](clients.md#codex), [OpenClaw](clients.md#openclaw)).
So one tree with three manifest folders serves five clients.
Claude Code's validator raises no warning for the other clients' folders ([Claude Code](clients.md#claude-code)).
No other source read here says a client rejects a package for them.
Separate trees per client would add copies for no gain that these sources show.

The Agent Plugins build keeps the path `plugins/<name>/`.
The Hermes install commands, the `homepage` URLs and the README links stay valid.

Both builds hold regular files only, and the conformance check fails on a symlink under either.
Claude Code reads only `.claude-plugin/plugin.json`, and fails on a manifest that is not JSON ([Claude Code](clients.md#claude-code)).
Claude Code, Codex and Oh-My-Pi fetch a marketplace with git on the user's machine ([Claude Code](clients.md#claude-code), [Codex](clients.md#codex), [Oh-My-Pi](clients.md#oh-my-pi)).
With `core.symlinks` false, git checks a symlink out as a plain file holding the link text.
Git for Windows disables symlink support by default.
Its installer enables symlinks only under Developer Mode, or when a test link succeeds for the installing user.
So a default Windows checkout turns a symlinked manifest into text, and Claude Code fails to load it.
Codex also fails its hook-trust hash on any entry that is neither a regular file nor a directory ([Codex](clients.md#codex)).
A CI job cannot settle the question.
GitHub's Windows runner image installs Git with symlinks enabled.
A job there loads a symlink that a default user checkout breaks.

The Agent Plugins build holds the only root manifest, and it holds no other manifest.
Agent Plugins 1.0.0 §5.1 says no other file can "replace, supplement, or override the core fields in root `plugin.json`".
The cost of two builds is the same skills twice, which the builder and CI keep equal.

## What conformance buys

Agent Plugins 1.0.0 describes a plugin as a directory with a single root (§4.1).
A conforming client can at least load a plugin from a directory path (§11.1).
Every `plugins/<name>/` keeps its manifest at the root with the canonical `$schema` (§5.1, §5.2).
Its skills sit in the fixed `skills/` location (§6.1).

A client that implements Agent Plugins 1.0.0 can load `plugins/<name>` directly.
`bundles/<name>/` is not an Agent Plugins package, and [Two builds from one source](#two-builds-from-one-source) says why it has no root `plugin.json`.

The specification defines no repository-level catalogue.
How a client gets from this repository to a plugin root is specific to that client.
So each install command in the [README](../README.md#install) cites that client's own source.

## Icons are rendered from SVG

Each bundle ships one listing icon, `.claude-plugin/icon.png`.
The Anthropic directory finds it there without a manifest field, and it reports the `icon` field as a field from another tool's manifest ([Anthropic plugin directory](clients.md#anthropic-plugin-directory)).
Codex reads it through `interface.composerIcon` and `interface.logo`, and Cursor through `logo` ([Codex](clients.md#codex), [Cursor](clients.md#cursor)).
The directory accepts a PNG or a JPEG and no SVG ([Anthropic plugin directory](clients.md#anthropic-plugin-directory)), so the shipped file is the one binary in the tree.
Its source is `src/<name>/icon.svg`, which a diff can show, and the builder renders it on every run like every other build file.
The Agent Plugins build carries no icon, because the 1.0.0 manifest has no field for one.

The builder accepts one resvg version, 0.48.1, and refuses any other.
Another version renders other PNG bytes, and a commit that carries them releases every package, because cocogitto counts a package's builds.
CI installs that version from its release archive, checked by a SHA-256 digest committed in the workflow.
CI still leaves `bundles/*/.claude-plugin/icon.png` out of both tree comparisons.
Whether one resvg version writes the same bytes on every system was not measured, and a comparison would fail on a difference nobody made.
The directory profile in CI fails a bundle whose icon is missing.

The icons follow the plugin list of claude.ai, where every plugin is drawn as one glyph of the app's own icon font in a dark tile.
The tile colour, the line colour and the stroke width were measured on that page, and each icon draws its own object in that frame.
Two alternatives lost.
A hand-drawn PNG as the source makes every change invisible in a diff and needs an image editor.
A renderer that runs only by hand leaves the builder unable to write the whole bundle.

## Skill names carry no plugin prefix

Claude Code, Codex and Hermes prefix a plugin skill with a namespace ([Claude Code](clients.md#claude-code), [Codex](clients.md#codex), [Hermes](clients.md#hermes)).
So a skill named after its plugin reads `/triz-thinking:triz-thinking` in Claude Code.
Claude Code also answers a bare `/<skill>` while no other command uses that name ([Claude Code](clients.md#claude-code)).
Oh-My-Pi shows the bare name, keeps the first skill of each name, and drops the rest ([Oh-My-Pi](clients.md#oh-my-pi)).
A generic name such as `review` collides in Oh-My-Pi with any other source that ships one.

A skill name is therefore distinctive without the plugin prefix, and never repeats the plugin name.
It is one word, or one compound such as `root-cause`, so it stays short in Oh-My-Pi's bare list and still names its method.
The directories under `src/*/skills/` hold the names in use:

| Package | Skills |
| :-- | :-- |
| cognitive-load | `extraneous` |
| design-review | `red-flags` |
| distilled-research | `triangulate`, `vet-sources` |
| prose-discipline | `house-style` |
| toc-thinking | `root-cause` |
| triz-thinking | `contradiction`, `ariz` |

A package holds a second skill when one skill carried two jobs with different triggers.
In `triz-thinking`, `ariz` walks ARIZ-85C, a nine-part algorithm that the matrix route never opens.
`contradiction` keeps the matrix route, and hands a problem it did not crack to `ariz`.
In `distilled-research`, `vet-sources` rates a list of sources on its own, in the main thread.
`triangulate` runs the full research and reads the files `vet-sources` owns, so the two install together.
`vet-sources` reads nothing from `triangulate`: the dependency runs one way.
Its vetter brief defines the plan fields it reads, so the skill stands alone.
`toc-thinking` stays one skill.
Its five trees form one sequence, and each tree's output is the next one's input.

A rename changes every invocation, so it ships as a breaking release.
A Hermes `skills.auto_load` entry names the skill, so a rename breaks that entry too.

## One rules file, one documented route per client

`prose-discipline` ships a writing standard that should be active in every session, without the user invoking it.
Each client documents a different route for standing instructions:

- Claude Code: a `SessionStart` hook's plain stdout, and `SubagentStart`'s `additionalContext` for subagents ([Claude Code](clients.md#claude-code)).
- Codex: hooks declared in `.codex-plugin/plugin.json`, run after the user trusts them ([Codex](clients.md#codex)).
- Cursor and Oh-My-Pi: a plugin `rules/` file with `alwaysApply: true` ([Cursor](clients.md#cursor), [Oh-My-Pi](clients.md#oh-my-pi)).
- Hermes: the user's `skills.auto_load` list, which loads a named skill in full ([Hermes](clients.md#hermes)).

OpenClaw and Kiro document no route.
OpenClaw detects `hooks/hooks.json` and runs nothing from it, runs no hooks file that a Codex manifest declares, and reads no plugin-root `rules/` ([OpenClaw](clients.md#openclaw)).
Kiro documents `skills/` and `mcp.json` as its components ([Kiro](clients.md#kiro)).
In both, `prose-discipline` loads its skill and nothing else.

`src/prose-discipline/rules/prose-discipline.md` is the one source of the rules.
Between `<!-- hook-text:start -->` and `<!-- hook-text:end -->` it holds the short form, which the hooks print.
The `.mdc` rule and the `rules` region of the `house-style` skill carry the full text, written without that region and its markers.
`tools/regions.sh` extracts both and stops on a lone, duplicate or reversed marker, so no copy of the full text can still hold the short form.
The short form is a subset of the rules, and its last line points to the skill for the reasons.
It states facts, as Claude Code advises for hook text ([Claude Code](clients.md#claude-code)).

Hermes loads no hooks and no `rules/` from a package ([Hermes](clients.md#hermes)).
So `skills/house-style/SKILL.md` carries the full rules in a generated region.
The package README shows the `skills.auto_load` entry, with the qualified name `tools/regenerate.sh` computes from the manifest `name`.

Python lost.
A Hermes native plugin can add a system-prompt section, but it needs `plugin.yaml` and an `__init__.py` ([Hermes](clients.md#hermes)).
When a directory holds both manifests, Hermes loads the native one and skips the portable `plugin.json`.
A native half would stop Hermes from loading the package as Agent Plugins.

In Claude Code, Cursor and Oh-My-Pi, invoking `house-style` puts the rules in context a second time.
The skill body stays anyway, because it is the only carrier Hermes loads.
In Hermes, the user adds one config entry, and nothing else loads the rules.
In Codex, the user trusts the hook once, and again after each release ([Codex](clients.md#codex)).

## No hook blocks the agent

Clients offer ways to force a standard, not only to state it.
A Claude Code `Stop` hook can return `"decision": "block"` and keep Claude working.
A `PreToolUse` hook can deny a tool call.
A `UserPromptSubmit` hook can add context to every prompt.
In Oh-My-Pi, a TTSR rule aborts a response on a match and retries it ([Oh-My-Pi](clients.md#oh-my-pi)).

`prose-discipline` states the standard and enforces nothing.
It ships no blocking hook, no per-prompt reminder and no TTSR rule file.
A gate on prose halts real work over a style match.
Repeating text already in context adds tokens and no fact.
The rules enter each context once, and again where the client dropped them, as after compaction ([Claude Code](clients.md#claude-code)).

Compliance therefore rests with the model, and nothing in the package checks the output.

### Literal hooks

The two hooks files hold literal output commands.
No script runs and no file is read, so no command can fail on a missing file or a script that did not start.
`SessionStart` runs `echo` with the short form in single quotes, and Claude Code adds plain stdout to the context ([Claude Code](clients.md#claude-code)).
`SubagentStart` runs `printf '%s'` with one JSON object in single quotes.
The object is `hookSpecificOutput`, with the event name and an `additionalContext` that holds the short form.
Claude Code documents no plain-stdout route for `SubagentStart` ([Claude Code](clients.md#claude-code)).
`printf` carries the JSON because the result of `echo` is implementation-defined when an operand holds a backslash, and the JSON escapes line feeds as `\n`.
The commands name no variable, no command substitution and no wildcard.
The plugin directory's checklist restricts all three in a hook command ([Anthropic plugin directory](clients.md#anthropic-plugin-directory)).

Codex's file adds a `commandWindows` to each hook.
Codex runs `COMSPEC` or `cmd.exe /C` on Windows and documents `commandWindows` as the Windows-only override ([Codex](clients.md#codex)).
The override holds one `echo` per line, joined by `&`, with `echo:` for a blank line.
The integration job runs it under `cmd /C` on a Windows runner and compares what it prints with the short form.

### What the builder refuses

`tools/build.sh` stops on a short form that breaks a limit, before it deletes anything.
Each limit prevents one failure:

- **Characters.** Only ASCII letters, digits, space, line feed and `. , : - _ / #` pass.
  Single quotes delimit the text in `sh` and PowerShell, and a backslash changes what `echo` prints.
  cmd.exe runs `& | < > ^ %` as operators.
  The directory restricts variables, command substitution and wildcards.
- **Line starts.** Every line starts with a letter, a digit, `#` or `- `.
  cmd.exe prints help for `echo /?` instead of the line.
- **Size.** The short form stays under 8000 bytes.
  Codex moves hook context over 2,500 tokens to a file, and Claude Code caps hook output at 10,000 characters ([Codex](clients.md#codex), [Claude Code](clients.md#claude-code)).
- **Windows command.** The `commandWindows` string stays under 8191 characters, the command-line limit of cmd.exe.
  Each line adds `echo` and `&`, so a text under 8000 bytes can still exceed it.

`conformance.yml` feeds the builder one bad input per limit and fails when it accepts one.
The `hooks.json` and `codex.json` files carry no `additionalContextLimit`, the Codex key that moves the spill threshold ([Codex](clients.md#codex)).

### Where each client's hooks sit

Claude Code's file is `hooks/hooks.json`, the path Claude Code loads by default.
The Claude manifest declares no `hooks` field.
It is also the only hooks path that the platform-support page names for Cowork ([Claude Code](clients.md#claude-code)).

Codex's file is `hooks/codex.json`, declared in `.codex-plugin/plugin.json`.
A declared `hooks` entry replaces Codex's default `hooks/hooks.json`, so Codex never runs Claude's file ([Codex](clients.md#codex)).
Only Codex needs a Windows command.
Cowork rejected a plugin over `commandWindows` in a hooks file ([Claude Code](clients.md#claude-code)).
Putting Codex's commands in their own file keeps that field out of the file Claude reads.

Claude Code without Git Bash runs a shell-form hook in PowerShell, and the `SubagentStart` command uses `printf` ([Claude Code](clients.md#claude-code)).
No check here runs that command in PowerShell.
GitHub's Windows runner image installs Git, and Git for Windows brings Git Bash, so CI cannot show the gap.
The risk is that `SubagentStart` prints nothing there.

## Codex declares its hooks in its own manifest

Codex documents plugin hooks under `extensions.com.openai` in a root `plugin.json` ([Codex](clients.md#codex)).
Its loader returns no hooks for a package in Agent Plugins format, and two open issues report it ([Codex](clients.md#codex)).
A root manifest in that format also outranks every manifest folder ([Codex](clients.md#codex)).

Codex documents `.codex-plugin/plugin.json` as a compatibility fallback, and says legacy packages can declare `hooks` there ([Codex](clients.md#codex)).
The loader reads the declared file ([Codex](clients.md#codex)).
So `bundles/prose-discipline/` has no root `plugin.json`, and its Codex manifest declares `./hooks/codex.json`.

A fallback is the route Codex can drop.
The integration job installs Codex 0.155.1, which reads the catalogue, the local entry shape, `.codex-plugin/plugin.json` and a declared hooks file ([Codex](clients.md#codex)).
It runs the installed hook commands and compares their output with the short form.
That proves the commands print the text, and not that Codex delivers it, because no job starts a Codex session.

Codex skips plugin hooks until the user trusts them, and it ties trust to a hash of the whole installed plugin ([Codex](clients.md#codex)).
Every release changes `version` in the manifests, so Codex asks again after each release.
The rules in every Codex session outweigh that prompt.

## `prose-discipline` is not submitted to the Anthropic directory

The directory's Validate blocks a hook and a `.mdc` file from an organization that is not Verified ([Anthropic plugin directory](clients.md#anthropic-plugin-directory)).
`prose-discipline` ships both, and no page read says how an organization becomes Verified (same section).
So the package is not submitted, a decision of 2026-11-18.
Claude Code installs it from this repository's catalogue, where the hooks run.

A build without hooks lost.
The directory and the catalogue would read the same folder, so it needs a third build.
From it, Claude Code would load the rules only when the skill fires.

## Releases come from cocogitto, straight to main

Claude Code keeps users on their cached copy until `version` changes ([Claude Code](clients.md#claude-code)).
It documents release tags of the form `<plugin-name>--v<version>` ([Claude Code](clients.md#claude-code)).
A version moved by hand gets forgotten, and users then keep an old copy.
A release should follow the commit that earned it, with no release pull request to merge.

[cocogitto](https://github.com/cocogitto/cocogitto) releases every package.
`cog bump --auto` derives each package's next version from the conventional commits that touched its paths.
A package's paths are `src/<name>/` and, through `include` in `cog.toml`, `bundles/<name>/**` and `plugins/<name>/**`.
Shared files such as `tools/build.sh` are not paths of any package.
A commit to one therefore releases the packages whose builds it changes, because CI requires it to carry those builds.
The bump runs a hook per package that writes the new version into `src/<name>/source.json` and runs the builder, so every manifest in both builds carries the version in the version commit.
A package whose source did not change gets byte-identical output, so the version commit holds no change for it.
A failing hook fails the release job, and no tag is pushed.
It writes one version commit and one tag per bumped package.
`cog.toml` sets the separator `--` and the prefix `v`, so tags read `<name>--v<version>`.
A workflow on each push to `main` runs the bump and publishes one GitHub release per new tag.
It pushes with `GITHUB_TOKEN`, and a push made with that token starts no workflow run.
So the version commit cannot start the release again.

Three other tools lost.
release-please works through release pull requests.
A pull request opened with `GITHUB_TOKEN` starts its workflow runs in an approval-required state.
So every release would wait for a person to approve its checks and merge a second pull request.
semantic-release does not officially support monorepos.
Its FAQ also advises against committing the release back to the branch.
git-cliff computes the next version and the changelog.
The commit, the tags and the push would then be a shell loop kept here.

### Seed tags

Without a tag, cocogitto reads a package's history from the repository's first commit.
It also starts that package from version 0.0.0.
For `prose-discipline`, at 1.3.0, that would release a lower version than the one users hold.
So each package has one seed tag at `232aaba`, carrying the version its manifest held there:
`cognitive-load--v0.1.0`, `design-review--v0.1.0`, `prose-discipline--v1.3.0`, `toc-thinking--v0.1.0` and `triz--v0.1.0`.
The release workflow refuses to run while any package in `cog.toml` has no reachable tag.

### Breaking changes

[CONTRIBUTING.md](../CONTRIBUTING.md#write-commits) gives the commit types and the versions they release.
`prose-discipline` is past 1.0.0, so its rename to `house-style`, a `feat!` commit, releases it as 2.0.0.

### Changelogs

Each package keeps a `CHANGELOG.md` in `src/<name>/`, written by the bump from `tools/templates/changelog.tera`.
cocogitto's default package template adds an inline-HTML `BREAKING` badge, and credits the author and co-authors on every line.
The template keeps `BREAKING:` as text, and drops the HTML and the author credit, which says who, not what.

### Merges and commit messages

[CONTRIBUTING.md](../CONTRIBUTING.md#write-commits) gives the rules; these are their reasons.
A squash merge folds a branch's commits into one commit, and the bump then loses each commit's type and paths.
So the repository settings allow merge commits only (GitHub API, read 2026-09-25).
The bump drops a commit whose message does not parse, and says nothing.
That is why CI checks the messages of pull request commits that touch `src/`, `bundles/`, `plugins/` or a file the builder shares.

### Trade-offs

The release runs beside the conformance run on the same push, not after it.
The same checks run on a pull request that changes a path they read, before its merge.
A release can still publish a commit whose check on `main` then fails.

## CI checks structure and installation

CI runs these checks without a model:

- the conformance check against the vendored schema, and the regeneration diff, which covers the builds and the catalogues;
- one probe per builder limit and per conformance rule, each feeding a bad input in a scratch copy and failing when it passes;
- the builder on each pull request commit that changes `src/` or a file the builder shares, and the messages of pull request commits that touch a path the release reads;
- the validators that Claude Code, the Agent Skills project and Hermes publish: `claude plugin validate --strict` on every bundle and on the Claude catalogue, the same command with `--profile directory` on every bundle, and `skills-ref` and `hermes plugins validate` on `plugins/<name>`;
- the evals runner's selftest, and `tools/evals.py validate` over every folder under `evals/`;
- an install matrix, where each client installs every package from the checkout.

In the matrix, Claude Code, Codex and Oh-My-Pi install through the catalogues at the root, which point at `bundles/<name>`, and Hermes installs from `plugins/<name>`.
Claude Code, Codex and Oh-My-Pi must list every skill after the install.
Hermes cells check that each package is installed and enabled, and no more.
Hermes 0.21.5 has no model-free command that prints a portable package's skills ([Hermes](clients.md#hermes)).
The matrix leaves out Hermes on Windows.
There the installer clones a branch before it checks out the pinned commit, and it failed in run 36183358181 ([Hermes](clients.md#hermes)).
Every client installs on the hosted runners with no account signed in ([How each client loads a package](clients.md)).
For `prose-discipline`, the Claude Code and Codex cells also run the installed hook commands, `sh -c` on every runner and `cmd /C` for Codex's `commandWindows` on Windows.
They compare what the commands print with the short form in `src/`.
That proves the commands print the text, not that a client delivers it.

Three clients have no install check.
The `cursor` job only reports the check as not run, and it cannot fail.
Cursor's documentation names no command that installs a plugin from a catalogue, and the CLI's API-key route reads `CURSOR_API_KEY` ([Cursor](clients.md#cursor)).
A step that could fail without that route would assert nothing about Cursor.
No job installs OpenClaw or Kiro, so their rows in the README rest on documentation and source alone.
Nothing in CI catches a change in either client that falsifies them.

## Behavioural evals run after each release

The conformance check, the validators and the install matrix prove structure and installation.
None of them shows that a skill triggers on a matching request, or that it improves the answer.
After each release, `.github/workflows/evals.yml` measures both for every released skill that has cases in `evals/`.
It is the only workflow here that calls a model.

`release.yml` calls it as a job of the release run.
A workflow triggered by the tags or the releases would never start, because the release makes both with `GITHUB_TOKEN`.
It can also run by hand on existing tags.
A re-run of the release job skips the evals, because its bump step then finds no releasable commit.
So a run by hand is the recovery when a release run created its tags but stopped before the evals job.

Each skill has positive and near-miss prompts in `evals/<package>/<skill>/cases.yaml`.
The folder sits outside the packages, so no installed package carries the prompts.
A positive prompt runs with the package and again without it, and a near-miss prompt runs with it.
Each prompt runs three times in each of three clients: Claude Code with `haiku`, Codex with `gpt-6-luna`, and Oh-My-Pi with `openrouter/z-ai/glm-5.3-flash`.
The three repeats follow the Agent Skills guide on trigger tests.
The prompts cover each clause of the description once, and no two test the same clause in the same way.
Ten of each kind, the guide's count, cost 100 sessions per skill and client on every release.
On `distilled-research--v0.1.1` the positive sessions cost the most: $0.53 of Claude Code's $0.72, and 45.5M of Codex's 52.1M input tokens.

A release runs only the sessions its changes can affect.
`run` copies a session from the latest complete run of the same skill, client and repeat when the session's inputs are equal and it did not fail.
The inputs of a session without the package are the client command, which holds the prompt, the model and the flags.
A session with the package adds the package tree the client installs, less the manifests' `version`, the listing icon, README and LICENSE.
The tree covers the whole package, because a skill reads its siblings' files: `triangulate` reads `../vet-sources/SKILL.md`, and Codex counts that read as a load of `vet-sources`.
So a release that changed only a README or an icon runs no session, and a skill edit reruns the sessions with the package of every skill in its package.
The sessions without the package rerun when their prompt or the client command changes, or when the last run's session failed.
When the fresh sessions ran on another model than the copied ones, the copied ones run again, so a record holds one model.
Jev's scores of a copied answer stay while the rubric and the Jev model are the same, and otherwise Jev grades the answer again.
A copied session keeps the tag and client version it ran on.
The client installs at its latest version, so `improvement` can subtract an older client's answers without the package from a newer client's answers with it.
A client update can then move `improvement` with no change to the skill, and an issue names every client version behind it.
A run by hand passes `--fresh` and copies nothing.
A change to how a session runs or is parsed, such as `run_session`, an adapter's `parse` or an install step, is not part of the inputs, so it needs a run by hand.
A skill may add five positive and five near-miss prompts in `held-out.yaml`.
They run with the package once per client, on the first repeat, and are not graded.
Nobody reads them while editing a description, so their load count checks the trigger rate on prompts the description was not tuned on.
The same guide warns against adding keywords from failed queries to a description, and a held-out set is what shows whether that happened.
Oh-My-Pi runs `z-ai/glm-5.3-flash`, because in Oh-My-Pi 18.8.6 it loaded `red-flags` in 3 of 3 sessions.
`deepseek-v4-flash` loaded it in 1 of 3, and `gemini-3.1-flash-lite` in 0 of 3.
Claude Code runs `haiku`, so that every release can afford its run.
On the same five release tags in Claude Code 2.1.318, `haiku` loaded the on-demand skills on 10–60% of positive prompts per repeat, and `sonnet` on 60–100%.
So a Claude Code `improvement` mostly reflects how often a skill loads, and `sonnet` users see larger gains than the records show.
TypeSafe's Jev grades each positive answer against the yes-or-no questions in `rubric.yaml`.
It is pinned to `jev-1.13.0`, because `jev-latest` moves to each new stable release and its answers can change with it.
A question that lists `cases` is asked only of the answers to those positive prompts.

Four of the rubric rules in [CONTRIBUTING.md](../CONTRIBUTING.md#write-a-skills-evals-cases) rest on one run of `design-review--v0.2.0` and `prose-discipline--v2.0.0`.
A prompt asks for its result in the reply.
On the two prompts that asked for a file, Codex and Oh-My-Pi wrote the file and replied with a summary of it, and Claude Code was refused the write and replied with an apology.
A question every answer passes is dropped.
`no_filler`, `no_inflation` and `plain_verbs` were yes on all 20 `house-style` answers labelled for them, from both arms.
Jev's mean for each lay between 0.87 and 0.97, on 90 answers with the package and 90 without.
No question asks about sentence structure.
On "never joins two thoughts with a semicolon or a dash", `jev-1.13.0` gave a mean of 0.26 to the 12 answers with neither and 0.24 to the 8 with one.
On "each sentence the answer writes carries one thought", it gave 0.51 to the 3 answers labelled yes and 0.34 to the 17 labelled no.
Criteria stay only where they lower Jev's error on both halves of a labelled sample.
`evals/<package>/<skill>/calibration.json` holds each labelled answer with its evidence, its half of the split, and Jev's score with and without the criteria.
The samples are 144 `house-style` answers and 40 `red-flags` answers from that run.

The without arm removes a different set in each client.
Claude Code disables this package alone, with `claude plugin disable` and the package name.
Codex turns off its `plugins` feature with `--disable plugins`.
With it, Codex 0.161.0 listed only its four built-in skills and none from this package.
Oh-My-Pi disables every skill with `--no-skills` and every rule with `--no-rules`.
So a comparison of `improvement` across clients compares different removals.

Each session records the tools the model called: the skill or file for Claude Code, the whole command for Codex, and the path for Oh-My-Pi.
They show which of the skill's files the model read.
A Claude Code session also records the plugins and skills that its `init` event lists.

Each skill and client gets four numbers per repeat:

- `trigger_hit`, the share of completed positive sessions with the package in which the skill loaded;
- `false_fire`, the share of completed near-miss sessions in which it loaded;
- `compliance`, Jev's mean on answers where the skill loaded;
- `improvement`, Jev's mean with the package minus its mean without.

`compliance` uses only those answers, so it does not mix following the skill with triggering it.
`improvement` keeps every graded answer with the package, because a user who installs the package gets both.
Each Jev mean averages an answer's questions first, and then the answers.
So an answer weighs the same however many questions apply to its prompt.
A session that errored leaves every denominator, and an answer Jev did not grade leaves the two Jev means.
The job summary lists both under `Excluded` with the reason.
It shows each figure with the sessions or answers behind it, so a share of 7 sessions is never read as a share of 10.
Below the figures, one block per skill and client gives the mean of each question in three columns.
The columns are answers where the skill loaded, every graded answer with the package, and every graded answer without it.
The block also lists how often the skill loaded on each positive prompt, and on each near-miss prompt where it loaded at least once.
For Claude Code it counts, in each arm, the sessions whose plugin list holds the package.
In `prose-discipline--v2.0.0`, the package's rules reach two clients without the skill (see [the rules route](#one-rules-file-one-documented-route-per-client)).
A hook prints them into every Claude Code session, and Oh-My-Pi puts the rules file into every system prompt.
The hook does the same in a Codex session once the user trusts it ([Codex](clients.md#codex)), and no evals session trusts it.
A with-package answer in Claude Code or Oh-My-Pi can follow the rules without the model loading `house-style`, and `trigger_hit` counts only that load.
So `cases.yaml` lists such clients under `always_on`.
For them the summary shows `trigger_hit` and `compliance` as `n/a`, and `compare` skips both.
Their block leaves out the skill-loaded column and the loads per positive prompt.

The run publishes each repeat's record to `ghcr.io/akurganow/pegboard-evals` as an immutable OCI artifact tagged `<tag>_<skill>_<client>_<stamp>a<attempt>_r<repeat>`.
Earlier releases' `evals.json` assets stay on their releases as frozen history, and the runner writes no new ones.
A metric regressed when the three repeats of this release and of the package's previous release do not overlap, and the new ones are worse.
The spread between repeats is the tolerance, so the rule has no threshold.
For each skill and client, `previous_results` selects the package's newest earlier complete run: three non-broken repeats with one `client_version`.
Where no such run exists, nothing is compared.
`release.yml` runs one release at a time, its evals included, so a release's records exist before the next release compares against them.
A regression opens an issue.
Two releases are compared only when their `cases.yaml` and their `rubric.yaml` are byte-identical.
They are also compared only when both ran the same model, because a model change moves every metric.
`held-out.yaml` is outside that comparison, so adding or changing it does not break the chain.
Each run installs the client's latest release, so the issue shows both client versions.

Four repository secrets reach the run, each only in the steps that need it: `ANTHROPIC_API_KEY`, `OPENAI_API_KEY`, `OPENROUTER_API_KEY` and `TYPESAFE_API_KEY`.
The step that runs a client's sessions sets that client's key alone, and the runner removes every key value from the published results.
`TYPESAFE_API_KEY` is set only in the report job, which grades the answers and runs no client.
A Codex or Oh-My-Pi session has a shell, and the shell can read `/proc/<pid>/environ` of the job's other processes, `tools/evals.py` among them.
So removing a key from the session's environment does not hide it from the session.
A `PTRACE_MODE_READ_FSCREDS` check governs that file, and Yama's `ptrace_scope` restricts only attach mode.
GitHub's hosted runners give the runner's user passwordless `sudo`, so no separation inside one job would hold.
The report job grades the runs one after another.
In two jobs of run 39507094886, the step that ran forty sessions and graded twenty answers took at most 3 s longer than the sessions.
Every session makes model calls billed to its key, and so does every Jev request.
No session has a time or cost limit, because no measurement shows that a limit would prevent a failure.
GitHub terminates a hosted job at six hours of execution, and that is the only bound.
A session or a grade that errors does not fail its job.
A run job fails when the client does not install or every session errors.
The grading step fails when every grade of a run errors, and that run is left out of the published records.
`conformance.yml` runs `python tools/evals.py selftest`, which checks the event parsers and the arithmetic without a model.
How each client shows a loaded skill is written beside its parser in `tools/evals.py`, with the source it was read from.

Hermes is not measured.
The runner reads skill loads from a client's JSON event stream.
Hermes's stream, `--format stream-json`, implies one-shot mode.
Hermes leaves plugin skills out of the system prompt's skill index, and its `skills_list` tool shows them ([Hermes](clients.md#hermes)).
In one-shot mode the system prompt's skills section is loading guidance followed by that index, which lists each skill as its name and description.
So the one-shot prompt shows the description of no plugin skill.
The guidance tells the model to load a skill only for knowledge it lacks, such as an API, a tool's commands or a project's conventions.
It names testing, debugging and review methodology as general process skills not to load for work the model knows how to do.
`red-flags` reviews a design, and `root-cause` finds the core problem behind many symptoms.
`extraneous` diagnoses what a reader must hold in mind to do a task.
`ariz` and `contradiction` resolve a hard problem or a trade-off with TRIZ.
`house-style` applies a prose standard to anything an agent writes.
The five descriptions other than `house-style`'s each name a method, and none describes knowledge of a particular API, a tool's commands or a project's conventions.
So for those five skills a Hermes trigger rate would measure Hermes's prompt, not the description.
For `house-style` that conclusion rests on the index fact alone, because the one-shot prompt shows no plugin skill's description.

Five alternatives lost.
In Claude Code 2.1.293, `claude plugin eval` wrote the final reply only as the evidence of an LLM grader.
That grader runs a judge model of its own.
`claude plugin eval` has no custom-code graders, so Jev could not take the judge's place.
Concurrent sessions of one client sharing one configuration were not tested, so each job runs on a runner of its own.
A separate workflow on `workflow_run` would have to recover the release's tags, and would also start on every push that releases nothing.
A pinned client version would measure an older client than the one a user installs that day.
Prompts inside a package would reach every user who installs it, because Claude Code copies the plugin directory into its cache.

## The repository records no maintainer verification

A sentence about what the maintainer ran describes one machine on one date.
[How each client loads a package](clients.md) shows what takes its place: every fact cites its kind and source.
