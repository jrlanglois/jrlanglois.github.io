---
layout: post
title: "Why JUCE Modules Are a Dream Kitchen"
date: 2025-12-23
---

## Intro

Imagine you're baking a cake. JUCE modules are like a beautifully organised kitchen where every ingredient is in its own jar, labelled, pre-measured, and easy to grab. The mixing bowls are laid out in the order you'll need them, and you can swap in different frosting flavours without ever touching the dry ingredients. You can whip up a cake in record time and iterate: more sugar? more cocoa? done.

CMake, on the other hand... well, it's like someone handed you a recipe where the ingredients are hidden in three different pantries, some instructions are written in an alien language, and half of the tools are buried in boxes you're supposed to build yourself before you even get to mixing. You can make the cake, eventually, but it will take a lot more time and patience - and you'll spend more energy figuring out where the flour is than actually baking. You may, in fact, be stuck milling your own flour, exclusively when the planets align, the moon is a particular shade of red, and Mercury has just decided to retrograde.

## In This Kitchen, Everything Just Works.

Here's why:

### Ingredients are Always Where You Expect Them

Every module is self-contained, with its own headers, source files, and resources neatly organised. Adding, removing, or modifying ingredients is trivial — no scavenger hunt across pantries. You can glance at the shelf and know exactly what you've got.

### Standardised Recipes

JUCE enforces conventions for naming, platform targets, and library imports. It's like having a baking manual that tells you not just what to do, but how to arrange your workspace so you never drop the eggs or forget the sugar. For contributors and maintainers, this reduces mistakes and friction.

### Clean, Readable Preparation Steps

Headers and source files are streamlined, and conditional compilation works like a pre-measured spice shaker: add a flag, and the compiler automatically includes just the right bits for your system or platform. You're not juggling a dozen separate mixing bowls while trying to remember which one contains what.

### Unity Builds: the Turbo Mixer

The real secret weapon: unity builds. Modules are designed to compile together quickly, so your edit -> compile -> run cycle is almost instantaneous. It's like having a turbo mixer that churns the batter for you while you're still deciding on frosting flavours. Fast iteration is built in, not bolted on.

## The Bitter Notes

Of course, no kitchen is perfect:

### Hidden Ingredients and Secret Spices

Some behaviour is controlled by macros that are buried in the module source files. You can use them to tweak your recipe, but if you're not aware of them, you might accidentally combine flavours that clash. Documentation exists, but it's not always obvious where to look — sometimes you feel like you're decoding a secret family recipe.

### Rules are Flexible... Sometimes Too Flexible

JUCE itself occasionally bends its own conventions — the graphics module is split into multiple files to speed up compilation, for example. That's perfectly fine for the framework maintainers, but it sends a mixed signal to kitchen visitors: can we even follow this approach with our own dishes? There's no real way for users to do that, so consistency relies on experience and judgement.

### Implicit Expectations

Some dependencies and include orders are implicit. You can follow the recipe perfectly and still encounter subtle quirks unless you understand the hidden structure. Think of it as a sourdough starter: the results are amazing once you know the trick, but beginners might struggle at first.

## Conclusion

JUCE's module system isn't perfect - no kitchen is. Some ingredients are hidden, various rules are implicit, and occasionally even the head chef bends the conventions. But the system's strengths far outweigh the quirks: a tidy, predictable layout, standardised recipes, and most importantly, blazing-fast iteration thanks to unity builds.

CMake, by contrast, is more like a sprawled workshop than a kitchen: flexible, powerful, and theoretically capable of anything — but you spend half your time just figuring out where everything is and how it fits together, and for whatever reason fending off greybearded shop techs that use the same dull tools and ancient, worn out textbooks. JUCE modules, for most application developers, feel like the better kitchen: everything you need is at hand, the workflow is intuitive, and you can focus on baking amazing cakes — or, in our case, building great software.

At the end of the day, understanding the trade-offs is key. Love it or grumble at it, JUCE's module format is a pragmatic, productivity-first design that rewards those willing to learn its quirks. And honestly sometimes a little magic flour under a red moon is worth it for a smooth, speedy bake. (But really, just never go full CMake...)

So yes, I like JUCE's module format. A lot. Not because it's flashy - but because it's a kitchen that actually lets you bake.
