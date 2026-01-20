---
layout: default
title: REPL Mode
permalink: repl
nav_order: 10
---

# REPL mode

Version 1.1 added a REPL mode to Pip.

## Basic usage

Run the interpreter with the `-R` flag to enter REPL mode.

Enter statements at the prompt to execute them. Entering an expression displays its repr. Incomplete statements/expressions can be continued on subsequent lines:

    >> "Hello".
    .. "world"
    "Helloworld"
    >> Fi\,3
    .. Pi
    1
    2
    3

The `-R` flag can be combined with certain other flags:

- `-w` to display warnings (off by default)
- List-formatting flags (only affects the str of a list; the repr is still used for displaying the results of top-level expressions)

REPL mode does not currently accept command-line arguments. Local variables `a` through `g` are all initialized to nil at top level (but can be assigned to, as usual).

## REPL-specific features

The variables `$_`, `$__`, and `$___` store the values of the last three top-level expressions:

    >> 1
    1
    >> $_+1
    2
    >> [$_$__]
    [2;1]

Certain comments are treated as REPL commands:

- `;warnings` toggles display of warning messages (can also be invoked as `;warnings off` or `;warnings on`). The initial setting depends on whether the REPL was invoked with the `-w` flag or not.
- `;quit` quits the REPL.
- `;exit` is identical to `;quit`.
- `;help` displays a help message. If followed by a space and an operator or global variable, it displays information about that operator or variable:
    - Operator: arity, full name, precedence, and associativity. Operators with two arities list separate information for each arity.
    - Global variable: initial value.

These commands can be abbreviated to any prefix of the command. For example, `;q` works for `;quit`, and `;warn off` works for `;warnings off`.

The REPL can also be exited via keyboard interrupt (usually Ctrl-C).
