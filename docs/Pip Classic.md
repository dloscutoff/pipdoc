---
layout: default
title: Pip Classic
permalink: pip-classic
nav_order: 10
---

# Differences from Pip Classic

The [2018-10-25 commit](https://github.com/dloscutoff/pip/releases/tag/v0.18) of Pip is known as Pip Classic. This is the version of Pip available at [Try It Online!](https://tio.run/#pip) If you're trying to run a Pip program on TIO and something isn't working the way it should, you might be using a language feature that isn't in Pip Classic. Here is a catalog of the differences between the versions and how to work around them.

Note: "lhs" = left-hand side argument of an operator and "rhs" = right-hand side argument (including the single argument of a unary operator).

## Flags

- The `-x` flag is not supported. Evaluate the arguments explicitly: use `Va` for `a`, `V*g` for `g`, etc.

## Syntax

- The Else branch of an If statement begins with `E`, not `EL`.
- For loops do not support destructuring assignment. Switching to a functional programming approach will usually be shorter anyway: `F[ab]lPaRb'_` -> `P{aRb'_}MUl` with the appropriate list-formatting flag.
- The [Unify statement](https://github.com/dloscutoff/pip/blob/2355d3c383c69b35539c44a640a7bdc5c2dbab14/Documentation/Commands.md#unify) exists.
- Arbitrary-length variable names starting with `$` are not supported.
- There is no block comment syntax.

## Missing operators

- Unary `%`. Mod by 2 explicitly: `%a` -> `a%2`.
- Unary `**`. Raise 2 to the power explicitly: `**a` -> `2**a`.
- Unary `<>`. Group into size-2 chunks explicitly: `<>a` -> `a<>2`.
- `\?` (ternary), `\|` and `\&` (binary), and `\!` (unary). Use a curly-brace function instead of a lambda, or look for another way to express the formula: `_\|'x` -> `{a|'x}`; `\!_` -> `_=0` if the argument is guaranteed to be a number.
- `AD` (binary). Subtract and take the absolute value instead: `aADb` -> `AB(a-b)`.
- `D` (unary). Use `--` instead, but note the slight difference in precedence: `Da` -> `--a`; `Da@<2` -> `--(a@<2)`.
- `E` (unary and binary). Use `**` instead: `Ea` -> `2**a`; `aEb` -> `a**b`.
- `EE` (unary and binary). Use the full formula instead: `EEa` -> `10**a`; `aEEb` -> `a*10**b`.
- `FD` (unary and binary). Use `FB` or roll your own base-conversion: `aFDb` -> `$+a*b**RV,#a`, or `(Ja)FBb` if `b` is 36 or less and all digits are less than 10.
- Unary `FI`. Filter by the identity function instead: `FIa` -> `_FIa`.
- `OG` (unary and binary). Use one of `ZG`, `MC`, or `CG` instead: `OGa` -> `1+ZGa` or `1MCa`; `aOGb` -> `1+(aZGb)` or `1MMaCGb`.
- `RE` (unary). Use an explicit function call instead: `REa` -> `(fa)`.
- Unary `R`. Use `RV` instead: `Ra` -> `RVa`.
- `SQ` (unary). Multiply the number by itself or use `**` instead: `SQa` -> `a*a` or `a**2`.
- `TD` (unary and binary). Use `TB` or roll your own base-conversion: `aTDb` -> `^aTBb` if `b` is 10 or less.
- `U` (unary). Use `++` instead, but note the slight difference in precedence: `Ua` -> `++a`; `Ua@<2` -> `++(a@<2)`.

## Operators with different behavior

- Unary `#`, `A`, `AB`, `C`, `FB`, and `SG` have higher precedence than binary `@`, `@>`, and `@<`. Use parentheses or another precedence-manipulation strategy as needed: `A*s@<3` -> `A*(s@<3)` or `A*Ys@<3`; `#l@1` -> `#(l1)`
- `:` does not support destructuring assignment. For simple cases, use the `U` statement: `[xyz]:a` -> `UxyzWa`. More-complex cases may need to use a series of assignments and/or unifications: `C:[xyz]` -> `C:xC:yC:z`; `[[wx][yz]]:a` -> `UwxW@aUyzWa@1`.
- Numeric and string equality operators (`=`, `<=`, `>=`, `Q`, `LE`, and `GE`) always return falsey when their arguments are not comparable, rather than returning truthy if the arguments are identical. (In particular, nil is not equal to nil, and a Pattern is not equal to itself under numeric comparison.) If this becomes a problem, you can explicitly check for exact equality first: `a<=b` -> `a==b|a<=b`.
- `<>` does not work with a negative rhs. To group from right to left, use `RV` twice: `a<>-4` -> `RV*(RVa<>4)`.
- `<>` does not accept a List or Range as rhs. To return a list of different groupings, map a lambda function: `a<>[2 4]` -> `a<>_M[2 4]`.
- `MC` does not accept a height/width List as rhs. Use binary `CG` with `MM` instead, but note that `MM` does not unpack the coordinate pairs: `_.s.BMC[ab]` -> `_@0.s._@1MMaCGb`.
- `N` and `NI` do not accept a List/Range lhs with a Scalar rhs. Map a lambda function instead: `[1 2 4]Na` -> `_NaM[1 2 4]`.

## Missing variables

(These still act as variables, but their initial values are nil rather than the useful values they have in current Pip.)

- `p`: use `"()"` instead.
- `G`: use `{g}` instead, or rework your lambda function using `_` and `B` if possible: `2*$+G` -> `{2*$+g}` or `2*$+{g}` or, if you know there will always be two arguments, `2*_+2*B`.

## Bugs

- Using `<>` with a rhs of 0 or a negative number results in an infinite loop. Only use `<>` with positive rhs. See above for how to group from right to left.
- A Scalar with leading whitespace in a numeric context evaluates to `0`, rather than ignoring the whitespace. If leading whitespace is a possibility, strip it explicitly using `|>`.
- A non-integer rhs to `\,` crashes the interpreter. Only use `\,` with integer rhs. If a non-integer rhs is a possibility, int-divide it by 1 to truncate it to an integer.
- Using `A` with a Scalar rhs matching the regex `0+(\.0+)?` results in nil rather than 48. Concatenating space or some other character to the end of the Scalar is one possible workaround.
- `<` returns 1 when given two Lists that are equal. Swap the arguments and use `>` instead.
- `#` and the length-comparison operators crash the interpreter when given infinite Ranges. Try to avoid taking the length of infinite Ranges. If you need to test the upper bound of a Range, use `MX`.
- Iterating over an infinite Range with a lower bound of nil crashes the interpreter. Use a lower bound of 0 instead.
- Indexing into an empty iterable and then attempting to assign a value to that expression crashes the interpreter. Make sure iterables are nonempty before attempting to assign to their items.
