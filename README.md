# ccrun

`ccrun`, aka *C* or *C*++ *Run*ner, compiles and executes C or C++ code base automatically.

## Warning

`ccrun` will compile and execute target source. Hence, DON'T USE `ccrun` to run UNTRUSTED source.

## Why `ccrun`?

C or C++ are compiled languages. We have to compile its source before executing it. Nevertheless, it is tedious to compile C or C++ source manually. For small code base, it is overkill to write Makefile or other project configuration file as well.

To address the issue, `ccrun` can automatically compile and execute C or C++ source without any project configuration file, handy for small code base.

## System Requirements

`ccrun` itself is written in POSIX shell. Besides, you need a C or C++ compiler to compile target source.

By default, `ccrun` will invoke `gcc` or `g++` for compilation tasks. You may change to another C or C++ compiler by setting related environment variables.

We tested `ccrun` against several Unix or Unix-like systems:

* Ubuntu 20.04 LTS
* Rocky Linux 8.5
* openSUSE Leap 15.3
* FreeBSD 13.0

It should work on other Unix or Unix-like systems as well.

## Supported File Formats

`ccrun` supports the following file formats:

* *.c* for C source
* *.cpp*, *.cxx* or *.cc* for C++ source

`ccrun` can handle projects that mix C and C++ together.

## Usage

Add exec mode for `ccrun` before using it:

```
$ chmod +x path/to/ccrun
```

It is recommended to copy `ccrun` to a valid **$PATH** like *$HOME/bin* or */usr/local/bin*.

Run single source:

```
$ ccrun path/to/file.c
```

Run multiple sources in a project:

```
$ ccrun path/to/*.c
```

Run multiple C and C++ mixed sources in a project:

```
$ ccrun path/to/*.c path/to/*.cpp
```

Run target sources with arguments:

```
$ ccrun path/to/*.c -- --opt param_a param_b param_c
```

## Environment Variables

You can adjust the behavior of `ccwarn` with the following environment variables:

* **CC** to set GCC compiler
* **CXX** to set G++ compiler
* **OUT_FILE** to set the name of a temporary output file
* **CFLAGS** to set custom include paths and compiler flags for C
* **CXXFLAGS** to set custom include paths and compiler flags for C++
* **LDFLAGS** to set custom lib paths
* **LIBS** to set custom library linkages
* **LD_LIBRARY_PATH** to set custom binary file paths

All environment variables are optional, set with sensible default values.

## Design Philosophy (Retrospective)

`ccrun` was designed as a minimal companion tool to `ccwarn`, focusing on a different stage of the development workflow: execution.

While `ccwarn` answers the question:

> *"Does this code compile cleanly?"*

`ccrun` focuses on:

> *"Can this code be compiled and run quickly without setup?"*

### Why another tool?

In C and C++, even small programs require explicit compilation before execution. For quick experiments or small code bases, writing a Makefile or configuring a build system introduces unnecessary friction.

`ccrun` removes that friction by providing a zero-configuration way to compile and run code immediately.

### Why support multiple source files?

Although designed for small code bases, `ccrun` allows multiple source files to be compiled together, including mixed C and C++ projects.

This enables simple experiments that go beyond single-file programs without requiring a full build system.

### Why use `--` for runtime arguments?

`ccrun` uses `--` to separate compiler inputs from runtime arguments. This design follows conventions used by many CLI tools and avoids ambiguity between source files and program arguments.

### Safety considerations

Unlike `ccwarn`, `ccrun` executes compiled binaries. This makes it inherently unsafe when used with untrusted source code.

Users are responsible for ensuring that input code is trusted before execution.

### Scope and limitations

`ccrun` is intentionally minimal and does not aim to replace build systems. It does not:

- resolve complex dependencies
- manage large projects
- provide incremental builds

Instead, it focuses on:

- fast iteration
- zero configuration
- simple workflows

### Relationship with `ccwarn`

`ccrun` and `ccwarn` are designed to complement each other:

- `ccwarn` checks code quality and portability
- `ccrun` enables quick compilation and execution

Together, they form a lightweight toolset for small C/C++ development workflows.

## Note

If you want to check code quality and conform some language standard for your C or C++ source, see [ccwarn](https://github.com/cwchentw/ccwarn).

## Copyright

Copyright (c) 2019 Michelle Chen. Licensed under [MIT](https://opensource.org/licenses/MIT).
