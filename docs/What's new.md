---
layout: default
title: What's New
permalink: whats-new
nav_order: 11
---

# What's new in Pip

Release notes for each minor version of Pip after 1.0.


## Pip 1.3 (released 2026-01-19)

### Loop counter variables

Loops (`F`, `W`, `T`, `L`, and `LR`) now automatically set a local variable to their current iteration count. The outermost loop in a local scope uses `e` as its counter variable; loops nested at deeper levels use `d`, then `c`, and so on. The iteration count is 0-based. After the loop, the value of the counter variable equals the total number of times the loop ran.

These local variables are also still used for program/function arguments. When a loop begins, it overwrites any existing value in its counter variable. This should almost never cause a problem, since functions seldom use more than two arguments and loops are seldom nested more than two deep.

### Index arguments from functional operators

Functional operators that traditionally passed one argument to their function (such as `M`, `FI`, and `SK`) now pass an extra argument representing the current index in the iterable. (This means that `{[ab]}Mg` is now equivalent to `{[ba]}MEg`.) Operators affected are `M`, `MF`, `MJ`, `MM`, `MQ`, `MS`, `FI`, `FF`, `FJ`, `FN`, `FQ`, `SK`, `DK`, `MK`, and `NK`. In the case of `MM`, two extra arguments are passed, representing the index in the outer map (`b`) and the inner map (`c`).

Existing code should be unaffected, since the functions passed to these operators would previously have used their first argument and ignored the rest.

### New operators

- New mapping operator: `MQ` (MapUnique) uniquifies the mapping result.
- New filtering operators: `FF` (FilterFlatten) flattens the filter result by one level; `FQ` (FilterUnique) uniquifies the filter result.
- `MK` (MaxKeyed) finds the maximum value in an iterable by a key function (compare `DK`).
- `NK` (MinKeyed) finds the minimum value in an iterable by a key function (compare `SK`).
- New base-conversion operators: `TH` (ToHex) converts a number to hexadecimal; `FH` (FromHex) converts from hexadecimal.

### New regex variables

- `XB` matches word boundaries (`\b`)
- `XH` matches hexadecimal digits (`[0-9a-f]`, case-insensitive)
- `XS` matches whitespace characters (`\s`)
- `NB` matches non-boundaries (`\B`)
- `ND` matches non-digit characters (`\D`)
- `NS` matches non-space characters (`\S`)
- `NW` matches non-word characters (`\W`)

### Miscellaneous

- Ending a program with a semicolon suppresses autoprinting of the final expression.
- Regex variables `XC` (consonants), `XV` (vowels), and `XY` (vowels including Y) have been changed to case-insensitive.
- `TB` and `FB` now handle bases up to 62.
- `j` is now a regular variable. (Since Pip 1.0, it had been reserved for possible future syntax, but that idea has been abandoned.) For now, its initial value is nil.
- In REPL mode, typing `;help ` followed by an operator or a global variable prints some information about that operator or variable.


## Pip 1.2 (released 2024-03-20)

### Regex changes

- Regex flags are no longer concatenated to the pattern text itself, thanks to a change in Python 3.11 that made this approach stop working. Instead, they are attached to the pattern object and indicated in its repr by unary operators (`A-,.`) before the pattern.
- Regex flag operators now toggle their respective flags rather than simply adding them.
- The default order of the arguments to `~` and `~=` is now string first, regex second. Both operators have reversible operands, but the order can make a difference because...
- When both the string and regex arguments of `~`, `~=`, or `MR` are scalars, the regex argument is converted from a scalar to a pattern. This behavior matches the existing behavior of `LR`.

### New meta-operator

The scan meta-operator `\$` has been added. It works the same as fold `$`, but returns all the intermediate results as a list.

### New operators

- New filtering operators: `FJ` (FilterJoin) joins the filter result into a string; `FX` (FilterIndexes) passes two arguments to the filter function, an index and a value, and creates a list of *indices* that gave truthy results.
- New sorting operator: `DK` (DescendingKeyed) sorts an iterable in descending order by the return values of a key function (compare `SK`).
- New string operators: `TC` title-cases a string (capitalizing the first letter of every run of letters); `IC` initial-caps a string (capitalizing the first character).
- Rounding operators: `|<` rounds a number down (floor); `>|` rounds a number up (ceil); `RN` rounds a number to the nearest integer; and `RZ` rounds a number toward zero (down for positive numbers, up for negative numbers). The binary versions take a second argument specifying the precision level: for example, `a>|5` rounds a number up to the next multiple of 5.
- New logarithm operators: `LB` (BinaryLog) takes the log base 2; `LD` (DecimalLog) takes the log base 10.
- `BL` (BitLength) returns the bit-length of a number: the number of bits in the binary representation of its absolute value.
- `HU` (HalveUp) divides by 2 and rounds up (as compared to `HV`, which rounds down).
- `FU` (FilterUnpack) now has a unary version.

### Miscellaneous

- Thanks to a series of tweaks to the parser, blocks now always have the correct repr instead of the old "raw parse tree wrapped in curly braces" repr. (This change was also backported to version 1.1.1.)
- The `pip()` function in `pip.py` now raises a `FatalError` exception instead of calling `sys.exit(1)` and returns instead of calling `sys.exit(0)`, making things nicer for any third-party code that might want to call it.


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

