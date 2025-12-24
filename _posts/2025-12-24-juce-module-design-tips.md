---
layout: post
title: "JUCE Module Design Tips (From Real Projects)."
date: 2025-12-24
---

# Introduction

This post collects a set of design tips and common pitfalls I've encountered while writing and maintaining private and public JUCE modules intended for reuse.

None of these are theoretical - they're the result of real design considerations, experiences like build failures and portability issues, and general integration pain that only show up once a custom JUCE module becomes a dependency.

With great power comes great responsibility - JUCE modules give you a powerful way to package code for reuse, but that power comes with the responsibility of managing APIs, dependencies, and platform-specific behaviour very carefully.

## So What's a JUCE Module, Really?

Surely, after starting your first JUCE project with CMake and/or the Projucer, you've seen [the JUCE Module Format specs](https://github.com/juce-framework/JUCE/blob/develop/docs/JUCE%20Module%20Format.md), or at least seen [the modules from JUCE itself](https://github.com/juce-framework/JUCE/tree/develop/modules).

From a conceptual point of view, consider a module as a public API contract where the implementation details are hidden in `.cpp`/`.mm` files. Headers define what your consumers can rely on; everything else is internal. Consumers being users as developers; people integrating your module(s) into their app code or, at a higher level, into their own module code.

### Formatting & Expectations

Naming conventions are important: filenames, functions, classes, namespaces, the occasional macro... everything should be descriptive, unique, and most importantly - consistent.

This importance goes beyond _just names for the sake of names_ - it's communication. Consumers should be able find and localise information quickly, in the most digestable way you can concoct: building mental models about your code should be straightforward.

#### Filenames

First, you should consider naming your files based on their intents: is it capturing a class definition like an `Array` in [`juce_Array.h`](https://github.com/juce-framework/JUCE/blob/develop/modules/juce_core/containers/juce_Array.h)? Or maybe you're capturing a group of concepts like changing values smoothly in [juce_SmoothedValue.h](https://github.com/juce-framework/JUCE/blob/develop/modules/juce_audio_basics/utilities/juce_SmoothedValue.h)?

With that in mind, I strongly recommend prefixing your filenames with your module name (eg: `juce_XYZ.h`, `squarepine_XYZ.h`). This avoids clashing filenames when searching and listing files, and makes it less confusing to read.

As a side note: please stop using plain `Utility` or `Utilities` or `Helpers` as a vague, catch-all bucket file. This is an extraordinarily bad habit and doesn't help consumers internalise the _goal_ of _what_ code needs to be found in these files. You're creating a goose-chase that can be avoided by segregating _concepts_; concepts are searchable.

Let's make it plain with an _in-code_ comparison:

```c++
// Bad: vague, catch-all
#include "Utilities.h"

// Good: concept-specific, prefixed
#include "squarepine_EffectProcessorChain.h"
```

Using `find` or `CTRL/CMD+F`, it becomes abundantly clear where a file lives and which module it originates from (or at least _who_ it originates from) when applying a concept-specific naming approach.

#### Definitions

Single responsibility: one cohesive area per module.

Clear API surface: minimal, boring, platform-agnostic headers.

Implementation vs interface separation: platform includes and heavy logic in .cpp.

Predictable build behaviour: no hidden macros or unexpected dependencies.

### Transitive Awareness

Exposed headers affect all downstream users. You have to be exceptionally cautious when

## Don't Leak Native or Platform Headers

Avoid exposing platform-specific headers in module headers.

Keep native includes in .cpp.

Platform-specific tips:

macOS/iOS: .mm files for Objective-C++ segregation.

Windows: JUCE_CORE_INCLUDE_COM_SMART_PTR=1 in .cpp if COM helpers are needed.

## Public Headers ≠ Convenience Headers

Only include what's needed for the user to consume the module.

Forward-declare where possible.

Minimal headers = reduced coupling, faster compile times, fewer ABI issues.

## Be Intentional About Module Dependencies

Avoid unnecessary JUCE or external module dependencies.

Use internal helpers instead of pulling in large dependencies unnecessarily.

Every dependency is a hidden obligation for users.

## Avoid "Header-Only by Accident"

Keep definitions, platform logic, and non-template code in .cpp.

Inline only truly necessary things.

Prevent ABI instability and excessive compile times.

## Platform Code Belongs Behind a Wall

Keep `#if JUCE_WINDOWS`, `#if JUCE_MAC`, and any other native things tucked away in the implementation files; keeph headers neutral.

Use .mm for Objective-C++ where necessary.

Benefits: easier maintenance, porting, testing.

## Modules Are Long-Term Commitments

Public API changes are painful.

Design names and types carefully.

Treat modules as reusable libraries, not convenient folders.

## Unit Test Integration

JUCE UnitTest system has no formal module guidelines.

Provide config macros to enable/disable tests:

```c++
#ifndef SQUAREPINE_ENABLE_UNIT_TESTS
 #define SQUAREPINE_ENABLE_UNIT_TESTS 0
#endif
```

Guard all test classes with the macro to avoid polluting downstream test runners.

Insight: Separating module tests from consuming project tests prevents accidental breakage.

## Android Integration Gotchas

JUCE requires unwritten macros and scaffolding for Android:

JNI_CLASS_MEMBERS for JNI bindings.

#define JUCE_CORE_INCLUDE_JNI_HELPERS 1 in .cpp before any includes.

Document all macros clearly, keep them in .cpp, and provide usage examples.

Insight: Explicit scaffolding prevents build errors and builds trust with module consumers.

## Final Takeaway

JUCE modules are powerful but sharp: most pain comes from accidental exposure or hidden dependencies.

Keep headers minimal, segregate platform code, manage dependencies deliberately.

Modules like squarepine_core demonstrate careful boundary management.

Following these practices saves build headaches, fragile code, and subtle platform bugs.
