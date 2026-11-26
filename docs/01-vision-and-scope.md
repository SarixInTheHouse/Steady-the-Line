# Vision & Scope

## 1. Vision
A 2d top-down Simulator of historical warfare, in which units behave the way real soldiers would have, by following real drill-instructions of the time.

**Primary Goal** is to emulate real troop movement. A soldier does not magically know where to go, they can only follow a small set of rules based on his neighbors and leader. As a result a group of soldiers can only make a set amount of formations.

**Secondary Goal** is to emulate real combat. In many strategy games you will see soldiers breaking formation and the frontline becomes a field of duels. Historically that rarely ever happened, soldiers would not break formation in combat, if they did it was usually a massacre on their side. 

**Tertiary Goal** is to emulate real troop behavior. Soldiers weren't perfect, an officer may charge without orders, an order might not make it to a unit in time or a unit straight up refuses to follow it.

## 2. First milestone: "Marching Simulator" tech demo

A sandbox that shows and stress-tests troop behaviour. It has no opponent, no objectives and no combat.

**In scope**
- A hellenistic Phalanx unit, following the Asclepiodotus, Tactics (1st c. BC)
- A limited set of historically accurate drill commands. This will likely not reflect the entire set of commands a real unit would have known.
- A few dozen to at most around a hundred soldiers
- scalable pathfinding and soldier-simulation
- Simple 2d top-down rendering and basic user input
- Debugging tools and instruments

**Out of scope for this milestone**
- Combat, morale, casualties
- Opposing forces or AI commanders
- Terrain beyond a flat plane
- Multiple eras or army types (but the architecture must allow them, see §3)
- Audio, polish, menus, save/load

## 3. Quality goals (non-functional requirements)

Listed in priority order.

1. **Modularity and replaceability.** The core simulation must not depend on any specific era. Drill systems are interchangeable modules and the simulation is separate from rendering
2. **Clean engineering.** No hacks or shortcuts that break the documented design. If the design is wrong, change the design, don't work around it in code.
3. **Scalability.** Ultimately there will be thousands of troops if not more. The Design must be made such that this is a matter of optimization, not rewriting.
4. **Correctness and traceability.** Behaviour should be traceable to a documented rule, and ideally to a historical source.

## 4. Development model and constraints

- **Language:** Rust
- **Development Method:** Shape-Up, adapted to a solo-dev working on a side-project.
- **Determinism:** The same simulation state and inputs always produce the same next state. Soldier updates are pure functions of the previous tick's state (read old, write new), which makes them safe to run in parallel. Wherever parallel results are combined or conflicts resolved, a fixed order is used.
- **Modules:** The code will be highly modularized, enforced via separate crates in a Cargo workspace.
- **Decisions and Documentation:** Major Decisions will be stored in (simple) Architecture Design Records (ADR). There will be plenty of documentation made during the cooldown phase.