# IX-Marine-H2-Retrofit Scope Lock

## Purpose

IX-Marine-H2-Retrofit is a concept-stage engineering repository for a harbor and short-sea vessel retrofit architecture that combines:

- protected seawater intake
- water treatment to electrolyzer-grade feedwater
- berth-oriented onboard hydrogen generation
- compressed hydrogen storage
- fuel-cell and battery hybrid power integration
- safety, ventilation, shutdown, and monitoring logic
- proof-of-concept packaging
- full bill of materials
- concept-stage assembly and integration guidance

## What this repository is trying to solve

This repository is built to study a cleaner retrofit path for selected marine vessels that need a disciplined way to:

1. take seawater in without turning the intake into a debris and maintenance nightmare
2. produce clean process water suitable for hydrogen generation
3. generate hydrogen onboard when external electrical power is available
4. store and use that hydrogen safely in a marine environment
5. combine hydrogen power with battery support for operational resilience
6. keep controls, sensing, logging, and emergency functions alive under degraded conditions
7. expose the real penalties, risks, and integration burdens instead of hiding them

## Core framing

The repository is framed as a **measurement-first marine hydrogen retrofit architecture**.

That means every meaningful claim in the repo must be tied to one or more of the following:

- a defined requirement
- a stated assumption
- a measurable variable
- a hazard case
- an acceptance check
- a stated non-claim

## Locked design direction

The repo is locked to the following design direction:

- vessel class focus: harbor / port utility / short-sea workboat style platforms
- energy architecture focus: hydrogen plus battery hybrid
- hydrogen production focus: onboard electrolysis using treated seawater-derived process water
- operating focus: hydrogen generation primarily while berthed and connected to external power
- housekeeping energy focus: small auxiliary harvesters may support controls and sensing, but they are not counted as main propulsion or main hydrogen-production energy
- licensing focus: Apache-2.0
- documentation focus: concept-stage engineering rigor, not marketing language

## What this repository is not

This repository is not:

- a perpetual-motion system
- a claim that vessel drag or wave action alone can power full ship hydrogen production
- a class-approved vessel package
- a yard-issued installation release
- a bunkering manual for live commercial service
- a certified firefighting doctrine
- a substitute for formal class, flag, owner, insurer, or port approval
- a promise of positive project payback in all cases
- a universal fuel answer for every marine vessel class

## Out of scope

The following are intentionally out of scope for this repository:

- methanol retrofit architecture
- ammonia retrofit architecture
- deep-sea endurance vessel design
- military mission systems
- weaponization use cases
- hidden or unverifiable claims
- unsupported range or efficiency promises
- direct dependence on private repositories for explanatory context

## Repository quality bar

A file belongs in this repository only if it helps one or more of these:

- define the architecture clearly
- reduce ambiguity
- expose a failure mode
- support a decision
- support a test
- support assembly or integration understanding
- support maintainability and safe operation framing

If a file does not help one of those purposes, it does not belong here.
