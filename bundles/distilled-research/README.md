# distilled-research

<!-- description:start -->

Vets sources, collapses copies to independent origins, and grades each claim by how many independent origins support it.

<!-- description:end -->

## Install

<!-- install:start -->

### Claude Code

```
/plugin marketplace add Akurganow/pegboard
/plugin install distilled-research@pegboard
```

Source: Claude Code documentation, <https://code.claude.com/docs/en/discover-plugins>. CI installs it on Ubuntu, macOS and Windows.

### Codex

```
codex plugin marketplace add Akurganow/pegboard --ref main
codex plugin add distilled-research@pegboard
```

Source: Codex documentation, <https://developers.openai.com/plugins/build/plugins>, for `marketplace add`; Codex source, [`plugin_cmd.rs`](https://github.com/openai/codex/blob/e3e5ad28470f6a225301518c30a66e749a880164/codex-rs/cli/src/plugin_cmd.rs), for `plugin add`. CI installs it on Ubuntu, macOS and Windows.

### Oh-My-Pi

```
omp plugin marketplace add Akurganow/pegboard
omp plugin install distilled-research@pegboard
```

Source: Oh-My-Pi documentation, [`docs/marketplace.md`](https://github.com/can1357/oh-my-pi/blob/a33cc26824e3c91edd9fa42d681f10dceb4ac2f0/docs/marketplace.md). CI installs it on Ubuntu, macOS and Windows.

### Hermes

```
hermes plugins install Akurganow/pegboard/plugins/distilled-research --no-enable
hermes plugins list
hermes plugins enable distilled-research
```

Keep the `plugins/distilled-research` suffix: without it Hermes copies the whole repository, and its [two-level scan](https://github.com/NousResearch/hermes-agent/blob/a0ca7c19204e514f9590ce3b812e029b315ab9e9/website/docs/user-guide/features/plugins.md) finds no package.

Source: Hermes documentation, [`developer-guide/plugins/index.md`](https://github.com/NousResearch/hermes-agent/blob/a0ca7c19204e514f9590ce3b812e029b315ab9e9/website/docs/developer-guide/plugins/index.md), for the commands; Hermes source, [`plugins_cmd.py`](https://github.com/NousResearch/hermes-agent/blob/a0ca7c19204e514f9590ce3b812e029b315ab9e9/hermes_cli/plugins_cmd.py) (`_resolve_git_url`), for the subdirectory form and what happens without it. CI installs it on Ubuntu and macOS.

### Cursor

Cursor's documentation names no command that installs from a repository. It names three routes:

- Public marketplace: open **Customize**, find the plugin, select **Install**. A plugin appears there only after Cursor reviews a submitted repository, and this repository claims no listing.
- Team marketplace, on Teams and Enterprise plans: in **Dashboard**, **Plugins & MCPs**, **Team Marketplaces**, select **Add Marketplace**, then **Import from Repo**, and paste `https://github.com/Akurganow/pegboard`. Developers then install from **Customize**.
- Local: copy `bundles/distilled-research` to `~/.cursor/plugins/local/distilled-research`, then restart Cursor or run **Developer: Reload Window**.

Source: Cursor documentation, [Plugins](https://cursor.com/docs/plugins), read 2026-11-04, for the three routes; [Plugins reference](https://cursor.com/docs/reference/plugins), read 2026-11-04, for the submission and review. CI does not install it.

### OpenClaw

```
openclaw plugins install distilled-research --marketplace Akurganow/pegboard
```

Source: OpenClaw documentation, [`docs/cli/plugins/install.md`](https://github.com/openclaw/openclaw/blob/db6ac584cf205ea9a72de7ae83a4e65199b926a4/docs/cli/plugins/install.md#L277-L283). OpenClaw reads this repository's `.claude-plugin/marketplace.json` (OpenClaw source, [`marketplace.ts`](https://github.com/openclaw/openclaw/blob/db6ac584cf205ea9a72de7ae83a4e65199b926a4/src/plugins/marketplace.ts#L35-L38)). CI does not install it.

### Kiro

No install command is given. Kiro's documentation says Powers follow the Agent Plugins specification, and `plugins/distilled-research/plugin.json` carries every field the documentation requires. The documentation does not say how Kiro finds several packages in one repository. CI does not install it.

Source: Kiro documentation, [Create a power](https://kiro.dev/docs/powers/create) and [Installation](https://kiro.dev/docs/powers/installation), read 2026-11-04.

<!-- install:end -->

## Usage

Ask a research question in your own words. Both skills trigger from the text of the request:

```text
Is it true that a monorepo helps a team ship faster than many repositories?
Survey what the research says about monorepos versus many repositories across many sources, and tell me which sources only repeat each other.
```

`triangulate` fires on questions about what the evidence says: whether a claim is well supported, what many sources agree on, why studies contradict each other, which sources copy one origin, or a survey of a field. For a single-fact lookup, a summary of one page or a code search, ask directly. `vet-sources` fires when you ask whether a site, paper or repository can be relied on, or want sources rated before you cite them. It does not cover install safety, malware or licence checks.

### How triangulate sizes a run

The agent picks the size from your request and does not ask.

- **Direct run:** one claim or at most two sub-questions, answered from at most about five sources that you named or pasted or that the agent finds. It works in the conversation, sends no plan, writes no files and starts no child agents. No independent verifier runs, so an Established point shows as Probable.
- **Survey:** more than about five sources, or three or more sub-questions. The agent sends one short plan with the sub-questions, the depth with its ceiling on child agents, and the folder for the run's files, then waits for your go-ahead, because child agents cost you money. A change that raises the ceiling needs a new go-ahead. [`depth.md`](skills/triangulate/references/depth.md) gives the quick, standard and deep depths. A survey reads kept tier A or B primary sources up to the ceiling and lists the rest as not read. A fresh verifier rechecks the grades and fetches up to five quotes.

The plan does not ask about tools, hosts, query strings or shell access. Your harness's permission settings decide those.

### What the agent sends and writes

- **Records** that the agent chooses receive a public hostname, a published name, a DOI, a repository path or a package name, and nothing else. They never receive your question, your text or a local path.
- **Web search** receives the search strings of the run: words of your question, one string worded as the opposite claim, a source's hostname or title for the check from outside, and a source's kind and place to find records.
- **Pages** of the sources are fetched on public hosts. The agent never fetches a private, internal or IP-literal host.
- **Files:** a direct run writes none. A survey writes the run folder named in the plan after your go-ahead. When the harness cannot start child agents, the run goes on without waiting and still writes the folder. The folder holds a `.gitignore` with the single line `*`. It never edits your own `.gitignore` and never reuses an existing run folder.
- **Paid checkers:** the agent names an installed paid checker and the exact inputs it would receive, and runs it only after you say yes.
- **Child agents:** a survey only, up to the ceiling in the plan. A child writes only the file its brief names, starts no further child, and reads no environment variables, credential files, key files or dot-files.

### What the reply holds

The reply opens with a direct answer, then a legend and a table of points. Each row shows a grade, the counts `N (M) + K`, the evidence and the strongest dissent. [`origins-and-grades.md`](skills/triangulate/references/origins-and-grades.md) holds the grade table and the counts: `N` independent origins, `M` of them measurements read in full with a literal quote, and `K` sources that repeat the claim without a traced origin.

- **Grades:** Established, Probable, Tentative, Not established, and Contested, which stands outside the ladder. On a science or health topic, Established needs a tier A measurement.
- **Pasted sources:** a pasted excerpt is text you supplied, not a page the agent opened. It is marked "as pasted" and may count toward `N` but never toward `M`, so no point reaches Established on pasted text alone.
- **Quotes:** a fetch tool may return a summary of a page and not its text. A quote counts as literal only when the tool returned the page's own text. Otherwise it is `paraphrase`, and an origin whose quotes are all `paraphrase` never counts toward `M`. Source: Claude Code [tools reference](https://code.claude.com/docs/en/tools-reference#webfetch-tool-behavior), documentation, read 2026-11-05: the result is a separate model call, "lossy by design". On a harness whose fetch tool summarises, `M` stays 0 and no point reaches Established.
- **Tail:** Contested positions, Not established points, caveats and skipped sources appear only when present. Every reply ends with a header line that gives the mode, the date, the read levels and the verifier mode.

Grades and tiers are ordinal and uncalibrated. They rank claims within one run and give no probability. On a health question the reply says that the grades describe how the sources agree and are no advice for your case. When you ask for another length or form, the reply takes it and adds the grades in a short note.

### Other starts

- **Rating alone:** `vet-sources` rates up to 15 sources per reply and lists the rest as not rated. It chooses outside records that fit each source's kind and place, reads each source's page once, and gives the record as found and a tier. It never calls a source safe.
- **No search or page-reading tool:** the agent reads pages through the shell when it reaches the web. Otherwise it works from sources you paste, and with none gives what it knows from memory, marked "from memory, not graded".
- **No subagents:** a survey runs the briefs in turn at quick depth, with no wait after the plan. Verification is a shared-context check, labelled so, and Established points show as Probable.
- **Nobody to answer:** in a non-interactive session the agent does not wait for a go-ahead and answers as a direct run.

## What's inside

| Path | What it is |
| :-- | :-- |
| [`skills/triangulate/SKILL.md`](skills/triangulate/SKILL.md) | the research method: direct mode in full, survey mode in brief, and the rules that hold in every mode |
| [`skills/triangulate/references/survey.md`](skills/triangulate/references/survey.md) | the survey: terms, plan message, stages, pasted sources and the dispatch template |
| [`skills/triangulate/references/depth.md`](skills/triangulate/references/depth.md) | the three depths, their ceilings on child agents, and the shards |
| [`skills/triangulate/references/run-folder.md`](skills/triangulate/references/run-folder.md) | file rules, the `plan.md` fields, the files and their writers, the id check, resume |
| [`skills/triangulate/references/origins-and-grades.md`](skills/triangulate/references/origins-and-grades.md) | origins, the grade table with its legend text |
| [`skills/triangulate/references/output.md`](skills/triangulate/references/output.md) | the reply format |
| [`skills/triangulate/references/lead.md`](skills/triangulate/references/lead.md) | the files only the lead of a survey writes, the verifier's verdicts and stage 8 without subagents |
| [`skills/triangulate/references/briefs/`](skills/triangulate/references/briefs) | the briefs of the collector, reader, tracer and verifier |
| [`skills/vet-sources/SKILL.md`](skills/vet-sources/SKILL.md) | the rating skill, with the data rule and the topic types |
| [`skills/vet-sources/references/records.md`](skills/vet-sources/references/records.md) | what a lookup sends, how the agent chooses records, the statuses |
| [`skills/vet-sources/references/tiers.md`](skills/vet-sources/references/tiers.md) | tiers A, B and C, their legend text, and what moves a source |
| [`skills/vet-sources/references/briefs/vetter.md`](skills/vet-sources/references/briefs/vetter.md) | the vetter's brief, which is also the procedure `vet-sources` follows |
| `plugin.json` in `plugins/distilled-research/`; `.claude-plugin/`, `.codex-plugin/` and `.cursor-plugin/` manifests in `bundles/distilled-research/` | the Agent Plugins 1.0.0 manifest in the first build, one manifest per client in the second |
| [`LICENSE`](LICENSE) | the MIT license |

## Requirements and network

Research needs a search tool and a page-reading tool, or a shell that reaches the web, and a file-read tool or a shell for the skill's own files. A PDF reader helps with papers. Subagents are optional. The package needs no runtime, key or account.

The package lists no service. The agent chooses outside records for each source's kind and place. It uses a record only when it is public without a key or an account and passes the other tests in [`records.md`](skills/vet-sources/references/records.md). When no record fits, the row reads `not checked`. A record is never a verdict that a source is safe, and the reply quotes a record's own number only as that record's. The agent fetches the pages of the sources it reads on any public host, honours a list of hosts you ask it to avoid, and discards a page that a redirect brought from one.

## Trust

This plugin ships no scripts, tools or servers. It is instructions, and what they make an agent do can reach the network and your files. The agent looks up sources in public records it chooses, runs web searches with words of your question and with a source's hostname or title, and fetches the pages it reads. A survey starts child agents only after your go-ahead and up to the ceiling in the plan. Each child receives a written list of what it may read, write, fetch and search. Those are requests in text: what your harness's permission settings do not block, a child can still do, so set a tool list for children where your harness allows it. Web pages can carry instructions aimed at agents. The plugin tells the agent to treat all page, search and file text as data, and a model can still fail at that, so deny permissions you do not want a poisoned page to use. A survey writes a run folder that holds your question and text copied from pages. The plugin never holds or reads keys and asks before using a paid checker. Request safety is your responsibility.

## Boundaries

- As of 2026-11-05 the method's stages had run three times: once by hand and twice as the built plugin, on a science/health topic and on a practice/technology topic, with an earlier wording that asked for a report and a yes first. No news/facts topic was run.
- As of 2026-11-11 no recorded run covers the direct mode, the survey plan message, the handling of pasted sources or the self-check of a direct run.
- The evals run one turn in an empty directory, and the agent finds its own sources. They reach the direct mode and the survey's plan message, and no later survey stage, so dispatch, parallelism, folder writes and injection are not measured.
- No test has measured how often an Established point is right.
- Without a search or page-reading tool, and without a shell that reaches the web, the agent can only rate what you paste and otherwise answers from memory, marked as not graded.
- A fetch tool that follows redirects without showing the target can reach a host the agent would have skipped. The text names no check on redirect targets except for hosts you asked it to avoid.
- A retraction record can omit a notice, so a retracted source can go unflagged, though the agent also reads the paper's own page.
- The agent picks records from what its search finds, so two runs can differ.
- A date, claim or link known only from a search result or memory stays `unconfirmed` and is never a traced origin.

## License

MIT. See [LICENSE](LICENSE).

## Help

See [SUPPORT.md](https://github.com/Akurganow/pegboard/blob/main/SUPPORT.md). The [pegboard marketplace](https://github.com/Akurganow/pegboard#plugins) lists the other packages.
