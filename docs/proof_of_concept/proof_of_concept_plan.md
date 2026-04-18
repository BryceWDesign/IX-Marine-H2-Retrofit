# Proof-of-Concept Plan

## Purpose

This file defines the concept-stage proof-of-concept plan for
IX-Marine-H2-Retrofit.

It exists to turn the repo from a pure architecture study into a staged,
inspectable build-and-test pathway that a serious reviewer can actually follow.

This file answers the question:

**If we were going to prove the architecture in a bounded, honest way, what
would we physically build first, what would we instrument, what would we test,
what would count as success, and what would still remain unproven?**

This is not a shipyard construction release.
It is a disciplined proof path.

## Scope

This file covers:

- proof-of-concept objective
- PoC boundary
- what is physically included
- what is deliberately excluded
- subsystem stack for the PoC
- instrumentation set
- test campaign structure
- pass / fail basis
- known limitations of the PoC

## Requirements traceability

This file directly supports:

- **R-090** proof-of-concept path that can be inspected without hidden
  assumptions
- **R-091** full bill of materials at concept stage
- **R-092** concept-stage assembly and integration guidance
- **R-093** explicit non-claims where proof is incomplete

It also supports verification intent from:

- `docs/verification/verification_strategy.md`
- `docs/safety/hazard_register.md`
- `docs/safety/failure_modes_and_effects.md`
- `docs/safety/shutdown_interlocks_and_safe_states.md`

## PoC objective

The proof-of-concept objective is **not** to build a full vessel.

The proof-of-concept objective **is** to build an integrated, bounded test stack
that can prove the following at concept stage:

1. seawater-derived feedwater can be treated to a guarded electrolyzer-ready
   process path
2. hydrogen generation is correctly blocked when water quality, ventilation, or
   safety permissives are invalid
3. gas conditioning, storage-path logic, and hydrogen-use-path logic are
   understandable and interlocked correctly
4. fuel-cell plus battery hybrid supervisory logic behaves coherently
5. shutdown, degraded mode, logging, and black-start logic are not hand-waved
6. helper sources remain subordinate and do not contaminate primary-energy
   claims

## PoC boundary

The PoC boundary is intentionally smaller than the full vessel architecture.

### Included in the PoC
- intake surrogate and dirty-water simulation path
- pretreatment and water-quality gate logic
- desalination / polishing representative path or emulator-backed equivalent
- clean-water buffer logic
- electrolyzer control path or bounded real electrolyzer subsystem
- gas-path interlocks and compressor-control logic
- bounded hydrogen storage or safe storage-state emulation
- fuel-cell supervisory path or bounded real fuel-cell subsystem
- battery storage and DC-bus control logic
- housekeeping controls bus
- detector, ventilation, alarm, lockout, and ESD logic
- HMI, logging, and dispatch-state logic

### Excluded from the PoC
- full vessel structural integration
- full weather-deck storage installation on a live vessel
- full marine class-approved hazardous-zone validation
- final port-side service interface approval
- unrestricted live maritime operations
- claims of commercial readiness

## PoC philosophy

The PoC is locked to the following philosophy:

- prove the dangerous logic first
- prove the lockouts first
- prove the degraded states first
- use emulation where full live hazard hardware would be unreasonable at this
  stage
- use real measurements where they matter
- never treat the PoC as vessel equivalence

## PoC architecture stack

The PoC should be organized into seven integrated benches or skids.

### PoC-1 — Water intake and fouling simulation bench
Purpose:
- simulate dirty intake conditions
- simulate clogging, differential pressure rise, and flow degradation
- verify treatment lockout behavior

### PoC-2 — Water treatment and quality gate bench
Purpose:
- verify pretreatment, desalination, polishing, and product-water quality logic
- verify hard block on out-of-spec feed to electrolysis path

### PoC-3 — Hydrogen generation control bench
Purpose:
- verify electrolyzer startup permissives
- verify stop behavior on bad water, bad ventilation, and E-stop
- verify session energy accounting

### PoC-4 — Gas conditioning and storage logic bench
Purpose:
- verify compressor permissives
- verify charge-path isolation
- verify storage-state supervision
- verify trip logic without needing full-scale vessel storage installation

### PoC-5 — Fuel-cell plus battery power bench
Purpose:
- verify split-module dispatch logic
- verify battery reserve protection
- verify black-start behavior
- verify degraded operation logic

### PoC-6 — Safety and ventilation bench
Purpose:
- verify gas detector logic
- verify ventilation proving and ventilation-loss response
- verify ESD level escalation
- verify purge logic

### PoC-7 — Integrated controls and HMI bench
Purpose:
- verify state machine
- verify alarm classes
- verify event sequence logging
- verify dispatch classification
- verify blocked-start reason visibility

## Preferred PoC build sequence

The PoC should be built in this order:

1. controls and logging spine
2. housekeeping power and reserve spine
3. water-quality gate and treatment logic
4. electrolyzer permissive logic
5. gas-path and compressor logic
6. battery / DC bus / fuel-cell supervisory logic
7. integrated safety / ESD / HMI path
8. full scripted test campaign

That order matters because the controls spine must exist before complex PoC
behavior is reviewable.

## PoC operating modes

The PoC should support the same broad mode families as the repo:

1. cold / secured
2. housekeeping alive
3. berth readiness
4. water-treatment active
5. electrolysis active
6. hydrogen charging state
7. operational power mode
8. degraded mode
9. maintenance mode
10. emergency shutdown state

The PoC does not need vessel propulsion to prove those state transitions.

## Instrumentation set

The PoC should include at minimum the following instrumentation classes.

### Water-path instrumentation
- intake flow
- differential pressure across strainer / pretreatment stage
- product-water conductivity
- clean-water tank level
- treatment available / unavailable state
- simulated fouling and blockage flags where needed

### Hydrogen-generation instrumentation
- commanded run state
- inhibited / ready / running / stopping / tripped state
- power draw
- cumulative energy consumed
- hydrogen production estimate
- water-quality-valid state
- E-stop state

### Gas-path instrumentation
- compressor ready / run / fault
- charge-path valve state
- storage-state estimate
- pressure state
- trip reason state
- vent / relief event flag

### Fuel-cell / battery instrumentation
- Fuel Cell A state
- Fuel Cell B state
- battery SOC
- battery reserve state
- charge / discharge power
- main DC bus voltage
- degraded-mode flag
- black-start-ready flag

### Safety instrumentation
- hydrogen detector status
- detector health / fault state
- ventilation proof state
- flame or major-event input simulation state
- purge complete / purge fault state
- ingress alarm input
- ESD level

### Controls and logging instrumentation
- current system mode
- active alarms by class
- lockout reason code
- startup blocked reason
- event sequence log
- maintenance mode state
- dispatch classification state

## Live hardware versus emulation posture

The PoC is allowed to mix real hardware and bounded emulation.

### Strong candidates for real hardware in PoC
- strainer and differential-pressure sensing concept
- treatment-state instrumentation
- conductivity measurement
- battery / DC bus logic
- controls hardware
- HMI and logging stack
- low-power ventilation and detector logic
- selected low-power actuators and purge-path devices

### Candidates for bounded emulation or partial-scale representation
- full marine-scale hydrogen storage rack
- full vessel-scale compressor package
- full vessel-scale fuel-cell plant
- final weather-deck release geometry
- full-scale berth electrical interface
- vessel motion and stability effects

### Why emulation is acceptable here
Because the point of the PoC is to prove:
- logic correctness
- interlock correctness
- state behavior
- instrumentation visibility
- failure handling

not to fake a full ship in a lab.

## Core test campaign

The PoC test campaign is locked to six groups.

### Group T-1 — Nominal startup and controlled stop
Prove:
- normal startup path works only when all permissives are valid
- controlled stop reaches correct secured state
- event logging remains coherent

### Group T-2 — Water-path fault tests
Prove:
- clogged intake signal causes correct alarm / inhibit behavior
- bad conductivity blocks electrolysis
- low clean-water reserve blocks startup
- maintenance bypass cannot masquerade as normal state

### Group T-3 — Hydrogen-process fault tests
Prove:
- compressor fault causes correct isolate response
- downstream gas-path loss causes safe stop
- purge-fail blocks startup
- manual valve-state mismatch blocks or trips appropriately

### Group T-4 — Safety and ESD tests
Prove:
- gas alarm escalates correctly
- detector-fault state causes correct startup block
- ventilation-loss causes correct stop / inhibit
- ESD-1, ESD-2, and ESD-3 paths behave distinctly
- restart is blocked after serious trip

### Group T-5 — Power and degraded-mode tests
Prove:
- one fuel-cell module unavailable still yields bounded degraded mode
- battery reserve logic protects black-start margin
- bus loss drives correct recovery sequence
- load shedding preserves critical loads first

### Group T-6 — HMI, logging, and dispatch tests
Prove:
- blocked states explain themselves
- alarm classes are distinguishable
- sequence-of-events record is reconstructable
- dispatch class changes correctly under reduced capability

## Minimum pass criteria

The PoC is only considered credible if all of the following are true:

1. bad-water condition hard-blocks electrolysis
2. ventilation loss hard-blocks affected hydrogen process functions
3. gas-trip logic isolates the correct path and preserves event visibility
4. black-start sequence does not rely on the hydrogen path already being alive
5. degraded mode is explicit and readable
6. event log preserves enough sequence clarity to reconstruct the fault
7. helper-source accounting never appears as main-energy accounting
8. no serious trip auto-restarts without deliberate re-enable path

## Fail / redesign triggers

The PoC must be treated as needing redesign if any of the following occur:

- hydrogen-generation logic can continue after invalid water-quality state
- hydrogen-process logic can continue after required ventilation proof is lost
- critical trip reason is not visible to the operator
- system restarts automatically after an ESD-2 or ESD-3 style event
- reserve logic cannot preserve black-start-support loads
- detector fault can be hidden or ignored without visible degraded state
- maintenance mode can be cleared accidentally or remain hidden
- event sequence is too poor to understand what happened

## Data package expectations

Each PoC test package should include:

- test ID
- objective
- preconditions
- setup
- instrumentation list
- procedure
- expected result
- observed result
- pass / limitation / redesign outcome
- screenshots or log excerpts where appropriate
- requirement links
- hazard links

## PoC limitations

The PoC must explicitly admit what it does not prove.

### The PoC does not prove
- final vessel stability
- full marine vibration survivability
- final weather-deck hydrogen storage acceptability
- final dispersion or hazardous-zone approval
- final port emergency doctrine
- commercial readiness
- fleet economics
- deep-sea applicability

### Why that honesty matters
If the repo treats a skid or bench PoC as vessel proof, the repo becomes weak
and unserious.

## Relationship to later assembly guidance

The PoC is intended to feed later repo sections on:

- concept-stage assembly walkthrough
- concept BOM
- verification evidence packaging
- HMI and controls logic
- future bounded pilot-vessel integration planning

That means the PoC should be built in a way that is:
- inspectable
- repeatable
- instrumented
- clearly labeled
- not dependent on hidden external knowledge

## What this file can and cannot solve

### What it can solve now
It can lock:
- what the PoC is for
- what the PoC includes
- what is real hardware versus bounded emulation
- what tests must exist
- what counts as pass or redesign

### What it cannot finalize now
It cannot finalize:
- exact lab layout
- exact vendor hardware for every bench
- final gas-handling permits
- final shipboard pilot test program
- final marine environmental qualification standard

## Explicit non-claims

This file does **not** claim:
- the PoC is already built
- the PoC proves class approval
- the PoC proves unrestricted vessel readiness
- the PoC proves final economics
- the PoC removes the need for later dockside and vessel testing

It defines the honest proof path.

## Summary

The IX-Marine-H2-Retrofit proof-of-concept is a bounded integrated test stack,
not a pretend ship.

Its job is to prove that the water gate, hydrogen gate, safety gate, power gate,
degraded modes, shutdown logic, and logging logic all behave coherently before
anyone talks as if the architecture deserves trust beyond concept stage.
