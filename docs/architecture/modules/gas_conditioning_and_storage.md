# Gas Conditioning & Storage Module

## Purpose

This file defines the Gas Conditioning & Storage Module for IX-Marine-H2-Retrofit.

This module is responsible for taking hydrogen from the Hydrogen Generation
Module, conditioning it into a storage-appropriate state, moving it into the
vessel storage architecture, and later delivering it under controlled
conditions to the fuel-cell path.

This module exists to solve the following problems:

- raw hydrogen leaving production is not yet storage-ready by default
- hydrogen compression, manifold routing, and storage isolation are safety-
  critical functions
- marine hydrogen storage volume and arrangement penalties are real and must be
  exposed
- the storage path must support isolation, venting, maintenance access, and
  emergency response without being trapped in an unserviceable arrangement

## Module role in the full architecture

This module sits between:

- the **Hydrogen Generation Module**
- the **Fuel Cell / Power Conversion Module**
- the **Safety & Ventilation Module**
- the **Monitoring & Controls Module**
- berth-side service and emergency interfaces where applicable

It receives:

- hydrogen from the generation path
- supervisory commands and permissives
- shutdown and trip commands
- enclosure ventilation and gas-state conditions

It provides:

- conditioned hydrogen ready for storage
- regulated hydrogen supply toward the fuel-cell path
- storage-state information
- charge and discharge isolation behavior
- pressure, temperature, and fault-state visibility

This module does **not**:

- create hydrogen
- perform electrolysis
- eliminate the storage-volume penalty of hydrogen
- justify unsafe enclosure or poor venting practice

## Requirements traceability

This module directly supports:

- **R-031** include gas drying, isolation, pressure management, and storage
  control functions
- **R-032** storage arranged for venting, isolation, and maintenance access
- **R-033** storage volume and mass treated as first-class design penalties
- **R-040** fuel-cell and battery paths to common electrical concept
- **R-050** hydrogen-specific gas detection integration
- **R-051** ventilation proving for hydrogen-bearing spaces or enclosures
- **R-052** safe state on loss of required ventilation
- **R-053** layered emergency shutdown states
- **R-060** concept-level tank volume and machinery footprint allowances
- **R-062** maintainability and accessible replacement/service behavior
- **R-063** manual isolation devices remain reachable
- **R-082** lockouts and interlocks for unsafe state conflicts

It also operates under:

- **A-002** harbor / short-sea vessel focus
- **A-009** maintenance access is first-order
- **A-010** split-module redundancy preferred
- **A-011** hazard visibility matters more than simplicity theater
- **C-004** no hidden energy accounting
- **C-006** no fake class certainty
- **C-007** no maintenance-hostile arrangement
- **C-008** no single-point safety philosophy

## Locked baseline storage choice

The baseline storage choice for the reference architecture is:

**compressed hydrogen storage at 350 bar class**

### Why this is the locked baseline

This choice is not made because compressed storage is easy.
It is made because it is the most inspectable and conceptually tractable fit
for the selected harbor-vessel retrofit framing.

Reasons:

- conceptually consistent with modular rack-based marine arrangement
- easier to describe honestly than cryogenic liquid hydrogen in this repo
- compatible with weather-deck storage philosophy
- aligns with split-module and maintainable manifold thinking
- makes storage volume penalty visible instead of hiding it

This file does **not** claim 350 bar is best for every vessel or every owner.

## Locked reference sizing

The Gas Conditioning & Storage Module is locked to the following concept-stage
reference sizing:

- **gross storage mass target:** approximately 90 kg hydrogen
- **usable mission inventory target:** approximately 80 kg hydrogen
- **storage pressure class:** 350 bar
- **internal gas volume order of magnitude:** approximately 135 to 140 ft³
- **installed rack / enclosure allowance:** approximately 230 to 280 ft³

These are concept-stage allowances for the reference vessel only.

## Core design philosophy

The module is locked to the following design philosophy:

- hydrogen storage is a real vessel-layout burden
- storage must be accessible enough to isolate and maintain
- venting and relief must be deliberate
- manifolds must be readable and serviceable
- charge path and discharge path logic must be explicit
- weather-deck storage is preferred when practicable
- no trapped hydrogen-bearing equipment in casually occupied zones

## Submodule breakdown

The Gas Conditioning & Storage Module is divided into seven submodules:

1. Gas Drying and Quality Assurance Submodule
2. Compression Submodule
3. Charge Manifold and Isolation Submodule
4. Storage Rack Submodule
5. Pressure Relief and Venting Submodule
6. Supply Regulation to Fuel Cells Submodule
7. Storage Supervisory Logic Submodule

---

## 1) Gas Drying and Quality Assurance Submodule

### Function

Prepare generated hydrogen for safe and appropriate downstream handling.

### Why it exists

Hydrogen leaving production is not treated as perfect storage-ready gas by
default.

This stage exists to support:

- moisture reduction
- basic quality verification
- controlled handoff to compression and storage path
- fault visibility before gas enters the storage manifold

### Required concept functions

This submodule shall support:

- drying / moisture control concept
- gas-quality or purity indication as available at concept level
- blocked-path detection where relevant
- bypass control only under explicitly safe service conditions
- alarm and trip propagation to supervisory logic

### Failure posture

If gas quality is not acceptable for downstream storage logic:

- charging shall be inhibited
- production may stop or ramp down safely depending on upstream logic
- operator must be shown the reason clearly

---

## 2) Compression Submodule

### Function

Raise hydrogen pressure from the generation path to the storage pressure class.

### Locked concept

Use a **dedicated compressor stage** with conservative supervisory treatment.

### Why compression matters

Compression is not a side note.
It introduces:

- additional energy demand
- heat
- vibration
- pressure risk
- maintenance burden
- failure modes that can halt replenishment

### Required concept behavior

This submodule shall support:

- commanded start and stop
- pressure-target-based operation
- overtemperature protection
- overspeed or abnormal-current awareness where relevant
- vibration or abnormal-mechanical-state visibility
- local isolation behavior
- relief-path integration

### Mandatory interlocks

Compression shall remain blocked unless all of the following are true:

- downstream storage path is available
- venting / enclosure state is acceptable
- no hydrogen-gas trip is active in affected zone
- required valves are in correct state
- thermal state is acceptable
- maintenance mode is not active

### Failure posture

On severe compressor fault:

- compressor stops
- charge path isolates as required
- production path transitions to safe stop or hold state
- fault is latched and logged
- automatic restart is not assumed

---

## 3) Charge Manifold and Isolation Submodule

### Function

Route conditioned hydrogen from compression into the storage system under
controlled valve-state logic.

### Locked philosophy

The charge path must be readable and controllable.

### Required concept elements

The charge manifold should support:

- upstream isolation
- downstream isolation
- nonreturn / no-backflow behavior where relevant
- pressure-state visibility
- manual isolation access
- commanded stop and fail-safe positioning logic
- maintenance isolation capability

### Why this matters

A hydrogen storage system that cannot be clearly isolated is operationally weak
even if the cylinders themselves are sound.

### Design rule

Manual isolation devices must remain physically reachable within the concept
layout.

That is not optional.

---

## 4) Storage Rack Submodule

### Function

Contain hydrogen inventory in a marine-compatible storage arrangement.

### Locked arrangement philosophy

The preferred baseline concept is:

**weather-deck storage rack with protective structural framing, controlled
manifold enclosure, and deliberate vent strategy**

### Why this is preferred

Weather-deck preference exists because it can:

- reduce the chance of trapped accumulation inside deep enclosed spaces
- simplify outward venting and relief routing
- improve emergency visual separation
- improve replacement and heavy-access logistics
- avoid burying high-pressure storage in maintenance-hostile locations

### Required concept characteristics

The storage rack should be designed conceptually to support:

- mechanical restraint and marine motion tolerance
- protected manifold routing
- clear cylinder grouping
- replaceable or serviceable rack logic
- crane or practical removal path
- no casual exposure to impact-prone traffic paths
- no adjacency to routine accommodation openings or HVAC intakes

### Arrangement warning

This repo does not claim weather-deck storage eliminates all hazard.
It claims only that it is the clearer baseline for this bounded retrofit
concept.

---

## 5) Pressure Relief and Venting Submodule

### Function

Manage overpressure, relief discharge, and deliberate vent routing.

### Locked philosophy

Relief and venting must be intentional, segregated, and visible in the design.

### Required concept functions

This submodule shall support:

- pressure relief routing
- high-point vent discharge philosophy
- keep-clear concept around vent outlets
- no vent routing toward routine occupancy or air intakes
- support for controlled maintenance depressurization concept
- emergency vent awareness

### Provisional layout assumption

For concept layout only, later files may assume:

- approximately **10 ft** horizontal keep-clear around active vent or transfer
  outlet concept
- approximately **20 ft** vertical keep-clear above vent outlet concept

These are design placeholders only, not class-approved distances.

### Non-claim

This repo does not claim final hazardous-zone geometry or final vent dispersion
approval for a real vessel.

---

## 6) Supply Regulation to Fuel Cells Submodule

### Function

Provide controlled hydrogen delivery from storage to the Fuel Cell / Power
Conversion Module.

### Required concept functions

This submodule shall support:

- storage-side isolation
- pressure regulation for downstream fuel-cell use
- commanded supply enable / disable
- shutdown on leak, fault, or unresolved permissive loss
- startup only after purge and state validation rules are satisfied
- pressure and temperature visibility

### Why it matters

Storage is only half the problem.
Supplying hydrogen safely to the consumer path is equally important.

### Design philosophy

The supply path should favor:

- simple readable routing
- minimal unnecessary fittings
- maintainable valve placement
- clear shutdown state
- no ambiguous partial-open logic

---

## 7) Storage Supervisory Logic Submodule

### Function

Coordinate charge, hold, isolate, discharge, vent, and trip behavior for the
full module.

### Locked philosophy

Storage logic must be permissive-based and fault-visible.

### Minimum required charge permissives

Charging into storage shall require at minimum:

- gas quality path healthy
- compressor healthy
- storage pressure below allowed threshold
- manifold valves in correct state
- no active gas trip in affected storage/conditioning zone
- ventilation proven where required
- no maintenance lockout
- no emergency stop active

### Minimum required discharge permissives

Storage discharge toward fuel cells shall require at minimum:

- downstream path healthy
- no unresolved leak trip in affected supply path
- required purge and startup logic completed
- fuel-cell path ready
- manual and automatic isolation state valid

### Required stop / isolate triggers

This module shall isolate to safe state on at least:

- severe leak trip
- ignited release trip
- severe compressor fault
- emergency stop
- critical valve-state mismatch
- unsafe ventilation loss in affected enclosure
- overpressure / severe abnormal pressure state

### Logging expectations

The supervisory layer shall log at minimum:

- charge session start / stop
- discharge enable / disable
- storage pressure trend
- isolation events
- relief or vent event flag
- trip reason
- unavailable time
- maintenance-state time

---

## Reference footprint and arrangement allowances

### Storage rack envelope

Allow approximately:

- **230 to 280 ft³** total installed rack / protective structure / manifold
  envelope for the reference concept
- location on weather deck near centerline where practicable
- protected but accessible routing toward the fuel-cell machinery zone

### Compressor and conditioning footprint

Allow approximately:

- **8 ft × 8 ft** local footprint for compressor, drying, and immediate support
  hardware, subject to later package refinement
- direct service access at front and local isolation access
- thermal and vibration monitoring access

### Vent mast and relief path allowance

Allow approximately:

- **4 ft × 4 ft** plan allowance for dedicated vent/relief support geometry
- clear vertical routing with no casual conflict with occupancy or HVAC intake

### Placement philosophy

The module should be arranged so that:

- storage mass is controlled and not thrown arbitrarily high or outboard
- battery and heavier low-voltage equipment can help counter raised storage CG
- piping runs are not absurdly long
- maintenance staff can access isolation and instrumentation safely

---

## Weight and vessel impact awareness

This module is one of the main sources of marine retrofit penalty visibility.

It carries implications for:

- added topside weight
- raised vertical center of gravity
- structural support needs
- vent-routing geometry
- maintenance logistics
- safety-zone encroachment

The repo must later keep those penalties visible rather than hiding them in
generic system diagrams.

## Failure modes this module must expect

This module must be written as though the following can happen:

- gas quality out of bounds
- compressor overtemperature
- abnormal vibration
- charge manifold valve mismatch
- storage pressure sensor disagreement
- leak in conditioning enclosure
- relief event
- blocked vent path
- maintenance isolation left in wrong state
- supply regulator issue
- false permissive from failed sensor
- emergency stop while charging
- spray ingress into conditioning cabinet or manifold area

Detailed hazard logic is handled later, but this module must assume those cases
are real.

## Degraded operation behavior

If the charge path fails:

- hydrogen replenishment stops
- vessel may still operate later on remaining stored hydrogen plus battery if
  dispatch permits
- berth-side battery charging may still continue if safely separated

If the discharge path to the fuel cells fails:

- the vessel may need to fall back to battery-dominant degraded return mode
- dispatch may be blocked or restricted
- storage should remain safely isolated

If storage itself enters unsafe state:

- hydrogen use path is blocked
- emergency isolation logic takes priority
- non-hydrogen functions may remain alive only if safe

## Maintainability requirements

The module should support access to at minimum:

- compressor service points
- dryer or conditioning service points
- manual isolation valves
- pressure sensing points
- relief devices
- manifold inspection points
- cylinder/rack replacement path
- vent-path inspection access

A storage system that cannot be maintained is a bad storage system.

## Monitoring and controls interface

This module shall provide the Monitoring & Controls Module with at minimum:

- storage pressure
- storage temperature trend or representative state
- charge enabled / disabled / tripped
- discharge enabled / disabled / tripped
- compressor ready / running / faulted
- manifold state valid / invalid
- isolation valve state
- relief event flag
- vent-path status where instrumented
- maintenance lockout state
- hydrogen inventory estimate
- trip reason code

## Proof-of-concept expectations

Later proof-of-concept artifacts for this module should make it possible to
inspect:

- whether the charge path is understandable
- whether the storage arrangement is believable for the reference vessel
- whether venting and isolation are treated deliberately
- whether compressor burden and fault sensitivity are visible
- whether supply-to-fuel-cell routing is not hand-waved
- whether maintenance access exists in principle

## Explicit non-claims

This module does **not** claim:

- hydrogen storage is compact or penalty-free
- final hazardous-zone approval
- final dispersion-study approval
- universal vessel compatibility
- liquid hydrogen equivalence
- final structural reinforcement adequacy
- final class-approved rack arrangement

## Summary

The Gas Conditioning & Storage Module is the hydrogen-handling bridge between
production and use in IX-Marine-H2-Retrofit.

Its job is to dry and condition hydrogen, compress it, store it in a weather-
deck-focused marine arrangement, vent and relieve it intentionally, and deliver
it under controlled conditions to the fuel-cell path while keeping storage
penalties, isolation needs, and fault behavior fully visible.
