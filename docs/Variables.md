---
layout: default
title: Variables
permalink: vars
nav_order: 4
---

# Variables

There are four kinds of variables in Pip:

- *Local variables* have different bindings at each scope level. Only their values at the current scope are accessible.
- *Global variables* have the same bindings anywhere in a Pip program. Many of them have useful initial values.
- *Special variables* have side effects when accessed and/or assigned.
- *Regex match variables* can be accessed normally, but they are automatically set each time a regex match is completed. See also the section on [regex in Pip](regex).

Note: unlike other lowercase letters, `j` is not a variable; it is reserved for future use.

## Local variables

`a` First argument of the current function (at top level, first argument to the main program)

`b` Second argument of the current function (at top level, second argument to the main program)

`c` Third argument of the current function (at top level, third argument to the main program)

`d` Fourth argument of the current function (at top level, fourth argument to the main program)

`e` Fifth argument of the current function (at top level, fifth argument to the main program)

`f` The current function (at top level, the main program as a function)

`g` Full list of arguments of the current function (at top level, full list of arguments to the main program)

## Global variables

Note: any sequence of two uppercase letters that isn't a command or an operator is a global variable. The ones not listed here are initialized to nil.

`_` Identity function (== `{a}`)

`h` 100

`i` 0

`k` `", "`

`l` Empty list

`m` 1000 (mnemonic: Roman numeral M)

`n` Newline character

`o` 1

`p` `"()"`

`s` Space character

`t` 10

`u` Nil

`v` -1

`w` Pattern matching one or more whitespace characters (<code>\`\s+\`</code>)

`x` Empty string

`y` Empty string (modified by `Y` operator)

`z` Lowercase alphabet a to z

`B` Block that returns its second argument (`{b}`)

`G` Block that returns its argument list (`{g}`)

`\a` First argument to the main program

`\b` Second argument to the main program

`\c` Third argument to the main program

`\d` Fourth argument to the main program

`\e` Fifth argument to the main program

`\f` The main program as a function

`\g` Full list of arguments to the main program

`AZ` Uppercase alphabet A to Z

`CZ` Lowercase consonants b to z

`PA` All **P**rintable **A**SCII characters, 32 through 126

`PI` Pi (3.141592653589793)

`VD` Date of the latest interpreter update in YYYY-MM-DD format

`VN` Current version number in X.Y.Z format

`VW` Lowercase vowels a to u

`VY` Lowercase vowels a to y

`XA` Pattern matching one (ASCII) letter (<code>\`[A-Za-z]\`</code>)

`XC` Pattern matching one (lowercase ASCII) consonant (<code>\`[bcdfghjklmnpqrstvwxyz]\`</code>)

`XD` Pattern matching one digit (<code>\`\d\`</code>)

`XI` Pattern matching an integer (<code>\`-?\d+\`</code>)

`XL` Pattern matching one lowercase (ASCII) letter (<code>\`[a-z]\`</code>)

`XN` Pattern matching an integer or decimal number (<code>\`-?\d+(?:\.\d+)?\`</code>)

`XU` Pattern matching one uppercase (ASCII) letter (<code>\`[A-Z]\`</code>)

`XV` Pattern matching one (lowercase ASCII) vowel, not including y (<code>\`[aeiou]\`</code>)

`XW` Pattern matching one word character--letter, number, or underscore (<code>\`\w\`</code>)

`XX` Pattern matching any one character (<code>\`.\`</code>)

`XY` Pattern matching one (lowercase ASCII) vowel, including y (<code>\`[aeiouy]\`</code>)

## Special variables

`q` Reads and returns a line of input each time it is accessed

`r` Returns a random number 0 <= `r` < 1 when it is accessed; assigning to `r` seeds the random-number generator

## Regex match variables

`$0` Entire match

`$1` Contents of capture group 1 (and similarly for 2-9)

`$$` List of all capture group contents

`$(` Start index of match

`$)` End index of match

`$[` List of start indices of capture groups

`$]` List of end indices of capture groups

<code>$`</code> The part of the string before the match

`$'` The part of the string after the match
