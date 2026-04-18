# Proof-of-Concept Test Matrix

## Purpose

This file defines the concept-stage proof-of-concept test matrix for
IX-Marine-H2-Retrofit.

It takes the higher-level proof plan and turns it into a concrete set of test
cases that can be executed, reviewed, repeated, and linked back to requirements
and hazards.

This file answers the question:

**Exactly what tests should exist if the PoC is going to be taken seriously?**

## Scope

This matrix covers:

- nominal startup and normal-stop tests
- water-path fault tests
- hydrogen-process fault tests
- safety and shutdown tests
- power and degraded-mode tests
- HMI, logging, and dispatch tests

This is a concept-stage matrix.
It does not claim final yard, class, or vessel trial acceptance procedures.

## How to use this file

Each test case below includes:

- **Test ID**
- **Objective**
- **Preconditions**
- **Stimulus / fault injection**
- **Expected system behavior**
- **Primary measured variables**
- **Pass criteria**
- **Requirement links**
- **Hazard / FMEA links**

A future test report should reuse the same test IDs so evidence can be traced
cleanly.

## Test outcome language

The intended outcome labels are:

- **Pass**
- **Pass with limitation**
- **Needs redesign**
- **Invalid / insufficient instrumentation**

These align with `docs/verification/verification_strategy.md`.

---

## Group T-1 — Nominal startup and controlled stop

### T-001 — Housekeeping-only wakeup

#### Objective
Prove that the system can move from cold / secured to housekeeping alive without
accidentally energizing hydrogen processes or main propulsion power paths.

#### Preconditions
- system in cold / secured state
- no active maintenance mode
- no active ESD-2 or ESD-3 state
- housekeeping reserve available

#### Stimulus / procedure
- command transition to housekeeping-alive state

#### Expected system behavior
- critical 48V controls bus energizes
- controls, logging, and safety visibility come alive
- gas detector health becomes visible
- hydrogen generation remains inhibited
- compressor remains off
- fuel-cell startup remains blocked until later permissives are satisfied

#### Primary measured variables
- housekeeping bus voltage
- controls alive state
- detector-health state
- electrolysis state
- compressor state
- fuel-cell state
- event log sequence

#### Pass criteria
- housekeeping state achieved
- no hydrogen process starts
- event log clearly shows state transition
- no ambiguous “partially running” state appears

#### Requirement links
- R-041
- R-080
- R-083

#### Hazard / FMEA links
- H-010
- FME-010
- FME-011

---

### T-002 — Normal berth-readiness to electrolysis-ready transition

#### Objective
Prove that the system can enter a valid berth-ready state and enable
electrolysis only when all required baseline permissives are true.

#### Preconditions
- housekeeping alive
- berth-power source healthy
- water-treatment path healthy
- clean-water reserve above threshold
- detector health normal
- required ventilation proven
- no maintenance lockout

#### Stimulus / procedure
- command berth-readiness checks
- request electrolysis-ready state

#### Expected system behavior
- controls confirm berth-ready state
- operator sees no blocking lockout
- electrolysis-ready state becomes available
- compressor remains in ready state only, not forced running yet

#### Primary measured variables
- berth-power healthy status
- clean-water reserve
- conductivity in-spec status
- ventilation proven status
- detector health status
- startup-ready state
- HMI blocked / unblocked reason field

#### Pass criteria
- electrolysis-ready state reached only when all permissives are valid
- HMI clearly shows ready condition
- no unrelated subsystem falsely trips

#### Requirement links
- R-012
- R-023
- R-051
- R-082

#### Hazard / FMEA links
- H-003
- H-005
- FME-003
- FME-005

---

### T-003 — Controlled end-of-session stop

#### Objective
Prove that a normal replenishment session can stop cleanly without leaving the
system in a confusing or unsafe intermediate state.

#### Preconditions
- electrolysis active
- charge path active
- no active fault

#### Stimulus / procedure
- command normal stop / ESD-0

#### Expected system behavior
- electrolyzer ramps down or stops in controlled manner
- compressor stops in proper order
- charge path closes to secured state
- alarms remain clear
- controls, detector visibility, and event logging remain alive
- system returns to secured or standby state

#### Primary measured variables
- electrolyzer run state
- compressor run state
- valve-state transitions
- event sequence
- final system mode

#### Pass criteria
- clean stop achieved
- no fault or trip alarm caused by normal stop
- final state is readable and secured

#### Requirement links
- R-053
- R-080
- R-083

#### Hazard / FMEA links
- FME-006
- shutdown safe-state basis

---

## Group T-2 — Water-path fault tests

### T-010 — Intake restriction detection

#### Objective
Prove that intake blockage or severe feed restriction is detected and translated
into visible action before water starvation becomes a silent process condition.

#### Preconditions
- water-treatment bench active
- controls and logging active

#### Stimulus / fault injection
- impose controlled flow restriction at intake / strainer surrogate

#### Expected system behavior
- differential-pressure or flow alarm rises
- maintenance-required indication appears
- if restriction crosses severe threshold, electrolysis path is blocked or
  stopped
- fault is logged

#### Primary measured variables
- intake flow
- differential pressure
- severity class of alarm
- electrolysis availability state
- event log time order

#### Pass criteria
- restriction becomes visible before silent collapse
- severe restriction blocks or stops hydrogen generation path
- no false “healthy” water-path state remains

#### Requirement links
- R-020
- R-021
- R-024
- R-082

#### Hazard / FMEA links
- H-004
- FME-004

---

### T-011 — Product-water conductivity out of spec before startup

#### Objective
Prove that bad product-water quality blocks electrolysis startup.

#### Preconditions
- system in berth-ready state
- clean-water reserve available
- electrolysis not yet started

#### Stimulus / fault injection
- force product-water conductivity signal out of allowed range

#### Expected system behavior
- electrolysis startup request is denied
- HMI explicitly shows bad-water lockout
- event log records denial reason
- other unaffected subsystems remain visible and stable

#### Primary measured variables
- conductivity value / state
- startup request state
- lockout reason code
- HMI text / state
- event log sequence

#### Pass criteria
- startup blocked every time bad-water signal is present
- operator sees specific lockout reason
- no hidden bypass occurs

#### Requirement links
- R-022
- R-023
- R-082

#### Hazard / FMEA links
- H-005
- FME-005

---

### T-012 — Product-water conductivity goes out of spec during active generation

#### Objective
Prove that an active hydrogen-generation session stops safely when water quality
goes invalid during operation.

#### Preconditions
- electrolysis active
- no other active fault

#### Stimulus / fault injection
- force conductivity transition from in-spec to out-of-spec

#### Expected system behavior
- electrolyzer commanded to safe stop
- lockout reason latched
- compressor and charge path transition consistently with generation stop
- restart blocked until valid water state restored and re-enable performed

#### Primary measured variables
- conductivity state transition time
- electrolysis stop command
- compressor stop state
- lockout latch state
- event sequence

#### Pass criteria
- active session does not continue after bad-water fault
- stop sequence is visible and logged
- no automatic restart after fault clears without deliberate re-enable

#### Requirement links
- R-023
- R-053
- R-082

#### Hazard / FMEA links
- H-005
- FME-005

---

### T-013 — Low clean-water reserve startup block

#### Objective
Prove that insufficient clean-water reserve blocks electrolysis startup.

#### Preconditions
- berth-ready state
- conductivity valid
- reserve threshold parameter loaded

#### Stimulus / fault injection
- force clean-water level below startup threshold

#### Expected system behavior
- startup blocked
- low-reserve reason visible
- no partial electrolysis start occurs

#### Primary measured variables
- clean-water tank level
- startup request result
- lockout reason
- event log entry

#### Pass criteria
- startup denied consistently
- reason visible and specific

#### Requirement links
- R-023
- R-082

#### Hazard / FMEA links
- H-004
- H-005

---

## Group T-3 — Hydrogen-process fault tests

### T-020 — Compressor fault during active charge

#### Objective
Prove that compressor failure causes the correct safe response in the charging
path and upstream generation path.

#### Preconditions
- electrolysis active
- charge path active
- storage available
- no other fault

#### Stimulus / fault injection
- inject compressor overtemperature or faulted-run signal

#### Expected system behavior
- compressor stops
- charge path isolates as required
- upstream generation stops or transitions to safe stop
- fault latches
- restart blocked until cleared and re-enabled

#### Primary measured variables
- compressor run / fault state
- charge-path valve state
- electrolysis stop state
- fault latch state
- event sequence

#### Pass criteria
- charging does not continue through compressor fault
- upstream stop logic behaves coherently
- operator can reconstruct cause from log and HMI

#### Requirement links
- R-031
- R-053
- R-054

#### Hazard / FMEA links
- H-006
- FME-006

---

### T-021 — Purge incomplete blocks fuel-cell startup

#### Objective
Prove that a missing or incomplete purge state prevents fuel-cell startup.

#### Preconditions
- hydrogen supply path otherwise healthy
- battery reserve sufficient
- no active gas trip

#### Stimulus / fault injection
- force purge-complete signal false or purge-fault state active

#### Expected system behavior
- fuel-cell startup denied
- blocked-start reason visible
- no partial hydrogen-use enable occurs
- log records purge-related block

#### Primary measured variables
- purge state
- startup request state
- fuel-cell state
- lockout reason
- event log

#### Pass criteria
- startup blocked every time purge condition is invalid
- reason visible and specific
- no hidden manual override path in normal operation

#### Requirement links
- R-053
- R-054
- R-082

#### Hazard / FMEA links
- H-007
- FME-007

---

### T-022 — Valve-state mismatch blocks startup

#### Objective
Prove that a wrong manual or commanded isolation-valve state blocks the related
startup or charging action.

#### Preconditions
- otherwise valid startup condition
- controls reading valve-state feedback

#### Stimulus / fault injection
- force one required valve to mismatched position

#### Expected system behavior
- affected startup or charge action denied
- mismatch reason visible
- event logged
- no ambiguous partially enabled state appears

#### Primary measured variables
- valve-state feedback
- requested mode
- lockout reason
- event log
- subsystem ready / not-ready state

#### Pass criteria
- mismatch causes deterministic block
- operator can identify the specific mismatch

#### Requirement links
- R-031
- R-063
- R-082

#### Hazard / FMEA links
- H-012
- FME-013

---

## Group T-4 — Safety and ESD tests

### T-030 — Detector health failure blocks startup

#### Objective
Prove that critical gas-detector health loss blocks startup of affected
hydrogen-process functions.

#### Preconditions
- affected zone otherwise healthy
- no active gas alarm

#### Stimulus / fault injection
- force critical detector fault / heartbeat loss

#### Expected system behavior
- startup denied in affected process segment
- detector-health fault visible
- degraded or lockout state visible
- fault logged

#### Primary measured variables
- detector health
- startup request outcome
- lockout / degraded-state display
- event log

#### Pass criteria
- affected startup blocked
- detector-health fault not silently ignored
- operator sees clear reason

#### Requirement links
- R-050
- R-055
- R-082

#### Hazard / FMEA links
- H-008
- H-009
- FME-008
- FME-009

---

### T-031 — Gas alarm in charging enclosure drives hydrogen isolate response

#### Objective
Prove that a gas alarm in a hydrogen-bearing enclosure causes the correct
shutdown depth and isolation behavior.

#### Preconditions
- active charge session or charging readiness state
- affected zone under detector supervision

#### Stimulus / fault injection
- force gas detector into trip-level alarm in charging enclosure

#### Expected system behavior
- charging path stops
- relevant hydrogen path isolates
- ESD-2 or higher entered according to configured logic
- restart blocked
- controls, logging, and safety visibility remain alive if safe

#### Primary measured variables
- gas-alarm class
- ESD level
- isolation valve states
- compressor state
- electrolysis state
- event sequence

#### Pass criteria
- stop and isolate sequence is correct
- trip reason and ESD level visible
- no casual auto-restart occurs

#### Requirement links
- R-050
- R-053
- R-054

#### Hazard / FMEA links
- H-001
- H-009
- FME-001
- FME-009

---

### T-032 — Ventilation-loss trip in hydrogen-bearing enclosure

#### Objective
Prove that loss of required ventilation blocks or stops the affected
hydrogen-related function.

#### Preconditions
- affected enclosure in operating or startup-ready state
- ventilation proof healthy initially

#### Stimulus / fault injection
- force ventilation proof false or fan-failure state

#### Expected system behavior
- affected process stops or startup is denied
- alarm raised
- restart blocked until ventilation proof restored
- event logged

#### Primary measured variables
- ventilation proof state
- subsystem run state
- alarm class
- lockout state
- event log

#### Pass criteria
- no affected hydrogen function continues after loss of required ventilation
- operator sees ventilation-specific block reason

#### Requirement links
- R-051
- R-052
- R-054

#### Hazard / FMEA links
- H-003
- FME-003

---

### T-033 — Major-event ESD-3 escalation

#### Objective
Prove that a major-event input forces the deepest shutdown state and blocks
restart until deliberate recovery.

#### Preconditions
- system in any active operational or hydrogen-process state
- controls, logging, and safety layers alive

#### Stimulus / fault injection
- inject ignited-release or major-event trigger

#### Expected system behavior
- ESD-3 entered
- hydrogen sources isolated as required
- fuel cells tripped
- nonessential affected-zone equipment de-energized
- major-event state latched
- no restart allowed without formal reset path

#### Primary measured variables
- ESD state
- storage isolation state
- fuel-cell states
- nonessential affected-zone power state
- event log and restart inhibit state

#### Pass criteria
- ESD-3 response is distinct from lower shutdown levels
- restart remains blocked after trigger clears until deliberate reset
- event sequence supports clear post-event reconstruction

#### Requirement links
- R-053
- R-054
- R-083

#### Hazard / FMEA links
- H-002
- FME-002

---

## Group T-5 — Power and degraded-mode tests

### T-040 — Single fuel-cell module failure yields degraded but bounded operation

#### Objective
Prove that loss of one fuel-cell module drives the correct degraded-state logic
instead of full system confusion.

#### Preconditions
- normal operational state
- both fuel-cell modules available initially
- battery SOC adequate

#### Stimulus / fault injection
- force Fuel Cell A fault or unavailable state

#### Expected system behavior
- Fuel Cell A removed from service
- Fuel Cell B remains available if healthy
- dispatch class recalculated
- degraded-mode state visible
- battery remains available for peak support

#### Primary measured variables
- Fuel Cell A state
- Fuel Cell B state
- dispatch class
- degraded-mode flag
- battery discharge support state
- event log

#### Pass criteria
- degraded state is clear and bounded
- no false full-availability indication remains
- system does not collapse unnecessarily

#### Requirement links
- R-011
- R-043
- R-080
- R-081

#### Hazard / FMEA links
- FME-014
- FME-015

---

### T-041 — Battery reserve floor protection

#### Objective
Prove that battery reserve-protection logic prevents critical reserve from being
consumed below protected black-start / return margin without visible downgrade.

#### Preconditions
- battery-powered operation possible
- reserve thresholds configured

#### Stimulus / procedure
- drive simulated mission load until reserve threshold crossed

#### Expected system behavior
- reserve warning appears
- dispatch class degrades as required
- lower-priority loads may shed if configured
- black-start-ready state changes appropriately
- hard floor blocks unsafe further use if required by logic

#### Primary measured variables
- SOC
- reserve state
- dispatch class
- load-shed state
- black-start-ready state
- event log

#### Pass criteria
- reserve protection acts before critical continuity is lost
- degraded status visible
- H-1 loads remain protected

#### Requirement links
- R-011
- R-041
- R-081
- R-082

#### Hazard / FMEA links
- H-013
- FME-011

---

### T-042 — Dead-bus recovery / black-start sequence

#### Objective
Prove that the black-start sequence restores critical visibility first and does
not depend circularly on already-running hydrogen power.

#### Preconditions
- simulated or actual main-bus loss
- housekeeping reserve available

#### Stimulus / procedure
- initiate black-start recovery sequence

#### Expected system behavior
1. housekeeping bus restored or preserved
2. safety controls and logging restored
3. gas detection and ventilation proof become visible
4. main battery bus restored
5. fuel-cell permissives checked
6. fuel-cell startup allowed only if all required conditions are true
7. nonessential loads restored later in sequence

#### Primary measured variables
- housekeeping bus voltage
- controls alive state
- detector status
- main bus state
- fuel-cell start permissive
- recovery sequence timestamps
- event log order

#### Pass criteria
- critical visibility restored before major process restart
- recovery stalls cleanly if a required permissive is missing
- no unsafe auto-advance occurs

#### Requirement links
- R-041
- R-042
- R-083

#### Hazard / FMEA links
- H-010
- H-013
- FME-010
- FME-011

---

## Group T-6 — HMI, logging, and dispatch tests

### T-050 — Blocked-start reason visibility

#### Objective
Prove that a blocked start explains itself clearly to the operator.

#### Preconditions
- one known startup-blocking condition active, such as bad water or detector
  fault

#### Stimulus / procedure
- request blocked startup action

#### Expected system behavior
- startup denied
- HMI shows specific blocking condition
- event log stores specific reason code
- system does not display ambiguous “unavailable” only

#### Primary measured variables
- HMI message
- lockout reason code
- event log content
- subsystem state

#### Pass criteria
- operator can tell exactly what blocked the start
- no generic message hides the true cause

#### Requirement links
- R-080
- R-081
- R-082

#### Hazard / FMEA links
- supports all lockout-related hazards and FMEA cases

---

### T-051 — Sequence-of-events reconstruction after multi-step fault

#### Objective
Prove that the event log preserves enough ordering to reconstruct a compound
fault sequence.

#### Preconditions
- logging active
- system in active or startup-ready state

#### Stimulus / procedure
- inject ordered compound sequence, for example:
  1. ventilation warning
  2. detector fault
  3. startup request
  4. startup denial
  5. maintenance mode entry

#### Expected system behavior
- each event recorded in order
- state transitions visible
- no missing critical event record

#### Primary measured variables
- timestamped event records
- state transitions
- alarm state transitions

#### Pass criteria
- reviewer can reconstruct what happened first, second, and why startup failed
- no critical loss of event order

#### Requirement links
- R-080
- R-083

#### Hazard / FMEA links
- supports all sequence-sensitive hazards, especially H-008 through H-012

---

### T-052 — Dispatch classification downgrade on reduced capability

#### Objective
Prove that dispatch class changes correctly when subsystem capability is reduced.

#### Preconditions
- system initially at green dispatch
- inventory and battery state healthy

#### Stimulus / fault injection
- remove one fuel-cell module or reduce hydrogen inventory below planned mission
  threshold

#### Expected system behavior
- dispatch changes from green to amber or red according to configured logic
- HMI explains the operational consequence
- event log records class change

#### Primary measured variables
- hydrogen inventory estimate
- fuel-cell availability
- dispatch class
- HMI explanatory text
- event log

#### Pass criteria
- dispatch logic changes state correctly
- crew-facing explanation is readable
- no false green classification remains

#### Requirement links
- R-080
- R-081
- R-100

#### Hazard / FMEA links
- H-013
- FME-014
- FME-015

---

### T-053 — Maintenance-mode misuse prevention

#### Objective
Prove that maintenance mode cannot be hidden or cleared accidentally in a way
that allows unsafe startup.

#### Preconditions
- maintenance mode available in controls
- one subsystem selected for maintenance

#### Stimulus / procedure
- enter maintenance mode
- attempt normal startup of affected subsystem
- attempt incomplete exit from maintenance mode

#### Expected system behavior
- startup blocked while maintenance mode active
- incomplete exit still blocks startup
- HMI shows maintenance-state conflict
- event log records maintenance entry and failed startup attempt

#### Primary measured variables
- maintenance-state flag
- startup request outcome
- HMI message
- event log

#### Pass criteria
- maintenance conflict is visible
- unsafe startup not allowed
- maintenance state does not disappear silently

#### Requirement links
- R-082
- R-083

#### Hazard / FMEA links
- H-012
- FME-013

---

## Minimum coverage rule

The PoC is not considered meaningfully complete unless the executed test set
covers all of the following categories at least once:

- nominal startup
- normal stop
- bad-water lockout
- intake / water-path degradation
- compressor-fault handling
- purge-fail startup block
- detector-fault handling
- gas-trip shutdown
- ventilation-loss shutdown
- major-event ESD escalation
- single-module degraded operation
- reserve-protection behavior
- black-start recovery
- dispatch downgrade
- maintenance-state conflict handling
- blocked-start reason visibility
- event-sequence reconstruction

## Required evidence per executed test

Each executed test package should include:

- test ID from this matrix
- date and configuration
- hardware / emulation boundary used
- instrumentation actually active
- preconditions satisfied
- raw measurements or captured states
- screenshots / log extracts as needed
- observed outcome
- pass / limitation / redesign classification
- unresolved notes

## What this matrix can and cannot do

### What it can do now
It can lock:
- which tests must exist
- what each test is trying to prove
- what measurements matter
- what pass actually means

### What it cannot do now
It cannot finalize:
- exact equipment lists for every bench
- final marine witness procedures
- final port or class acceptance tests
- vessel-sea-trial-level acceptance metrics

## Explicit non-claims

This matrix does **not** claim:
- the tests are already run
- passing these tests proves commercial readiness
- passing these tests proves class approval
- every future implementation must use identical thresholds or hardware

It defines the minimum serious PoC test backbone.

## Summary

The IX-Marine-H2-Retrofit PoC only becomes worth trusting if it passes a test
matrix that attacks the real weak points:

bad water, bad ventilation, gas faults, purge faults, compressor faults, module
loss, reserve abuse, blackout recovery, maintenance misuse, and operator-facing
ambiguity.

This file locks that attack plan.
