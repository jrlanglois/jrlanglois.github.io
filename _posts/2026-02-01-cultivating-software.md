---
layout: post
title: "Cultivating Software: My Approach to Development"
date: 2026-02-01
---

# Cultivating Software: My Approach to Development

Software isn't static. It's malleable, messy, and constantly changing. I treat it like a system to experiment with, shape, and adapt - sometimes chaotic, always deliberate. Concepts change, approaches change, needs change—and the code should evolve alongside them.

Here's how I approach building software that actually works—for both the system and the people using it.

## Explore Before You Strategize

I don't wait to understand everything before touching the code. Sometimes the fastest way to learn a system is to dive in, experiment, and see what breaks. Hacking around isn't reckless - it's exploratory intelligence.

* Get your hands dirty: Modify, poke, and probe the code to understand its quirks, hidden dependencies, and failure modes.
* Zoom out and think top-down: As you explore, keep the bigger picture in mind. Look for ways to reformulate solutions holistically, align components, or simplify architecture.
* Strategize from insight: The combination of bottom-up tinkering and top-down perspective lets you identify high-leverage interventions that are both practical and elegant.

Exploration and tinkering teach you the code's mechanics (typically historical ones), and it will teach you about any preexisting holes, redundancies, possible efficiencies and simplifications, and most importantly it will teach you about any gaps or under representations. On the flip side of the coin, top-down thinking lets you redesign intelligently and deliberately. Together, they let you improve the system in ways that are robust, adaptable, and well-considered.

## Shape the Code, Don't Baby It

Once I know the terrain, I cultivate the code like a living system: flexible, modular, evolving, yet seeking a way to be organised and communicative all at once.

* Modular design: Components should plug in, swap out, or disappear without collapsing the system.
* Iterative experimentation: Testing and code review are small experiments - catch chaos early, learn fast, pivot if needed.
* Pragmatism over dogma: I follow patterns and rules when they serve the system. I ignore them when they don't. The goal isn't purity - it's adaptability.
  * Being unconventional is perfectly fine, but I consider the reader first in these cases.

Code isn't made of metal or concrete, and I definitely won't treat it like a sacred artifact. I guide its shape, prune what doesn't work, and push it to adapt as requirements, concepts, and approaches shift - sometimes it's just plainly to better its use, its integration, or sometimes delete the damn thing altogether because I found a better way to resolve those code smells I couldn't resolve at the time (ie: there's a better way).

## Grow the Parts That Actually Matter

Growth isn't just outward-facing features. Some of the most important work happens behind the scenes. I focus on both the visible branches and the soil that supports them.

* System-level interventions: Refactors, architecture tweaks, and stabilizing the foundation give the system room to evolve without collapsing under its own weight. 
* Developer experience as infrastructure: Tools, workflows, and documentation aren't fluff - they're the soil that lets ideas take root without chaos.
  * Consider the "how" for when you use code: if you find yourself taking a long time to get set up, integrating, and building with your new library, maybe your approach is wrong.
  * Did I mention I hate Cmake?
* Exploration fuels strategy: Even small, seemingly “trivial” changes teach you how the system behaves, reveal hidden bottlenecks, and uncover opportunities to make bigger improvements later.
  * You can leverage this approach to further document code, reconceptualise it by revealing patterns that can be separated and reused elsewhere, and so on.

By tending both the visible branches and the underlying soil, the software—and the people working on it—stays strong, adaptable, and resilient.

## TL;DR

Software is malleable. I approach it like a living system: explore to learn its quirks, zoom out to redesign holistically, shape pragmatically, and focus on growth that matters—both externally and internally. Chaos is inevitable; how you guide it is what counts.
