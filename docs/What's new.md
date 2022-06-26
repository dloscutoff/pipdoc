---
layout: default
title: What's New
permalink: whats-new
nav_order: 11
---

# What's new in Pip

Release notes for each minor version of Pip after 1.0.

## Pip 1.1 (released 2022-06-25)

### REPL mode

Pip now has a REPL mode. Run the interpreter with the `-R` flag to enter it.

Enter statements at the prompt to execute them. Entering an expression displays its value. The variables `$_`, `$__`, and `$___` store the values of the last three top-level expressions. Incomplete statements/expressions can be continued on subsequent lines:

    >> "Hello".
    .. "world"
    "Helloworld"
    >> Fi\,3
    .. Pi
    1
    2
    3
    >> $_
    "Helloworld"

Certain comments are treated as REPL commands:

- `;warnings` toggles display of warning messages (can also be invoked as `;warnings off` or `;warnings on`)
- `;quit` quits the REPL (`;exit` also works)
- `;help` displays a help message

See the [REPL mode](repl) page for a full description of REPL features.

### Global variables for the main program's arguments

The variables `\a` through `\e` are set to the main program's first five arguments at the beginning of execution. Similarly, `\g` is set to a list of all the main program's arguments, and `\f` is set to the main function. These variables can be useful when the main arguments or function need to be referenced inside a curly-brace function, where the local variables `a` through `g` have been bound to different values.

### Updated precedence levels for some operators

Some operators have changed precedence to fit better in situations where they are commonly used.

- Unary `FI` and `V` now have lower precedence than binary map and filter operators. Rationale: `FI({...}Ma)` is a common pattern (map a function and then filter out the falsey results).
- Unary trig operators (`SI`, `CO`, `TA`, `SE`, `CS`, `CT`, `AT`, `RD`, and `DG`) now have the same precedence as `BN`: lower than arithmetic operators. Rationale: `SI(a*PI/4)` seems like an important use case; if the result of the trig operation needs to be part of an expression, it can often be reworked to put the trig operator on the rhs of the arithmetic operator.
- Binary exponentiation operators (`E`/`**`, `EE`, and `RT`) now have higher precedence than their unary counterparts. Rationale: `EaEb` should be equivalent to `2EaEb`, which is `2E(aEb)` rather than `(2Ea)Eb`.

### New operators

- List-flattening operators: `FL` (Flatten) flattens a list by one level (equivalent to `$AL`); `FA` (FlattenAll) flattens all levels, resulting in a completely flat list.
- New mapping operator: `MF` (MapFlatten) flattens the mapping result by one level.
- New filtering operators: `FN` (FilterNot) keeps elements for which the function returns a *falsey* value; `FE` (FilterEnumerate) passes two arguments to the filter function, an index and a value; `FU` (FilterUnpack) expects each element to be an iterable and passes it to the function as multiple arguments.
- New sorting operators: `DN` (DescendingNumeric) sorts an iterable in descending order using numeric comparison; `DS` (descending-string) does the same thing using string comparison.
- `CH` (Chop) is the converse of `<>` (Group): where `a<>b` partitions `a` into chunks of size `b`, `aCHb` partitions `a` into `b` chunks of approximately equal size.
- `ZJ` (ZipJoin) zips two iterables (or transposes a list of iterables) and then converts the result into a list of strings. Missing values are filled with spaces. Should be useful for ASCII-art challenges.
- `SH` (Shuffle) randomly permutes an iterable. Unlike Python's `random.shuffle`, it returns a new iterable rather than modifying its argument in place.
- Unary `M` is now an alias for `MX` (Max).
- Unary `N` is now an alias for `MN` (Min).

### Miscellaneous

- Unary `ZD` uses empty string for the default value instead of nil.

