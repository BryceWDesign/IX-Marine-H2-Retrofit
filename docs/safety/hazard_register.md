# Hazard Register

## Purpose

This file defines the concept-stage hazard register for IX-Marine-H2-Retrofit.

It exists to make the repository answer the hard question directly:

**What can go wrong, what triggers it, what detects it, what does the system do,
what is the likely consequence if it is missed, and what barriers are supposed
to stand in the way?**

This file is not a class-approved HAZID, HAZOP, FMEA, or bow-tie package for a
real vessel.
It is the concept-stage master hazard register that the rest of the repo must
stay consistent with.

## Scope

This hazard register covers the named hazard cases already locked into the repo,
including:

- hydrogen leak
- ignited release
- ventilation failure
- seawater intake blockage
- water-quality drift damaging the electrolyzer
- compressor overtemperature / abnormal mechanical state
- purge failure
- sensor failure
- false-negative gas detection vulnerability
- blackout / black-start recovery failure
- flooding or spray ingress into hydrogen spaces
- maintenance error states

This file also includes a small number of closely related cross-cutting hazard
cases that are necessary to keep the system logic coherent.

## Hazard treatment philosophy

This file is built on the following rules:

- arrangement is the first barrier
- detection is not enough without action
- no single barrier is trusted for critical hydrogen risk
- restart after major event is deliberate, not casual
- degraded operation must be explicit
- every major hazard should have:
  - initiating mechanisms
  - detection paths
  - automatic system actions
  - design barriers
  - operational barriers
  - residual consequence statement

## Severity and likelihood language

To keep this file readable, consequence is expressed qualitatively:

- **High consequence** — serious personnel hazard, serious vessel hazard, or
  major operational loss
- **Moderate consequence** — major mission disruption, equipment damage, or
  bounded personnel / vessel exposure if handled correctly
- **Lower consequence** — nuisance, contained disruption, or recoverable loss
  with limited escalation potential

Likelihood is not numerically claimed in this repo because no vessel-specific
frequency study has been completed.

## Hazard fields

Each hazard record contains:

- **ID**
- **Hazard**
- **Primary initiating mechanisms**
- **Primary detection paths**
- **Automatic system response**
- **Design barriers**
- **Operational barriers**
- **Residual consequence if barriers fail**
- **Module link**
- **Traceability notes**

---

## H-001 — Hydrogen leak in hydrogen-bearing enclosure or supply path

### Hazard
Uncontrolled release of hydrogen from conditioning, manifold, storage, or
fuel-cell supply path.

### Primary initiating mechanisms
- fitting or seal failure
- tubing or hose failure
- valve-seat leakage
- maintenance misassembly
- vibration-induced loosening
- component fatigue or damage
- improper isolation-state transition

### Primary detection paths
- hydrogen gas detectors in relevant enclosure
- enclosure pressure or extraction anomaly
- pressure decay / unexpected pressure trend
- abnormal compressor or supply behavior
- operator observation if external leak is visible

### Automatic system response
- escalate alarm tier
- stop affected hydrogen process segment
- isolate relevant storage or supply path
- block restart
- maintain or command required ventilation if safe and available
- enter ESD-2 or higher depending on severity and location

### Design barriers
- minimize threaded joints where practical
- weather-deck storage preference
- readable manifold layout
- enclosure extraction
- manual isolation access
- no-backfeed / no ambiguous flow path logic

### Operational barriers
- leak-test discipline after maintenance
- formal lockout/tagout
- no casual override of gas trip
- pre-departure readiness checks

### Residual consequence if barriers fail
**High consequence** due to potential accumulation and ignition risk.

### Module link
- Gas Conditioning & Storage Module
- Safety & Ventilation Module
- Monitoring & Controls Module

### Traceability notes
Supports:
- R-050
- R-051
- R-052
- R-053
- R-054
- R-055

---

## H-002 — Ignited hydrogen release

### Hazard
Hydrogen release ignites in or near affected enclosure, manifold zone, or
service area.

### Primary initiating mechanisms
- leak followed by ignition source exposure
- inadequate isolation after leak
- energized equipment remaining active in affected zone
- uncontrolled maintenance or hot-work violation
- abnormal vent interaction with ignition source

### Primary detection paths
- flame detection
- rapid temperature rise
- gas alarm history preceding ignition
- operator visual confirmation
- abnormal pressure / event state

### Automatic system response
- immediate escalation to ESD-3
- isolate hydrogen sources as required
- trip fuel cells and hydrogen production path
- de-energize nonessential affected-zone equipment
- preserve only essential safety / communications functions where safe
- log major-event state and block restart

### Design barriers
- separation from occupied zones
- weather-deck storage preference
- outward relief / vent philosophy
- ignition-aware equipment arrangement
- short readable hydrogen routing
- gas-safe or gas-managed machinery integration approach

### Operational barriers
- hot-work controls
- restricted access during service
- emergency drill and response procedure
- maintenance gas-freeing rules

### Residual consequence if barriers fail
**High consequence** for personnel, vessel, and mission.

### Module link
- Safety & Ventilation Module
- Gas Conditioning & Storage Module
- Fuel Cell / Power Conversion Module

### Traceability notes
Supports:
- R-053
- R-054

---

## H-003 — Loss of required ventilation in hydrogen-bearing enclosure

### Hazard
Required extraction or ventilation for a hydrogen-bearing space or enclosure is
lost while hazardous accumulation remains possible.

### Primary initiating mechanisms
- fan failure
- fan power loss
- blocked duct
- failed airflow proving
- control logic fault
- maintenance isolation left active

### Primary detection paths
- fan-status signal
- airflow / differential-pressure proving
- detector trend
- motor fault indication
- controls state mismatch

### Automatic system response
- inhibit electrolysis in affected zone
- inhibit compression in affected zone
- inhibit or stop hydrogen charging / discharge path as applicable
- maintain safety-state visibility
- block restart until ventilation proof returns

### Design barriers
- dedicated extraction for critical zones
- segregated ventilation philosophy
- high-point extraction approach
- serviceable ventilation equipment
- ventilation proving logic

### Operational barriers
- fan inspection and service
- startup permissive checks
- maintenance-state control
- detector bump-test discipline

### Residual consequence if barriers fail
**High consequence** if combined with undetected leak;
**moderate consequence** if no release occurs but operation continues unsafely.

### Module link
- Safety & Ventilation Module
- Hydrogen Generation Module
- Gas Conditioning & Storage Module

### Traceability notes
Supports:
- R-051
- R-052
- R-054

---

## H-004 — Seawater intake blockage or severe fouling

### Hazard
Seawater intake path becomes sufficiently blocked or fouled that process water
availability degrades or collapses.

### Primary initiating mechanisms
- debris ingestion
- marine growth buildup
- rope or plastic obstruction
- neglected strainer service
- backflush failure
- sea chest fouling

### Primary detection paths
- intake flow loss
- pretreatment differential pressure rise
- cavitation or abnormal pump behavior
- operator inspection
- low clean-water reserve trend

### Automatic system response
- alarm and maintenance state
- block or stop electrolysis if water-path integrity is insufficient
- allow battery charging only if independent and safe
- preserve stored-hydrogen operation logic if dispatch permits

### Design barriers
- protected intake
- coarse debris guard
- serviceable strainer cassette
- pretreatment monitoring
- clean-water day tank buffer
- backflush / cleanout path where practical

### Operational barriers
- inspection schedule
- service countdown visibility
- pre-generation water-path health checks

### Residual consequence if barriers fail
**Moderate consequence** due to loss of replenishment capability and possible
upstream equipment stress; higher if bad-water feed reaches electrolyzer.

### Module link
- Intake & Water Treatment Module
- Monitoring & Controls Module

### Traceability notes
Supports:
- R-020
- R-021
- R-023
- R-024
- R-054

---

## H-005 — Water-quality drift damaging electrolyzer or forcing unsafe run

### Hazard
Process water quality degrades below acceptable threshold, threatening stack
life or unsafe continued hydrogen generation.

### Primary initiating mechanisms
- polishing exhaustion
- RO degradation
- contamination ingress
- wrong maintenance state / bypass
- conductivity sensor issue
- operator error

### Primary detection paths
- conductivity out-of-range
- polishing service due state
- treatment-train fault
- water-quality mismatch trend
- controls lockout status

### Automatic system response
- hard electrolyzer lockout
- safe stop if degradation occurs during operation
- event logging
- restart block until water quality restored and permissives satisfied

### Design barriers
- post-treatment polishing stage
- clean-water day tank
- mandatory conductivity gate
- no casual direct feed to electrolyzer
- serviceable treatment hardware

### Operational barriers
- service countdown logic
- maintenance checklists
- no bypass-as-normal operation
- operator-visible lockout reason

### Residual consequence if barriers fail
**Moderate to high consequence** due to stack damage potential and loss of
replenishment capability.

### Module link
- Intake & Water Treatment Module
- Hydrogen Generation Module
- Monitoring & Controls Module

### Traceability notes
Supports:
- R-022
- R-023
- R-030
- R-054
- R-082

---

## H-006 — Compressor overtemperature / abnormal mechanical state

### Hazard
Hydrogen compressor overheats, vibrates excessively, or enters unsafe mechanical
state during charging operation.

### Primary initiating mechanisms
- thermal overload
- lubrication or internal mechanical problem
- cooling issue
- control fault
- blocked downstream path
- abnormal duty cycle
- bearing failure precursor

### Primary detection paths
- temperature monitoring
- vibration monitoring or abnormal mechanical-state indication
- motor current anomaly
- discharge pressure abnormality
- faulted compressor status

### Automatic system response
- stop compressor
- isolate charge path as required
- stop or ramp down upstream hydrogen production safely
- latch fault
- block automatic restart

### Design barriers
- conservative compressor sizing
- cooling / thermal monitoring
- readable service access
- relief-path integration
- interlock with storage-path readiness

### Operational barriers
- service schedule
- vibration and temperature trend review
- no forced run against unresolved fault

### Residual consequence if barriers fail
**Moderate to high consequence** due to pressure-system fault escalation and
loss of replenishment capability.

### Module link
- Gas Conditioning & Storage Module
- Monitoring & Controls Module
- Safety & Ventilation Module

### Traceability notes
Supports:
- R-031
- R-053
- R-054

---

## H-007 — Purge failure or incomplete gas clearing

### Hazard
Required purge or gas-clearing step does not complete, yet startup or service
continues as if the state were safe.

### Primary initiating mechanisms
- purge valve failure
- blocked purge path
- incorrect valve state
- control logic fault
- operator bypass
- flow confirmation failure

### Primary detection paths
- purge incomplete flag
- valve-state mismatch
- pressure not decaying as expected
- flow-switch or process-state mismatch
- startup permissive denial

### Automatic system response
- block fuel-cell startup
- block related hydrogen-process startup
- alarm and log
- require purge completion or maintenance action before restart

### Design barriers
- purge-state logic
- valve-state confirmation
- explicit startup permissives
- dedicated purge-path concept

### Operational barriers
- maintenance procedure discipline
- no forced startup around unresolved purge fault
- service training

### Residual consequence if barriers fail
**Moderate to high consequence** depending on affected volume and subsequent
ignition or leak conditions.

### Module link
- Safety & Ventilation Module
- Fuel Cell / Power Conversion Module
- Monitoring & Controls Module

### Traceability notes
Supports:
- R-053
- R-054
- R-082

---

## H-008 — Sensor failure or critical instrumentation loss

### Hazard
Critical sensor or detector fails, drifts, or reports stale/false data in a way
that undermines safe operation.

### Primary initiating mechanisms
- detector failure
- wiring failure
- calibration loss
- communications fault
- controller I/O fault
- environmental damage
- power continuity loss

### Primary detection paths
- heartbeat / health status loss
- disagreement between sensors
- impossible or stale values
- failed bump-test or calibration check
- controls self-diagnostics

### Automatic system response
- degrade or inhibit affected function based on criticality
- block startup where critical measurement is required
- log sensor fault
- maintain visibility of degraded instrumentation state

### Design barriers
- redundant sensing for critical hydrogen safety cases
- separable safety supervision layer
- detector-health monitoring
- state logging

### Operational barriers
- bump-test routine
- calibration intervals
- maintenance countdown
- fault review before restart

### Residual consequence if barriers fail
**Moderate to high consequence** because instrumentation failure can mask other
hazards.

### Module link
- Safety & Ventilation Module
- Monitoring & Controls Module
- All major process modules

### Traceability notes
Supports:
- R-054
- R-055
- R-082
- R-083

---

## H-009 — False-negative gas detection vulnerability

### Hazard
Hydrogen release occurs, but gas detection does not trigger or triggers too
late.

### Primary initiating mechanisms
- detector failure or misplacement
- inadequate detector count
- drift not detected by maintenance
- local flow / ventilation masking
- release in poorly monitored geometry
- maintenance omission

### Primary detection paths
There is no single perfect direct detection for this hazard once the detector
has failed.
The concept therefore depends on layered secondary indicators:

- detector self-health and bump-test history
- enclosure ventilation anomaly
- pressure trend anomaly
- mass-balance inconsistency
- adjacent detector behavior
- manual gas-testing during maintenance

### Automatic system response
- inhibit startup when critical detector health is not proven
- treat detector-health loss as degraded or locked-out state where required
- preserve alarm visibility for detector fault itself

### Design barriers
- multiple detectors in critical zones
- detector placement aligned to likely accumulation path
- high-point monitoring
- enclosure extraction
- non-sensor barriers such as arrangement, venting, and isolation

### Operational barriers
- mandatory bump-test program
- calibration program
- no operation with unresolved detector-health issues in critical zones

### Residual consequence if barriers fail
**High consequence** because other protective layers may be degraded without
operator awareness.

### Module link
- Safety & Ventilation Module
- Monitoring & Controls Module

### Traceability notes
Supports:
- R-054
- R-055

---

## H-010 — Blackout or failed black-start recovery

### Hazard
Main power is lost and the vessel cannot restore enough control, safety
visibility, and power-path readiness to recover safely.

### Primary initiating mechanisms
- bus undervoltage or bus collapse
- battery reserve depleted too far
- housekeeping reserve failure
- converter fault
- logic sequence stall
- simultaneous fault with hydrogen-start permissives blocked

### Primary detection paths
- main bus loss
- reserve low or critical state
- startup-sequence stall
- black-start ready / not-ready state
- event log discontinuity or recovery alarms

### Automatic system response
- preserve housekeeping bus if possible
- restore safety controls first
- restore gas detection and required ventilation proof first
- block unsafe advance to hydrogen use if prerequisites are missing
- show explicit recovery-block reason

### Design barriers
- protected reserve margin
- battery-first black-start philosophy
- staged recovery sequence
- low-voltage housekeeping continuity
- explicit startup permissives

### Operational barriers
- black-start drill and test
- reserve-protection discipline
- no dispatch that destroys protected startup margin

### Residual consequence if barriers fail
**Moderate to high consequence** depending on vessel location and concurrent
hazards.

### Module link
- Fuel Cell / Power Conversion Module
- Housekeeping Energy Module
- Monitoring & Controls Module

### Traceability notes
Supports:
- R-041
- R-054
- R-083

---

## H-011 — Flooding or spray ingress into hydrogen-related equipment zone

### Hazard
Water, spray, humidity, or localized flooding reaches a hydrogen-related cabinet,
enclosure, or critical support subsystem in a way that compromises safe
operation.

### Primary initiating mechanisms
- spray ingress
- washdown intrusion
- drain blockage
- seal failure
- compartment wetting
- storm / weather exposure beyond intended protection
- piping leak

### Primary detection paths
- water ingress sensor
- humidity anomaly
- cabinet conductivity probe
- operator inspection
- enclosure fault state
- local protection trip

### Automatic system response
- isolate affected electrical or hydrogen process segment
- block startup or continue only if safe unaffected path exists
- preserve alarm visibility
- escalate to higher shutdown state if hazard grows

### Design barriers
- weather-rated enclosure philosophy
- raised coaming / drainage concept
- weather-deck storage preference
- cabinet placement away from obvious splash pathways
- drain-path visibility

### Operational barriers
- drain inspection
- weather-exposure procedure
- washdown control near sensitive equipment
- maintenance seal checks

### Residual consequence if barriers fail
**Moderate to high consequence** depending on affected equipment and combined
faults.

### Module link
- Safety & Ventilation Module
- Gas Conditioning & Storage Module
- Monitoring & Controls Module

### Traceability notes
Supports:
- R-054

---

## H-012 — Maintenance error state

### Hazard
Equipment is left in maintenance configuration or reassembled incorrectly, and
the vessel attempts normal operation.

### Primary initiating mechanisms
- valve left in wrong state
- maintenance lockout not cleared correctly
- detector not restored
- purge path misassembled
- electrical connector left loose
- service bypass left active
- incomplete post-maintenance checkout

### Primary detection paths
- maintenance-state flag
- valve-state mismatch
- detector-health fault
- startup permissive failure
- operator checklist exception
- abnormal process behavior on startup attempt

### Automatic system response
- block startup
- identify conflicting maintenance state
- log lockout reason
- require deliberate clear / restore sequence

### Design barriers
- maintenance-mode state in controls
- visible manual isolation positions
- accessible inspection points
- no buried service items
- startup permissives tied to restored state

### Operational barriers
- lockout/tagout
- post-maintenance checklist
- independent verification where appropriate
- maintenance training

### Residual consequence if barriers fail
**Moderate to high consequence** depending on subsystem involved.

### Module link
- Monitoring & Controls Module
- Safety & Ventilation Module
- All process modules

### Traceability notes
Supports:
- R-054
- R-082

---

## H-013 — Battery reserve depletion below protected startup / return margin

### Hazard
Battery is dispatched so deeply or is degraded so severely that black-start,
critical-control continuity, or safe degraded return capability is no longer
credible.

### Primary initiating mechanisms
- excessive dispatch draw
- failed reserve logic
- operator override culture
- battery condition degradation
- inaccurate SOC estimate
- prolonged degraded operation

### Primary detection paths
- reserve threshold crossing
- dispatch classification downgrade
- black-start readiness false
- battery protection / health alarms
- event log of reserve incursions

### Automatic system response
- degraded dispatch classification
- load shedding
- startup restrictions
- mission block if reserve falls below hard minimum

### Design barriers
- protected reserve band
- battery placement as core asset, not convenience
- black-start-first architecture

### Operational barriers
- dispatch policy
- reserve review
- degraded-mode training

### Residual consequence if barriers fail
**Moderate consequence** that can escalate to high if combined with other faults
or emergency return needs.

### Module link
- Fuel Cell / Power Conversion Module
- Housekeeping Energy Module
- Monitoring & Controls Module

### Traceability notes
Supports:
- R-011
- R-041
- R-081
- R-082

---

## H-014 — Berth power unavailable or unhealthy during planned replenishment

### Hazard
The vessel reaches berth expecting hydrogen generation or recharge support, but
the electrical interface is unavailable, unstable, or unsuitable.

### Primary initiating mechanisms
- shore power outage
- incompatible or faulted berth interface
- connection failure
- operational restriction at berth
- emergency stop relationship unresolved

### Primary detection paths
- berth power unhealthy status
- connection verification failure
- startup permissive denial
- operator / shore interface status

### Automatic system response
- block electrolysis
- allow battery charging only if separately valid
- force planning decision toward backup hydrogen loading or reduced dispatch

### Design barriers
- explicit berth-power prerequisite
- dual-path replenishment strategy
- controls visibility of interface health

### Operational barriers
- berth readiness checks
- contingency replenishment plan
- dispatch policy tied to inventory and berth outcome

### Residual consequence if barriers fail
**Lower to moderate consequence** as a direct safety issue, but high operational
impact.

### Module link
- Operations / berth interface
- Monitoring & Controls Module
- Hydrogen Generation Module

### Traceability notes
Supports:
- R-070
- R-071
- R-100

---

## Cross-hazard observations

The most important cross-hazard truths in this register are:

1. hydrogen leak risk is never managed by a single barrier
2. bad-water protection is as much a system-integrity issue as a chemistry issue
3. black-start reserve is a safety issue, not just an availability issue
4. maintenance state is one of the most credible initiating mechanisms in the
   whole architecture
5. berth dependency is operationally central and should not be hidden
6. weather-deck storage helps, but it does not erase hydrogen hazard
7. a readable arrangement is itself a safety feature

## What later files must do

Later safety, proof-of-concept, BOM, and assembly files must support this hazard
register by showing:

- where barriers physically live
- how the controls logic enforces them
- what maintenance or operator actions support them
- what the proof path is for each major barrier
- where the concept still has unresolved real-world approval dependencies

## Explicit non-claims

This file does **not** claim:

- numerical risk acceptance
- final SIL, PL, or equivalent safety integrity assignment
- final class hazard acceptance
- vessel-specific dispersion results
- vessel-specific quantitative risk analysis
- that every listed barrier is already validated in the real world

It is the concept-stage hazard backbone for the repo.

## Summary

The IX-Marine-H2-Retrofit hazard register makes the system's ugly truths
visible:

hydrogen can leak, ignite, and become dangerous; water quality can quietly
damage the core process; compressors, sensors, ventilation, and maintenance can
fail; black-start can collapse if reserve is abused; and berth dependence can
wreck the operating rhythm.

The architecture is only credible if the rest of the repo behaves as though
these hazards are real.
