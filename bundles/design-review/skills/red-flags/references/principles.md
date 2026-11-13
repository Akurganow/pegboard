<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [The design principles](#the-design-principles)
  - [Deep and shallow](#deep-and-shallow)
  - [General purpose, and its limit](#general-purpose-and-its-limit)
  - [Pull complexity downward](#pull-complexity-downward)
  - [What matters](#what-matters)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# The design principles

`SKILL.md` lists the sixteen principles of the second edition's "Summary of
Design Principles" with their chapters. The first edition lists fifteen: items
1 to 15, with item 11 worded "Define errors (and special cases) out of
existence". Item 16 belongs to chapter 21, which the second edition added. "1e" or "2e" after a
quotation names the edition whose wording is quoted.

The book calls these "the most important software design principles discussed
in this book". A principle is a direction the review can cite, not a rule the
code fails.

## Deep and shallow

Principle 4: "imagine that each module is represented by a rectangle ... The
top edge of a rectangle represents the module's interface; the length of that
edge indicates the complexity of the interface. The best modules are deep: they
have a lot of functionality hidden behind a simple interface" (§4.4, 1e). "The
benefit provided by a module is its functionality. The cost of a module (in
terms of system complexity) is its interface." A review asks what a caller must
know to use the module (the cost) against what the module does for the caller
(the benefit). "A shallow module is one whose interface is relatively complex
in comparison to the functionality that it provides" (§4.5, 1e).

Ousterhout on why the pair is the measure: it "captures both sides of the
tradeoff; it will tell you when a decomposition is good and also when
decomposition makes things worse" (`aposd-vs-clean-code`, Method Length).

The extreme: "classitis, which stems from the mistaken view that 'classes are
good, so more classes are better'" (§4.6, 1e). The small classes each have an
interface, and "these interfaces accumulate to create tremendous complexity at
the system level."

## General purpose, and its limit

Principle 7 carries the book's own qualifier, "somewhat general-purpose" (§6.1
title). The counterweight is Google's reviewer guide, which asks reviewers to
be "especially vigilant about over-engineering" and adds: "Encourage developers
to solve the problem they know needs to be solved now, not the problem that the
developer speculates might need to be solved in the future."

## Pull complexity downward

Chapter 8: "Most modules have more users than developers, so it is better for
the developers to suffer than the users" (§8, 2e), and "if a class throws an
exception, every caller of the class will have to deal with it" (§8, 1e).
Principles 6 and 10 are, in this skill's reading, one idea seen from the
interface and from the implementation.

Configuration is the book's example of moving complexity up instead of down
(§8.2, 1e). Its test before adding a parameter: "will users (or higher-level
modules) be able to determine a better value than we can determine here?"

## What matters

Principle 16 is the second edition's addition: "One of the most important
elements of good software design is separating what matters from what doesn't
matter" (§21, 2e). In a review it decides which findings to report at all.
