<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [What to look for under each red flag](#what-to-look-for-under-each-red-flag)
  - [Shallow Module](#shallow-module)
  - [Information Leakage](#information-leakage)
  - [Temporal Decomposition](#temporal-decomposition)
  - [Overexposure](#overexposure)
  - [Pass-Through Method](#pass-through-method)
  - [Repetition](#repetition)
  - [Special-General Mixture](#special-general-mixture)
  - [Conjoined Methods](#conjoined-methods)
  - [Comment Repeats Code](#comment-repeats-code)
  - [Implementation Documentation Contaminates Interface](#implementation-documentation-contaminates-interface)
  - [Vague Name](#vague-name)
  - [Hard to Pick Name](#hard-to-pick-name)
  - [Hard to Describe](#hard-to-describe)
  - [Nonobvious Code](#nonobvious-code)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# What to look for under each red flag

`SKILL.md` holds the definition and section of each flag. This file says what
a flag looks like in code and quotes the book's own test where it gives one.
Every "Look for" is this skill's, not the book's. "1e" or "2e" after a quotation
names the edition whose wording is quoted.

The book's list is its selection, and its chapters name other flags. A flag is
a symptom, and a symptom can have a reason, so weigh a reason for the structure
before filing the finding. The book does not number the flags.

## Shallow Module

Look for a class or function whose signature, options and documented behaviour
take as long to learn as its body takes to read. A wrapper that forwards every
parameter. A one-line method that callers must understand anyway. The book's
own example of shallow methods is getters and setters (§19.6).

## Information Leakage

Look for a file format, wire encoding, table layout or naming rule that two
modules both know, so that a change to one forces the same change in the
other. Parnas' criterion is the test: hide a design decision from the other
modules (`decisions.md`).

## Temporal Decomposition

Look for modules named after phases (read, parse, validate, write) that share
knowledge of one format. Parnas 1972 calls the same mistake decomposing "on the
basis of a flowchart".

## Overexposure

The book's flag box follows its example "defaults in HTTP responses". Look for
a required parameter that almost every caller sets to the same value. A
constructor with eight arguments where two are in use. A configuration a caller
must read before the first call.

## Pass-Through Method

Look for two layers with the same abstraction: "if different layers have the
same abstraction, such as pass-through methods or decorators, then there's a
good chance that they haven't provided enough benefit to compensate for the
additional infrastructure they represent" (§7.6, 2e).

## Repetition

Look for the same sequence of calls in several places. The remedy is to bring
the pieces together. Repeating a trivial line is not this flag.

## Special-General Mixture

Look for a general mechanism with a branch for one caller, or a library
function that knows one product's rule. The remedy is to separate the two; the
second edition adds "Push specialization upwards (and downwards!)" (§6.6).

## Conjoined Methods

Look for reading one function and having to open another to follow it.
Ousterhout's test: "If you've ever found yourself flipping back and forth
between the implementations of two methods as you read code, that's a red flag
that the methods might be entangled" (`aposd-vs-clean-code`, Method Length).

## Comment Repeats Code

Look for a comment that restates the line below it. The `prose-discipline`
package, when installed, calls this a narrator comment.

## Implementation Documentation Contaminates Interface

Look for a public doc comment that names the data structure, algorithm or cache
behind the call. A caller who reads it now depends on it.

## Vague Name

Look for `data`, `info`, `handle`, `process`, `manager`, or a `result` that
holds one specific thing.

## Hard to Pick Name

Look for a name the author changed twice. The book: "If you find it difficult
to come up with a name for a particular variable that is precise, intuitive,
and not too long, this is a red flag. It suggests that the variable may not
have a clear definition or purpose" (§14.3, 1e).

## Hard to Describe

Look for an interface comment that needs three paragraphs: "If a method or
variable requires a long comment, it is a red flag that you don't have a good
abstraction" (§15.3, 1e).

## Nonobvious Code

Look for a reader who says it is unclear. That is the whole test (ch. 18, 2e,
quoted in `complexity.md`). The `cognitive-load` package, when installed,
carries the reader-side catalogue for this flag.
