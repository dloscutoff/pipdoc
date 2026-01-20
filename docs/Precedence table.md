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
- **Associativity** determines how to parse an expression containing multiple operators with the same precedence. **Left-associative** operators break the tie in favor of the leftmost subexpression: `x-y-z` is equivalent to `(x-y)-z`. **Right-associative** operators break the tie in favor of the rightmost subexpression: `x:y:z` is equivalent to `x:(y:z)`. Unary operators do not have an associativity.
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
`YO`   | YankOutput | No        | No
`YP`   | YankPrint  | No        | No

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
`==`   | ObjEqual | `1`          | No        | No

## Functional operators

### Unary

Symbol | Name          | Itemwise? | In lambda?
------ | ------------- | --------- | ----------
`V`    | Eval          | No        | No
`FI`   | Filter        | No        | No
`FN`   | FilterNot     | No        | No
`FU`   | FilterUnpack  | No        | No
`FX`   | FilterIndexes | No        | No
`FJ`   | FilterJoin    | No        | No
`FF`   | FilterFlatten | No        | No
`FQ`   | FilterUnique  | No        | No
`RE`   | Recurse       | No        | No

### Binary (right-associative)

Symbol | Name            | Fold default | Itemwise? | In lambda?
------ | --------------- | ------------ | --------- | ----------
`M`    | Map             | `[]`         | No        | No
`MC`   | MapCoords       | `[]`         | No        | No
`ME`   | MapEnumerate    | `[]`         | No        | No
`MJ`   | MapJoin         | `""`         | No        | No
`MM`   | MapMap          | `[]`         | No        | No
`MP`   | MapPairs        | `[]`         | No        | No
`MS`   | MapSum          | `0`          | No        | No
`MU`   | MapUnpack       | `[]`         | No        | No
`MF`   | MapFlatten      | `[]`         | No        | No
`MQ`   | MapUnique       | `[]`         | No        | No
`FI`   | Filter          | `[]`         | No        | No
`FN`   | FilterNot       | `[]`         | No        | No
`FE`   | FilterEnumerate | `[]`         | No        | No
`FU`   | FilterUnpack    | `[]`         | No        | No
`FX`   | FilterIndexes   | `[]`         | No        | No
`FJ`   | FilterJoin      | `[]`         | No        | No
`FF`   | FilterFlatten   | `[]`         | No        | No
`FQ`   | FilterUnique    | `[]`         | No        | No
`SK`   | SortKeyed       | `[]`         | No        | No
`DK`   | DescendingKeyed | `[]`         | No        | No
`MK`   | MaxKeyed        | `[]`         | No        | No
`NK`   | MinKeyed        | `[]`         | No        | No
`V`    | Eval            | None         | No        | No

### Ternary (right-associative)

Symbol | Name     | Fold default | Itemwise? | In lambda?
------ | -------- | ------------ | --------- | ----------
`MR`   | MapRegex | `[]`         | No        | No
`MZ`   | MapZip   | `[]`         | No        | No

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
`<`    | NumLess      | `1`          | No        | Yes
`>`    | NumGreater   | `1`          | No        | Yes
`=`    | NumEqual     | `1`          | No        | Yes
`<=`   | NumLessEq    | `1`          | No        | Yes
`>=`   | NumGreaterEq | `1`          | No        | Yes
`!=`   | NumNotEqual  | `1`          | No        | Yes
`LT`   | StrLess      | `1`          | No        | Yes
`GT`   | StrGreater   | `1`          | No        | Yes
`Q`    | StrEqual     | `1`          | No        | Yes
`LE`   | StrLessEq    | `1`          | No        | Yes
`GE`   | StrGreaterEq | `1`          | No        | Yes
`NE`   | StrNotEqual  | `1`          | No        | Yes
`#=`   | LenEqual     | `1`          | No        | Yes
`#<`   | LenLess      | `1`          | No        | Yes
`#>`   | LenGreater   | `1`          | No        | Yes
`~=`   | FullMatch    | `1`          | No        | Yes

## In and not in

### Binary (left-associative)

Symbol | Name  | Fold default | Itemwise? | In lambda?
------ | ----- | ------------ | --------- | ----------
`N`    | In    | None         | No        | Yes
`NI`   | NotIn | None         | No        | Yes

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
`RC`     | RandChoice       | No        | Yes
`SH`     | Shuffle          | No        | Yes
`SN`     | SortNum          | No        | Yes
`SS`     | SortString       | No        | Yes
`DN`     | DescendingNum    | No        | Yes
`DS`     | DescendingString | No        | Yes
`UQ`     | Unique           | No        | Yes
`EN`     | Enumerate        | No        | Yes
`PM`     | Permutations     | No        | Yes
`FL`     | Flatten          | No        | Yes
`FA`     | FlattenAll       | No        | Yes

## Append, push, and pop

### Binary (left-associative)

Symbol | Name        | Fold default | Itemwise? | In lambda?
------ | ----------- | ------------ | --------- | ----------
`AE`   | AppendElem  | `[]`         | No        | Yes
`AL`   | AppendList  | `[]`         | No        | Yes
`PE`   | PrependElem | `[]`         | No        | Yes
`PU`   | Push        | `[]`         | No        | Yes
`PB`   | PushBack    | `[]`         | No        | Yes
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
`^@`   | SplitAt          | `[]`         | No        | Yes
`@?`   | Find             | None         | No        | Yes
`@*`   | FindAll          | `[]`         | No        | Yes
`<>`   | Group            | `[]`         | No        | <br> Yes
`CH`   | Chop             | `[]`         | No        | <br> Yes
`J`    | Join             | `""`         | No        | Yes
`JW`   | JoinWrap         | None         | No        | Yes
`RL`   | RepeatList       | `[]`         | No        | Yes
`Z`    | Zip              | `[]`         | No        | Yes
`ZD`   | ZipDefault       | `[]`         | No        | Yes
`ZJ`   | ZipJoin          | `[]`         | No        | Yes
`H`    | Prefix           | `[]`         | No        | Yes
`S`    | Suffix           | `[]`         | No        | Yes
`WV`   | Weave            | `[]`         | No        | Yes
`UW`   | Unweave          | `[]`         | No        | Yes
`CP`   | CartesianProduct | `[]`         | No        | Yes
`CG`   | CoordinateGrid   | None         | Both      | Yes
`ZG`   | ZeroGrid         | None         | Both      | Yes
`OG`   | OneGrid          | None         | Both      | Yes
`TD`   | ToDigits         | `[]`         | No        | Yes
`FD`   | FromDigits       | `[]`         | No        | Yes

### Ternary (left-associative)

Symbol | Name          | Fold default | Itemwise? | In lambda?
------ | ------------- | ------------ | --------- | ----------
`RA`   | ReplaceAt     | None         | No        | Yes
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
`QR`     | QuadReflect      | No        | Yes
`QP`     | QuadPalindromize | No        | Yes
`Z`      | Zip              | No        | Yes
`ZD`     | ZipDefault       | No        | Yes
`ZJ`     | ZipJoin          | No        | Yes
`H`      | Prefix           | No        | Yes
`S`      | Suffix           | No        | Yes
`WV`     | Weave            | No        | Yes
`UW`     | Unweave          | No        | Yes
`CP`     | CartesianProduct | No        | Yes
`CG`     | CoordinateGrid   | Both      | Yes
`ZG`     | ZeroGrid         | Both      | Yes
`OG`     | OneGrid          | Both      | Yes
`EY`     | IdentityMatrix   | Both      | Yes
`TD`     | ToDigits         | No        | Yes
`FD`     | FromDigits       | No        | Yes

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
`~`    | FirstMatch | `""`         | Yes       | Yes

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
`K`    | KleeneStar | List      | Yes

## Remove

### Binary (left-associative)

Symbol | Name        | Fold default | Itemwise? | In lambda?
------ | ----------- | ------------ | --------- | ----------
`RM`   | Remove      | `""`         | No        | Yes
`DC`   | DeleteChars | `""`         | Both      | Yes

## String repetition

### Binary (left-associative)

Symbol | Name   | Fold default | Itemwise? | In lambda?
------ | ------ | ------------ | --------- | ----------
`X`    | StrMul | `""`         | Both      | Yes

## Strip, trim, and case conversion

### Binary (left-associative)

Symbol | Name   | Fold default | Itemwise? | In lambda?
------ | ------ | ------------ | --------- | ----------
`||`   | Strip  | `""`         | List      | Yes
`|>`   | LStrip | `""`         | List      | Yes
`<|`   | RStrip | `""`         | List      | Yes
`TM`   | Trim   | `""`         | List      | Yes

### Unary

Symbol | Name        | Itemwise? | In lambda?
------ | ----------- | --------- | ----------
`||`   | Strip       | List      | Yes
`|>`   | LStrip      | List      | Yes
`<|`   | RStrip      | List      | Yes
`TM`   | Trim        | List      | Yes
`LC`   | Lowercase   | List      | Yes
`UC`   | Uppercase   | List      | Yes
`SC`   | Swapcase    | List      | Yes
`TC`   | Titlecase   | List      | Yes
`IC`   | InitialCaps | List      | Yes

## Range and to-base

### Binary (left-associative)

Symbol | Name      | Fold default | Itemwise? | In lambda?
------ | --------- | ------------ | --------- | ----------
`,`    | Range     | None         | Both      | Yes
`\,`   | InclRange | None         | Both      | Yes
`RR`   | RandRange | `0`          | Both      | Yes
`TB`   | ToBase    | `0`          | Both      | Yes

### Unary

Symbol | Name        | Itemwise? | In lambda?
------ | ----------- | --------- | ----------
`,`    | RangeTo     | Both      | Yes
`\,`   | InclRangeTo | Both      | Yes
`RR`   | RandRangeTo | Both      | Yes
`TB`   | ToBase      | Both      | Yes
`TH`   | ToHex       | Both      | Yes

## Low-precedence numeric operators

### Binary (left-associative)

Symbol | Name         | Fold default | Itemwise? | In lambda?
------ | ------------ | ------------ | --------- | ----------
`BA`   | BitwiseAnd   | `-1`         | Both      | Yes
`BO`   | BitwiseOr    | `0`          | Both      | Yes
`BX`   | BitwiseXor   | `0`          | Both      | Yes
`AT`   | Arctan       | None         | Both      | Yes
`CM`   | NumCmp       | `0`          | No        | Yes
`|<`   | Floor        | `0`          | Both      | Yes
`>|`   | Ceil         | `0`          | Both      | Yes
`RN`   | RoundNearest | `0`          | Both      | Yes
`RZ`   | RoundZero    | `0`          | Both      | Yes

### Unary

Symbol | Name         | Itemwise? | In lambda?
------ | ------------ | --------- | ----------
`BN`   | BitwiseNot   | Both      | Yes
`SI`   | Sine         | Both      | Yes
`CO`   | Cosine       | Both      | Yes
`TA`   | Tangent      | Both      | Yes
`SE`   | Secant       | Both      | Yes
`CS`   | Cosec        | Both      | Yes
`CT`   | Cotan        | Both      | Yes
`AT`   | Arctan       | Both      | Yes
`RD`   | Radians      | Both      | Yes
`DG`   | Degrees      | Both      | Yes
`BL`   | BitLength    | Both      | Yes
`|<`   | Floor        | Both      | Yes
`>|`   | Ceil         | Both      | Yes
`RN`   | RoundNearest | Both      | Yes
`RZ`   | RoundZero    | Both      | Yes

## Addition and subtraction

### Binary (left-associative)

Symbol | Name         | Fold default | Itemwise? | In lambda?
------ | ------------ | ------------ | --------- | ----------
`+`    | Add          | `0`          | List      | Yes
`-`    | Sub          | `0`          | List      | Yes
`AD`   | AbsoluteDiff | `0`          | Both      | Yes

## Multiplication and division

### Binary (left-associative)

Symbol | Name   | Fold default | Itemwise? | In lambda?
------ | ------ | ------------ | --------- | ----------
`*`    | Mul    | `1`          | Both      | Yes
`/`    | Div    | `1`          | Both      | Yes
`%`    | Mod    | `0`          | Both      | Yes
`//`   | IntDiv | `1`          | Both      | Yes

## High-precedence numeric operators

### Unary

Symbol   | Name        | Itemwise? | In lambda?
-------- | ----------- | --------- | ----------
`+`      | Pos         | List      | Yes
`-`      | Neg         | Both      | Yes
`/`      | Invert      | Both      | Yes
`%`      | Mod2        | Both      | Yes
`E`/`**` | Pow         | Both      | Yes
`EE`     | PowerOfTen  | Both      | Yes
`RT`     | Sqrt        | Both      | Yes
`SQ`     | Square      | Both      | Yes
`HV`     | Halve       | Both      | Yes
`HU`     | HalveUp     | Both      | Yes
`DB`     | Double      | Both      | Yes
`EX`     | Exponential | Both      | Yes
`LN`     | NaturalLog  | Both      | Yes
`LB`     | BinaryLog   | Both      | Yes
`LD`     | DecimalLog  | Both      | Yes

### Binary (right-associative)

Symbol   | Name       | Fold default | Itemwise? | In lambda?
-------- | ---------- | ------------ | --------- | ----------
`E`/`**` | Pow        | `1`          | Both      | Yes
`EE`     | PowerOfTen | `1`          | Both      | Yes
`RT`     | Root       | `1`          | Both      | Yes

## Very high-precedence operators

### Binary (left-associative)

Symbol | Name     | Fold default | Itemwise? | In lambda?
------ | -------- | ------------ | --------- | ----------
`FB`   | FromBase | `0`          | Both      | Yes

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
`FB`   | FromBase | Both      | Yes
`FH`   | FromHex  | Both      | Yes

## Highest-precedence operators

### Binary (left-associative)

Symbol | Name    | Fold default | Itemwise? | In lambda?
------ | ------- | ------------ | --------- | ----------
`@`    | At      | None         | No        | Yes
`@<`   | LeftOf  | None         | No        | Yes
`@>`   | RightOf | None         | No        | Yes

### Unary

Symbol | Name    | Itemwise? | In lambda?
------ | ------- | --------- | ----------
`@`    | At      | No        | Yes
`@<`   | LeftOf  | No        | Yes
`@>`   | RightOf | No        | Yes
`++`   | Inc     | List      | Yes
`--`   | Dec     | List      | Yes
