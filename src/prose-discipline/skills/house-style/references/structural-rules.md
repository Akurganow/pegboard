# Structural rules: depth

Extends "Sentences and paragraphs" and "Keep the text whole" in the core rules, which give each limit with its STE rule number.

## The limits

The limits are ASD-STE100 Issue 9 rules, without its approved-word lists. STE counts warnings and cautions in the 20-word limit (5.1) and lets two simultaneous actions share a sentence (5.2). It counts a hyphenated compound (8.7), a number, an abbreviation, an identifier, quoted text and a title as one word each (8.6). This standard adds the guard against choppy text, and lets the passive stand where the actor does not matter, which STE does not address.

The numbers are a convention with a source, not a measured optimum. GOV.UK asks for sentences of 25 words or fewer. Digital.gov sets no limit and asks for one idea per sentence. The one screen-reader study (Kadayat and Eika, 2020, 21 participants, audio) found the best comprehension at 16 to 20 words.

## Why the guard against choppy text exists

Anthropic's guide for Claude Fable 5.2 warns that a hard limit, such as 20 words per instruction, can make prose choppy. It recommends STE without numbers. The eval records of release prose-discipline--v2.2.1 (2026-11-06) show the drift. With the plugin, the share of sentences under six words rose in all three clients: from 15% to 21% in Claude, 11% to 16% in Codex and 16% to 18% in Oh-My-Pi. At most 7% of sentences passed 25 words, so the ceiling rarely bound. Anthropic's guide for Fable 5 gives the goal: choose clear over short.

## The rules, each with its reason

- **One main thought.** A reason, condition or consequence stays in the sentence, because a connective keeps the link the reader needs. A second thought takes a second sentence.
- **Keep the link.** Fragments such as "Certificate expired. Error rate up." make the reader guess the cause. Join them with because, so, but or then.
- **No arrow chains or coined labels.** `A -> B -> fails` drops the verbs. A label such as "the sweep" names nothing to a reader who was not there.
- **Reasoning stays in a paragraph.** Bullets drop the connectives that carry the logic. They fit parallel items.
- **Passive.** Rewrite "is handled by X" with X as the subject.
- **Noun clusters.** Four nouns in a row hide which word governs. Established terms and component names are exempt.
- **Punctuation.** Join a thought to its reason with a connective, because a dash there is a listed sign of generated text (see `vocabulary.md`). A dash that grammar requires stays.
