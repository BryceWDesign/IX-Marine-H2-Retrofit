# System Overview

## Purpose

This file defines the top-level architecture for IX-Marine-H2-Retrofit.

It answers one question:

**What is the full system now, in one place, without marketing language?**

This is the top-level system view that later files will decompose into
individual modules, hazards, interfaces, and verification logic.

## One-sentence definition

IX-Marine-H2-Retrofit is a concept-stage retrofit architecture for a harbor /
port utility vessel that uses treated seawater-derived process water, berth-side
electrolysis, compressed hydrogen storage, fuel-cell plus battery hybrid power,
and layered safety controls to support lower-emission marine operation without
pretending that ship motion alone can supply the required primary energy.

## Top-level architecture blocks

The full architecture is composed of seven primary modules:

1. Intake & Water Treatment Module
2. Hydrogen Generation Module
3. Gas Conditioning & Storage Module
4. Fuel Cell / Power Conversion Module
5. Safety & Ventilation Module
6. Housekeeping Energy Module
7. Monitoring & Controls Module

These modules together support a berth-oriented hydrogen production and use
cycle for the reference vessel.

## System intent

The architecture is designed to do the following:

- admit seawater in a debris-tolerant and maintainable way
- convert that seawater into process water suitable for electrolysis
- generate hydrogen onboard when external electrical power is available
- store hydrogen in a marine-appropriate arrangement
- convert stored hydrogen into electrical power through fuel cells
- buffer vessel power demand through battery support
- maintain safe operation through interlocks, shutdown logic, detection, and
  ventilation
- preserve control, sensing, logging, and recovery behavior even when the main
  process plant is unavailable

## High-level operating philosophy

The operating philosophy is intentionally split into two different energy
functions:

### Primary energy function
The primary energy function supports:
- hydrogen generation
- vessel power delivery
- propulsion support
- hotel and auxiliary electrical loads

This function depends on:
- external berth power for electrolysis
- hydrogen storage
- fuel-cell output
- battery support

### Secondary / housekeeping energy function
The housekeeping function supports:
- controls
- sensing
- event logging
- purge support
- state retention
- black-start support logic
- non-mission-critical auxiliary monitoring

This function may accept contribution from:
- low-voltage DC conversion
- battery backup
- supercap hold-up
- small auxiliary harvesters
- optional motion- or intake-assisted helper sources

The housekeeping function is explicitly not treated as the main propulsion or
main hydrogen-production power source.

## System boundary

The system boundary for this repository includes:

- seawater intake interface at the vessel
- treatment of seawater to process water
- hydrogen production onboard
- gas conditioning and storage onboard
- fuel-cell and battery integration onboard
- control, safety, shutdown, and monitoring logic onboard
- berth electrical interface and replenishment logic
- operator-facing concept operations

The system boundary does **not** include:
- class approval execution
- port-side permanent civil works design
- final vessel structural drawings
- final approved firefighting doctrine
- universal commercial deployment rules

## Top-level block flow

The conceptual process flow is:

1. seawater enters through protected intake
2. solids and debris are rejected or filtered
3. seawater is treated through pretreatment and desalination
4. process water is polished and stored
5. electrolyzer uses clean water and external electrical power to produce hydrogen
6. hydrogen is separated, dried, conditioned, and compressed
7. conditioned hydrogen is routed to storage
8. stored hydrogen is regulated to fuel-cell feed conditions
9. fuel cells convert hydrogen to electrical power
10. battery system buffers transients, supports black-start, and handles
    short-duration peak loads
11. control and safety systems supervise the entire chain and force safe states
    when required

## Reference architecture sizing

The locked reference concept for this repository assumes:

- **vessel class:** harbor / port utility workboat retrofit
- **fuel-cell capacity:** 2 × 125 kW PEM modules
- **battery capacity:** 500 kWh LFP
- **electrolyzer capacity:** 450 kW PEM
- **hydrogen storage:** approximately 90 kg gross, about 80 kg usable
- **storage pressure:** 350 bar class
- **mission basis:** approximately 0.9 to 1.1 MWh/day

These values are concept-stage anchors for the reference vessel and must not be
treated as universal.

## Design priorities

The architecture is driven by the following priorities, in order:

1. physical honesty
2. operational safety
3. maintainability
4. berth-oriented practicality
5. measurable energy accounting
6. degraded-mode operability
7. modularity and inspectability

That order matters.

If a later file proposes a cleaner-looking arrangement that weakens safety,
maintainability, or energy honesty, that later proposal is weaker than this
system overview.

## Primary design decisions already locked

The following decisions are already locked at system level:

### D-001 — Hydrogen plus battery hybrid
The reference vessel will not be framed as hydrogen-only.

### D-002 — Berth-oriented electrolysis
Onboard hydrogen generation is primarily a berth activity using external
electrical input.

### D-003 — Treated-water pathway
The baseline electrolyzer path uses treated process water derived from seawater
intake, not untreated raw seawater direct feed.

### D-004 — Weather-deck hydrogen storage preference
Hydrogen storage is preferred in a weather-deck arrangement with managed venting
and access rather than buried in inaccessible low spaces if avoidable.

### D-005 — Gas-safe or gas-managed separation philosophy
Hydrogen-bearing hardware is separated from accommodation and normal occupied
spaces through enclosure, ventilation, isolation, and shutdown logic.

### D-006 — Split-module architecture
Major subsystems are divided where practical to improve redundancy,
maintainability, and partial operability.

### D-007 — Auxiliary harvesters are subordinate
Small harvesters may assist low-power functions but do not get counted as the
core source of hydrogen-production energy.

## Energy truth statement

The architecture accepts the following as part of its identity:

- electrolysis is energy intensive
- compression is not free
- ventilation and safety systems add parasitic load
- water treatment is real but smaller than electrolysis in the total energy
  picture
- hydrogen storage volume is a real marine penalty
- battery support is necessary, not decorative
- port and berth infrastructure are part of the system whether convenient or not

## Top-level failure posture

This architecture is not built on “everything will work normally” logic.

It is built on the expectation that some combination of the following will
eventually happen:

- intake fouling
- water quality drift
- sensor disagreement
- purge fault
- compressor fault
- ventilation fault
- leak alarm
- blackout or bus upset
- maintenance misconfiguration

The architecture therefore uses:
- layered shutdown states
- permissive-based startup
- lockouts
- fallback operation
- logging and traceability

## System states

The top-level system is expected to operate in the following broad states:

1. **Cold / de-energized**
2. **Housekeeping alive**
3. **Berth process ready**
4. **Electrolysis active**
5. **Hydrogen storage replenishment active**
6. **Vessel operational on fuel-cell plus battery**
7. **Battery-dominant degraded mode**
8. **Hydrogen process lockout**
9. **Emergency shutdown state**

Later files define these more precisely.

## Why this architecture could matter

This architecture matters only if it solves the right problem honestly.

It is not trying to prove that every vessel should use hydrogen.

It is trying to provide a disciplined reference architecture for a class of
marine retrofit where the operator needs to understand:

- what equipment is really required
- what the space and mass penalties look like
- what the safety burden looks like
- what berth dependence looks like
- what can still operate when things go wrong
- what a proof-of-concept path would actually require

## What this file does not solve

This file does not finalize:
- detailed module interfaces
- exact hazardous-zone dimensions
- final class compliance
- final vendor selections
- final structural reinforcement
- final stability results
- detailed capex pricing
- detailed assembly sequence

Those are handled later.

## Traceability anchors

This system overview is directly tied to:
- `docs/project/reference_vessel.md`
- `docs/project/requirements_basis.md`
- `docs/project/non_claims.md`
- `docs/project/assumptions_and_constraints.md`

Later module files should align with this system overview unless they declare a
bounded alternative.

## Summary

At the highest level, IX-Marine-H2-Retrofit is a harbor-vessel retrofit concept
that uses berth-powered electrolysis, treated seawater-derived process water,
compressed hydrogen storage, fuel-cell plus battery hybrid power, and layered
marine safety logic to create a reviewable, non-magical hydrogen retrofit
architecture.
