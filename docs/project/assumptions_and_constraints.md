# Assumptions and Constraints

## Purpose

This file locks the core assumptions and constraints that IX-Marine-H2-Retrofit
is allowed to use.

Its job is simple:

- prevent hidden assumptions
- stop scope creep
- force physical honesty
- expose the conditions under which the concept is being judged

If a later file relies on an assumption that is not present here or in a
properly bounded file, that later file is incomplete.

## Assumption format

Each assumption is given an ID so later files can reference it.

- **A-xxx** = assumption
- **C-xxx** = constraint

Assumptions are concept-stage working premises. They are not guarantees.
Constraints are hard design boundaries for this repository unless later files
explicitly create a bounded variant.

---

## A-001 — Vessel duty pattern

The reference vessel is assumed to return to berth routinely enough that
external electrical energy can be used for recharge and onboard hydrogen
generation.

### Why it matters
Without this assumption, the berth-oriented electrolysis concept becomes weak
and the architecture drifts toward unrealistic underway self-generation claims.

---

## A-002 — Vessel class focus

The architecture is assumed to target a harbor / port utility / short-sea
workboat style vessel rather than a deep-sea endurance platform.

### Why it matters
This keeps storage volume, berth dependence, maintenance access, and range
expectations inside a defensible operating envelope.

---

## A-003 — Hydrogen is not the only electrical source onboard

The concept assumes hydrogen power is paired with a battery system and that
both are required for the reference vessel to operate credibly.

### Why it matters
Battery support is needed for:
- transient load absorption
- black-start
- degraded return-to-berth mode
- smoothing of fuel-cell transients
- safe recovery after faults

---

## A-004 — Onboard electrolysis is mainly a berth activity

Hydrogen generation onboard is assumed to occur primarily while the vessel is
berthed and supplied with external electrical power.

### Why it matters
This prevents the repo from quietly slipping into a false narrative that the
vessel makes all of its own hydrogen underway from ocean motion or hull drag.

---

## A-005 — Seawater is feedstock, not the primary energy source

The concept assumes seawater is a process feedstock for treated water
production, not the origin of net propulsion-scale energy.

### Why it matters
The repo is not allowed to imply that seawater itself solves the energy balance.

---

## A-006 — Auxiliary harvesters are real but limited

The concept assumes low-power auxiliary harvesters may be useful for
housekeeping functions such as:
- controls
- sensing
- logging
- purge actuation support
- maintenance telemetry
- black-start hold-up support

The concept does not assume those harvesters replace the main energy path.

### Why it matters
This keeps useful innovation without turning weak sources into fake main-power
claims.

---

## A-007 — Treated water is mandatory for the selected baseline electrolyzer path

The concept assumes the baseline hydrogen-generation path uses treated,
electrolyzer-suitable water derived from seawater intake and water treatment.

### Why it matters
This repo is not built around a casual raw-seawater electrolysis claim.

---

## A-008 — The vessel operator values local emissions reduction

The concept assumes the operator has real interest in at least one of these:
- lower local emissions in port
- quieter operation
- technology demonstration value
- strategic decarbonization positioning
- preparation for stricter harbor emissions rules

### Why it matters
The concept is not framed as a pure fuel-savings retrofit.

---

## A-009 — Maintenance access is a first-order design concern

The architecture assumes that serviceability matters from the start and is not
something to be fixed later.

### Why it matters
A marine retrofit that cannot be maintained cleanly is operationally weak even
if the process diagram looks elegant.

---

## A-010 — Split-module redundancy is preferable

The concept assumes multiple smaller modules are generally better than one
monolithic unit where that improves:
- fault isolation
- partial operability
- maintainability
- replacement logistics

### Why it matters
This assumption strongly affects fuel-cell and subsystem arrangement.

---

## A-011 — Hazard visibility is more important than simplicity theater

The repo assumes that it is better to expose ugly realities than hide them for
presentation value.

That includes:
- storage penalties
- ventilation burden
- water quality lockouts
- compressor faults
- training burden
- berth dependency
- unclear payback

### Why it matters
This assumption is part of the repo identity.

---

## A-012 — Concept-stage numbers are reference-vessel numbers

Unless a file explicitly says otherwise, all sizing, timing, footprint, and
mass numbers in this repository are tied to the reference vessel concept.

### Why it matters
This prevents readers from treating bounded sizing logic as universal truth.

---

## C-001 — No perpetual-motion framing

The repository must not claim or imply that:
- hull drag
- intake flow
- wave action
- vessel motion
- weak ambient harvesting

can by themselves sustain the full hydrogen-production energy demand for the
reference vessel.

---

## C-002 — No universal vessel applicability

The repository must not frame the retrofit as automatically suitable for:
- all workboats
- all ferries
- all tugs
- all commercial ships
- all naval vessels

The design is bounded.

---

## C-003 — No dependence on inaccessible source material

This repository must stand on its own technical footing.

It may be informed by prior thinking, but it must not require readers to know,
read, or trust private repositories or hidden work in order to understand:
- the architecture
- the hazards
- the assumptions
- the decisions
- the proof-of-concept path

---

## C-004 — No hidden energy accounting

The repository must not bury major energy penalties such as:
- intake pumping
- pretreatment
- desalination
- polishing
- electrolysis
- gas drying
- compression
- storage and conversion losses
- ventilation parasitics

If an energy-consuming subsystem matters, it must be visible in the repo.

---

## C-005 — No “green” claim without source-boundary clarity

The repository must not imply strong climate benefit without separating:
- tank-to-wake effects
- berth electricity source effects
- strategic versus direct economic value

---

## C-006 — No class-like certainty where class data is missing

The repository must not present concept-level placeholders as final class-ready
answers for:
- hazardous zoning dimensions
- ventilation rates approved for a real hull
- structural reinforcement sufficiency
- intact or damage stability acceptance
- fire boundary acceptance
- final bunkering arrangement approval

---

## C-007 — No maintenance-hostile arrangement

The architecture must not trap routine-service hardware in a way that requires
major structural teardown for basic replacement or inspection where a more
serviceable arrangement is available.

---

## C-008 — No single-point safety philosophy

The architecture must not rely on a single barrier for critical hydrogen risk
control.

The concept must use layered protection for at least:
- detection
- isolation
- ventilation
- shutdown
- access control
- maintenance state awareness

---

## C-009 — No fake economic certainty

The repo must not pretend:
- payback is guaranteed
- retrofit cost is universal
- electricity pricing is stable
- port support is always available
- downtime is trivial

Economic framing must stay conditional.

---

## C-010 — No unfinished file may overrule this file silently

A later file may refine or bound an assumption or constraint, but it may not
quietly contradict this file without saying so.

---

## Design interpretation rule

If a reader sees an aggressive claim elsewhere in the repository, that claim
must be interpreted through the assumptions and constraints in this file.

If the aggressive claim cannot survive that test, the aggressive claim is weak.

## Summary

The architecture only makes sense if all of the following remain true at the
same time:

- berth-oriented hydrogen generation
- bounded harbor / short-sea vessel use case
- hydrogen plus battery hybrid logic
- treated-water electrolysis path
- transparent energy accounting
- safety layering
- maintenance realism
- no miracle-energy storytelling

That is the discipline line for IX-Marine-H2-Retrofit.
