# Housekeeping Energy Module

## Purpose

This file defines the Housekeeping Energy Module for IX-Marine-H2-Retrofit.

This module exists to keep a very important boundary honest:

small auxiliary or weak-source energy helpers may be useful, but they are not
the vessel's primary propulsion or primary hydrogen-production energy source.

The Housekeeping Energy Module is responsible for:

- preserving critical low-voltage control power
- supporting sensing, logging, and safety-state continuity
- supporting purge-valve and low-power actuator availability where needed
- supporting black-start hold-up behavior
- integrating optional weak or intermittent helper sources without letting them
  distort the repo's main energy claims

## Module role in the full architecture

This module interfaces with:

- the **Fuel Cell / Power Conversion Module**
- the **Monitoring & Controls Module**
- the **Safety & Ventilation Module**
- selected sensors, valves, communications, and low-voltage auxiliaries
- optional small-scale helper sources such as motion-, intake-, or thermal-
  assisted harvesters where justified

It receives or may receive:

- stepped-down DC power from the main battery or main DC bus
- hold-up or supercap support energy
- optional low-power auxiliary harvesting inputs
- control-state commands and reserve policies

It provides:

- 48V-class critical controls power
- continuity for sensing and event logging
- power for low-duty purge / valve / monitoring functions where appropriate
- black-start support continuity before the main system is fully restored
- visibility into auxiliary contribution without overstating it

This module does **not**:

- replace the main propulsion energy path
- replace berth power for electrolysis
- justify a perpetual-motion claim
- convert weak ambient sources into fake primary-energy narrative

## Requirements traceability

This module directly supports:

- **R-014** auxiliary energy harvesters may support controls, sensing, logging,
  purge logic, and housekeeping loads
- **R-015** auxiliary harvesters must not be counted as the principal energy
  source for propulsion or full-scale hydrogen generation
- **R-041** controlled recovery from bus loss
- **R-042** precharge, isolation, and no-backfeed logic at concept level
- **R-080** monitoring and controls concept
- **R-082** lockouts and control continuity for unsafe state handling

It also operates under:

- **A-003** hydrogen is not the only electrical source onboard
- **A-006** auxiliary harvesters are real but limited
- **A-011** hazard visibility over simplicity theater
- **C-001** no perpetual-motion framing
- **C-004** no hidden energy accounting
- **C-008** no single-point safety philosophy

## Locked role definition

The Housekeeping Energy Module is locked to the following role:

**keep the brain, safety awareness, and low-duty support functions alive when
main process power is not yet active, temporarily unavailable, or intentionally
isolated.**

That means the module is allowed to help with:

- critical PLC / controller power
- safety controller and gas detector continuity
- local communications
- event logging
- purge logic support
- low-duty solenoid or valve actuation support where designed
- black-start sequencing support
- maintenance telemetry
- low-power health monitoring

It is not allowed to become a hidden substitute for the main vessel energy
architecture.

## Core design philosophy

This module is locked to the following philosophy:

- always-on critical low-voltage support matters
- weak sources should be accepted honestly and measured honestly
- source-specific conditioning matters
- no source should backfeed in unsafe ways
- reserve logic matters more than decorative harvesting claims
- black-start support must survive even when high-power functions are down
- helper sources are subordinate to the battery-backed control architecture

## Submodule breakdown

The Housekeeping Energy Module is divided into seven submodules:

1. Critical 48V Controls Bus Submodule
2. Hold-Up / Reserve Energy Submodule
3. Source Conditioning and Isolation Submodule
4. Optional Auxiliary Harvester Interface Submodule
5. Low-Duty Actuation Support Submodule
6. Critical Load Priority and Shedding Submodule
7. Housekeeping Supervisory Logic Submodule

---

## 1) Critical 48V Controls Bus Submodule

### Function

Provide the main low-voltage bus for critical controls and safety continuity.

### Locked concept

Use a **48V-class critical controls bus** as the main housekeeping backbone.

### Why 48V class is used

A 48V-class bus is chosen conceptually because it offers a practical middle
ground for:

- control-system continuity
- lower-current distribution than very low-voltage-only arrangements
- reasonable support for low-duty actuators and communications hardware
- compatibility with controlled DC conversion from main energy sources

### Required concept loads

This bus should be capable of supporting at minimum:

- safety PLC or equivalent
- gas detection electronics
- ventilation proving logic
- communications and logging core
- selected local HMIs
- critical sensors
- selected purge or isolation actuators if designed for this voltage class

### Design rule

The critical controls bus must remain alive through startup, shutdown, and
degraded-mode transitions as far as the architecture allows.

---

## 2) Hold-Up / Reserve Energy Submodule

### Function

Provide short-duration continuity and reserve support so the control and safety
layer does not collapse during brief disturbances or startup transitions.

### Locked concept

Use a **battery-backed and optionally supercap-assisted reserve layer** for
hold-up and transition support.

### Why it exists

This submodule exists to support:

- controller continuity during bus disturbances
- clean transition between off-state and active-state logic
- safe completion of critical logging or state memory actions
- short-duration support for low-duty critical actuators
- black-start sequencing continuity

### Design philosophy

This reserve layer should be treated as an engineered part of startup and fault
recovery, not an afterthought.

### Required visibility

At minimum, the architecture should expose:

- reserve healthy / low / unavailable
- hold-up event occurrence
- recharge state
- reserve isolation or fault state

---

## 3) Source Conditioning and Isolation Submodule

### Function

Condition incoming housekeeping-energy sources and prevent unsafe interaction
between them.

### Locked philosophy

Different small sources behave differently.
They must not be merged casually.

### Required concept behavior

This submodule shall support:

- DC conversion from main battery or main bus to housekeeping bus
- source-specific conditioning for optional helper inputs
- no-backfeed behavior
- reverse-current protection where appropriate
- source availability visibility
- clean failover to primary battery-backed support path

### Why it matters

Without source conditioning and isolation, helper sources become a wiring
problem disguised as an innovation.

### Design consequence

All optional helper sources must pass through a disciplined conditioning layer
before touching the housekeeping bus.

---

## 4) Optional Auxiliary Harvester Interface Submodule

### Function

Allow bounded contribution from small-scale helper sources without overstating
their role.

### Locked philosophy

Helper sources are allowed only if their role stays honest.

### Conceptually acceptable helper-source categories

The architecture may include bounded interfaces for:

- hull-motion or internal motion harvester concepts
- intake-flow-assisted helper generation concepts
- small local solar where relevant
- thermally assisted low-power generation where practical
- vibration-assisted sensing power for remote or distributed nodes where useful

### Explicit boundary

These sources may support:

- sensing
- local monitoring
- telemetry
- hold-up contribution
- minor housekeeping offsets

They must not be counted as the main source for:

- primary hydrogen generation
- main propulsion
- major hotel loads

### Measurement rule

If a helper source exists, its contribution must be logged separately so the
repo never hides behind vague "energy assist" language.

---

## 5) Low-Duty Actuation Support Submodule

### Function

Provide bounded support for low-duty actuators needed by controls and safety
logic.

### Examples of relevant loads

This may include:

- purge valve actuation
- low-duty isolation valve command support
- relay or contactor command support
- critical fan or damper control logic support
- local indicator and signaling loads

### Locked philosophy

Actuation support must be treated as duty-bounded and load-aware.

The repo is not allowed to imply that every valve or support actuator can run
indefinitely from a weak-source harvester.

### Design consequence

Where low-duty actuators depend on housekeeping power, the architecture should
show:

- energy source
- reserve requirement
- fail-safe position philosophy
- command authority and lockout behavior

---

## 6) Critical Load Priority and Shedding Submodule

### Function

Define which housekeeping loads stay alive first and which may be shed when
reserve is limited.

### Locked philosophy

Not every low-voltage load is equally important.

### Priority classes

The concept should use at least three priority classes:

#### H-1 — Must stay alive
Examples:
- safety controller
- gas detection electronics
- event logging core
- critical communications
- essential state memory

#### H-2 — Prefer to keep alive
Examples:
- selected local HMI
- extended telemetry
- trend logging extras
- maintenance-support comms

#### H-3 — Shed first
Examples:
- convenience indicators
- nonessential diagnostics
- optional helper-source monitoring extras
- noncritical local displays

### Design rule

Reserve depletion logic should protect H-1 before H-2 and H-3.

---

## 7) Housekeeping Supervisory Logic Submodule

### Function

Coordinate source selection, reserve use, helper-source acceptance, load
priority, and event handling for the housekeeping layer.

### Locked philosophy

The housekeeping layer must be supervised like a real subsystem, not treated as
free background power.

### Required concept behavior

This logic shall support:

- primary source healthy / failed awareness
- reserve healthy / low / exhausted awareness
- helper-source contribution visibility
- critical-load-preservation logic
- load shedding under bounded reserve stress
- black-start support state
- restart and recovery logging
- no-backfeed and source conflict handling

### Minimum lockouts and protective behavior

The module shall prevent or flag at minimum:

- unsafe reverse power path
- loss of H-1 support without alarm
- helper source masquerading as primary source in reporting
- maintenance state conflict
- reserve depletion below protected threshold without entering controlled shed
  logic

### Logging expectations

The supervisory layer should log at minimum:

- primary source transitions
- reserve low events
- reserve support events during disturbances
- helper-source contribution time
- load-shed events
- recovery to normal state

---

## Operating philosophy

### Normal condition

Under normal condition, the housekeeping bus is expected to be fed from the
main battery-backed conversion path, with optional helper sources contributing
only as bounded supplements.

### Disturbance condition

During brief disturbances, the reserve layer should maintain continuity for
critical controls and safety visibility.

### Startup condition

During startup or black-start recovery:

- critical controls bus comes alive first
- safety logic and detectors come alive
- required permissives are checked
- main power path restoration follows later

### Degraded condition

If helper sources disappear, the module still remains credible because its core
support path is battery-backed.

If the primary low-voltage feed is lost, reserve logic preserves critical
functions long enough for controlled recovery or safe-stop behavior.

## Reference concept sizing intent

This module is intentionally not sized like a propulsion plant.

Its scale is conceptually modest relative to the main architecture.

### Design intent

The housekeeping module should be sized for:

- critical control continuity
- detector continuity
- communications continuity
- bounded actuator support
- black-start supervisory continuity

It should not be oversized for theatrical claims about self-power.

### Arrangement consequence

Because the module is smaller and lower power than the main plant, it should be
placed where:

- wiring runs to critical controls are sensible
- service access is preserved
- reserve components are protected
- the layout supports clear inspection and replacement

---

## Footprint and arrangement allowances

### Controls-bus and reserve hardware allowance

Allow approximately:

- **6 ft × 4 ft** concept envelope for the core housekeeping power equipment,
  DC conditioning, and reserve hardware cluster
- additional distributed node space where required for local functions

### Placement philosophy

The module should be arranged:

- near critical controls where practical
- away from casual mechanical damage paths
- with direct access to fuses, isolators, and service points
- without depending on difficult-to-reach compartments

### Wiring philosophy

Critical housekeeping circuits should favor:

- readable segregation
- accessible protection devices
- clear labeling
- avoidable shared-failure paths

---

## Failure modes this module must expect

This module must already assume the following can happen:

- main low-voltage feed loss
- reserve depletion
- converter fault
- source-conditioning fault
- helper-source failure
- false reporting of helper-source contribution
- no-backfeed device fault
- load priority conflict
- actuator command attempted with insufficient reserve
- maintenance isolation left active
- black-start sequence interrupted

Detailed hazard treatment comes later, but the module must be written as if
these are expected realities.

## Degraded operation behavior

If all helper sources disappear:
- no mission claim is lost, because they are not mission-critical by design

If the primary housekeeping feed is lost but reserve remains:
- H-1 functions stay alive
- H-2 may remain alive depending on reserve policy
- H-3 should shed first

If reserve falls below protected threshold:
- load shedding begins
- alarms rise
- unsafe restart or process enable remains blocked

The housekeeping architecture is only credible if it can fail gracefully.

## Maintainability requirements

The module should support access to at minimum:

- DC converters
- reserve storage components
- fuses or protection devices
- source-conditioning hardware
- no-backfeed / isolation devices
- wiring termination points
- local service indicators

A low-power subsystem can still become a maintenance nightmare if neglected.

## Monitoring and controls interface

This module shall provide the Monitoring & Controls Module with at minimum:

- housekeeping bus healthy / degraded / failed
- reserve healthy / low / critical
- primary feed state
- helper-source availability by source type if installed
- helper-source contribution flag
- load-shed active / inactive
- H-1 support guaranteed / threatened
- black-start support ready / not ready
- service / maintenance lockout active / inactive
- fault reason code

## Proof-of-concept expectations

Later proof-of-concept artifacts for this module should make it possible to
inspect:

- whether the housekeeping bus is truly independent enough for control
  continuity
- whether reserve logic is coherent
- whether helper sources are treated honestly
- whether no-backfeed logic is visible
- whether critical-load priority is defined
- whether black-start support avoids circular dependence on the main hydrogen
  path

## Explicit non-claims

This module does **not** claim:

- helper sources can replace the main energy architecture
- wave or intake assist can produce propulsion-scale energy in this repo
- perpetual hydrogen production support from weak ambient sources
- universal helper-source viability on all hulls
- final hardware selection for every helper-source interface

## Summary

The Housekeeping Energy Module is the low-power continuity layer of
IX-Marine-H2-Retrofit.

Its job is to keep controls, sensing, logging, and bounded low-duty support
functions alive through startup, shutdown, and degraded conditions while
allowing optional helper sources to contribute honestly and measurably without
ever being mistaken for the vessel's main propulsion or hydrogen-production
energy source.
