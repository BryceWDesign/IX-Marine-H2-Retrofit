# Layout and Arrangement Basis

## Purpose

This file defines the concept-stage arrangement basis for IX-Marine-H2-Retrofit.

It exists to answer the practical question that always kills vague retrofit
concepts:

**Where does all of this actually go, how much space does it take, how much
weight does it add, and what arrangement rules keep the vessel from becoming a
maintenance and stability problem?**

This file does not claim class approval or final yard drawings.
It locks the arrangement logic for the reference vessel so the repo stays
physically honest.

## Scope

This file covers concept-stage allowances for:

- tank volume
- electrolyzer footprint
- desalination footprint
- ventilation space
- hazardous-zone layout placeholders
- fuel-cell room or machinery integration philosophy
- weight-change allowances
- center-of-gravity and stability implications
- maintenance access envelope

## Requirements traceability

This file directly supports:

- **R-031** gas drying, isolation, pressure management, and storage control
- **R-032** storage arranged for venting, isolation, and maintenance access
- **R-033** storage volume and mass treated as first-class penalties
- **R-060** concept-level allowances for volume, footprint, and service
  clearances
- **R-061** center-of-gravity and stability effects treated as mandatory
- **R-062** routine service components should be replaceable without major
  teardown
- **R-063** manual isolation devices remain reachable
- **R-071** berth-side demand and replenishment logic reflected in arrangement
- **R-073** strong dependency on port procedures and shore-side coordination

It also operates under:

- **A-002** harbor / port utility vessel focus
- **A-009** maintenance access is first-order
- **A-012** concept-stage numbers are reference-vessel numbers
- **C-006** no fake class certainty
- **C-007** no maintenance-hostile arrangement

## Reference arrangement philosophy

The arrangement philosophy for the reference vessel is locked as follows:

- put **hydrogen storage high and outboard only as much as necessary**, but
  prefer **weather-deck near-centerline placement**
- put **battery mass low and near centerline**
- put **water-treatment hardware low and serviceable**
- put **electrolyzer and gas-conditioning hardware in a protected process zone**
  with rational service access
- keep **accommodation and control-adjacent spaces gas-safe where practicable**
- route **venting upward and away from routine occupancy**
- design for **inspection and removal paths from day one**
- never trade serviceability away for pretty block diagrams

## Arrangement zones

For concept purposes, the reference vessel is divided into six arrangement
zones.

### Z-1 — Weather-deck hydrogen storage zone

Primary use:
- compressed hydrogen rack
- protected manifold enclosure
- vent / relief routing interface

Arrangement intent:
- above main enclosed machinery spaces where practicable
- near centerline where practicable
- away from routine congregation points
- away from accommodation openings and HVAC intakes
- protected from direct impact and line-handling interference

### Z-2 — Hydrogen process room / process skid zone

Primary use:
- electrolyzer
- immediate gas-liquid separation interface
- selected conditioning equipment
- process isolation and instrumentation

Arrangement intent:
- enclosed, controlled-access machinery zone
- near water-treatment output and electrical feed
- arranged for ventilation, inspection, and safe isolation

### Z-3 — Water treatment zone

Primary use:
- pretreatment
- desalination
- polishing
- clean-water day tank
- drains and flush hardware

Arrangement intent:
- low in vessel where practical
- near sea chest / intake plumbing
- near drainage
- not buried behind unrelated machinery

### Z-4 — Fuel-cell and main electrical conversion zone

Primary use:
- 2 × 125 kW fuel-cell modules
- DC distribution
- conversion hardware
- cooling interfaces

Arrangement intent:
- protected machinery-adjacent zone
- serviceable front access
- short connection paths to main DC bus and propulsion interfaces
- kept as gas-safe or gas-managed as arrangement allows

### Z-5 — Low battery / power reserve zone

Primary use:
- 500 kWh LFP battery
- associated isolation and monitoring hardware

Arrangement intent:
- as low as practical
- close to centerline
- structurally supported
- protected from casual damage
- supportive of vessel stability rather than harmful to it

### Z-6 — Controls / housekeeping / safety core zone

Primary use:
- central controls
- safety I/O
- housekeeping energy hardware
- logging and HMI support

Arrangement intent:
- protected from spray and impact
- short path to critical cabling
- not embedded inside hydrogen-bearing volumes

## Locked concept arrangement

The baseline arrangement for the reference vessel is:

- **weather deck**
  - hydrogen storage rack
  - vent mast / relief path
  - protective framing and manifold enclosure

- **upper machinery-adjacent interior**
  - electrolyzer and process skid
  - gas-conditioning support hardware where enclosure logic supports it
  - dedicated ventilation hardware as required

- **lower machinery / utility level**
  - water treatment skid
  - clean-water reserve
  - battery system
  - part of main electrical conversion path where practical

- **protected electrical / controls area**
  - controls core
  - housekeeping power hardware
  - logging and interface equipment

This arrangement is chosen because it keeps the heaviest compensating mass low
while pushing the more hazardous compressed storage out of deep enclosed
volumes.

## Tank volume allowance

### Locked concept allowance

The reference concept assumes:

- **gross hydrogen mass target:** about 90 kg
- **usable hydrogen mass target:** about 80 kg
- **storage pressure class:** 350 bar
- **internal gas volume order-of-magnitude:** about 135 to 140 ft³
- **installed rack envelope:** about 230 to 280 ft³

### Arrangement interpretation

The installed rack envelope includes more than just cylinder volume.
It must also cover:

- structural rack framing
- manifold routing
- protective shielding
- service clearance at key points
- relief and instrumentation interface
- access for inspection and replacement

### Placement rule

The storage rack should be treated as a **weather-deck equipment package**, not
as loose cylinders placed wherever empty volume happens to exist.

## Electrolyzer footprint allowance

### Locked concept allowance

Allow approximately:

- **20 ft × 10 ft** main process-room envelope for the electrolyzer skid and
  immediate process interfaces
- **3 ft** preferred front service aisle
- **2 ft** minimum side access where service is expected
- overhead or extraction path for major service actions
- local access to isolation points and instrumentation

### What this envelope includes

This envelope is intended to cover:

- PEM electrolyzer skid
- immediate power-conditioning interface
- immediate water-feed interface
- local instrumentation
- startup / shutdown service access
- partial gas handoff interface

### What it does not include

This envelope does not automatically include the full compressor, vent mast, or
full storage rack arrangement.
Those are handled separately.

## Desalination and water-treatment footprint allowance

### Locked concept allowance

For the treatment path, allow approximately:

- **8 ft × 6 ft** intake-adjacent pretreatment and filtration cluster
- **8 ft × 6 ft** desalination and polishing skid cluster
- dedicated clean-water day tank space
- local access for filter and element service
- drain and flush routing space

### Arrangement implication

This hardware belongs low in the vessel where practical because it is:

- service-intensive
- water-bearing
- logically near sea chest and drains
- useful as low-placed mass compared with topside hydrogen storage penalty

## Ventilation space allowance

### Locked concept allowance

Reserve approximately:

- **6 ft × 8 ft** for dedicated extraction equipment and immediate support
  hardware where forced ventilation is required
- **4 ft × 4 ft** for vent / relief mast plan allowance
- enough local cabinet and duct routing volume that detector placement,
  extraction paths, and service access are not compromised

### Design rule

Ventilation and vent routing are not allowed to be treated as leftover space
problems.
They must be deliberate arrangement drivers.

### Routing rule

Vent routing should avoid:

- routine occupancy paths
- accommodation openings
- casual HVAC intake conflict
- trapped upward dead-end geometry inside enclosed spaces

## Hazardous-zone layout placeholders

### Honest boundary

Final hazardous-zone extents for a real vessel require a proper leak and
dispersion study plus class review.

### What is locked now

For concept layout discipline only, the repo will use the following placeholders
unless a later bounded file refines them:

- **10 ft horizontal keep-clear** around active vent or service point concept
- **20 ft vertical keep-clear** above vent outlet concept
- no routine personnel station inside those placeholder envelopes
- no accommodation opening or HVAC intake deliberately placed inside those
  placeholder envelopes

These are not approval distances.
They are arrangement guardrails.

## Fuel-cell room / machinery integration philosophy

### Locked philosophy

The reference arrangement should target a **gas-safe or gas-managed fuel-cell
machinery integration concept** rather than placing hydrogen-bearing equipment
casually throughout the vessel.

### Arrangement intent

The fuel-cell area should:

- be physically understandable
- preserve service access
- remain close to main electrical conversion path
- keep hydrogen-bearing supply hardware controlled and visible
- avoid unnecessary mixing with accommodation or routine occupied spaces

### Concept allowance

Allow approximately:

- **2 × (8 ft × 4 ft)** local module envelope for fuel-cell modules
- additional service and cooling access space
- local isolation access
- clear route for cooling and electrical interfaces

## Weight change allowances

### Added-system concept allowances

For concept-stage arrangement and stability thinking, use the following
order-of-magnitude installed weights:

- hydrogen rack + supports: **10,000 to 14,000 lbs**
- electrolyzer + compressor + dryer + BoP: **14,000 to 20,000 lbs**
- fuel-cell modules + cooling + DC/DC: **6,000 to 8,000 lbs**
- 500 kWh LFP battery + containment: **9,000 to 13,000 lbs**
- water treatment + tanks + controls: **2,000 to 4,000 lbs**
- ventilation / gas / fire / ESD hardware: **2,000 to 4,000 lbs**

### Gross added weight

Total gross added weight allowance:
**43,000 to 63,000 lbs**

### Removal credit possibility

If converting from a conventional diesel arrangement, removal of legacy
equipment may offset part of that burden, for example:

- main diesel engines
- exhaust hardware
- reduction gears
- diesel tanks and support hardware

That removal credit is vessel-specific and must not be assumed blindly.

### Net added weight concept target

For planning purposes, a defensible net added weight range is:

**15,000 to 30,000 lbs**

This is still a serious vessel-impact number and must not be minimized.

## Center-of-gravity and stability implications

### Locked reality

This architecture adds a real vertical-center-of-gravity penalty because
compressed hydrogen storage is intentionally placed high enough to support safer
venting and access.

### Countermeasure philosophy

The concept relies on these countermeasures:

- battery placed low and near centerline
- water treatment placed low
- fuel-cell and power-conversion hardware placed low or mid-low
- removal of some legacy high / distributed equipment where possible
- near-centerline storage preference rather than casual outboard placement

### Concept guardrails

Until a real vessel stability package exists, the repo uses the following
guardrails:

- do not accept **more than about 10% loss of GM** without deeper redesign
- do not accept **more than about 4 inches KG rise** without deeper redesign
- require later lightweight survey and updated stability package for any real
  vessel application

These are concept guardrails, not approval results.

### Honest boundary

Final intact and damage stability are unsolved for any real hull until the
actual vessel is analyzed.

## Maintenance access envelope

### Locked access philosophy

Every major subsystem must have a defined service envelope.
If it cannot be serviced rationally, it is not arranged correctly.

### Minimum concept access targets

The arrangement should preserve at minimum:

- **3 ft** preferred front service aisle for electrolyzer/compressor/dryer
  skids
- **2 ft** minimum side access where routine service is expected
- direct reach to manual isolation valves
- direct reach to detector test or replacement points
- direct reach to strainer and filter removal path
- removable path for compressor and fuel-cell service actions
- crane or extraction path for storage-rack major service or replacement
- protected access to battery isolation and monitoring hardware

### Forbidden arrangement pattern

The architecture must not:

- bury filters behind fixed heavy equipment
- bury storage manifolds where a person cannot inspect them
- place manual isolation where only teardown can reach it
- place service items where live hydrogen-bearing hardware must be disturbed
  unnecessarily to access them

## Structural and routing consequences

### Structural consequence

The arrangement implies later need for:

- rack support structure
- machinery foundations
- deck or compartment reinforcement
- vibration and shock support planning
- protected penetrations and pipe supports

### Routing consequence

The arrangement also implies later need for:

- short rational hydrogen supply paths
- segregated electrical and process routing where appropriate
- drain paths
- vent / relief paths
- cooling paths
- detector and controls cabling paths that remain maintainable

This repo does not claim final structural adequacy, but it does require that
these routing and support burdens stay visible.

## Berth-side arrangement implications

Because the reference concept is berth-supported, the arrangement must also
accommodate:

- berth electrical connection interface
- visible emergency isolation / shutdown point
- operational keep-clear around venting and service interface
- safe access for crew during replenishment
- no casual conflict between mooring operations and hydrogen hardware

## Arrangement review checklist

A proposed arrangement in this repo is only acceptable if the answer to all of
the following is yes:

1. can the hydrogen storage be isolated and vented intentionally
2. can the water-treatment path be serviced without major teardown
3. can the battery be placed low enough to help stability
4. can the electrolyzer be reached for real service
5. can ventilation equipment be inspected and maintained
6. can the fuel-cell path remain understandable and isolatable
7. can routine crew movement avoid obvious hydrogen conflict zones
8. can the arrangement support berth-oriented replenishment honestly
9. can the vessel still be treated as a vessel instead of a trapped machinery
   box

If the answer is no to any of those, the arrangement is weak.

## Explicit non-claims

This file does **not** claim:

- final class-approved arrangement
- final hazardous-zone approval
- final structural reinforcement sufficiency
- final stability acceptance
- universal fit for all harbor vessels
- final vendor packaging or exact crate dimensions
- guaranteed ability to retain all original payload or deck utility

## Summary

The arrangement basis for IX-Marine-H2-Retrofit is built around a simple truth:

compressed hydrogen storage drives topside penalty, so the architecture must
counter it with low battery placement, low water-treatment placement,
maintainable process zoning, deliberate venting, and clear service envelopes.

This file locks the concept-stage volume, footprint, weight, access, and
stability logic that the rest of the repo must respect.
