# Fuel Cell / Power Conversion Module

## Purpose

This file defines the Fuel Cell / Power Conversion Module for
IX-Marine-H2-Retrofit.

This module is responsible for turning stored hydrogen and battery energy into
usable vessel electrical power under a control philosophy that is explicit,
fault-aware, and maintainable.

This module exists to solve the following problems:

- deliver propulsion-supporting electrical power from hydrogen without claiming
  that fuel cells alone solve all vessel dynamics
- absorb transient vessel loads without abusing the hydrogen path
- provide black-start and degraded return capability
- keep the power path readable, isolatable, and measurable
- expose the real integration burden of fuel cells, battery storage, DC
  distribution, and conversion hardware

## Module role in the full architecture

This module sits between:

- the **Gas Conditioning & Storage Module**
- the vessel propulsion and hotel-load electrical interfaces
- the **Safety & Ventilation Module**
- the **Monitoring & Controls Module**
- the low-voltage housekeeping path where needed for coordination

It receives:

- regulated hydrogen from storage
- battery energy from the traction-support storage system
- supervisory commands and lockouts
- shutdown and fault-state commands
- thermal and ventilation status relevant to active equipment

It provides:

- main electrical power to the vessel DC distribution concept
- transient-load handling through battery buffering
- black-start capability
- degraded operating states
- power-path telemetry, fault status, and operating-state visibility

This module does **not**:

- create hydrogen
- remove the need for battery support
- guarantee full vessel capability after every fault
- hide conversion losses or thermal burdens

## Requirements traceability

This module directly supports:

- **R-010** hydrogen plus battery hybrid architecture
- **R-011** battery supports transient maneuvering, black-start, and degraded
  return-to-berth operation
- **R-040** fuel-cell path and battery path to a common electrical distribution
  concept
- **R-041** controlled recovery from bus loss
- **R-042** precharge, isolation, and no-backfeed logic
- **R-043** split-module redundancy where practical
- **R-050** hydrogen-specific gas detection integration where hydrogen is
  present
- **R-053** layered emergency shutdown states
- **R-060** concept-level machinery footprint and service clearances
- **R-061** center-of-gravity and stability treated as mandatory evaluation
  items
- **R-062** maintainability and service access
- **R-080** monitoring and controls concept
- **R-081** alarm prioritization
- **R-082** lockouts for unresolved gas alarm, maintenance conflict, and unsafe
  state mismatch

It also operates under:

- **A-003** hydrogen is not the only electrical source onboard
- **A-009** maintenance access is first-order
- **A-010** split-module redundancy is preferable
- **A-011** hazard visibility over simplicity theater
- **C-004** no hidden energy accounting
- **C-007** no maintenance-hostile arrangement
- **C-008** no single-point safety philosophy

## Locked baseline technology choices

The baseline choices for the reference concept are:

- **2 × 125 kW PEM fuel-cell modules**
- **1 × 500 kWh LFP battery system**
- **common DC distribution concept with controlled conversion to propulsion and
  ship-service loads**

### Why PEM fuel cells are the locked baseline here

PEM fuel cells are used in this concept because they fit the reference vessel
better than a vague generic fuel-cell label.

Reasons:

- compatible with hydrogen storage concept already locked in the repo
- supports modular skid-based integration
- practical for split-module redundancy
- aligns with the port / short-sea vessel duty framing
- fits the repo's hybrid power philosophy

### Why LFP battery chemistry is the locked baseline here

LFP is used as the concept battery baseline because it fits the repo's need for:

- operationally useful energy storage
- transient-load support
- black-start support
- thermal stability emphasis
- credible marine hybrid integration framing

This file does **not** claim these are the best choices for every vessel.
They are the locked baseline choices for this repository.

## Locked reference sizing

The Fuel Cell / Power Conversion Module is locked to the following concept-stage
reference sizing:

- **fuel-cell net continuous capacity:** 250 kW total
- **fuel-cell module split:** 2 × 125 kW
- **battery capacity:** 500 kWh
- **battery role:** transient support, black-start, degraded return, dispatch
  margin, and operational smoothing
- **reference daily vessel energy basis:** approximately 0.9 to 1.1 MWh/day
- **reference propulsion peak envelope:** approximately 400 to 500 kW
- **reference average operating demand:** approximately 120 to 180 kW

These are concept anchors only.

## Core design philosophy

This module is locked to the following philosophy:

- fuel cells handle steady base load
- battery handles fast peaks and recovery support
- black-start must not depend on the hydrogen path being already available
- split modules are preferred over monolithic power hardware
- the main bus must be measurable and isolatable
- degraded operation must be engineered, not improvised
- no reader should have to guess where the power goes during faults

## Submodule breakdown

The Fuel Cell / Power Conversion Module is divided into eight submodules:

1. Fuel Cell Module A
2. Fuel Cell Module B
3. Battery Energy Storage Submodule
4. Main DC Bus and Distribution Submodule
5. DC/DC and Inversion Interface Submodule
6. Thermal Management and Cooling Interface Submodule
7. Black-Start and Recovery Support Submodule
8. Power Supervisory Logic Submodule

---

## 1) Fuel Cell Module A

### Function

Provide one half of the baseline hydrogen-derived electrical generation path.

### Locked concept

Fuel Cell Module A is a 125 kW-class PEM module integrated as an independent
power block with its own:

- hydrogen inlet isolation awareness
- purge coordination
- thermal monitoring
- electrical output status
- fault reporting
- maintenance state visibility

### Why the split matters

Module A exists as a separately controllable block so the vessel can:

- isolate faults
- continue in reduced capability if Module B is unavailable
- stage maintenance more intelligently
- avoid total module dependence for all hydrogen-derived power

### Required visibility

At minimum, Module A should expose:

- ready / inhibited / starting / running / stopping / faulted
- output power
- stack health summary at concept level
- operating hours
- purge complete / purge fault status
- inlet permissive status
- local thermal state

---

## 2) Fuel Cell Module B

### Function

Provide the second half of the baseline hydrogen-derived electrical generation
path.

### Locked concept

Fuel Cell Module B mirrors the same concept intent as Module A and exists for
redundancy, dispatch flexibility, and partial-operability planning.

### Design expectation

The repo should treat Module B as a true independently supervised module rather
than a cosmetic duplication.

### Benefits of the split-module approach

The two-module architecture improves:

- fault isolation
- partial mission capability
- maintenance flexibility
- staged dispatch decisions
- degradation visibility

### Required visibility

At minimum, Module B should expose the same state signals as Module A.

---

## 3) Battery Energy Storage Submodule

### Function

Provide high-response electrical energy support, startup support, emergency
ride-through, and degraded return capability.

### Locked concept

Use a **500 kWh LFP battery system** as the reference vessel's primary
electrical buffer and black-start-capable storage layer.

### Why the battery is essential

The battery is not decorative.

It exists because the vessel needs:

- transient maneuvering support
- rapid load absorption
- dispatch reserve
- fuel-cell transition smoothing
- black-start capability
- partial operation when hydrogen systems are unavailable
- controlled response to bus disturbances

### Locked placement philosophy

The battery should be placed:

- low in the vessel
- near centerline where practical
- in a mechanically protected and serviceable arrangement
- where its weight helps counter higher storage-induced KG effects
- where cooling, isolation, and inspection can be handled rationally

### Required visibility

At minimum, the battery submodule should expose:

- state of charge
- available power state
- charge / discharge rate
- thermal state
- maintenance state
- contactor state
- fault / isolation state
- black-start reserve margin concept

### Operating rule

The battery shall retain a protected reserve band for:

- black-start
- critical control continuity
- degraded harbor return margin

The repo must not quietly allow the battery to be fully consumed by normal
dispatch if that destroys emergency recovery value.

---

## 4) Main DC Bus and Distribution Submodule

### Function

Provide the common electrical backbone that joins fuel-cell output, battery
output, conversion hardware, and vessel electrical consumers.

### Locked concept

Use a **measured, isolatable main DC bus** philosophy.

### Why DC-bus discipline matters

The main DC bus is where sloppy concept repos often cheat.

This repo is not allowed to hide:

- source priority assumptions
- backfeed risk
- precharge burden
- isolation needs
- fault propagation paths
- measurement boundaries

### Required concept functions

The main DC bus shall support:

- power intake from fuel-cell modules
- bidirectional battery interface where appropriate
- precharge behavior
- no-backfeed logic
- selective isolation
- bus voltage visibility
- event logging around bus disturbances
- load-shed logic in degraded states

### Design consequence

The bus must be treated as a control object, not just a line on a diagram.

---

## 5) DC/DC and Inversion Interface Submodule

### Function

Convert main DC-bus power into forms required by propulsion and vessel-service
loads.

### Required concept behavior

This interface shall support:

- propulsion power delivery path
- hotel / auxiliary load delivery path
- staged enable / disable behavior
- no unsafe energization into unresolved fault conditions
- visibility of conversion availability and fault state

### Why this matters

The fuel-cell and battery architecture only becomes real when it can actually
feed vessel loads under controlled rules.

### Design philosophy

The conversion path should favor:

- readable interfaces
- isolated failure behavior
- selective load shedding
- avoidance of cascading trip logic where practical
- maintainable module replacement path

---

## 6) Thermal Management and Cooling Interface Submodule

### Function

Manage the thermal burden of fuel cells, battery system, and associated power
electronics.

### Why it exists

Hydrogen and battery systems are not only electrical systems.
They are also thermal systems.

This submodule exists to support:

- fuel-cell thermal stability
- battery thermal protection
- converter cooling
- overtemperature trip logic
- degraded operation decisions tied to thermal state

### Required visibility

At minimum, the thermal interface should expose:

- fuel-cell cooling healthy / unhealthy
- battery thermal healthy / warning / trip
- power-conversion cooling healthy / unhealthy
- critical overtemperature trip state
- maintenance-needed trend where practical

### Design warning

A concept that ignores cooling routing and serviceability is a weak concept.

---

## 7) Black-Start and Recovery Support Submodule

### Function

Allow the vessel to recover from dead-bus or low-power states without requiring
the main hydrogen path to already be running.

### Locked philosophy

Black-start shall be battery-first.

### Why this matters

If the vessel needs hydrogen consumption hardware already alive in order to
restore the electrical brain that would authorize safe hydrogen use, the
architecture becomes circular and weak.

### Required concept sequence support

This submodule shall support at minimum:

1. critical controls alive
2. safety logic alive
3. gas detection alive
4. ventilation proof where required
5. main battery bus recovery
6. fuel-cell permissive check
7. staged fuel-cell start
8. staged propulsion / nonessential load restoration

### Protected reserve rule

The architecture shall preserve enough electrical reserve to support black-start
logic under bounded dispatch conditions.

---

## 8) Power Supervisory Logic Submodule

### Function

Coordinate the full Fuel Cell / Power Conversion Module across startup, normal
operation, degraded operation, and shutdown.

### Locked philosophy

Power behavior must be state-driven and fault-aware.

### Minimum startup permissives for fuel-cell operation

Fuel-cell startup shall require at minimum:

- hydrogen supply path healthy
- required purge completed
- no active unresolved hydrogen leak trip in affected supply path
- battery state adequate for startup and stabilization support
- bus state healthy or recoverable
- cooling path healthy
- no active maintenance lockout
- no emergency shutdown state prohibiting operation

### Minimum startup permissives for battery dispatch

Battery discharge to main vessel duty shall require at minimum:

- contactor and bus state valid
- thermal state acceptable
- no critical battery protection trip
- no lockout from maintenance state
- reserve protection logic satisfied

### Minimum stop / trip triggers

The module shall command stop, isolate, or degrade on at least:

- unresolved hydrogen leak affecting fuel-cell supply path
- ignited release trip in relevant zone
- battery critical protection trip
- severe cooling failure
- bus fault beyond controlled recovery envelope
- emergency shutdown command
- unresolved purge failure
- critical converter fault
- critical module controller fault

### Logging expectations

The supervisory layer shall log at minimum:

- module start / stop events
- bus up / bus lost events
- battery reserve crossing
- fuel-cell availability time
- degraded-mode entry and exit
- trip reason
- load-shed event
- black-start event

---

## Operating philosophy in vessel service

### Normal operation

In normal service:

- fuel-cell modules carry steady base load
- battery covers high transient demand
- battery smooths response and protects dispatch flexibility
- one or both fuel-cell modules may run depending on mission and state logic

### Low-load / maneuver transitions

During low-load or highly variable operation:

- battery absorbs spikes and dips
- fuel-cell output should avoid unnecessary violent cycling
- controls should prefer stable module behavior over theatrical responsiveness

### Degraded operation

Degraded operation may include:

- single fuel-cell mode
- battery-dominant harbor return
- no-hydrogen dispatch block with hotel systems alive
- reduced-speed / reduced-endurance return
- no-restart until berth inspection

The repo must treat these as real outcomes, not edge-case footnotes.

## Reference footprint and arrangement allowances

### Fuel-cell modules

Allow approximately:

- **2 × (8 ft × 4 ft)** local module envelope, plus service access
- clear front service access for inspection and replacement
- accessible local isolation and instrumentation points

### Battery system

Allow approximately:

- **10 ft × 8 ft** concept envelope for the 500 kWh-class battery installation,
  containment, and immediate service space
- low placement preferred
- protected route for cooling, isolation, and monitoring access

### Main bus / conversion gear

Allow approximately:

- **8 ft × 6 ft** concept envelope for main DC distribution and associated power
  conversion gear, subject to later refinement
- direct access to isolation and maintenance points
- separation from routine damage pathways

### Placement philosophy

The module should be arranged so that:

- the battery helps counter elevated hydrogen-storage CG penalty
- fuel-cell modules remain accessible
- bus and conversion gear are not buried behind unrelated equipment
- cooling paths are rational
- emergency isolation remains physically reachable

---

## Weight and vessel impact awareness

This module carries major vessel-integration consequences.

### Concept-stage weight awareness

The architecture should later preserve visibility into the approximate order of
magnitude for:

- battery system mass
- fuel-cell module mass
- converter and switchgear mass
- cooling and support-system mass

### Stability consequence

The battery is intentionally part of the stability strategy because its low
placement can offset some topside penalty introduced by hydrogen storage.

That does **not** solve final stability automatically.
It only makes the arrangement more defensible.

## Failure modes this module must expect

This module must already assume the following can happen:

- one fuel-cell module unavailable
- both fuel-cell modules unavailable
- battery protection trip
- low state-of-charge reserve conflict
- cooling fault
- bus undervoltage or bus upset
- precharge failure
- contactor-state mismatch
- converter fault
- purge fault blocking fuel-cell start
- operator dispatch request that exceeds safe degraded capability
- maintenance lockout blocking a restart path

Detailed hazard logic is handled later, but this module must be written as if
those failures are real and expected.

## Degraded operation behavior

If one fuel-cell module fails:

- the vessel may remain operable in reduced capability if battery and remaining
  module state allow

If both fuel-cell modules fail:

- battery-only degraded return may still be possible if reserve remains
- dispatch may be blocked depending on mission profile and reserve state

If the battery enters critical protection state:

- fuel-cell-only continuation may be possible only within bounded load
  conditions
- black-start margin may be lost
- vessel speed / load limits may need immediate reduction

The power system is only credible if these consequences are visible.

## Maintainability requirements

The module should support access to at minimum:

- local module isolation points
- battery service isolation
- contactors and fuses where serviceable
- cooling interfaces
- sensors requiring inspection or replacement
- converter service points
- main bus isolation path
- local emergency stop interfaces

Maintenance access is a design requirement, not a courtesy.

## Monitoring and controls interface

This module shall provide the Monitoring & Controls Module with at minimum:

- Fuel Cell A state
- Fuel Cell B state
- battery state of charge
- battery state of health concept summary where available
- battery reserve state
- battery charge / discharge power
- main bus voltage
- main bus healthy / faulted
- converter availability
- black-start ready / not ready
- cooling healthy / warning / trip
- module operating hours
- trip reason codes
- degraded-mode active state

## Proof-of-concept expectations

Later proof-of-concept artifacts for this module should make it possible to
inspect:

- whether the power path is understandable
- whether the battery is genuinely essential rather than cosmetic
- whether split-module fuel-cell logic improves fault handling
- whether black-start logic avoids circular dependence
- whether the main bus is measurable and isolatable
- whether degraded operation is actually defined

## Explicit non-claims

This module does **not** claim:

- fuel cells alone are sufficient for the reference vessel duty envelope
- zero-loss conversion
- universal battery chemistry superiority
- final vendor packaging certainty
- universal marine integration simplicity
- final class-approved electrical design
- elimination of thermal burden or maintenance burden

## Summary

The Fuel Cell / Power Conversion Module is the electrical heart of
IX-Marine-H2-Retrofit.

Its job is to take stored hydrogen and battery energy, deliver controlled vessel
power through a measured and isolatable DC architecture, preserve black-start
and degraded return capability, and keep transient loads, module faults, bus
behavior, and thermal burden fully visible instead of hidden behind a generic
"hybrid power" label.
