---
status: accepted
superseded-by:
date: 2026-11-26
---
# ADR-0001 One crate per module

## Context
The Vision clearly states the project will be made in modules.
These modules may only act on interfaces of other modules but never their imeplementation.

## Decision
One crate per module in a cargo workspace.
By making each module a crate it is mechanically separated and the compiler won't even allow using another modules internal functions.

## Alternatives considered
+ One crate with 'mod' modules: Simpler to implement but doesn't mechanically separate.

## Consequences
- Each crate can only use the public interface of another
- more boilerplate
- some cross-crate inlining may require care for performance. To be revisited when scaling