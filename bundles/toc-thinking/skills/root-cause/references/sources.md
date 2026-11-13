<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Sources](#sources)
  - [Read](#read)
  - [Not read](#not-read)
  - [What the skill adds on its own](#what-the-skill-adds-on-its-own)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Sources

What the references were checked against, with each source's kind and the date read.

## Read

- **TOCICO Dictionary, second edition, 2012** (dictionary text). Read entry by entry from a public
  community copy, a Russian-annotated edition with a few mis-encoded characters, at
  <https://github.com/comm644/tocdic/tree/b9fada8c978d38cb803f7d900fa82df6cdad3da6> on 2026-09-23. The
  quotations were re-read on 2026-11-11 and match that copy, not the official file. Supports every
  TOCICO quotation. No later edition was found.
- **H. William Dettmer, *The Logical Thinking Process*, ASQ Quality Press, 2007, ISBN
  978-0-87389-723-5** (book text). Read from a Markdown conversion at
  <https://github.com/life-itself/reasoncommons/tree/74e50e4cc2c949b7be67212b99461fee03e1a954/library/logical-thinking-process-dettmer>:
  chapters 1, 2, 4, 5, 6 and 7 on 2026-09-23, the quoted passages again on 2026-11-11. Supports every
  Dettmer quotation.
- **Andreas Zeller, *The Debugging Book*, "Introduction to Debugging", "The Scientific Method"**
  (online text, CC BY-NC-SA 4.0): <https://www.debuggingbook.org/html/Intro_Debugging.html>, read
  2026-11-11. Supports the hypothesis, prediction and experiment loop in `clr.md`.
- **Richard I. Cook, *How Complex Systems Fail*** (online text, points 3, 7 and 8):
  <https://how.complexsystems.fail/>, read 2026-11-11. Supports the critique of root causes and the
  hindsight warning.
- **John Allspaw, "Each necessary, but only jointly sufficient"**, Kitchen Soap, 2012-02-10 (blog
  post): <https://www.kitchensoap.com/2012/02/10/each-necessary-but-only-jointly-sufficient/>, read
  2026-11-11. Supports the same critique.
- **Google, *Site Reliability Engineering*, chapter 15, "Postmortem Culture"** (online text):
  <https://sre.google/sre-book/postmortem-culture/>, read 2026-11-11. Supports the plural "root
  cause(s)".
- **Seonmin Kim, Victoria J. Mabin and John Davies, "The theory of constraints thinking processes:
  retrospect and prospect", *International Journal of Operations & Production Management* 28(2), 2008,
  pp. 155-184** (abstract, from Crossref, <https://api.crossref.org/works/10.1108/01443570810846883>,
  and OpenAlex, read 2026-11-11). It reviews papers from 1994 to early 2006, "identifies specific
  publication and research gaps" and calls the TOC body of knowledge "largely practice-led". The
  abstract gives no paper count and does not list the gaps, so this skill reports neither. The full
  text is behind the publisher's paywall and was not read.
- **Sildenir Alves Ribeiro and others, "Research Opportunities on the Application of the Theory of
  Constraints to Software Process Development", *Journal of Software* 12(4), 2017, pp. 227-239** (paper
  full text, <http://www.jsoftware.us/vol12/245-JSW15216.pdf>, read 2026-11-11). It surveys TOC in
  software process work and finds work that does "not present solidity in terms of either methodology
  or application". This skill makes no claim about how effective the Thinking Processes are.

## Not read

Nothing in this skill is quoted from these.

- The official *TOCICO Dictionary* file, which TOCICO's learning centre sells.
- Eliyahu M. Goldratt, *It's Not Luck*, North River Press, 1994, and Goldratt and Jeff Cox, *The Goal*
  (Dettmer cites the 1992 second edition).
- H. William Dettmer, *Goldratt's Theory of Constraints*, 1997, which the 2007 book's copyright page
  names as the book it rewrites.
- Lisa J. Scheinkopf, *Thinking for a Change*, 1999.

## What the skill adds on its own

These parts are this skill's adaptation for software work and not TOC as published:

- The classification in Step 1, the rule in Step 2 to report separate root causes when branches do not
  meet, the bridge in Step 3 from the core problem to D and D', and the "Observed by:" line in Step 6.
- "Scrutiny becomes checks" in `SKILL.md` and "Running a check" in `clr.md`: the predicted effect
  reservation applied to software, with Zeller's loop. TOCICO's entry says a present predicted effect
  "validates" the cause. The skill is more cautious: a present effect raises confidence, because a
  rival cause may predict it too.
- The delivery rules in `SKILL.md`, the Mermaid diagram, the reading in `tools.md`, "What a root cause
  is", and every software example in `clr.md`.
