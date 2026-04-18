# Requirements Basis

## Purpose

This file defines the concept-stage requirements basis for IX-Marine-H2-Retrofit.
It does not claim class approval, vendor commitment, or final regulatory
acceptance. Its purpose is to force the repository to answer clear engineering
questions instead of drifting into vague concept language.

## Requirement language

The following words are used with specific intent:

- **shall**: mandatory for the concept architecture
- **should**: strongly preferred unless a later file justifies deviation
- **may**: optional or exploratory
- **must not**: prohibited within this repository framing

## Top-level mission requirement

**R-001**  
The retrofit architecture **shall** support a harbor / port utility vessel duty
pattern in which the vessel routinely returns to berth and can access external
electrical power for recharge and onboard hydrogen generation.

## Energy architecture requirements

**R-010**  
The architecture **shall** use a hydrogen plus battery hybrid power approach.

**R-011**  
The battery system **shall** support transient maneuvering loads, black-start,
and degraded return-to-berth operation.

**R-012**  
Onboard hydrogen generation **shall** be framed primarily as a berth-oriented
process using external electrical energy.

**R-013**  
The repository **must not** claim that vessel drag, intake flow, or wave action
alone can supply the full energy required for primary hydrogen production.

**R-014**  
Small auxiliary energy harvesters **may** support controls, sensing, logging,
purge logic, and housekeeping loads.

**R-015**  
Auxiliary harvesters **must not** be counted as the principal energy source for
main propulsion or full-scale hydrogen generation.

## Water intake and treatment requirements

**R-020**  
The architecture **shall** include a protected seawater intake path with
serviceable debris rejection.

**R-021**  
The intake design **shall** assume exposure to trash, marine growth, suspended
solids, and clogging risk.

**R-022**  
The water-treatment train **shall** produce process water suitable for the
selected electrolyzer technology.

**R-023**  
The electrolyzer **shall** be prevented from operating when water quality is out
of acceptable range.

**R-024**  
The architecture **should** support flushing, cleanout, or backwash actions
without major structural disassembly.

## Hydrogen generation and storage requirements

**R-030**  
The hydrogen generation architecture **shall** use treated water rather than
assuming raw seawater can be fed directly into the core stack as the baseline
production path.

**R-031**  
The architecture **shall** include gas drying, isolation, pressure management,
and storage control functions.

**R-032**  
Hydrogen storage **shall** be arranged so that venting, isolation, and access
for maintenance can be addressed without trapping the system in an
unserviceable location.

**R-033**  
The repository **shall** treat hydrogen storage volume and mass as first-class
design penalties.

## Fuel-cell and power-conversion requirements

**R-040**  
The power-conversion architecture **shall** provide a fuel-cell path and a
battery path to a common electrical distribution concept.

**R-041**  
The architecture **shall** support black-start and controlled recovery from bus
loss.

**R-042**  
The architecture **shall** include precharge, isolation, and no-backfeed logic
at a concept level.

**R-043**  
The architecture **should** allow split-module redundancy where practical so
that partial capability remains available during maintenance or fault isolation.

## Safety requirements

**R-050**  
The architecture **shall** include hydrogen-specific gas detection.

**R-051**  
The architecture **shall** include ventilation proving for hydrogen-bearing
spaces, cabinets, or enclosures.

**R-052**  
Hydrogen process equipment **shall** enter a safe state on loss of required
ventilation.

**R-053**  
The architecture **shall** define layered emergency shutdown states.

**R-054**  
The architecture **shall** include explicit handling for hydrogen leak,
ignited release, purge failure, sensor failure, compressor fault, flooding or
spray ingress, and blackout recovery.

**R-055**  
The architecture **must not** rely on a single unverified sensor as the sole
barrier against hazardous hydrogen accumulation.

## Space, mass, and maintainability requirements

**R-060**  
The architecture **shall** define concept-level allowances for tank volume,
machinery footprint, ventilation space, and service clearances.

**R-061**  
The architecture **shall** treat center-of-gravity and stability effects as
mandatory evaluation items.

**R-062**  
Routine maintenance components **should** be replaceable without major cutting,
deck removal, or structural teardown.

**R-063**  
Manual isolation devices **shall** remain physically reachable within the
concept arrangement.

## Operations and port-interface requirements

**R-070**  
The architecture **shall** define when hydrogen is generated onboard versus when
it is loaded from shore.

**R-071**  
The architecture **shall** define berth-side electrical demand and expected
berth time for typical replenishment.

**R-072**  
The architecture **shall** include a concept for emergency response interfaces
between vessel and shore.

**R-073**  
The architecture **should** assume strong dependency on port procedures and
shore-side coordination rather than pretending the vessel is infrastructure
independent.

## Monitoring and controls requirements

**R-080**  
The architecture **shall** include a monitoring and controls concept with
process state visibility, safety state visibility, and maintenance visibility.

**R-081**  
The architecture **shall** support alarm prioritization.

**R-082**  
The architecture **shall** include lockouts for bad water quality, failed
ventilation proof, unresolved gas alarms, and maintenance-state conflicts.

**R-083**  
The architecture **should** preserve event logs across blackout or restart
events.

## Proof-of-concept and documentation requirements

**R-090**  
The repository **shall** include a proof-of-concept path that can be inspected
without requiring the reader to trust undocumented assumptions.

**R-091**  
The repository **shall** include a full bill of materials at concept stage.

**R-092**  
The repository **shall** include concept-stage assembly and integration
guidance, clearly labeled as non-certified and non-yard-issued.

**R-093**  
The repository **shall** include explicit non-claims wherever a reader could
mistake concept framing for operational endorsement.

## Economic and decision requirements

**R-100**  
The repository **shall** present capex, downtime, maintenance burden, training
load, and operating dependency as decision variables.

**R-101**  
The repository **must not** present universal payback claims.

**R-102**  
The repository **should** make clear where the concept is justified by
strategic, emissions, or operational goals rather than direct short-term fuel
savings alone.

## Explicit prohibited claims

The repository **must not** claim any of the following without later hard
evidence that is not currently available in this repo:

- class approval
- guaranteed regulatory acceptance
- guaranteed positive return on investment
- universal vessel applicability
- perpetual self-fueling from seawater and ship motion
- final hazardous-zone dimensions for all real installations
- final intact or damage stability approval for a real vessel

## Traceability intent

Later files in this repository should reference these requirement IDs wherever
possible so the reader can follow:

- requirement
- architecture choice
- hazard case
- verification idea
- stated limitation

That traceability is part of the repository's core discipline.
