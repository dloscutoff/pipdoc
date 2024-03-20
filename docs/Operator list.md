---
layout: default
title: List of Operators
permalink: operators
nav_order: 6
---

# List of operators

Operators are listed in ASCII order. See also the [operator precedence chart](precedence).

### Meta-operators

The following operators change the way other operators are used, when applied on them.

`$` Fold, `\$` Scan: occur before a binary operator; the resulting compound operator is unary, with the same precedence as the original binary operator

`*` Map: occurs after a unary operator; arity and precedence remain the same

`:` Modify-assign: occurs after a unary, binary, or ternary operator; the resulting compound operator has the same arity but is right-associative and has the same precedence as `:`

### Operators

<code>!a</code> Logical not

<code>a!=b</code> Numeric not equal

<code>#a</code> Length

<code>a#&lt;b</code> Length less than

<code>a#=b</code> Length equal

<code>a#>b</code> Length greater than

<code>a%b</code> Modulo

<code>%a</code> Modulo 2

<code>a&b</code> Logical and (short-circuiting)

<code>a&ast;b</code> Multiplication; if one operand is a Pattern, regex repetition

<code>a&ast;&ast;b</code> Alias for [binary `E`](#pow)

<code>&ast;&ast;a</code> Alias for [unary `E`](#pow-of-2)

<code>a+b</code> Addition; if both operands are Patterns, regex concatenation

<code>+a</code> Cast Scalar as number; with Pattern, repeat regex 1 or more times

<code>++a</code> Increment (always comes before operand, never `a++`); higher-precedence version of [`U`](#inc)

<code>a,b</code> Range; if both operands are Patterns, regex alternation

<code>,a</code> Range from 0 up to; set multiline flag on Pattern

<code>a-b</code> Subtraction

<code>-a</code> Numeric negation; set case-insensitive flag on Pattern

<code>--a</code> Decrement (always comes before operand, never `a--`); higher-precedence version of [`D`](#dec)

<code>a.b</code> Concatenation

<code>.a</code> Set dotall flag on Pattern; no-op on other data types

<code>a/b</code> Division

<code>/a</code> Reciprocal

<code>a//b</code> Integer division

<code>a:b</code> Assign `b` to `a`; if `a` is a list of lvalues, pair them with values from `b` and assign one by one (destructuring assignment)

<code>a::b</code> Swap values of `a` and `b` (supports destructuring assignment); expression evaluates to (new value of) `a`

<code>a&lt;b</code> Numeric less than

<code>a&lt;=b</code> Numeric less than or equal

<code>a&lt;>b</code> Group iterable `a` into sections of length `b`; with negative `b`, groups right-to-left

<code>&lt;>a</code> Group iterable `a` into sections of length 2

<code>a&lt;|b</code> Strip characters in `b` from right of `a`

<code>&lt;|a</code> Strip whitespace from right of `a`

<code>a=b</code> Numeric equal

<code>a==b</code> Exactly equal

<code>a>b</code> Numeric greater than

<code>a>=b</code> Numeric greater than or equal

<code>a>|b</code> Round `a` up to smallest multiple of `b` that is >= `a`

<code>>|a</code> Round `a` up to smallest integer that is >= `a` (ceil)

<code>a?bc</code> Ternary If operator (short-circuiting)

<code>a@b</code> Get item/slice at index

<code>@a</code> Get item at index 0

<code>a@&ast;b</code> Find all indices of item `b` in `a` (find Scalar in Range, Pattern match or Scalar substring in Scalar, or any type in List)

<code>a@&lt;b</code> Slice of iterable left of index `b`

<code>@&lt;a</code> Slice of iterable left of index -1 (i.e. all but the last item)

<code>a@>b</code> Slice of iterable right of index `b`

<code>@>a</code> Slice of iterable right of index 0 (i.e. all but the first item)

<code>a@?b</code> Find first index of item `b` in `a` (find Scalar in Range, Pattern match or Scalar substring in Scalar, or any type in List)

<code>Aa</code> Convert first char of Scalar to ASCII value (or Unicode point); set ASCII-only flag on Pattern

<code>ABa</code> Absolute value of number

<code>aADb</code> Absolute difference (i.e. absolute value of the difference) of two numbers

<code>aAEb</code> List `a` with element `b` appended

<code>aALb</code> List `a` with List `b` appended

<code>aATb</code> Arctan2 (with `a` being the y-coordinate and `b` being the x-coordinate)

<code>ATa</code> Arctangent

<code>aBAb</code> Bitwise and

<code>BLa</code> Bitlength

<code>aBNb</code> Bitwise not

<code>aBOb</code> Bitwise or

<code>aBXb</code> Bitwise xor

<code>Ca</code> Convert ASCII value/Unicode point to character

<code>aCBb</code> List of all combinations of `b` elements from iterable `a`

<code>aCGb</code> Coordinate grid of `a` rows by `b` columns (`[0 0]` to `[a b]`)

<code>CGa</code> Coordinate grid of `a` rows by `a` columns (`[0 0]` to `[a a]`)

<code>aCHb</code> Chop iterable `a` into `b` pieces of roughly equal length

<code>CHa</code> Chop iterable `a` into 2 pieces of roughly equal length

<code>aCMb</code> Numeric comparison (-1 if `a < b`, 0 if `a = b`, 1 if `a > b`)

<code>COa</code> Cosine

<code>aCPb</code> Cartesian product of two iterables

<code>CPa</code> Cartesian product of a List of iterables

<code>CSa</code> Cosecant

<code>CTa</code> Cotangent

<code id="dec">Da</code> Decrement (modifying argument in-place)

<code>DBa</code> Double: `a` times 2

<code>aDCb</code> Delete all occurrences of characters in Scalar `b` from Scalar `a`

<code>DGa</code> Convert radians to degrees

<code>aDKb</code> Sort iterable `b` in descending order using Block `a` as key function

<code>DQa</code> Dequeue item from back of iterable (modifying argument in-place)

<code>DNa</code> Sort iterable in descending order using numeric comparison

<code>DSa</code> Sort iterable in descending order using string comparison

<code id="pow">aEb</code> Exponentiation

<code id="pow-of-2">Ea</code> Exponentiation with base 2

<code>aEEb</code> E notation: `a` times 10 to the power of `b`

<code>EEa</code> Unary E notation: 10 to the power of `a`

<code>ENa</code> Enumerate an iterable (gives List of `[index item]` Lists)

<code>EXa</code> Exponential (base *e*)

<code>EYa</code> Identity matrix (abbreviation from Matlab's eye() function)

<code>FAa</code> Flatten all levels of List/Range `a`, resulting in a flat List

<code>aFBb</code> Convert number from given base to decimal integer

<code>FBa</code> Convert number from binary to decimal integer

<code>aFDb</code> Convert iterable containing digits in given base to decimal integer

<code>FDa</code> Convert iterable containing digits in binary to decimal integer

<code>aFEb</code> Filter-enumerate: keep items from iterable `b` which return truthy results when function `a` is called with the index and the item as arguments

<code>aFIb</code> Filter: keep items from iterable `b` which return truthy results when passed to function `a`

<code>FIa</code> Unary filter: keep items from iterable `a` which are truthy

<code>aFJb</code> Filter iterable `b` by Block `a` and join results into Scalar

<code>FJa</code> Keep items from iterable `a` which are truthy and join results into Scalar

<code>FLa</code> Flatten one level of List/Range `a` (equivalent to `$AL`)

<code>aFNb</code> Filter negated: keep items from iterable `b` which return falsey results when passed to function `a`

<code>FNa</code> Unary filter negated: keep items from iterable `a` which are falsey

<code>aFUb</code> Filter-unpack: keep items from iterable `b` which return truthy results when function `a` is called with the item unpacked into zero or more function arguments

<code>aFXb</code> Filter indexes: List of indexes into iterable `b` which return truthy results when function `a` is called with the index and the item as arguments

<code>FXa</code> Unary filter indexes: List of indexes of truthy items in iterable `a`

<code>aGTb</code> String greater than

<code>aGEb</code> String greater than or equal

<code>aHb</code> Get prefix of `a` that is `b` elements long (mnemonic: **H**ead); with negative `b`, get prefix of length len(`a`)+`b`

<code>Ha</code> Get prefix of `a` containing all but the last element of `a`

<code>HUa</code> Halve up: `a` divided by 2 and rounded up

<code>HVa</code> Halve: `a` divided by 2 and rounded down

<code>ICa</code> Convert to initial caps (capitalize the first character: `aB Cd` -> `Ab cd`)

<code>aJb</code> Join iterable on separator

<code>Ja</code> Join iterable on empty string

<code>aJWb</code> Join iterable on separator and wrap result in separator as well

<code>Ka</code> Apply Kleene star (repeat 0 or more times) to a Pattern

<code>LBa</code> Binary logarithm (log base 2)

<code>LCa</code> Convert to lowercase (`aB Cd` -> `ab cd`)

<code>LDa</code> Decimal logarithm (log base 10)

<code>aLEb</code> String less than or equal

<code>LNa</code> Natural logarithm (log base e)

<code>aLTb</code> String less than

<code>aMb</code> Map Block `a` to iterable `b`, returning List

<code id="max">Ma</code> Maximum of iterable, using numeric comparison

<code>aMCb</code> Map Block `a` to each x,y in `b`x`b` grid of coordinate pairs; if `b` is a two-element Range or List of Scalars, map to `b@0`x`b@1` grid

<code>aMEb</code> Map Block `a` to index/value pairs for items in iterable `b`, returning List

<code>aMFb</code> Map Block `a` to iterable `b` and flatten results by one level

<code>aMJb</code> Map Block `a` to iterable `b` and join results into Scalar

<code>aMMb</code> Map Block `a` to each subitem of iterable `b`, returning List of Lists

<code>MNa</code> Alias for [unary `N`](#min)

<code>aMPb</code> Map Block `a` to consecutive pairs of items from iterable `b`, returning List

<code>aMRbc</code> Map Block `a` to each regex match of Pattern `b` in Scalar `c` (operands are rearrangeable)

<code>aMSb</code> Map Block `a` to iterable `b` and sum results

<code>aMUb</code> Map Block `a` to iterable `b`, unpacking each item as function arguments (like Python's `itertools.starmap`); returns List

<code>MXa</code> Alias for [unary `M`](#max)

<code>aMZbc</code> Map Block `a` to two iterables, passing zipped pairs of elements as arguments; returns List

<code id="in">aNb</code> In (returns count of occurrences or 0 if none)

<code id="min">Na</code> Minimum of iterable, using numeric comparison

<code>aNEb</code> String not equal

<code>aNIb</code> Not in (returns truth value 0 or 1)

<code>Oa</code> Output value and pass through unchanged (same as `P` but without trailing newline)

<code>aOGb</code> Grid of ones (`a` rows by `b` columns)

<code>OGa</code> Grid of ones (`a` rows by `a` columns)

<code>Pa</code> Print value with newline and pass through unchanged (output format for Lists depends on command-line flags; nil gives no output and also suppresses trailing newline)

<code>aPBb</code> Push item to back of iterable (modifying argument in-place)

<code>aPEb</code> List `a` with element `b` prepended

<code>PMa</code> List of all permutations of iterable

<code>aPKb</code> Pick out item from index `b` of iterable `a` (modifying `a` in-place)

<code>POa</code> Pop item from front of iterable (modifying argument in-place)

<code>aPUb</code> Push item to front of iterable (modifying argument in-place)

<code>PZa</code> Palindromize iterable, appending its reverse but without repeating the central item

<code id="stringequal">aQb</code> String equal

<code>QPa</code> Quad-palindromize iterable, palindromizing it and also each of its items

<code>QRa</code> Quad-reflect iterable, reflecting it and also each of its items

<code>aRbc</code> Replace each occurrence in Scalar `a` of substring or Pattern `b` with replacement `c`

<code id="reverse">Ra</code> Reverse

<code>aRAbc</code> Replace item in iterable `a` at index `b` with replacement `c`

<code>RCa</code> Uniformly random choice of single item from iterable

<code>RDa</code> Convert degrees to radians

<code>REa</code> Call the current function recursively with argument `a`

<code>RFa</code> Reflect iterable, appending its reverse

<code>aRLb</code> Repeat List `a` `b` times

<code>aRMb</code> Remove occurrences of `b` from `a` (removes items from List or Range; removes substrings or regex matches from Scalar)

<code>aRNb</code> Round `a` to nearest multiple of `b`

<code>RNa</code> Round `a` to nearest integer

<code>RPa</code> Like Python's `repr`: convert to an unambiguous string representation (numeric Scalar becomes `123.45`; non-numeric Scalar becomes `"abc"`; Pattern becomes `` `abc` ``; Range becomes `(1,4)`; List becomes `[1;2;"three"]`; Nil becomes `()`)

<code>aRRb</code> Random integer in range from `a` to `b`

<code>RRa</code> Random integer in range from 0 to `a`

<code>aRTb</code> `a`th root of `b`

<code>RTa</code> Square root of `a`

<code>RVa</code> Alias for [unary `R`](#reverse)

<code>aRZb</code> Round `a` to next multiple of `b` closer to zero

<code>RZa</code> Round `a` to next integer closer to zero (truncate)

<code>aSb</code> Get suffix of `a` that is `b` elements long; with negative `b`, get suffix of length len(`a`)+`b`

<code>Sa</code> Get suffix of `a` containing all but the first element of `a`

<code>SCa</code> Swap case: `Hello, World!` becomes `hELLO, wORLD!`

<code>SEa</code> Secant

<code>SGa</code> Sign of number (-1, 0, or 1)

<code>SHa</code> Shuffle: random permutation of iterable

<code>SIa</code> Sine

<code>aSKb</code> Sort iterable `b` using Block `a` as key function

<code>SNa</code> Sort iterable in ascending order using numeric comparison

<code>SQa</code> `a` squared

<code>SSa</code> Sort iterable in ascending order using string comparison

<code>STa</code> Convert to string (for Lists, the format of the result depends on command-line flags)

<code>TAa</code> Tangent

<code>aTBb</code> Convert decimal integer `a` to base `b`

<code>TBa</code> Convert decimal integer `a` to binary

<code>TCa</code> Convert to title case (`aB Cd` -> `Ab Cd`)

<code>aTDb</code> Convert decimal integer `a` to list of digits in base `b`

<code>TDa</code> Convert decimal integer `a` to list of digits in binary

<code>aTMb</code> Trim Scalar `a` by `b` characters from front and end (Scalar `b` trims same amount on both sides; Range `b` trims different amounts)

<code>TMa</code> Trim first and last characters from Scalar `a`

<code>aTRbc</code> Transliterate `a` from characters in `b` to those in `c` (with `b` or `c` Scalar, transliterates one letter to another; with `b` or `c` Range or List of numbers, translates character codes)

<code id="inc">Ua</code> Increment (modifying argument in-place)

<code>UCa</code> Convert to uppercase (`aB Cd` -> `AB CD`)

<code>UQa</code> Keep only unique values from iterable

<code>aUWb</code> Unweave iterable `a` into a List of `b` strands

<code>UWa</code> Unweave iterable `a` into a List of two strands

<code>aVb</code> Call Block as function with arglist (equivalent to `a(*b)` in Python)

<code>Va</code> Evaluate Block in current context, returning value of final expression or nil if there isn't one

<code>aWRb</code> Wrap Scalar or Pattern with a delimiter

<code>aWVb</code> Weave two iterables together, alternating their items

<code>WVa</code> Weave all subitems in an iterable together

<code>aXb</code> Repeat Scalar `a` `b` times

<code>Xa</code> Covert Scalar or List/Range to equivalent regex Pattern (escaping special characters as necessary)

<code>Ya</code> Yank value into the variable `y` (equivalent to `(y:a)`)

<code>YOa</code> Output value, then yank it (equivalent to `(y:Oa)`)

<code>YPa</code> Print value, then yank it (equivalent to `(y:Pa)`)

<code>aZb</code> Zip two Lists together (clipping to the shorter length)

<code>Za</code> Zip a List of Lists together (clipping to the shortest length)

<code>aZDb</code> Zip a List of Lists together, filling missing values with default value `b`

<code>ZDa</code> Zip a List of Lists together, filling missing values with default value `""`

<code>aZGb</code> Grid of zeros (`a` rows by `b` columns)

<code>ZGa</code> Grid of zeros (`a` rows by `a` columns)

<code>aZJb</code> Zip two iterables together, filling missing values with `" "`, and join each pair of values into a string

<code>ZJa</code> Zip a List of iterables together, filling missing values with `" "`, and join each group of values into a string

<code>\!a</code> Logical not (can be used in lambda expressions)

<code>a\&b</code> Logical and (non-short-circuiting, can be used in lambda expressions)

<code>a\,b</code> Inclusive range

<code>\,a</code> Inclusive range from 1

<code>a\?bc</code> If-then-else operator (non-short-circuiting, can be used in lambda expressions)

<code>a\|b</code> Logical or (non-short-circuiting, can be used in lambda expressions)

<code>a^b</code> Split Scalar `a` on separator `b`

<code>^a</code> Split Scalar `a` into List of characters

<code>a^@b</code> Split iterable `a` at index or List of indices `b`

<code>a|b</code> Logical or (short-circuiting)

<code>a|&lt;b</code> Round `a` down to largest multiple of `b` that is &lt;= `a`

<code>|&lt;a</code> Round `a` down to largest integer that is &lt;= `a` (floor)

<code>a|>b</code> Strip characters in `b` from left of `a`

<code>|>a</code> Strip whitespace from left of `a`

<code>a||b</code> Strip characters in `b` from `a`

<code>||a</code> Strip whitespace from `a`

<code>a~b</code> Find first regex match of `b` in Scalar `a` (reversible)

<code>a~=b</code> Test if Pattern `b` fully matches Scalar `a` (reversible)
