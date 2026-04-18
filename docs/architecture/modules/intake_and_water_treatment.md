# Intake & Water Treatment Module

## Purpose

This file defines the Intake & Water Treatment Module for IX-Marine-H2-Retrofit.

This module is responsible for one of the most easily underestimated parts of
the whole architecture:

turning real harbor seawater into process water that the hydrogen-generation
path can accept without pretending that dirty marine water is a trivial input.

This module exists to solve four problems at once:

- debris and marine-growth exposure at the intake
- serviceability of the intake and pretreatment path
- water-quality protection for downstream hydrogen hardware
- explicit lockout when feedwater quality is not good enough

## Module role in the full architecture

This module sits between the vessel's seawater interface and the Hydrogen
Generation Module.

It provides:

1. protected seawater admission
2. debris rejection
3. pretreatment and suspended-solid reduction
4. desalination
5. polishing to electrolyzer-suitable water
6. clean-water reserve buffering
7. water-quality validation signals to controls

The module does **not** create net vessel energy.
It creates process water.

## Requirements traceability

This module directly supports:

- **R-020** protected seawater intake path
- **R-021** intake exposed to trash, growth, and clogging risk
- **R-022** treated water suitable for selected electrolyzer path
- **R-023** lockout when water quality is unacceptable
- **R-024** flushing / cleanout / backwash support
- **R-060** concept-level footprint and service clearances
- **R-082** bad-water and fault lockout behavior

It also operates under:

- **A-007** treated water is mandatory for the baseline electrolyzer path
- **A-009** maintenance access is first-order
- **C-004** no hidden energy accounting
- **C-007** no maintenance-hostile arrangement

## Operating intent

The module is designed around this truth:

harbor seawater is not clean laboratory feedstock.

It may contain:

- floating debris
- rope fragments
- weeds and marine growth
- silt
- organic load
- oils or surface contamination
- biological fouling potential
- variable salinity and temperature
- suspended solids from port activity

The architecture must therefore reject, isolate, or detect those conditions
instead of assuming them away.

## Locked design philosophy

The module is locked to the following design philosophy:

- passive rejection first
- serviceable filtration second
- automated assistance where justified
- water-quality proof before electrolysis
- failure visibility instead of silent degradation
- clean-water reserve as a buffer against transient upstream faults

## Submodule breakdown

The Intake & Water Treatment Module is divided into seven submodules:

1. Intake Interface Submodule
2. Primary Debris Rejection Submodule
3. Pretreatment Submodule
4. Desalination Submodule
5. Polishing Submodule
6. Clean-Water Buffer Submodule
7. Water-Quality Instrumentation and Lockout Submodule

---

## 1) Intake Interface Submodule

### Function

Admit seawater into the vessel in a protected and serviceable way.

### Locked concept

The intake path should use a **protected sea chest / recessed intake**
philosophy rather than a delicate exposed opening.

### Core design features

- recessed or shielded intake opening
- coarse external guard geometry
- intake lip geometry that discourages large debris entry
- low chance of direct ram ingestion of large trash
- inspection and service access path from inside the vessel where practical
- drain and isolation points

### Design intent

The intake should be arranged so that:

- debris rejection begins before the first fine filtration stage
- the intake does not become a single hidden clog point
- service personnel can inspect the early path without major structural tearout

### Non-claim

This repo does not claim that a single intake geometry prevents all fouling.
It claims only that the intake should be designed to avoid being a fragile
open-mouth collector.

---

## 2) Primary Debris Rejection Submodule

### Function

Stop large debris and reduce the load on downstream treatment hardware.

### Locked concept

Use a **coarse guard + serviceable strainer** approach.

### Recommended concept components

- coarse external guard or grate
- wedge-wire or similarly robust coarse strainer
- removable strainer cassette or basket
- differential pressure indication across the serviceable screen section
- flush or backwash path where practical

### Design logic

This stage is expected to deal with:

- plastic trash
- seaweed
- drift fragments
- rope strands
- larger marine growth fragments
- large suspended solids

### Service intent

The operator should be able to:

- inspect
- remove
- clean
- reinstall

the primary strainer without destroying surrounding structure.

### Failure posture

If the primary debris stage begins to clog, the system should:

- alarm early
- allow planned flush or cleaning
- lock out hydrogen generation before water starvation damages downstream
  equipment

---

## 3) Pretreatment Submodule

### Function

Condition incoming seawater before desalination.

### Locked concept

Use a conservative pretreatment train rather than assuming the desalination
stage can solve everything alone.

### Recommended concept chain

- coarse screened intake feed
- automatic strainer or duplex media / cartridge stage
- suspended solids reduction stage
- pressure monitoring across filters
- sampling points before and after pretreatment

### Design intent

Pretreatment is intended to reduce:

- suspended solids loading
- fouling load on membranes
- maintenance shock on downstream equipment
- rapid degradation of desalination performance

### Instrumentation expectations

The pretreatment section should expose:

- inlet pressure
- outlet pressure
- differential pressure
- flow
- maintenance-required trend
- cleaning or element-change triggers

### Operating truth

Pretreatment consumables and cleaning burden are real operating costs and
must be visible in the repo later.

---

## 4) Desalination Submodule

### Function

Convert seawater feed into low-salinity product water suitable for later
polishing.

### Locked baseline concept

Use a **reverse osmosis-centered desalination path** as the baseline concept
for the reference vessel.

This is selected because it is a mature, inspectable, and physically honest
path for a marine retrofit concept.

### Baseline process intent

The desalination stage should:

- reduce salinity
- reduce dissolved solids to a level suitable for polishing
- produce stable feed for the clean-water buffer
- provide reject handling path visibility

### Concept sizing basis

The reference architecture assumes a process-water demand on the order of
roughly:

- **600 to 800 liters/day** minimum practical need for hydrogen-production
  duty and reserve
- oversized concept allowance to about **250 gallons/day** class so that
  fouling margin, cleaning cycles, and reserve are not ignored

This is a concept allowance, not a final vendor commitment.

### Design consequences

The desalination stage requires:

- feed pumping
- reject handling
- membrane health tracking
- maintenance consumables
- flush and shutdown logic

### Non-claim

This repo does not claim desalination is the dominant energy load.
It is smaller than electrolysis in the full energy picture, but it still
matters and cannot be hidden.

---

## 5) Polishing Submodule

### Function

Bring desalinated water to the quality needed by the selected electrolyzer
path.

### Locked concept

Use a **post-RO polishing stage** with conductivity-based acceptance logic.

### Recommended concept elements

- deionization or equivalent polishing stage
- final conductivity measurement
- optional pH verification where relevant
- clean-water sample point
- replacement / regeneration maintenance access

### Why this matters

The repo is not allowed to act as though slightly cleaned seawater is good
enough for the baseline electrolyzer path.

The polishing stage is part of the core protection logic for:

- stack life
- contamination control
- water-quality interlock integrity

### Lockout rule

If product-water quality is out of bounds, the electrolyzer shall remain
inhibited.

That lockout is mandatory, not optional.

---

## 6) Clean-Water Buffer Submodule

### Function

Provide a clean-water reserve between the treatment train and the hydrogen
generation hardware.

### Locked concept

Use a **clean-water day tank / buffer tank** concept.

### Why it exists

The clean-water buffer allows the system to:

- decouple short transients in treatment performance from electrolyzer startup
- support controlled startup checks
- avoid immediate process collapse from a short upstream disturbance
- store verified-quality water
- make water inventory visible to controls and operator

### Design expectations

The buffer should support:

- level measurement
- low-level lockout
- drain and cleanout
- contamination awareness if possible
- no hidden dead-leg stagnation trap where practical

### Startup use

Electrolysis startup should require:

- minimum clean-water reserve above threshold
- valid recent quality check
- no active contamination alarm

---

## 7) Water-Quality Instrumentation and Lockout Submodule

### Function

Measure water-path health and enforce electrolyzer protection.

### Locked instrumentation set

The concept should include at minimum:

- intake flow indication
- pretreatment differential pressure
- desalination health indication
- product-water conductivity
- clean-water tank level
- maintenance-needed indicators tied to treatment stages

### Core lockouts

The Hydrogen Generation Module shall remain blocked if any of the following
are true:

- product-water conductivity out of range
- clean-water reserve below minimum
- pretreatment path in severe blockage or maintenance state
- desalination path unavailable
- active leak or major ventilation fault in hydrogen process spaces
- maintenance bypass active without approved override state

### Alarm behavior

Water-related alarms should use at least three classes:

- advisory trend warning
- action required before next generation cycle
- immediate lockout / process stop

### Philosophy

The point is not to produce a pretty dashboard.
The point is to stop bad water from quietly becoming hydrogen-system damage.

---

## Reference concept sizing and layout allowances

These are concept-stage allowances for the reference vessel.

### Intake and pretreatment envelope

Allow roughly:

- **8 ft × 6 ft** for intake-adjacent pretreatment hardware cluster
- internal service access for basket or cassette removal
- drain and flush routing
- safe access for inspection

### Desalination and polishing envelope

Allow roughly:

- **8 ft × 6 ft** main process skid area
- additional local envelope for consumables and clean-water tank interface
- service access in front of replaceable elements

### Clean-water buffer allowance

Assume a dedicated clean-water reserve sized to support:
- startup
- short upset tolerance
- maintenance discipline

The exact tank volume is left to later detailed sizing, but it must be large
enough to avoid a fragile start-stop process rhythm.

### Recommended placement philosophy

- low in vessel where practical
- near centerline where practical
- near drainage and service paths
- close enough to the electrolyzer to avoid absurd plumbing runs
- not buried behind unrelated equipment

---

## Failure modes this module must expect

This module must be designed with the expectation of at least the following
failure or degradation modes:

- intake blockage
- gradual fouling
- sudden debris loading
- strainer differential pressure rise
- pretreatment consumable saturation
- desalination degradation
- polishing exhaustion
- bad-water feed to clean-water buffer attempt
- sensor drift or failure
- maintenance omission
- leakage in water-treatment skid
- freeze or thermal issue if climate requires protection

These hazards are developed in dedicated hazard files later, but this module
must already assume they are real.

## Degraded operation behavior

If this module degrades, the system should be able to do one of the following
depending on severity:

- continue monitoring only
- continue battery charging while blocking hydrogen generation
- continue stored-hydrogen vessel operation without replenishment
- enter maintenance-required berth state
- force process lockout

The water-treatment path should not be allowed to fail silently and still feed
the electrolyzer.

## Maintainability requirements

The module should be arranged so that routine service items can be accessed
without major vessel teardown.

That includes, at minimum:

- coarse strainer removal path
- cartridge or element replacement path
- membrane service path
- conductivity probe access
- isolation valve access
- drain and flush access

Routine service hostility is a design flaw.

## Monitoring and controls interface

This module shall provide the Monitoring & Controls Module with at least:

- intake available / unavailable
- blockage advisory / blockage severe
- pretreatment differential pressure status
- desalination available / unavailable
- product-water in-spec / out-of-spec
- clean-water reserve low / healthy
- maintenance due flags
- active bypass or service state

## Verification intent

Later proof-of-concept work for this module should make it possible to inspect:

- whether intake protection is coherent
- whether service access exists
- whether water quality can actually block electrolysis
- whether fouling and blockage are visible in the logic
- whether reserve water buffering is treated seriously

## Explicit non-claims

This module does **not** claim:

- universal suitability for all port water qualities
- zero fouling
- zero maintenance burden
- zero membrane replacement burden
- raw seawater direct-feed viability as the baseline path
- final class approval of any intake arrangement

## Summary

The Intake & Water Treatment Module is the seawater-to-clean-water backbone of
IX-Marine-H2-Retrofit.

Its job is to admit real harbor seawater, reject debris, reduce fouling load,
desalinate and polish the feed, buffer clean water, and block electrolysis when
water quality is not good enough.

That is the only honest way to begin the hydrogen path.
