---
layout: default
title: Getting Started
permalink: getting-started
nav_order: 2
---

# Getting started

There are a few ways to run Pip online, or you can clone the repository and run it locally.

## Online interpreters

The quickest way to get started using Pip is at [Attempt This Online](https://ato.pxeger.com/run?L=pip). (Thanks to [pxeger](https://github.com/pxeger) for adding Pip support to ATO.) Type your program in the Code box, enter command-line arguments as a JSON-formatted list of strings in the Arguments box, and enter command-line flags (again, as a JSON list of strings) in the Options box. If you want to take input from stdin, put it in the Input box. Click Execute to run your code.

Another online interpreter that supports Pip is [Do Stuff Online](https://dso.surge.sh/#pip). (Thanks to [emanresu A](https://github.com/chunkybanana) for adding Pip support to DSO.) The program goes in the Code box, and the flags and space-separated command-line arguments go in the Arguments box. Click the Run button (big triangle at the top) to run your code. Note that DSO will hang your browser if your code takes a long time to run.

Pip is also available on [Try It Online](https://tio.run/#pip). (Thanks to [Dennis](https://github.com/DennisMitchell) for adding Pip support to TIO.) It works similarly to ATO, except that flags and arguments all go in the Arguments section; each flag or argument should be placed in a separate box, not JSON-formatted. Note, however, that the version of Pip on TIO is [Pip Classic](pip-classic), which doesn't have any of the updates and new features since 2018.

An up-to-date version of Pip with a command-line interface is also hosted at [Replit](https://replit.com/@dloscutoff/pip). Clicking the run button will drop you into a [REPL session](repl). If you exit the REPL, you can run the interpreter using one of the invocation styles below.

## Command-line

Pip is implemented in Python 3. The main interpreter is the `pip.py` file. It should run on most systems with Python 3 installed simply by invoking `pip.py` in the directory where you put it (for \*nix systems, use `./pip.py`).

You may also wish to modify the `PATH` environment variable to include the path to Pip, so that you can invoke it from anywhere. 

## Invoking the interpreter

### Executing a Pip program from file

`pip.py [flags] path/to/codefile.pip [args]`

### Executing a Pip program directly

`pip.py [flags] -e 'code' [args]`

### Pip shell (interactive mode)

`pip.py`

### Pip REPL

`pip.py -R`

### Usage message

For more detailed information on how to invoke the interpreter:

`pip.py --help`
