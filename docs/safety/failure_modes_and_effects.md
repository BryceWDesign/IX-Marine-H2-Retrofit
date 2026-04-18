# Failure Modes and Effects

## Purpose

This file provides a concept-stage FMEA-style view for IX-Marine-H2-Retrofit.

It complements the hazard register by forcing each major failure case into a
more mechanical format:

- what fails
- how it fails
- what the immediate effect is
- what the larger system effect is
- how the failure is detected
- what the automatic response is
- what barriers exist
- what recovery path is allowed
- what verification idea should prove the response path

This file is not a class-approved FMEA and does not claim quantitative failure
rates or certified risk reduction.

## Scope

This file covers the highest-value failure cases for the locked reference
architecture, including:

- hydrogen containment and release failures
- ventilation and purge failures
- water-path failures
- compressor and gas-path failures
- battery / bus / black-start failures
- instrumentation and detector failures
- maintenance-state and configuration errors
- berth-interface failures

## FMEA rating language

To avoid fake precision, this file uses qualitative rating language only.

### Severity
- **S1 — Lower**
- **S2 — Moderate**
- **S3 — High**
- **S4 — Critical**

### Detectability
- **D1 — Easy to detect**
- **D2 — Detectable with normal instrumentation**
- **D3 — Harder to detect or depends on layered indicators**
- **D4 — Difficult without multiple barriers**

### Operational recoverability
- **R1 — Recoverable without major mission loss**
- **R2 — Recoverable with degraded mission**
- **R3 — Requires berth return / repair before normal dispatch**
- **R4 — Emergency-state consequence**

These labels are concept-stage guides, not certified reliability metrics.

## Traceability basis

This file supports and expands:

- `docs/safety/hazard_register.md`
- `docs/architecture/modules/intake_and_water_treatment.md`
- `docs/architecture/modules/hydrogen_generation.md`
- `docs/architecture/modules/gas_conditioning_and_storage.md`
- `docs/architecture/modules/fuel_cell_and_power_conversion.md`
- `docs/architecture/modules/safety_and_ventilation.md`
- `docs/architecture/modules/housekeeping_energy.md`
- `docs/architecture/modules/monitoring_and_controls.md`

---

## FME-001 — Hydrogen tubing, fitting, or seal leak in hydrogen-bearing enclosure

### Failed item
Hydrogen supply tubing, fitting, seal, or manifold joint.

### Failure mode
- loss of containment
- slow leak
- sudden leak after vibration, service error, or damage

### Immediate local effect
Hydrogen enters enclosure or local zone.

### System effect
- gas alarm escalation
- hydrogen process segment must stop
- storage or supply path isolation required
- dispatch may downgrade or block

### Detection means
- enclosure hydrogen detector
- pressure decay trend
- abnormal charge / discharge behavior
- operator observation in some external cases

### Automatic response
- trip affected hydrogen segment
- isolate relevant valves
- inhibit restart
- keep required ventilation active if available
- escalate to ESD-2 or ESD-3 depending on severity

### Existing barriers
- readable routing
- enclosure extraction
- detector coverage
- manual isolation access
- no-backfeed logic
- maintenance lockout / leak-test discipline

### Severity
**S4 — Critical**

### Detectability
**D2 to D3**
Normally detectable, but may degrade toward D3 if detector coverage is poor or
false-negative conditions exist.

### Operational recoverability
**R3 to R4**
Usually berth-return or emergency-state depending on leak scale and ignition.

### Verification idea
- controlled low-rate leak test in safe proof setup
- detector response confirmation
- isolation timing confirmation
- restart inhibit confirmation

---

## FME-002 — Ignited hydrogen release

### Failed item
Hydrogen containment plus ignition control chain.

### Failure mode
Leak occurs and ignition follows.

### Immediate local effect
Flame or high-consequence abnormal event.

### System effect
- major-event shutdown
- hydrogen isolation
- affected electrical zone de-energization
- likely dispatch loss
- possible personnel or vessel hazard

### Detection means
- flame detector
- thermal rise
- gas alarm history
- operator observation

### Automatic response
- ESD-3
- isolate hydrogen sources
- trip fuel cells and charging path
- de-energize nonessential affected-zone equipment
- preserve essential safety and communications if safe

### Existing barriers
- separation and layout
- weather-deck storage preference
- venting philosophy
- ignition control
- gas detection
- hot-work controls
- purge and maintenance controls

### Severity
**S4 — Critical**

### Detectability
**D2**
Usually detectable if ignition occurs, but prevention depends on prior barrier
performance.

### Operational recoverability
**R4**
Emergency-state consequence.

### Verification idea
- flame detector proving
- ESD-3 logic test
- affected-zone de-energization test
- post-event restart inhibit confirmation

---

## FME-003 — Required ventilation fan fails or ventilation proof is lost

### Failed item
Fan, duct, proving device, or ventilation control path.

### Failure mode
Hydrogen-bearing enclosure loses required extraction.

### Immediate local effect
Accumulation risk increases if leak occurs.

### System effect
- electrolysis or compression inhibit
- charging or supply path blocked in affected segment
- startup denied
- possible degraded mode

### Detection means
- fan-status signal
- airflow or differential-pressure proof
- controls mismatch
- maintenance-state conflict
- gas detector trend

### Automatic response
- stop affected process
- inhibit startup
- log ventilation fault
- preserve safety visibility
- block automatic restart

### Existing barriers
- dedicated extraction
- fan proving
- segregated routing
- alarm logic
- maintenance countdown

### Severity
**S3 — High**

### Detectability
**D1 to D2**
Ventilation failure should be easy to detect if proving is correctly designed.

### Operational recoverability
**R2 to R3**
Often recoverable with degraded mission or berth hold, depending on which zone
is affected.

### Verification idea
- simulated fan failure
- airflow-proving loss test
- startup denial confirmation
- process stop confirmation during active operation

---

## FME-004 — Intake blockage or severe seawater fouling

### Failed item
Sea chest, intake guard, strainer, or pretreatment inlet path.

### Failure mode
Flow restriction or loss of usable feedwater.

### Immediate local effect
Reduced water treatment performance or stoppage.

### System effect
- electrolyzer cannot run or must stop
- hydrogen replenishment unavailable
- battery charging may remain possible if independent
- dispatch shifts to stored hydrogen only or reduced mission

### Detection means
- low intake flow
- pressure differential rise
- pump anomaly
- clean-water reserve decline
- operator inspection

### Automatic response
- alarm and maintenance-required state
- block electrolysis if feedwater path insufficient
- preserve non-water-dependent functions where safe

### Existing barriers
- protected intake
- coarse guard
- serviceable strainer
- flush/backwash concept
- clean-water buffer
- service countdown logic

### Severity
**S2 to S3**
Usually operationally severe rather than immediately hazardous, unless combined
with bad-water feed through failed lockout.

### Detectability
**D1 to D2**

### Operational recoverability
**R2 to R3**
Usually recoverable after service, but mission impact can be major.

### Verification idea
- induced restriction test
- differential-pressure alarm test
- electrolysis lockout confirmation
- operator maintenance workflow validation

---

## FME-005 — Product water conductivity out of spec / bad water reaches electrolyzer gate

### Failed item
RO / polishing / conductivity gate chain.

### Failure mode
Water quality degrades below acceptable threshold.

### Immediate local effect
Electrolyzer feed becomes unsafe for baseline PEM process.

### System effect
- electrolyzer lockout or safe stop
- replenishment unavailable
- stack damage risk if lockout fails
- mission may continue only on stored inventory

### Detection means
- conductivity instrumentation
- treatment-train fault
- service due state
- controls lockout reason

### Automatic response
- hard lockout or safe stop
- inhibit restart
- log bad-water event
- maintain visibility to operator

### Existing barriers
- polishing stage
- clean-water day tank
- conductivity gate
- no direct raw-seawater baseline
- maintenance logic

### Severity
**S3 — High**
High mainly because it threatens expensive core equipment and replenishment
capability.

### Detectability
**D1 to D2**
Good if conductivity gate is healthy; worse if instrumentation is degraded.

### Operational recoverability
**R3**
Requires correction before normal hydrogen generation resumes.

### Verification idea
- simulated out-of-spec water signal
- startup inhibit confirmation
- running-process stop logic confirmation
- no-bypass-as-normal logic review

---

## FME-006 — Compressor overtemperature, overspeed, or abnormal vibration

### Failed item
Hydrogen compressor and immediate support systems.

### Failure mode
Mechanical or thermal fault during charge session.

### Immediate local effect
Charging path becomes unsafe or unavailable.

### System effect
- storage replenishment stops
- upstream hydrogen generation may need safe stop
- berth session may fail
- dispatch may rely on remaining inventory only

### Detection means
- temperature alarm
- vibration monitoring
- abnormal current
- discharge pressure anomaly
- compressor fault state

### Automatic response
- stop compressor
- isolate charge path
- stop or hold upstream generation
- latch fault
- block automatic restart

### Existing barriers
- thermal monitoring
- vibration awareness
- cooling interface
- maintenance access
- supervisory interlocks

### Severity
**S3 — High**

### Detectability
**D2**
Should be detectable with proper instrumentation.

### Operational recoverability
**R3**
Usually berth repair or service before normal use.

### Verification idea
- simulated overtemperature trip
- simulated abnormal vibration / fault signal
- upstream safe-stop coordination test
- restart inhibit confirmation

---

## FME-007 — Purge valve or purge path failure

### Failed item
Purge valve, purge path, or purge-state logic.

### Failure mode
Required purge does not occur or is incomplete.

### Immediate local effect
Unsafe startup condition remains possible.

### System effect
- fuel-cell or hydrogen-process startup must be blocked
- false-ready state creates leak / ignition exposure
- dispatch may be delayed or blocked

### Detection means
- purge-complete missing
- valve-state mismatch
- unexpected pressure behavior
- flow-state mismatch
- startup permissive denial

### Automatic response
- block startup
- raise alarm
- log purge failure
- maintain shutdown or safe isolated state

### Existing barriers
- purge-state logic
- valve-state sensing
- startup permissives
- maintenance controls
- operator procedure

### Severity
**S3 to S4**
Potentially critical if startup occurs without safe purge.

### Detectability
**D2**
Reasonably detectable if logic and instrumentation are in place.

### Operational recoverability
**R2 to R3**
Usually recoverable after correction, but dispatch is affected.

### Verification idea
- simulated stuck-valve case
- startup denial proof
- purge completion dependency test
- fault-clear and re-enable path test

---

## FME-008 — Critical gas detector failure

### Failed item
Hydrogen detector, detector power, or detector signal path.

### Failure mode
Detector fails, drifts, or goes unavailable.

### Immediate local effect
Loss of one detection layer.

### System effect
- affected process may need startup inhibit
- degraded safety posture
- maintenance action required
- false sense of safety if poorly managed

### Detection means
- detector heartbeat loss
- self-diagnostic failure
- bump-test failure
- impossible value
- disagreement with peer detector or other indicators

### Automatic response
- alarm detector fault
- degrade or inhibit affected process based on criticality
- log maintenance-required state
- block restart where detector health is mandatory

### Existing barriers
- multi-detector concept in critical zones
- detector health monitoring
- maintenance countdown
- gas-safe arrangement philosophy
- ventilation barriers

### Severity
**S3 — High**
Because it weakens protection against more severe hazards.

### Detectability
**D1 to D2**
Detector failure itself should be detectable if health monitoring exists.

### Operational recoverability
**R2 to R3**
Depends on which zone loses coverage.

### Verification idea
- simulated detector-loss signal
- startup-inhibit logic proof
- degraded dispatch visibility proof
- maintenance countdown / bump-test state review

---

## FME-009 — False-negative gas detection condition

### Failed item
Overall gas-detection assurance chain rather than a single component.

### Failure mode
Leak exists but is not detected promptly.

### Immediate local effect
Hazardous accumulation risk without alarm.

### System effect
- loss of one of the main early-warning barriers
- increased dependence on arrangement, ventilation, and pressure-trend clues
- possible escalation to ignited release

### Detection means
Indirect only:
- detector health history
- pressure anomaly
- ventilation anomaly
- adjacent detector behavior
- maintenance gas-test result
- mass-balance inconsistency

### Automatic response
There is no perfect direct automatic response if the leak is missed.
The architecture therefore responds by:
- blocking operation when detector health is not proven
- using multiple detectors in critical spaces
- relying on isolation and arrangement layers that do not depend on one sensor

### Existing barriers
- multiple detectors
- detector placement strategy
- ventilation
- weather-deck storage preference
- readable routing
- detector testing program

### Severity
**S4 — Critical**

### Detectability
**D4**
By definition, this is one of the hardest conditions to detect cleanly.

### Operational recoverability
**R4** if leak escalates;
**R3** if vulnerability is found before event escalation.

### Verification idea
- detector coverage review
- placement review against likely accumulation geometry
- bump-test discipline review
- mass-balance and pressure-trend alarm logic review

---

## FME-010 — Main DC bus collapse / blackout

### Failed item
Main DC bus, power conversion path, or upstream power continuity.

### Failure mode
Main power distribution becomes unavailable.

### Immediate local effect
Propulsion and major process power paths drop out or become unstable.

### System effect
- vessel may lose normal power-delivery path
- black-start sequence required
- hydrogen process may stop
- safety visibility must transfer to housekeeping power layer

### Detection means
- bus undervoltage
- bus lost state
- converter fault
- contactor-state anomaly
- sequence-of-events log

### Automatic response
- preserve housekeeping bus if possible
- transition to black-start / recovery logic
- stop unsafe process functions
- keep detectors and safety logic alive if reserve permits
- block unsafe restart steps

### Existing barriers
- battery reserve policy
- housekeeping bus
- staged recovery sequence
- protected controls power
- event logging

### Severity
**S3 to S4**
Can become critical if it occurs during maneuvering or alongside other hazards.

### Detectability
**D1**
Bus collapse should be obvious to controls.

### Operational recoverability
**R2 to R4**
Depends on location, reserve state, and concurrent faults.

### Verification idea
- dead-bus recovery simulation
- staged recovery test
- event ordering test
- restart-block-on-missing-permissive test

---

## FME-011 — Black-start reserve depleted below protected minimum

### Failed item
Battery reserve policy, battery availability, or reserve enforcement.

### Failure mode
Battery is too depleted to preserve control continuity and recovery margin.

### Immediate local effect
Recovery capability weakens.

### System effect
- black-start may fail
- degraded return mode may be lost
- dispatch should be downgraded or blocked
- safety visibility can be threatened during later faults

### Detection means
- reserve threshold crossing
- SOC and reserve margin logic
- dispatch downgrade
- black-start-ready false

### Automatic response
- degraded dispatch classification
- load shedding
- mission block if below hard minimum
- preserve H-1 housekeeping loads

### Existing barriers
- protected reserve band
- dispatch logic
- load-shed policy
- battery monitoring
- operator visibility

### Severity
**S3 — High**

### Detectability
**D1 to D2**

### Operational recoverability
**R2 to R3**
Usually recoverable at berth, but major operational penalty.

### Verification idea
- reserve-threshold crossing logic test
- dispatch downgrade proof
- H-1 load-preservation test
- black-start-ready status test

---

## FME-012 — Water or spray ingress into hydrogen-related cabinet or enclosure

### Failed item
Cabinet sealing, drainage, or environmental protection of hydrogen-related
hardware.

### Failure mode
Water or humidity enters protected space.

### Immediate local effect
Electrical fault, detector error, corrosion, or unsafe enclosure condition.

### System effect
- affected hydrogen process segment isolated
- possible loss of compression, detection, or controls in local zone
- startup blocked
- maintenance required

### Detection means
- ingress sensor
- humidity anomaly
- local electrical fault
- operator inspection
- enclosure alarm

### Automatic response
- isolate affected segment
- block startup or continue only on unaffected path if safe
- log ingress event
- escalate if coupled with other faults

### Existing barriers
- weather-rated enclosures
- drainage paths
- raised coaming / cabinet design
- placement away from direct spray
- inspection points

### Severity
**S2 to S3**
Usually moderate, but can be high if it disables critical safety or gas-path
equipment.

### Detectability
**D2**

### Operational recoverability
**R2 to R3**

### Verification idea
- ingress alarm test
- drain-path inspection logic review
- local process isolation response test

---

## FME-013 — Maintenance valve left in wrong state / maintenance lockout conflict

### Failed item
Manual isolation state, service bypass, or maintenance mode discipline.

### Failure mode
System attempts operation with equipment not fully restored to normal service.

### Immediate local effect
Startup conflict, wrong flow path, or hidden unsafe state.

### System effect
- startup blocked if controls catch it
- unsafe operation if controls miss it
- mission delay or equipment damage risk
- hydrogen hazard if wrong path exposes gas

### Detection means
- valve-state mismatch
- maintenance-state active
- startup permissive failure
- abnormal process behavior
- checklist discrepancy

### Automatic response
- block startup
- identify conflicting state
- log lockout reason
- require deliberate maintenance clear sequence

### Existing barriers
- visible valve access
- maintenance-mode logic
- startup permissives
- post-maintenance checklist
- operator procedure

### Severity
**S3 — High**
Can escalate to critical depending on subsystem and missed condition.

### Detectability
**D2 to D3**
Depends on how instrumented the affected path is.

### Operational recoverability
**R2 to R3**

### Verification idea
- simulated wrong-valve-state case
- startup-block proof
- maintenance-mode clearance procedure review

---

## FME-014 — Fuel Cell Module A unavailable

### Failed item
Fuel Cell A or its local support path.

### Failure mode
Module fault, cooling issue, supply-path issue, or startup fault.

### Immediate local effect
Loss of one 125 kW-class module.

### System effect
- reduced hydrogen-derived steady-state capability
- battery must carry more transient or peak burden
- dispatch may downgrade to amber
- vessel may still operate in reduced mode

### Detection means
- module fault
- startup failure
- output power unavailable
- cooling fault
- purge fault

### Automatic response
- isolate or stop failed module
- continue with Module B if safe
- recalculate dispatch class
- preserve degraded-mode visibility

### Existing barriers
- split-module architecture
- battery support
- dispatch classification logic
- cooling monitoring

### Severity
**S2 — Moderate**

### Detectability
**D1**

### Operational recoverability
**R1 to R2**
Often recoverable with degraded mission.

### Verification idea
- single-module failure simulation
- amber dispatch classification proof
- continued reduced-power operation review

---

## FME-015 — Fuel Cell Module B unavailable

### Failed item
Fuel Cell B or its local support path.

### Failure mode
Same family as FME-014.

### Immediate local effect
Loss of second 125 kW-class module path if it is the failed one.

### System effect
Same operational family as FME-014:
- reduced hydrogen-derived capacity
- greater battery reliance
- dispatch downgrade likely

### Detection means
- module fault
- startup failure
- output unavailable
- cooling or purge fault

### Automatic response
- isolate or stop failed module
- continue with Module A if safe
- recalculate dispatch class
- preserve degraded-state visibility

### Existing barriers
- split-module architecture
- battery support
- dispatch logic
- cooling / purge supervision

### Severity
**S2 — Moderate**

### Detectability
**D1**

### Operational recoverability
**R1 to R2**

### Verification idea
- mirrored proof path to Module A failure case

---

## FME-016 — Berth power unavailable or unhealthy during planned electrolysis session

### Failed item
Shore power interface or berth-side electrical availability.

### Failure mode
Planned berth replenishment cannot begin or cannot continue safely.

### Immediate local effect
Electrolysis unavailable.

### System effect
- hydrogen replenishment lost for that session
- operator may need backup hydrogen loading or reduced dispatch
- vessel depends on stored inventory and battery only

### Detection means
- berth-power unhealthy signal
- connection verification failure
- power-quality fault
- operator and shore coordination status

### Automatic response
- block electrolysis
- preserve battery-only or independent charging logic if valid
- generate dispatch-impact visibility

### Existing barriers
- hybrid replenishment strategy
- berth-readiness checks
- operator dispatch logic
- backup loading concept

### Severity
**S2 — Moderate**
Mainly operationally significant rather than intrinsically hazardous.

### Detectability
**D1**

### Operational recoverability
**R2 to R3**
Depends on available stored hydrogen and backup logistics.

### Verification idea
- berth-power loss / unavailability scenario review
- electrolysis start-block confirmation
- dispatch-downgrade proof

---

## Cross-cut priorities

From the FMEA view, the highest-priority concept areas are:

1. hydrogen containment + detection + ventilation as one chain
2. water-quality lockout integrity
3. compressor fault handling
4. battery reserve protection and black-start continuity
5. maintenance-state discipline
6. berth dependency visibility
7. split-module degraded operation clarity

These are the areas where the repo gains the most credibility if the later
proof-of-concept and assembly files remain disciplined.

## What later files must prove

Later files in the repo should prove, at concept stage, that the architecture
can:

- detect the failure modes listed here
- force the intended automatic responses
- preserve visibility of lockouts and degraded states
- avoid casual restart after serious safety events
- preserve enough reserve and control continuity to recover from a blackout
- expose which failures are operationally manageable and which are emergency
  cases

## Explicit non-claims

This file does **not** claim:

- numerical occurrence rates
- certified diagnostic coverage
- SIL or PL assignment
- vessel-specific reliability allocation
- final approved FMEA by class or owner
- full completeness for every possible marine failure case

It is the concept-stage failure-effects backbone for the repo.

## Summary

This FMEA view shows that IX-Marine-H2-Retrofit only works as a serious repo if
it behaves like a real system under failure:

leaks must isolate, bad water must block electrolysis, ventilation loss must
stop hydrogen processes, compressor faults must not cascade silently, battery
reserve must protect recovery, maintenance errors must be visible, and berth
dependency must remain explicit.

If the later repo files fail to honor those truths, the concept weakens fast.
