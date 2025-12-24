---
layout: post
title: "JUCE Module Design Tips (From Real Projects)."
date: 2025-12-24
---

# Introduction

This post collects a set of design tips and common pitfalls I’ve encountered while writing and maintaining private and public JUCE modules intended for reuse.

None of these are theoretical - they’re the result of real design considerations, experiences like build failures and portability issues, and general integration pain that only show up once a custom JUCE module becomes a dependency.

## What's a JUCE Module, Really?

Surely, after starting your first JUCE project with CMake and/or the Projucer, you've seen [the JUCE Module Format specs](https://github.com/juce-framework/JUCE/blob/develop/docs/JUCE%20Module%20Format.md), or at least seen [the modules from JUCE itself](https://github.com/juce-framework/JUCE/tree/develop/modules).

From a conceptual point of view, consider a module as a public API contract where the implementation details are hidden in `.cpp`/`.mm` files. Headers define what users can rely on; everything else is internal.

Transitive awareness: exposed headers affect all downstream users.

Expectations:

Naming conventions: descriptive, unique, consistent.

Single responsibility: one cohesive area per module.

Clear API surface: minimal, boring, platform-agnostic headers.

Implementation vs interface separation: platform includes and heavy logic in .cpp.

Predictable build behaviour: no hidden macros or unexpected dependencies.

## Don’t Leak Native or Platform Headers

Avoid exposing platform-specific headers in module headers.

Keep native includes in .cpp.

Platform-specific tips:

macOS/iOS: .mm files for Objective-C++ segregation.

Windows: JUCE_CORE_INCLUDE_COM_SMART_PTR=1 in .cpp if COM helpers are needed.

## Public Headers ≠ Convenience Headers

Only include what’s needed for the user to consume the module.

Forward-declare where possible.

Minimal headers = reduced coupling, faster compile times, fewer ABI issues.

## Be Intentional About Module Dependencies

Avoid unnecessary JUCE or external module dependencies.

Use internal helpers instead of pulling in large dependencies unnecessarily.

Every dependency is a hidden obligation for users.

## Avoid “Header-Only by Accident”

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
