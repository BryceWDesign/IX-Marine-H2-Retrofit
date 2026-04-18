# Reference Vessel Definition

## Purpose

This file locks the concept reference vessel for IX-Marine-H2-Retrofit so that
the architecture, mass allowances, machinery footprint assumptions, safety
zones, and operational logic stay tied to one defensible target instead of
drifting into generic claims.

## Selected reference vessel class

The reference vessel for this repository is a:

**harbor / port utility workboat retrofit**

This is the best fit for the repository because it offers:

- enough physical volume for added process equipment
- short-duty or day-duty operating patterns that support berth-side charging
  and berth-side hydrogen generation
- operational relevance for emissions reduction in ports and near populated
  waterfronts
- lower endurance pressure than deep-sea cargo applications
- better suitability for fuel-cell plus battery hybrid operation

## Reference vessel envelope

The reference vessel is assumed to fall inside the following concept envelope:

- **length overall:** 85 to 95 ft
- **beam:** 24 to 28 ft
- **displacement:** 130 to 180 tons
- **service type:** harbor service, tug-assist support, port utility,
  inspection, line handling, or short-sea support duty
- **operating pattern:** daily return to berth
- **berth availability:** routine overnight or extended layover connection
  possible
- **crew concept:** small professional marine crew with formal operating and
  maintenance procedures

These values are design anchors only. They are not a claim that every vessel
inside the range will accept the retrofit unchanged.

## Operational assumptions

The reference vessel is assumed to operate under the following concept duty:

- short transit legs
- frequent low-to-moderate power operation
- intermittent peak maneuvering power
- return-to-berth cycle compatible with overnight recharge or hydrogen
  generation
- high value placed on local emissions reduction, reduced noise, and
  technology demonstration potential

## Electrical duty basis

The retrofit architecture is sized against the following concept mission basis:

- **daily electrical energy target:** 0.9 to 1.1 MWh/day
- **continuous average operating demand:** 120 to 180 kW
- **peak propulsion / maneuvering demand:** 400 to 500 kW
- **hotel / auxiliaries:** included within the daily target envelope
- **black-start capability:** required
- **degraded return-to-berth mode:** required

These numbers are concept-stage design anchors used to size the fuel-cell,
battery, hydrogen inventory, and berth-side power demand logic.

## Why this vessel class was chosen

This repository intentionally does **not** use a deep-sea cargo ship, large
ferry, or naval platform as its base case.

The harbor / port utility vessel class was selected because:

1. it is more likely to tolerate the added machinery footprint and operational
   complexity of a hydrogen retrofit
2. it is more likely to have predictable berth access and external power
   availability
3. it is more likely to benefit from zero-emission or near-zero-emission
   operation in port-adjacent environments
4. it avoids pretending that hydrogen storage penalties are trivial at very
   long range
5. it offers a more credible proof-of-concept path for integration, testing,
   and phased adoption

## Reference arrangement intent

The retrofit is assumed to use the vessel in the following broad arrangement
style:

- weather deck or upper machinery-adjacent area for hydrogen storage rack
- low and near-centerline placement for battery system
- central machinery zone for fuel-cell modules and power conversion
- protected seawater intake path with serviceable pretreatment equipment
- berth-oriented process layout that allows safe hydrogen generation while
  moored
- safety-driven separation between hydrogen-bearing hardware and
  accommodation/control spaces

## Design consequences of this vessel choice

Because this repo is locked to a harbor utility vessel class, the architecture
must satisfy the following design consequences:

- onboard hydrogen generation is primarily a berth activity, not an underway
  fantasy loop
- battery buffering is essential for transient maneuvering load
- storage volume and weight must remain disciplined
- maintenance access cannot be treated as optional
- venting, isolation, and gas detection must be designed for repeated port use
- the repo must provide enough clarity that a yard or reviewer can decide
  whether the retrofit is even worth studying further for a real hull

## Explicit non-claims tied to the reference vessel

This reference vessel definition does **not** mean:

- every harbor workboat can accept this retrofit
- final stability has been solved for a real hull
- class approval has been achieved
- cost or payback is universal across vessel operators
- this concept scales cleanly to all marine platforms

## What later files must respect

All later files in this repository must stay consistent with this reference
vessel definition unless a file explicitly says it is exploring a bounded
variant.

That includes, but is not limited to:

- machinery footprint assumptions
- hydrogen inventory assumptions
- battery sizing assumptions
- berth power requirements
- maintenance access assumptions
- hazard and shutdown logic
- proof-of-concept framing
- bill of materials categories

