<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [The decisions a review asks about](#the-decisions-a-review-asks-about)
  - [Together or apart](#together-or-apart)
    - [Splitting a method](#splitting-a-method)
  - [Errors](#errors)
  - [Design it twice](#design-it-twice)
  - [Comments and names](#comments-and-names)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# The decisions a review asks about

The book's criteria for the steps that make these decisions. Section numbers
are the second edition's. "1e" or "2e" after a quotation names the edition
whose wording is quoted.

## Together or apart

Chapter 9 opens with signs that two pieces of code are related (§9, 1e):

- "They share information; for example, both pieces of code might depend on the
  syntax of a particular type of document."
- "They are used together: anyone using one of the pieces of code is likely to
  use the other as well. This form of relationship is only compelling if it is
  bidirectional." The counter-example: a disk block cache always involves a
  hash table, but hash tables serve many other uses, so the two stay apart.
- "They overlap conceptually, in that there is a simple higher-level category
  that includes both of the pieces of code."
- "It is hard to understand one of the pieces of code without looking at the
  other."

The chapter's sections are the criteria: bring together if information is
shared (§9.1), if it simplifies the interface (§9.2), to eliminate duplication
(§9.3); separate general-purpose and special-purpose code (§9.4). Its
conclusion: "The decision to split or join modules should be based on
complexity. Pick the structure that results in the best information hiding, the
fewest dependencies, and the deepest interfaces" (§9.9, 2e).

Parnas gave the criterion the book builds on: begin "with a list of difficult
design decisions or design decisions which are likely to change. Each module is
then designed to hide such a decision from the others" (Parnas 1972,
conclusion).

### Splitting a method

"Length by itself is rarely a good reason for splitting up a method. In
general, developers tend to break up methods too much. Splitting up a method
introduces additional interfaces, which add to complexity" (§9.7, 1e). Five
independent 20-line blocks in one method can be read one block at a time. The
second edition: "Depth is more important than length: first make functions
deep, then try to make them short enough to be easily read. Don't sacrifice
depth for length" (§9.8, 2e). The test for a split that went too far is the
Conjoined Methods flag.

## Errors

Chapter 10 gives three techniques and one answer for the rest.

1. **Define errors out of existence.** "The best way to eliminate exception
   handling complexity is to define your APIs so that there are no exceptions
   to handle" (§10.3, 1e). The example is Tcl's `unset`: it should ensure that a
   variable no longer exists, so deleting a missing one is no error. The second
   edition applies the move to special cases: "designing the normal case in a
   way that automatically handles the edge conditions without any extra code"
   (§6.8, 2e).
2. **Mask exceptions.** "An exceptional condition is detected and handled at a
   low level in the system, so that higher levels of software need not be aware
   of the condition" (§10.6, 1e). The example is TCP retransmission.
3. **Aggregate exceptions.** "Handle many exceptions with a single piece of
   code" (§10.7, 1e). It works best when an exception propagates several levels
   up before it is handled, the opposite of masking, which works best at a low
   level.
4. **Just crash.** For errors not worth handling, print diagnostic information
   and abort (§10.8).

The book ranks the first above the other two and no further (§10.10, 2e).
Masking and aggregation are alternatives that fit different shapes of problem.
The chapter also names the opposite failure, an "over-defensive style where
anything that looks even a bit suspicious is rejected with an exception"
(§10.2, 1e).

## Design it twice

"You'll end up with a much better result if you consider multiple options for
each major design decision: design it twice" (§11, 2e). Pick approaches that
are "radically different from each other", even when only one seems reasonable,
then list the pros and cons of each. "The most important consideration for an
interface is ease of use for higher level software."

A review writes the second design down briefly, with the reason it lost.
Nygard's decision-record template has a title and four parts, in this order:
Context, Decision, Status (proposed, accepted, deprecated or superseded) and
Consequences ("All consequences should be listed here, not just the 'positive'
ones"), and he wants each record "one or two pages long" (Nygard 2011). The
review does not require the format. It asks that the alternative and the reason
it lost survive where a later reader can find them.

## Comments and names

Chapter 12 answers four excuses for not writing comments, among them "Good code
is self-documenting". Its answer: "The overall idea behind comments is to
capture information that was in the mind of the designer but couldn't be
represented in the code" (§12.5, 1e). Chapter 13's rule: "comments should
describe things that aren't obvious from the code" (§13, 2e). Google's reviewer
guide agrees on the direction: comments "explain why some code exists, and
should not be explaining what some code is doing". A review that asks for a
comment therefore takes no side against common practice. The dispute is with
one book, and `positions.md` states it.

Names: "Names should be precise" (§14.3 title). The flags Vague Name and Hard to
Pick Name are the tests. The second edition's §14.6, "A different opinion: Go
style guide", gives the opposite view. Gerrand: "long names obscure what the
code does". Ousterhout: readability "must be determined by readers, not
writers" (§14.6; text read in the first edition's §14.5). He agrees with one
rule: "The greater the distance between a name's declaration and its uses, the
longer the name should be." A review that finds a short name therefore asks how
far it travels from its declaration, and whether readers have complained.
