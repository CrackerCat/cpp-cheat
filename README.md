# ![logo](logo.jpg) C++ Cheat

[![Build Status](https://travis-ci.org/cirosantilli/cpp-cheat.svg?branch=master)](https://travis-ci.org/cirosantilli/cpp-cheat)

C and C++ information, cheatsheets and mini-projects.

There may be other compiled languages here for which we don't have much material for a separate repository, specially when we interface that language with C. E.g.: Fortran.

Relies on <https://github.com/cirosantilli/cpp-boilerplate> to factor code out. See [its documentation](https://github.com/cirosantilli/cpp-boilerplate/blob/master/README.md) for information on how to use this project.

## Most useful files

- [c.c](c.c):              C cheatsheet.
- [cpp.cpp](main_cpp.cpp): C++ cheatsheet.
- [posix](posix/):         POSIX C API.
- [opengl/](opengl/)
- [kde/](kde/)

## Quickstart

On Ubuntu 12.04:

    ./configure
    make run

When there are multiple files compiled, e.g.:

    c.c -> c
    cpp.cpp -> cpp

run a given file by specifying the basename without extension:

    make run=c
    make run=cpp

The `=` sign is *not* optional!

Doing just `make run` in those cases will run the default file.

To print the generated assembly code to the screen use:

    make asm RUN=cpp

To get help on all options use:

    make help

## Style

Non-portable features shall be clearly separated from portable ones in either:

- ifdef macro blocks
- separate files
- separate directories
- separate repositories

This includes features which were not present in the first standardized version of languages. E.g., C99 features must be put inside `#ifdf __STDC_VERSION__` blocks.

Everything that can be checked in an assertion will be checked, and will not get printed.

For example, a C addition operator `+` test should be done as:

    assert(1 + 1 == 2);

and *never*:

    printf("%d\n", 1 + 1);

so that all can be verified automatically.

Features which yield unpredictable outputs can print results to stdout. For example, `time(NULL)`

    printf("%d\n", 1 + 1);

Features that:

- require user input such as C `scanf`
- make programs wait for perceptible amounts of time

shall be put inside a block analogous to a `if (0){ ... }` to be turned on only when users want to test those specific features.

Cheat source comments are written in markdown *indented by headers* and commented out.

Every important keyword that one might search for in the feature has a hash before it, e.g. `#function`, `#include`, `#printf`, etc.