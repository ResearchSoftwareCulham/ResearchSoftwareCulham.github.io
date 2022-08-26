---
layout: post
title:  "Working with legacy code: UDA case study"
date:   2021-04-13
categories: jekyll
---

IDAM was a code originally written for the MAST experimental campaigns over 15 years ago. The purpose of the code was to isolate the users from the different data formats being used for MAST experimental data – some of which was in a custom binary format (IDA3) with newer analysis codes writing NetCDF files. IDAM was later renamed to UDA and this code has formed the basis of the data system for MAST-U as well becoming a component of the ITER IMAS data access library.

The code was used widely by users to access MAST data and was a part of the MAST data inter-shot acquisition system. While not being disused code it was over a decade old and had been developed and maintained by a sole developer with a build system and configuration heavily tailored to that user’s login environment. There was some user documentation but a lot of how the code was built and how the different components worked was not covered.

IDAM was largely a C code-base with wrappers in IDL, Fortran, Java and Python.

## Organising the code

When I first started working on IDAM (aka UDA) there were multiple versions of the code installed on various MAST machines and on the Freia cluster using bespoke build scripts, each having hardcoded paths and options to build for that system; none of which were well documented.

The first task was to put the code into version control and understand how to build the code (most of this work and some of the next step was done by Derek Sandiford). We also had to understand the various versions of the code on the different machines and how they differed. This largely involved trial and error and talking with the original IDAM developer to understand how they built the code and what the different flags were for.

## Replacing makefiles with CMake

The next step was to replace the hardcoded makefiles with CMake. CMake was used to allow for the dependencies to be extracted from the makefiles and made explicit, as well as finding all the conditional build flags and list them with default values. In this way it became possible to understand how the code was built and make it possible to build it on other systems without having to change hardcoded paths and options.

Over the years the UDA CMake has been tidied up with most of the conditional build flags removed. UDA is now fairly easy to build and has been built on a large range of systems, including on Windows (something that CMake makes possible).

## Automating tests

IDAM had quite a few tests. These tests were manually run though, requiring the user to read the test output printed to the console and understand what this output meant. Work was undertaken to automate some of these tests (using the C++ Catch testing framework) to allow them to be more easily run and the outputs to be pass/fail.

## Removing global state

One of the big problems with the code that made understanding, debugging and refactoring the code hard was the amount of global state – there was a large number of global variables that were used throughout the codebase. Removing the global variables made the code easier to understand, refactor and test and reduced the possibility of strange bugs occurring due to erroneously set global quantities.

Most of the global state could be fairly easily replaced with state being passed into the functions as additional arguments. This also had the benefit of making function dependencies explicit.

## Separating responsibilities

The other major refactoring work that was performed was to separate the code into separate sub-libraries to encapsulate responsibilities. For example, the code that was responsible for caching data was pulled out into a caching sub-library as this code did not depend on the rest of the codebase. CMake makes it easy to do this refactoring and even has the notion of a virtual library which removes the need to build lots of intermediate static libraries which then get pulled into a single library at the end.

The IDAM/UDA server has a plugin architecture where data-type specific functionality could be handled by a plugin written explicitly for that data type, i.e. an IDA3 plugin for reading IDA3 files. This architecture was only partially used in the original IDAM server with a lot of the file reading logic in the server itself. We he removed all of this logic from the server and moved it to the plugins. In this way the server code becomes much simpler and is solely responsible for communicating with the client and passing the data requests to the appropriate plugin.

## Other code cleaning

Over the years it also has been possible to remove large chunks of code that were no longer used, remove build flags that weren’t required anymore and refactor functions to simplify the logic. We have also moved the files from .c to .cpp in order to improve type checking and allow use of some C++ functionality to clean the code up. The code itself is still mostly C but newer functionality is being written as C++.

## Pyuda

The Python wrapper was completely rewritten to move from a thin wrapper around the C-API to a pythonic language binding with higher level data structures wrapping the low-level C calls.

## Conclusions

Developing IDAM/UDA has been a slow process of incrementally understanding and improving the codebase. This was made possible by the initial work of improving the build system, separating the code into sub-libraries, and removal of a lot of the global state. While the code is far from perfect it is much easier to build and maintain now that it was when I first start development on it.

