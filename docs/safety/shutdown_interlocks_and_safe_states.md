# Shutdown, Interlocks, and Safe States

## Purpose

This file defines the shutdown philosophy, startup interlock logic, safe-state
behavior, and restart rules for IX-Marine-H2-Retrofit.

It exists to answer one of the most important practical questions in the entire
repo:

**When something is wrong, what exactly is allowed to run, what must stop, what
must isolate, what must stay alive, and what has to be proven before the system
is trusted again?**

This file is concept-stage only.
It does not claim class approval or final certified control implementation.

## Scope

This file covers:

- emergency shutdown levels
- startup interlocks
- process permissives
- hydrogen isolation logic
- battery and black-start continuity expectations
- safe-state behavior by subsystem
- restart rules after normal stop, fault, or major event
- interaction between automated logic and crew action

## Requirements traceability

This file directly supports:

- **R-023** electrolyzer blocked on unacceptable water quality
- **R-031** gas drying, isolation, pressure management, and storage control
- **R-041** controlled recovery from bus loss
- **R-042** precharge, isolation, and no-backfeed logic
- **R-050** hydrogen-specific gas detection integration
- **R-051** ventilation proving for hydrogen-bearing spaces
- **R-052** safe state on loss of required ventilation
- **R-053** layered emergency shutdown states
- **R-054** explicit handling for leak, ignited release, purge failure, sensor
  failure, compressor fault, flooding or spray ingress, and blackout recovery
- **R-055** no single unverified sensor as sole barrier
- **R-082** lockouts for water quality, ventilation proof, unresolved gas alarm,
  and maintenance-state conflict
- **R-083** preserve event logs across blackout or restart events

It also operates under:

- **A-003** hydrogen is not the only electrical source onboard
- **A-004** onboard electrolysis is mainly a berth activity
- **A-011** hazard visibility over simplicity theater
- **C-008** no single-point safety philosophy

## Locked shutdown philosophy

The shutdown philosophy for this repo is:

- **stop the hazardous function before trying to preserve convenience**
- **preserve control visibility and event memory whenever safe**
- **isolate hydrogen deliberately**
- **do not collapse the whole vessel unnecessarily if a bounded isolate will do**
- **do not permit automatic restart after serious safety trips**
- **battery-backed controls and reserve energy are part of the safe-state design**

## Safe-state design rules

The architecture is locked to the following safe-state rules.

### Rule SS-001 — Hydrogen processes fail toward isolation
If a hydrogen process loses a critical permissive, the system should trend
toward:
- stopping the active process
- closing relevant isolation devices
- preserving alarm visibility
- blocking restart until the permissive is restored and acknowledged

### Rule SS-002 — Controls and safety visibility should survive where safe
A shutdown is weaker if it blinds the crew.

Where safe and architecturally justified, the system should keep alive:
- safety PLC or equivalent logic
- gas detection
- event logging
- critical communications
- HMI safety status
- required ventilation proving state

### Rule SS-003 — Not every fault deserves the same shutdown depth
Some faults justify:
- controlled stop only

Others justify:
- local process isolate
- hydrogen-wide isolate
- major event emergency shutdown

The repo must distinguish between them.

### Rule SS-004 — Restart is a separate event from stop
The architecture must not treat "fault gone" as identical to "safe to restart."

Restart requires:
- permissive restoration
- trip cause clarity
- acknowledgment or deliberate reset
- correct maintenance state
- valid process and safety state

### Rule SS-005 — Battery reserve is part of shutdown credibility
If the vessel cannot preserve enough low-voltage continuity to supervise the
shutdown and later black-start path, the design is weaker than it looks.

## Shutdown levels

The architecture uses four shutdown levels.

---

## ESD-0 — Controlled stop

### Use case
Normal commanded stop or nonhazardous process shutdown.

### Typical triggers
- end of berth replenishment session
- planned departure transition
- planned process pause
- maintenance entry after safe sequencing

### Required actions
- ramp electrolyzer down normally
- stop compressor in controlled fashion
- complete required purge or post-run transition logic
- close nonessential process valves to normal secured position
- preserve monitoring, logging, and safety visibility
- leave vessel in secured but nonalarm state if no fault exists

### What remains alive
- controls
- logging
- detector visibility
- housekeeping bus
- selected ventilation if required by normal post-run state

### Restart rule
Restart allowed if normal permissives are satisfied.

---

## ESD-1 — Process isolate

### Use case
Bounded process fault where hydrogen generation or charging must stop, but the
entire hydrogen inventory does not need immediate full emergency isolation.

### Typical triggers
- water quality out of spec
- compressor fault during charging
- downstream gas-path unavailable
- ventilation fault in electrolysis-support segment
- process instrumentation fault requiring stop
- berth power lost during active electrolysis session

### Required actions
- stop electrolyzer
- stop compressor
- isolate charge path as required
- preserve stored hydrogen in secured configuration
- keep fuel-cell path available only if unaffected and explicitly safe
- keep controls, detectors, and logging alive
- hold alarm / lockout until cause is cleared

### What remains alive
- housekeeping bus
- controls
- gas detection
- event logging
- battery charging path if separately safe and available
- vessel propulsion path only if unaffected and allowed by dispatch logic

### Restart rule
No automatic restart.
Requires restoration of process permissives and operator/supervisory re-enable.

---

## ESD-2 — Hydrogen isolate

### Use case
A hydrogen-specific abnormal condition requires wider isolation of stored or
supplied hydrogen.

### Typical triggers
- confirmed hydrogen leak in a storage/supply/conditioning segment
- unresolved severe gas alarm
- ventilation failure in critical hydrogen-bearing enclosure
- manifold valve-state conflict under hazardous condition
- supply-side abnormal pressure condition
- critical purge failure affecting hydrogen-use path

### Required actions
- close storage main isolation as required
- close affected supply-path isolations
- trip fuel-cell modules if affected by isolated path
- stop electrolysis and compression
- shed nonessential affected-zone loads
- preserve battery-supported degraded return mode if safe
- preserve controls, detectors, and alarm visibility
- latch trip and block restart

### What remains alive
- H-1 housekeeping loads
- safety controls
- logging
- detector and ventilation visibility
- battery-backed degraded maneuver / harbor return if safe and permitted

### What is no longer allowed
- hydrogen charging
- hydrogen discharge in affected path
- fuel-cell operation if supply integrity is not proven
- casual operator reset without diagnosis

### Restart rule
Requires:
- leak cause or isolation reason resolved
- detector and ventilation health restored
- valve-state confirmation valid
- deliberate reset
- startup permissives re-run from safe baseline

---

## ESD-3 — Major event emergency shutdown

### Use case
High-consequence or escalating event where preservation of convenience is
subordinate to hazard control.

### Typical triggers
- ignited hydrogen release
- severe escalating hydrogen leak
- major enclosure hazard
- serious flooding or spray ingress into critical hydrogen equipment zone
- severe detector / safety-state ambiguity during active hazardous condition
- emergency stop command under major event conditions

### Required actions
- isolate all hydrogen sources as required by arrangement
- trip all fuel-cell modules
- stop electrolysis and compression
- de-energize nonessential equipment in affected zones
- preserve only essential safety, alarm, and communications functions if safe
- hold vessel in emergency state
- force crew emergency procedure path
- preserve event memory and critical indications as far as the power architecture
  allows

### What remains alive if safe
- critical controls bus
- event logging
- communications
- selected gas / flame detection if architecture and damage state allow
- emergency lighting / indications if provided outside this repo's main scope

### Restart rule
No restart from ESD-3 without formal deliberate recovery sequence.
The concept assumes post-event inspection and procedural clearance are required.

---

## Startup interlock philosophy

The startup-interlock system is permissive-driven.

No major subsystem shall start unless all relevant permissives are true.

The startup interlocks are grouped into five families:

1. utility and power permissives
2. safety permissives
3. process-state permissives
4. maintenance-state permissives
5. subsystem-specific readiness permissives

## Common permissive families

### Utility and power permissives
- housekeeping bus healthy
- control logic healthy
- required power source available
- main bus state acceptable where relevant
- battery reserve above protected threshold for startup sequence

### Safety permissives
- no active ESD state prohibiting startup
- gas detector health acceptable in affected zones
- no unresolved gas trip in affected zones
- required ventilation proven
- no flame / major-event alarm active
- no unresolved ingress / flooding alarm affecting the subsystem

### Process-state permissives
- required valves in correct position
- required pressure path available
- no purge incomplete state where purge is mandatory
- no conflicting subsystem trip still active
- water quality in spec where required

### Maintenance-state permissives
- maintenance lockout not active
- no active service bypass being treated as normal operation
- required post-maintenance restore state completed

### Subsystem-specific readiness
- compressor healthy
- fuel-cell cooling healthy
- battery contactor and reserve status acceptable
- clean-water reserve sufficient
- downstream gas path ready for charge

## Startup permissive matrix

### Electrolyzer startup minimums
The electrolyzer shall not start unless all of the following are true:

- berth power healthy
- housekeeping controls alive
- no ESD-1/2/3 state affecting generation path
- clean-water quality valid
- clean-water reserve above startup threshold
- required ventilation proven in affected process enclosure
- no active gas trip in affected zones
- downstream gas path available
- compressor path available if charging is expected immediately
- required valves in correct commanded state
- maintenance lockout clear
- no critical instrumentation fault affecting safe operation

### Compressor startup minimums
The compressor shall not start unless all of the following are true:

- hydrogen generation output path valid or storage-top-up mode valid
- required ventilation proven
- no active gas trip in compressor / manifold enclosure
- downstream storage path available
- storage pressure below allowed target threshold
- compressor thermal and mechanical state healthy
- required valves and relief path available
- maintenance lockout clear
- no ESD state prohibiting charging

### Fuel-cell startup minimums
Fuel-cell startup shall not begin unless all of the following are true:

- storage supply path healthy
- required purge completed
- no active gas trip in affected supply path
- no ESD-2/3 state blocking hydrogen use
- battery reserve adequate to support startup and stabilization
- cooling path healthy
- main bus condition acceptable or black-start sequence is in correct stage
- maintenance lockout clear
- no unresolved critical sensor fault affecting fuel-cell safe operation

### Dispatch release minimums
The vessel shall not be released as green dispatch unless all of the following
are true:

- hydrogen inventory above mission threshold
- battery SOC and reserve above dispatch minimum
- no unresolved red-class trip
- no required subsystem in blocked state for the planned mission profile
- crew-visible dispatch class generated and accepted

## Shutdown response matrix

### Water quality out of spec during electrolysis
Minimum required response:
- stop electrolyzer
- log lockout reason
- preserve other unaffected systems if safe
- block restart until conductivity and water-path health restored

### Compressor fault during charge session
Minimum required response:
- stop compressor
- isolate charge path
- stop or hold upstream hydrogen generation safely
- log fault
- block automatic restart

### Required ventilation proof lost in hydrogen-bearing enclosure
Minimum required response:
- stop affected hydrogen process
- block charge or discharge in affected segment
- raise alarm to trip level if required by zone
- preserve detector and controls visibility
- latch fault until ventilation restored

### Confirmed gas alarm in affected hydrogen zone
Minimum required response:
- isolate relevant hydrogen path
- stop affected process
- escalate to ESD-2 unless situation or location requires ESD-3
- preserve battery-only degraded mode only if explicitly safe
- block restart

### Ignited release
Minimum required response:
- escalate to ESD-3
- isolate hydrogen sources
- trip fuel cells
- de-energize nonessential affected-zone equipment
- preserve essential emergency visibility if safe
- hold major-event state

### Battery reserve below protected floor
Minimum required response:
- downgrade dispatch class
- shed lower-priority loads as required
- block high-risk startup sequences
- preserve H-1 loads
- preserve black-start recovery margin if still possible

### Flooding / spray ingress in critical hydrogen cabinet
Minimum required response:
- isolate affected process equipment
- block startup or continue only on unaffected path if safe
- alarm and log
- escalate to ESD-3 if ingress creates broader immediate hazard

## What must stay alive after shutdown

When architecturally possible and safe, the following should survive ESD-0,
ESD-1, and most ESD-2 events:

- event logging
- critical controls bus
- gas detector status
- ventilation proving status
- alarm indication
- dispatch classification memory
- maintenance-state memory
- black-start readiness state

For ESD-3, the same functions should survive only as far as damage state and
power integrity safely allow.

## Subsystem safe states

### Intake & Water Treatment Module safe state
- intake isolated or left in nonhazardous secured state
- pumps off unless required for bounded safe flush
- no feed to electrolyzer
- bad-water lockout preserved

### Hydrogen Generation Module safe state
- electrolyzer off
- output path isolated as required
- no restart permitted without valid permissives
- oxygen-handling path in secured state

### Gas Conditioning & Storage Module safe state
- compressor off
- charge path isolated
- storage in secured isolated condition
- vent / relief path not obstructed
- supply path closed if ESD-2/3 requires it

### Fuel Cell / Power Conversion Module safe state
- fuel-cell modules unloaded or tripped as required
- battery retained for essential continuity and degraded return if safe
- bus state visible
- load shed applied as needed

### Safety & Ventilation Module safe state
- detectors and safety logic alive if safe
- required ventilation continued if beneficial and possible
- safety trip cause latched
- no unsafe auto-clear

### Housekeeping Energy Module safe state
- H-1 loads protected
- H-2 and H-3 shed as needed
- reserve-state visible
- no helper-source exaggeration in reporting

### Monitoring & Controls Module safe state
- trip reason preserved
- state clear to crew
- reset path blocked until permissives restored
- sequence-of-events retained as far as architecture allows

## Restart philosophy

Restart shall follow one of three paths:

### Restart Path A — Normal restart after ESD-0
Allowed when:
- no active fault
- normal startup permissives satisfied
- operator requests restart

### Restart Path B — Controlled restart after ESD-1
Allowed when:
- process fault corrected
- no residual safety trip
- maintenance state clear
- all startup permissives revalidated
- operator or supervisory logic re-enables process

### Restart Path C — Formal recovery after ESD-2 or ESD-3
Required when:
- hydrogen isolate or major event occurred

This path requires at minimum:
- trip reason identified
- safety devices healthy
- detector and ventilation states proven
- valve-state and isolation-state audit
- maintenance lockout clear
- operator deliberate reset
- startup sequence re-entered from known safe baseline
- dispatch class recomputed before release

No major-event restart is casual in this repo.

## Crew-facing meaning

The shutdown architecture must be understandable to crew in plain terms.

The HMI and procedures should make clear:

- what stopped
- why it stopped
- whether the vessel is still operable in degraded form
- whether hydrogen is isolated
- whether restart is blocked
- what must be corrected before restart

A safe state that the crew cannot interpret is weaker than it appears.

## Verification intent

Later proof-of-concept and controls artifacts should prove, at concept stage:

- every listed shutdown level can be entered intentionally
- required subsystems stop or isolate correctly
- protected functions remain alive where intended
- startup is blocked when a required permissive is absent
- restart after ESD-2/3 requires deliberate recovery
- trip reasons remain visible across power disturbance where the architecture
  allows

## Explicit non-claims

This file does **not** claim:

- final PLC programming
- certified ESD implementation
- final valve fail-position selection for every component
- final class-approved shutdown doctrine
- final response times for every device
- that every real vessel will use identical shutdown grouping

It defines the concept-stage safe-state discipline the repo is required to obey.

## Summary

IX-Marine-H2-Retrofit is only credible if its shutdown logic is stronger than
its concept art.

This file locks that discipline:

normal stop is orderly, process faults isolate locally where possible,
hydrogen-specific faults drive wider isolation, major events force emergency
shutdown, critical controls remain alive where safe, and no serious safety trip
gets a casual automatic restart.
