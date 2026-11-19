# Claims

This repository is read by people deciding whether their client can install
something. Every sentence about a client is therefore a claim someone will
act on, and the standing rule is that a claim is read in its source before it
is written.

## The rule

- **Documentation first, source only where it does not answer.** "The
  documentation is unreachable" is a claim to be tested, not accepted — and
  a vendor whose site is blocked usually publishes the same pages as
  Markdown in its own repository, which is documentation and is read first.
- **The text states the claim, and the commit says where it was read.** A
  document or a comment states a client's behaviour in the present tense. It
  carries no source link, revision, version or read date, because nothing
  updates one when the client moves. The commit that writes or changes the
  statement names the source and the revision read. It says which kind the
  source is: documentation, source, or a run of the client's own code. A
  link stands in a document only where the reader follows it to act, such as
  a client's install page. A skill's own bibliography, its
  `references/sources.md`, is the skill's content and keeps its sources.
- **Never invent a command.** Where a client's install command could not be
  verified, none is stated and the reason is given. Declining to answer is a
  correct answer here; a plausible command that does not exist is worse than
  a gap, because a gap is visible.
- **Separate "the standard says" from "this client does".** The first is
  quotable from a specification and stays true. The second is only as good as
  the client's own source and can change without notice, so it is stated as
  that client's behaviour, not as a property of the world.
- **A supported-surface list is a list of obligations.** A row is added when
  there is a source for it, and it is removed rather than left standing when
  the source stops supporting it.
- **A value another file owns is named by that file, never restated.** A
  version, a pin, a hash or a measured figure lives in the file or record
  that sets it. Nothing rewrites a hand-written sentence when that value
  changes, so a sentence that restates it goes stale unseen. The version in
  a standard's name and its section numbers identify the standard, and they
  stay.
- **A document is edited in place.** A change rewrites the sentence it makes
  stale, and adds a line only when no sentence covers the fact. A document
  says what is true now. What was tried, measured, replaced or released is
  history, and git holds it.

## Why it is written down rather than assumed

Fluent, confident, unsourced compatibility text is the easiest thing in this
repository to produce and the hardest thing to catch in review — it reads
exactly like the sourced kind. The rule is not "be careful"; it is that a
claim whose commit names no source is treated as not yet written, whoever
wrote it.

The sourcing order is owned here rather than borrowed: this file is where it
is written down, and it defers outward to nothing — a rule that lives
somewhere the reader cannot open is a rule this repository does not really
have.
