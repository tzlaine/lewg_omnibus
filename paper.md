---
title: "LEWG Omnibus Design Policy Paper"
document: D1655R0
date: 2019-06-01
audience: LEWG
author:
  - name: Zach Laine
    email: <whatwasthataddress@gmail.com>
toc: true

---

# Introduction

This paper is the beginning of an effort to establish some best practices for
making certain decisions in LEWG.  The idea here is to come up with guidelines
such that, for a given guideline, the guideline works in 90% (or higher) of
the cases to which it applies.  None of these guidelines is expected to be
standardized in normative wording.  Rather, the guidelines should be voted on
by LEWG, and act as *de facto* rules, applied both to increase the consistency
of LEWG decisionmaking, and to reduce the time that LEWG takes to process
papers.

Below, I have added sections for four different guidelines that have come up
in the past few meetings' LEWG sessions.  For each, I have included minimal
discussion and argument where I expect that the LEWG regular attendees will
have well-considered opinions already, or where a clear consensus has
previously been shown.

Each guideline has explicit polls which I think are warranted; each poll is
stated as an affirmative statement.  If one of these statements does not
achieve consensus, I think it would be useful to see if its negation can
achieve consensus instead (rather that leaving the *status quo*, which is not
to have a guideline at all).


# How LEWG Expects New Algorithms to be Proposed

Since we now have an effective fork of the standard algorithms into the
unconstrained ones in `std` and the concept-constrained ones in `std::ranges`,
*and* considering that we have parallel verions of most of the algorithms, how
do we want new algorithm submissions to be propoesed?

Suggested Poll: All new algorithms should be concept-constrained, and go into
`std::ranges`.

Suggested Poll: Parallel versions of new algorithms should not be part of an
initial proposal.


# The Proper Use of `explicit` in Types and Class Templates in the Standard Library

Tony Van Eerd has a very thorough analysis of when `explicit` should be
applied to constructors and conversion operators ([@Conv]).

Suggested Poll: A constructor callable with a single argument or a conversion
operator should be declared `explicit` unless it:

- is a conversion between two types that are essentially the same;
- preserves all data during conversion;
- imposes little or no performance penalty;
- does not throw; and
- results in a memory-safe value.

# The `is_` Prefix: Friend or Foe?

There are quite a few interfaces in the standard library that return `bool`
and are prefexed with `is_`.  However, most interfaces that return `bool`, and
have no `is_` prefix.  There are also the type traits; all the predicate-like
ones are prefixed with `is_`.

Note that there used to be an argument that we need `is_foo()` to disambiguate
two overloads of `foo()`, one of which returns `bool` and one of which returns
`void`.  Now that we have `[[nodiscard]]`, and that LWG sprinkles it liberally
on standard library interfaces, we don't really need this disambiguation.

Suggested Poll: Standard library functions that return `bool` should not be
prefixed with `is_`.

Suggested Poll: Predicate-like type traits should be prefixed with `is_`.


# `any_`: A Great Prefix for Naming Erased Types, or The Greatest Prefix for Naming Erased Types?

TODO

---
references:
  - id: Conv
    citation-label: Conv
    title: "Implicit and Explicit Conversions"
    author:
      - family: Tony \"T-Dog\"
        given: Van Eerd
    URL: https://github.com/tvaneerd/isocpp/blob/master/conversions.md
---
