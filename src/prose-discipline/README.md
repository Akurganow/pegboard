# prose-discipline

<!-- description:start -->

An engineering prose standard for agent-written text: short active sentences, plain words, comments that explain why, and labelled review comments.

<!-- description:end -->

## Install

<!-- install:start -->

### Claude Code

```
/plugin marketplace add Akurganow/pegboard
/plugin install prose-discipline@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Codex

```
codex plugin marketplace add Akurganow/pegboard --ref main
codex plugin add prose-discipline@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Oh-My-Pi

```
omp plugin marketplace add Akurganow/pegboard
omp plugin install prose-discipline@pegboard
```

CI installs it on Ubuntu, macOS and Windows.

### Hermes

```
hermes plugins install Akurganow/pegboard/plugins/prose-discipline --no-enable
hermes plugins list
hermes plugins enable prose-discipline
```

Keep the `plugins/prose-discipline` suffix: without it Hermes copies the whole repository, and its two-level scan finds no package.

CI installs it on Ubuntu and macOS.

### Cursor

Cursor's documentation names no command that installs from a repository. It names three routes:

- Public marketplace: open **Customize**, find the plugin, select **Install**. A plugin appears there only after Cursor reviews a submitted repository, and this repository claims no listing.
- Team marketplace, on Teams and Enterprise plans: in **Dashboard**, **Plugins & MCPs**, **Team Marketplaces**, select **Add Marketplace**, then **Import from Repo**, and paste `https://github.com/Akurganow/pegboard`. Developers then install from **Customize**.
- Local: copy `bundles/prose-discipline` to `~/.cursor/plugins/local/prose-discipline`, then restart Cursor or run **Developer: Reload Window**.

CI does not install it.

### OpenClaw

```
openclaw plugins install prose-discipline --marketplace Akurganow/pegboard
```

OpenClaw reads this repository's `.claude-plugin/marketplace.json`. CI does not install it.

### Kiro

No install command is given. Kiro's documentation says Powers follow the Agent Plugins specification, and `plugins/prose-discipline/plugin.json` carries every field the documentation requires. The documentation does not say how Kiro finds several packages in one repository. CI does not install it.

<!-- install:end -->

## Usage

The standard needs no prompt once the client loads it by the route in the table below.

To check existing text against the standard, ask for it:

```
Check this commit message against the house style: "Updated some stuff in auth so it works better now."
```

The agent reports each finding with its place, the rule and the smallest fix, and does not rewrite the text. Ask it to shorten or rewrite a text and it returns the new text with every fact of the original.

The routes by client:

| Client | Route | What you do |
| :-- | :-- | :-- |
| Claude Code | `SessionStart` and `SubagentStart` hooks | nothing |
| Codex | the same hooks, declared in `.codex-plugin/plugin.json` | trust the hooks, again after each release |
| Cursor | the `.mdc` rule, with `alwaysApply: true` | nothing |
| Oh-My-Pi | the `.mdc` rule, applied to every request | nothing |
| Hermes | the skill, pinned with `skills.auto_load` | add the lines below to `config.yaml` |
| OpenClaw | the skill only | nothing |

### Claude Code

The `SessionStart` hook prints the short form of the core rules as plain text,
and Claude Code adds that text to the context. The hook also runs on a resume, a fork, `/clear` and every compaction,
so the rules come back after `/clear` or a compaction removes them. The
`SubagentStart` hook hands each subagent the same text as `additionalContext`.

### Codex

The Codex manifest, `.codex-plugin/plugin.json`, declares
`"hooks": "./hooks/codex.json"`. A declared `hooks` entry replaces Codex's
default `hooks/hooks.json`, so Codex never runs Claude Code's hooks file. Codex skips a plugin's hooks until you review and trust the current
hook definition. When hooks are new or changed, Codex opens a "Hooks need
review" prompt at startup. Codex ties that trust to a hash of the whole installed plugin,
and every release changes `version` in the manifests, so it asks again after
each release. Codex also lists every installed skill and tells the model to
use one whose description matches the task.

### Oh-My-Pi

Oh-My-Pi reads `rules/prose-discipline.mdc` from the bundle that a
marketplace install copies. The file's `alwaysApply: true` puts its full text
into the system prompt of every request. The file names no agents, so
subagents get it too.

### Cursor

Cursor reads the same `rules/prose-discipline.mdc` from the bundle. Its
default discovery takes every `.mdc` file in `rules/`, and a rule with
`alwaysApply: true` applies to all files. Cursor's default discovery also
parses `hooks/hooks.json`, where the bundle holds Claude Code's hooks file.
The documentation does not say whether Cursor accepts that file, and nothing
here ran it. CI does not install the plugin into Cursor.

### OpenClaw

OpenClaw loads this plugin's skill and nothing else. It picks the Codex
manifest when a bundle holds several, detects `hooks/hooks.json` without
running it, reads a Codex manifest's `hooks` value as a list of hook
directories, so `hooks/codex.json` loads nothing, and reads no plugin-root
`rules/`. CI does not install the plugin into OpenClaw.

### Hermes

Hermes loads `plugin.json` and `skills/` from this package, and lists no
plugin skill in its system prompt. To keep the standard active, pin the
skill with `skills.auto_load` in `config.yaml`. Merge the lines into an
existing `skills:` block:

<!-- hermes-auto-load:start -->

```yaml
skills:
  auto_load:
    - agent-plugin-prose-discipline-cf518319:house-style
```

<!-- hermes-auto-load:end -->

Hermes then puts the whole skill, core rules included, into the system
prompt of every new session and marks it as active guidance. The name has
the form `agent-plugin-<slug>-<hash>:house-style`. The slug is
`plugin.json`'s `name` in lower case, with each character other than an ASCII
letter, digit, `_` or `-` turned into `-`. Hermes then strips leading and
trailing `-` and `_`. The hash is the
first eight hex digits of the SHA-256 of that `name`. Hermes builds the
namespace from that `name` for a package installed directly under the
plugins directory, and `hermes plugins install` installs it there under the
manifest `name`.

## What's inside

| Path | What it is |
| :-- | :-- |
| `src/prose-discipline/rules/prose-discipline.md` | the core rules, with a `hook-text` region for the short form the hooks print |
| `src/prose-discipline/skills/house-style/SKILL.md` | the skill: the core rules, the checking procedure and the reference guide |
| `src/prose-discipline/skills/house-style/references/` | structural rules, artifact formats, comment hygiene, vocabulary, slop pruning and a calibration corpus |
| `bundles/prose-discipline/hooks/hooks.json` | Claude Code's `SessionStart` and `SubagentStart` hooks |
| `bundles/prose-discipline/hooks/codex.json` | Codex's two hooks |
| `bundles/prose-discipline/rules/prose-discipline.mdc` | the full rules, with `alwaysApply: true`, for Cursor and Oh-My-Pi |
| `plugins/prose-discipline/plugin.json` | the Agent Plugins 1.0.0 manifest, for Hermes and Kiro |

`bundles/` and `plugins/` are generated from `src/`. No file is a script.

## Requirements and network

The hooks print text with a literal `echo` or `printf`. They read no file,
name no variable and run no script, so they need no `awk` and no runtime. On
Windows, Claude Code runs shell-form hooks in Git Bash when it is installed,
and in PowerShell otherwise.
The `SubagentStart` command uses `printf`. Whether PowerShell has a `printf`
is untested, so without Git Bash that command may print nothing, and a
subagent then gets no rules. Codex runs `cmd.exe` on Windows, and its file
carries a `commandWindows` for it. The skill still ships.

The builder keeps the short form under 8,000 bytes, because Codex's default
2,500-token threshold for hook context and Claude Code's 10,000-character cap
would otherwise cut it. It keeps the Windows command under 8,191 characters,
the command-line limit of cmd.exe, and refuses characters that `sh`,
PowerShell or cmd.exe would read as something other than text.
[About this repository's design](https://github.com/Akurganow/pegboard/blob/main/docs/design.md#no-hook-blocks-the-agent)
gives each reason.

The package makes no network requests, needs no credentials and writes no
files. It adds no MCP servers and no settings files.

## What the standard rests on

The limits come from [ASD-STE100 Issue 9](https://www.asd-ste100.org/assets/files/ASD-STE100_ISSUE9.pdf) (2025), read in full: 20 words for a step, 25 for any other sentence, one instruction per sentence, noun clusters of three words, paragraphs of six sentences. This package drops its controlled dictionary and adds rules against choppy text.

| Kind | Sources |
| :-- | :-- |
| Documentation | [Conventional Comments](https://conventionalcomments.org/), Google eng-practices [comments](https://github.com/google/eng-practices/blob/master/review/reviewer/comments.md), [descriptions](https://github.com/google/eng-practices/blob/master/review/developer/cl-descriptions.md), [Git SubmittingPatches](https://github.com/git/git/blob/master/Documentation/SubmittingPatches), [Linux submitting-patches](https://github.com/torvalds/linux/blob/master/Documentation/process/submitting-patches.rst), [Git CodingGuidelines](https://github.com/git/git/blob/master/Documentation/CodingGuidelines), [Google C++ style guide](https://google.github.io/styleguide/cppguide.html), Google style guide [word list](https://developers.google.com/style/word-list), [procedures](https://developers.google.com/style/procedures), [excessive claims](https://developers.google.com/style/excessive-claims), Digital.gov [style](https://digital.gov/guides/plain-language/writing/style), [clear and short](https://digital.gov/guides/plain-language/writing/clear-short), [GOV.UK error message](https://design-system.service.gov.uk/components/error-message/), [Windows UX guide](https://learn.microsoft.com/en-us/windows/win32/uxguide/mess-error), [Microsoft style guide](https://learn.microsoft.com/en-us/style-guide/top-10-tips-style-voice), [Agent Skills best practices](https://agentskills.io/skill-creation/best-practices), [OpenAI GPT-6 prompt guide](https://developers.openai.com/api/docs/guides/prompt-guidance), Anthropic [Claude](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices), [Fable 5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5), [Fable 5.2](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5-2), [Opus 5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-5), [Sonnet 5.5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-sonnet-5-5) |
| Blog posts and a recorded discussion | [Tim Pope, 2008](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), [Inside GOV.UK, 2014](https://insidegovuk.blog.gov.uk/2014/08/04/sentence-length-why-25-words-is-our-limit/), [Ousterhout and Martin](https://github.com/johnousterhout/aposd-vs-clean-code) |
| Papers | [Kadayat and Eika, abstract only](https://www.academia.edu/83424003/Impact_of_Sentence_Length_on_the_Readability_of_Web_for_Screen_Reader_Users), [Kobak et al.](https://arxiv.org/abs/2406.07016), [Juzek and Ward](https://arxiv.org/abs/2412.11385), [Liang et al.](https://arxiv.org/abs/2403.07183) |
| Descriptive field guide | [Wikipedia, signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) |

Three rules have no published source: the severity words, the quoted cuts and the verification line of a change description.

## Boundaries

- It governs how text is written and checks no fact.
- It governs replies and progress updates as well as artifacts.
- It is not a code linter. Behaviour-level checks belong to a linter. For
  the design of the code itself, use `design-review` or `cognitive-load`.
- It never blocks a reply and has no checker script: enforcement is model
  judgement over rule texts a person can read and argue with.

## License

MIT. See [LICENSE](LICENSE).

## Help

See [SUPPORT.md](https://github.com/Akurganow/pegboard/blob/main/SUPPORT.md). The [pegboard marketplace](https://github.com/Akurganow/pegboard#plugins) lists the other packages.
