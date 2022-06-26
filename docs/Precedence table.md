---
layout: default
title: Precedence Chart
permalink: precedence
nav_order: 7
---

# Precedence chart

Each table lists operators with the same precedence, one table for each precedence level. They are ordered from lowest precedence to highest. For descriptions of each operator, see the [operator list](operators). There's also a reasonably human-readable precedence table in [operators.py](https://github.com/dloscutoff/pip/blob/master/operators.py).

### Terminology

- **Unary** operators take one operand, **binary** operators take two, and **ternary** operators take three.
- **Associativity** determines how to parse an expression containing multiple operators with the same precedence. **Left-associative** operators break the tie in favor of the leftmost subexpression: `x-y-z` is equivalent to `(x-y)-z`. **Right-associative** operators break the tie in favor of the rightmost subexpression: `x:y:z` is equivalent to `x:(y:z)`.
- **Chaining** is a third type of associativity, used for comparison operators. For example, `x<y=z` isn't equivalent to either `(x<y)=z` (left-associative) or `x<(y=z)` (right-associative) but rather to `(x<y)&(y=z)`.
- **Fold default** is the value returned when folding an empty iterable on this operator. For example, `$+[]` returns `0`, while `$*[]` returns `1`. Unary operators cannot be folded and thus do not have a default value.
- **Itemwise** indicates whether the operator applies item-by-item to Lists, both Lists and Ranges, or neither.
- **In lambda** indicates whether the operator can be applied to functions (typically starting from the identity function `_`) to build bigger functions.

## Output and yank

### Unary

Symbol | Name       | Itemwise? | In lambda?
------ | ---------- | --------- | ----------
`O`    | Output     | No        | No
`P`    | Print      | No        | No
`Y`    | Yank       | No        | No
`YO`   | Yankoutput | No        | No
`YP`   | Yankprint  | No        | No

## Assignment

### Binary (right-associative)

Symbol | Name   | Fold default | Itemwise? | In lambda?
------ | ------ | ------------ | --------- | ----------
`:`    | Assign | None         | No        | No
`::`   | Swap   | None         | No        | No

## If-then-else

### Ternary (right-associative)

Symbol | Name | Fold default | Itemwise? | In lambda?
------ | ---- | ------------ | --------- | ----------
`?`    | Ifte | None         | No        | No

## Logical or

### Binary (left-associative)

Symbol | Name | Fold default | Itemwise? | In lambda?
------ | ---- | ------------ | --------- | ----------
`|`    | Or   | `0`          | No        | No

## Logical and

### Binary (left-associative)

Symbol | Name | Fold default | Itemwise? | In lambda?
------ | ---- | ------------ | --------- | ----------
`&`    | And  | `1`          | No        | No

## Logical not

### Unary

Symbol | Name | Itemwise? | In lambda?
------ | ---- | --------- | ----------
`!`    | Not  | No        | No

## Exact equality

### Binary (left-associative)

Symbol | Name     | Fold default | Itemwise? | In lambda?
------ | -------- | ------------ | --------- | ----------
`==`   | Objequal | `1`          | No        | No

## Functional operators

### Unary

Symbol | Name      | Itemwise? | In lambda?
------ | --------- | --------- | ----------
`V`    | Eval      | No        | No
`FI`   | Filter    | No        | No
`FN`   | Filternot | No        | No
`RE`   | Recurse   | No        | No

### Binary (right-associative)

Symbol | Name            | Fold default | Itemwise? | In lambda?
------ | --------------- | ------------ | --------- | ----------
`M`    | Map             | `[]`         | No        | No
`MC`   | Mapcoords       | `[]`         | No        | No
`ME`   | Mapenumerate    | `[]`         | No        | No
`MJ`   | Mapjoin         | `""`         | No        | No
`MM`   | Mapmap          | `[]`         | No        | No
`MP`   | Mappairs        | `[]`         | No        | No
`MS`   | Mapsum          | `0`          | No        | No
`MU`   | Mapunpack       | `[]`         | No        | No
`MF`   | Mapflatten      | `[]`         | No        | No
`FI`   | Filter          | `[]`         | No        | No
`FN`   | Filternot       | `[]`         | No        | No
`FE`   | Filterenumerate | `[]`         | No        | No
`FU`   | Filterunpack    | `[]`         | No        | No
`SK`   | Sortkeyed       | `[]`         | No        | No
`V`    | Eval            | None         | No        | No

### Ternary (right-associative)

Symbol | Name     | Fold default | Itemwise? | In lambda?
------ | -------- | ------------ | --------- | ----------
`MR`   | Mapregex | `[]`         | No        | No
`MZ`   | Mapzip   | `[]`         | No        | No

## If-then-else (for lambdas)

### Ternary (right-associative)

Symbol | Name | Fold default | Itemwise? | In lambda?
------ | ---- | ------------ | --------- | ----------
`\?`   | Ifte | None         | No        | Yes

## Logical or (for lambdas)

### Binary (left-associative)

Symbol | Name | Fold default | Itemwise? | In lambda?
------ | ---- | ------------ | --------- | ----------
`\|`   | Or   | `0`          | No        | Yes

## Logical and (for lambdas)

### Binary (left-associative)

Symbol | Name | Fold default | Itemwise? | In lambda?
------ | ---- | ------------ | --------- | ----------
`\&`   | And  | `1`          | No        | Yes

## Logical not (for lambdas)

### Unary

Symbol | Name | Itemwise? | In lambda?
------ | ---- | --------- | ----------
`\!`   | Not  | No        | Yes

## Comparison operators

### Binary (chaining)

Symbol | Name         | Fold default | Itemwise? | In lambda?
------ | ------------ | ------------ | --------- | ----------
`<`    | Numless      | `1`          | No        | Yes
`>`    | Numgreater   | `1`          | No        | Yes
`=`    | Numequal     | `1`          | No        | Yes
`<=`   | Numlesseq    | `1`          | No        | Yes
`>=`   | Numgreatereq | `1`          | No        | Yes
`!=`   | Numnotequal  | `1`          | No        | Yes
`LT`   | Strless      | `1`          | No        | Yes
`GT`   | Strgreater   | `1`          | No        | Yes
`Q`    | Strequal     | `1`          | No        | Yes
`LE`   | Strlesseq    | `1`          | No        | Yes
`GE`   | Strgreatereq | `1`          | No        | Yes
`NE`   | Strnotequal  | `1`          | No        | Yes
`#=`   | Lenequal     | `1`          | No        | Yes
`#<`   | Lenless      | `1`          | No        | Yes
`#>`   | Lengreater   | `1`          | No        | Yes
`~=`   | Fullmatch    | `1`          | No        | Yes

## In and not in

### Binary (left-associative)

Symbol | Name  | Fold default | Itemwise? | In lambda?
------ | ----- | ------------ | --------- | ----------
`N`    | In    | None         | No        | Yes
`NI`   | Notin | None         | No        | Yes

## String conversion

### Unary

Symbol | Name | Itemwise? | In lambda?
------ | ---- | --------- | ----------
`RP`   | Repr | No        | No
`ST`   | Str  | No        | No

## Low-precedence list operators

### Binary (left-associative)

Symbol | Name         | Fold default | Itemwise? | In lambda?
------ | ------------ | ------------ | --------- | ----------
`CB`   | Combinations | `[]`         | No        | Yes

### Unary

Symbol   | Name            	 | Itemwise? | In lambda?
-------- | ---------------- | --------- | ----------
`M`/`MX` | Max              | No        | Yes
`N`/`MN` | Min              | No        | Yes
`RC`     | Randchoice       | No        | Yes
`SH`     | Shuffle          | No        | Yes
`SN`     | Sortnum          | No        | Yes
`SS`     | Sortstring       | No        | Yes
`DN`     | Descendingnum    | No        | Yes
`DS`     | Descendingstring | No        | Yes
`UQ`     | Unique           | No        | Yes
`EN`     | Enumerate        | No        | Yes
`PM`     | Permutations     | No        | Yes
`FL`     | Flatten          | No        | Yes
`FA`     | Flattenall       | No        | Yes

## Append, push, and pop

### Binary (left-associative)

Symbol | Name        | Fold default | Itemwise? | In lambda?
------ | ----------- | ------------ | --------- | ----------
`AE`   | Appendelem  | `[]`         | No        | Yes
`AL`   | Appendlist  | `[]`         | No        | Yes
`PE`   | Prependelem | `[]`         | No        | Yes
`PU`   | Push        | `[]`         | No        | Yes
`PB`   | Pushback    | `[]`         | No        | Yes
`PK`   | Pick        | `[]`         | No        | Yes

### Unary

Symbol | Name    | Itemwise? | In lambda?
------ | ------- | --------- | ----------
`PO`   | Pop     | No        | Yes
`DQ`   | Dequeue | No        | Yes

## High-precedence list operators

### Binary (left-associative)

Symbol | Name             | Fold default | Itemwise? | In lambda?
------ | ---------------- | ------------ | --------- | ----------
`^`    | Split            | `[]`         | Both      | Yes
`^@`   | Splitat          | `[]`         | No        | Yes
`@?`   | Find             | None         | No        | Yes
`@*`   | Findall          | `[]`         | No        | Yes
`<>`   | Group            | `[]`         | No        | <br> Yes
`CH`   | Chop             | `[]`         | No        | <br> Yes
`J`    | Join             | `""`         | No        | Yes
`JW`   | Joinwrap         | None         | No        | Yes
`RL`   | Repeatlist       | `[]`         | No        | Yes
`Z`    | Zip              | `[]`         | No        | Yes
`ZD`   | Zipdefault       | `[]`         | No        | Yes
`ZJ`   | Zipjoin          | `[]`         | No        | Yes
`H`    | Prefix           | `[]`         | No        | Yes
`S`    | Suffix           | `[]`         | No        | Yes
`WV`   | Weave            | `[]`         | No        | Yes
`UW`   | Unweave          | `[]`         | No        | Yes
`CP`   | Cartesianproduct | `[]`         | No        | Yes
`CG`   | Coordinategrid   | None         | Both      | Yes
`ZG`   | Zerogrid         | None         | Both      | Yes
`OG`   | Onegrid          | None         | Both      | Yes
`TD`   | Todigits         | `[]`         | No        | Yes
`FD`   | Fromdigits       | `[]`         | No        | Yes

### Ternary (left-associative)

Symbol | Name          | Fold default | Itemwise? | In lambda?
------ | ------------- | ------------ | --------- | ----------
`RA`   | Replaceat     | None         | No        | Yes
`TR`   | Transliterate | None         | No        | Yes

### Unary

Symbol   | Name             | Itemwise? | In lambda?
-------- | ---------------- | --------- | ----------
`^`      | Split            | Both      | Yes
`<>`     | Group            | No        | Yes
`CH`     | Chop             | No        | Yes
`J`      | Join             | No        | Yes
`R`/`RV` | Reverse          | No        | Yes
`RF`     | Reflect          | No        | Yes
`PZ`     | Palindromize     | No        | Yes
`QR`     | Quadreflect      | No        | Yes
`QP`     | Quadpalindromize | No        | Yes
`Z`      | Zip              | No        | Yes
`ZD`     | Zipdefault       | No        | Yes
`ZJ`     | Zipjoin          | No        | Yes
`H`      | Prefix           | No        | Yes
`S`      | Suffix           | No        | Yes
`WV`     | Weave            | No        | Yes
`UW`     | Unweave          | No        | Yes
`CP`     | Cartesianproduct | No        | Yes
`CG`     | Coordinategrid   | Both      | Yes
`ZG`     | Zerogrid         | Both      | Yes
`OG`     | Onegrid          | Both      | Yes
`EY`     | Identitymatrix   | Both      | Yes
`TD`     | Todigits         | No        | Yes
`FD`     | Fromdigits       | No        | Yes

## Replace

### Ternary (left-associative)

Symbol | Name    | Fold default | Itemwise? | In lambda?
------ | ------- | ------------ | --------- | ----------
`R`    | Replace | None         | No        | No

## Low-precedence string/regex operators

### Binary (left-associative)

Symbol | Name       | Fold default | Itemwise? | In lambda?
------ | ---------- | ------------ | --------- | ----------
`WR`   | Wrap       | `""`         | Yes       | Yes
`~`    | Firstmatch | `""`         | Yes       | Yes

## Concatenate

### Binary (left-associative)

Symbol | Name | Fold default | Itemwise? | In lambda?
------ | ---- | ------------ | --------- | ----------
`.`    | Cat  | `""`         | Both      | Yes

## Regex modifiers

### Unary

Symbol | Name       | Itemwise? | In lambda?
------ | ---------- | --------- | ----------
`X`    | Regex      | No        | Yes
`.`    | Dot        | List      | Yes
`K`    | Kleenestar | List      | Yes

## Remove

### Binary (left-associative)

Symbol | Name        | Fold default | Itemwise? | In lambda?
------ | ----------- | ------------ | --------- | ----------
`RM`   | Remove      | `""`         | No        | Yes
`DC`   | Deletechars | `""`         | Both      | Yes

## String repetition

### Binary (left-associative)

Symbol | Name   | Fold default | Itemwise? | In lambda?
------ | ------ | ------------ | --------- | ----------
`X`    | Strmul | `""`         | Both      | Yes

## Strip, trim, and case conversion

### Binary (left-associative)

Symbol | Name   | Fold default | Itemwise? | In lambda?
------ | ------ | ------------ | --------- | ----------
`||`   | Strip  | `""`         | List      | Yes
`|>`   | Lstrip | `""`         | List      | Yes
`<|`   | Rstrip | `""`         | List      | Yes
`TM`   | Trim   | `""`         | List      | Yes

### Unary

Symbol | Name      | Itemwise? | In lambda?
------ | --------- | --------- | ----------
`||`   | Strip     | List      | Yes
`|>`   | Lstrip    | List      | Yes
`<|`   | Rstrip    | List      | Yes
`TM`   | Trim      | List      | Yes
`LC`   | Lowercase | List      | Yes
`UC`   | Uppercase | List      | Yes
`SC`   | Swapcase  | List      | Yes

## Range and to-base

### Binary (left-associative)

Symbol | Name      | Fold default | Itemwise? | In lambda?
------ | --------- | ------------ | --------- | ----------
`,`    | Range     | None         | Both      | Yes
`\,`   | Inclrange | None         | Both      | Yes
`RR`   | Randrange | `0`          | Both      | Yes
`TB`   | Tobase    | `0`          | Both      | Yes

### Unary

Symbol | Name        | Itemwise? | In lambda?
------ | ----------- | --------- | ----------
`,`    | Rangeto     | Both      | Yes
`\,`   | Inclrangeto | Both      | Yes
`RR`   | Randrangeto | Both      | Yes
`TB`   | Tobase      | Both      | Yes

## Low-precedence numeric operators

### Binary (left-associative)

Symbol | Name       | Fold default | Itemwise? | In lambda?
------ | ---------- | ------------ | --------- | ----------
`BA`   | Bitwiseand | `-1`         | Both      | Yes
`BO`   | Bitwiseor  | `0`          | Both      | Yes
`BX`   | Bitwisexor | `0`          | Both      | Yes
`AT`   | Arctan     | None         | Both      | Yes
`CM`   | Numcmp     | `0`          | No        | Yes

### Unary

Symbol | Name       | Itemwise? | In lambda?
------ | ---------- | --------- | ----------
`BN`   | Bitwisenot | Both      | Yes
`SI`   | Sine       | Both      | Yes
`CO`   | Cosine     | Both      | Yes
`TA`   | Tangent    | Both      | Yes
`SE`   | Secant     | Both      | Yes
`CS`   | Cosec      | Both      | Yes
`CT`   | Cotan      | Both      | Yes
`AT`   | Arctan     | Both      | Yes
`RD`   | Radians    | Both      | Yes
`DG`   | Degrees    | Both      | Yes

## Addition and subtraction

### Binary (left-associative)

Symbol | Name         | Fold default | Itemwise? | In lambda?
------ | ------------ | ------------ | --------- | ----------
`+`    | Add          | `0`          | List      | Yes
`-`    | Sub          | `0`          | List      | Yes
`AD`   | Absolutediff | `0`          | Both      | Yes

## Multiplication and division

### Binary (left-associative)

Symbol | Name   | Fold default | Itemwise? | In lambda?
------ | ------ | ------------ | --------- | ----------
`*`    | Mul    | `1`          | Both      | Yes
`/`    | Div    | `1`          | Both      | Yes
`%`    | Mod    | `0`          | Both      | Yes
`//`   | Intdiv | `1`          | Both      | Yes

## High-precedence numeric operators

### Unary

Symbol   | Name        | Itemwise? | In lambda?
-------- | ----------- | --------- | ----------
`+`      | Pos         | List      | Yes
`-`      | Neg         | Both      | Yes
`/`      | Invert      | Both      | Yes
`%`      | Mod2        | Both      | Yes
`E`/`**` | Pow         | Both      | Yes
`EE`     | Poweroften  | Both      | Yes
`RT`     | Sqrt        | Both      | Yes
`SQ`     | Square      | Both      | Yes
`HV`     | Halve       | Both      | Yes
`DB`     | Double      | Both      | Yes
`EX`     | Exponential | Both      | Yes
`LN`     | Naturallog  | Both      | Yes

### Binary (right-associative)

Symbol   | Name       | Fold default | Itemwise? | In lambda?
-------- | ---------- | ------------ | --------- | ----------
`E`/`**` | Pow        | `1`          | Both      | Yes
`EE`     | Poweroften | `1`          | Both      | Yes
`RT`     | Root       | `1`          | Both      | Yes

## Very high-precedence operators

### Binary (left-associative)

Symbol | Name     | Fold default | Itemwise? | In lambda?
------ | -------- | ------------ | --------- | ----------
`FB`   | Frombase | `0`          | Both      | Yes

### Unary

Symbol | Name     | Itemwise? | In lambda?
------ | -------- | --------- | ----------
`U`    | Inc      | List      | Yes
`D`    | Dec      | List      | Yes
`#`    | Len      | No        | Yes
`A`    | Asc      | Both      | Yes
`C`    | Chr      | Both      | Yes
`AB`   | Abs      | Both      | Yes
`SG`   | Sign     | Both      | Yes
`FB`   | Frombase | Both      | Yes

## Highest-precedence operators

### Binary (left-associative)

Symbol | Name    | Fold default | Itemwise? | In lambda?
------ | ------- | ------------ | --------- | ----------
`@`    | At      | None         | No        | Yes
`@<`   | Leftof  | None         | No        | Yes
`@>`   | Rightof | None         | No        | Yes

### Unary

Symbol | Name    | Itemwise? | In lambda?
------ | ------- | --------- | ----------
`@`    | At      | No        | Yes
`@<`   | Leftof  | No        | Yes
`@>`   | Rightof | No        | Yes
`++`   | Inc     | List      | Yes
`--`   | Dec     | List      | Yes
