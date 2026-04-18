# Verification Strategy

## Purpose

This file defines the concept-stage verification strategy for
IX-Marine-H2-Retrofit.

It exists because the repo is only useful if a reader can answer the question:

**What would we actually test, in what order, with what pass logic, before
claiming this architecture deserves further trust?**

This file does not claim class approval, full-scale vessel certification, or
completed testing.
It defines the staged proof path the repo is built around.

## Scope

This file covers:

- verification philosophy
- staged proof ladder
- what each stage is trying to prove
- what each stage is explicitly not proving
- minimum pass / fail logic categories
- how hazards and requirements connect to tests
- what must be measured rather than assumed

## Requirements traceability

This file directly supports:

- **R-090** include a proof-of-concept path that can be inspected without
  undocumented assumptions
- **R-091** include a full bill of materials at concept stage
- **R-092** include concept-stage assembly and integration guidance clearly
  labeled as non-certified
- **R-093** include explicit non-claims where proof is incomplete
- **R-100** present burden and decision variables honestly
- **R-102** make strategic justification visible instead of overselling

It also supports verification intent behind:

- **R-020** through **R-024** for intake and water-treatment behavior
- **R-030** through **R-033** for hydrogen generation, conditioning, and storage
- **R-040** through **R-043** for fuel-cell, battery, and bus behavior
- **R-050** through **R-055** for safety, ventilation, shutdown, and hazard
  handling
- **R-080** through **R-083** for controls, lockouts, logging, and recovery

## Locked verification philosophy

The verification philosophy for this repo is locked as follows:

- test the ugly parts first
- prove lockouts, not just happy-path operation
- measure energy, pressure, flow, and state transitions explicitly
- verify degraded and fault behavior, not just nominal behavior
- keep each stage bounded and honest
- do not claim vessel-level success from bench-level evidence
- do not skip from paper architecture to “works in the real world” storytelling

## What verification means in this repo

Verification in this repo means answering three kinds of questions:

1. **Does the architecture behave as intended under nominal conditions?**
2. **Does it refuse unsafe or invalid operation under fault or bad-input
   conditions?**
3. **Does it preserve enough visibility and control to fail safely and recover
   in a bounded way?**

If a proposed test does not help answer one of those, it is weak.

## Proof ladder

The repo is locked to a five-stage verification ladder.

1. analytic and architecture-level verification
2. benchtop subsystem verification
3. skid-level integrated proof-of-concept verification
4. dockside / pier-side integration verification
5. bounded vessel operational verification

These stages are intentionally sequential.
A later stage does not replace the need to pass the earlier stage.

---

## Stage 1 — Analytic and architecture-level verification

### Goal

Prove that the architecture is internally coherent on paper before hardware is
trusted.

### Questions this stage should answer

- are the subsystem boundaries clear
- are the major hazards visible
- are the shutdown states coherent
- are the module interfaces understandable
- are the arrangement penalties visible
- does the energy logic avoid fake perpetual-motion claims
- is the reference vessel use case bounded correctly

### Typical artifacts

- requirements basis
- assumptions and constraints
- architecture files
- layout basis
- hazard register
- FMEA-style review
- economics and alternative-pathway decision framing

### What this stage can prove

- conceptual coherence
- traceability
- boundedness of claims
- whether the repo hides obvious contradictions

### What this stage cannot prove

- actual equipment performance
- final vessel safety
- class approval
- real operational availability
- real black-start performance
- real leak / ventilation response timing

### Minimum pass logic

Stage 1 passes only if:

- no core contradiction remains between requirements, layout, hazards, and
  operating concept
- no module depends on a forbidden hidden assumption
- no file quietly claims perpetual or net-positive self-fueling from seawater
  motion alone
- hazard handling exists for the major named cases
- restart and shutdown logic are defined, not implied

---

## Stage 2 — Benchtop subsystem verification

### Goal

Prove that the key subsystem ideas work in bounded isolation before integrated
skid claims are made.

### Subsystem families to verify

1. intake and water-treatment logic
2. water-quality lockout logic
3. electrolyzer permissive and stop logic
4. gas-path conditioning and compression interlocks
5. battery reserve and black-start logic
6. gas detection and ventilation interlock behavior
7. controls logging, alarm, and state management

### Questions this stage should answer

- can bad water actually block electrolysis
- can blocked intake conditions be detected clearly
- can ventilation-loss logic force the required stop
- can gas alarm logic isolate the correct path
- can reserve-protection logic preserve black-start margin
- can event logging preserve cause / effect order under fault tests

### Example benchtop test families

- conductivity-out-of-range lockout simulation
- intake restriction and differential-pressure alarm test
- ventilation fan-failure input test
- gas detector fault and gas-trip simulation
- compressor-fault signal response test
- battery reserve-threshold crossing logic test
- purge-complete / purge-fail startup block test
- HMI blocked-start reason visibility test

### What this stage can prove

- logic behavior
- interlock integrity
- state transition correctness
- instrumentation visibility
- basic fault handling on bounded hardware or emulated inputs

### What this stage cannot prove

- real full-vessel dispersion behavior
- final marine survivability
- full integrated thermal behavior
- true vessel-level endurance or economics

### Minimum pass logic

Stage 2 passes only if:

- every safety-critical startup path can be blocked by at least one invalid
  permissive in test
- every major named fault has a visible logged response
- no critical unsafe function continues running after its hard interlock is
  deliberately invalidated in test
- event sequence is reconstructable after each test case

---

## Stage 3 — Skid-level integrated proof-of-concept verification

### Goal

Prove that the subsystem logic still behaves correctly when several modules are
integrated into a bounded PoC stack.

### PoC integration target

This stage is intended to integrate, at concept scale:

- intake / feedwater surrogate path
- treatment and water-quality gate logic
- electrolyzer-control surrogate or real bounded electrolyzer interface
- gas-conditioning and charge-path logic
- storage-state emulation or bounded safe storage interface
- fuel-cell and battery supervisory logic
- controls, alarms, and event logging
- shutdown and recovery sequence behavior

### Questions this stage should answer

- do module interfaces remain coherent when tied together
- does one fault propagate correctly without creating ambiguous system state
- are degraded modes understandable
- can the controls stack move between berth-generation, secured, and operational
  states coherently
- does black-start sequencing avoid circular dependence

### Test categories

#### Happy-path integrated tests
- normal berth readiness
- clean-water valid startup
- bounded replenishment session
- controlled stop
- pre-departure green dispatch logic

#### Fault-path integrated tests
- water quality invalid during active generation
- compressor fault during active charging
- gas-trip during supply-path readiness
- detector failure before startup
- ventilation-loss during active hydrogen-process state
- battery reserve crossing during simulated mission profile
- black-start recovery after simulated bus loss

### What this stage can prove

- integrated control coherence
- lockout propagation
- degraded-mode clarity
- proof-of-concept instrumentation and control credibility

### What this stage cannot prove

- full vessel dynamic behavior
- real port dispersion / exclusion approval
- final crew-procedure sufficiency in live service
- final structural adequacy

### Minimum pass logic

Stage 3 passes only if:

- every injected major fault produces the intended shutdown depth or degraded
  state
- no ambiguous “half-running” unsafe state persists after fault injection
- black-start sequence can be stepped and blocked safely
- operator can tell, from HMI and logs, why a state is blocked or degraded

---

## Stage 4 — Dockside / pier-side integration verification

### Goal

Prove that the architecture can be integrated into a vessel-adjacent or real
dockside context without collapsing under real interfaces.

### Typical targets

- shore power interface behavior
- berth readiness sequence
- real ventilation behavior in actual installed arrangement
- service / restricted-zone discipline
- real-world detector, alarm, and emergency-stop interface checks
- integrated charging / storage / dispatch preparation behavior
- actual maintenance access validation

### Questions this stage should answer

- can the vessel or dockside platform actually support the physical arrangement
- do access envelopes remain usable in reality
- do berth procedures make sense outside a diagram
- can restricted-zone logic be followed without operational nonsense
- do controls remain understandable with real cable, sensor, and hardware noise

### What this stage can prove

- arrangement realism
- service access realism
- berth-interface plausibility
- operational-procedure rough credibility
- actual installed-system visibility

### What this stage cannot prove

- unrestricted commercial readiness
- final class approval
- all-weather full-service robustness
- long-term lifecycle economics

### Minimum pass logic

Stage 4 passes only if:

- berth readiness sequence can be executed without procedural contradiction
- operators can safely identify service, vent, and restricted zones
- detectors, ventilation, ESD, and controls remain readable in the installed
  environment
- maintenance access is physically possible where the repo says it should be

---

## Stage 5 — Bounded vessel operational verification

### Goal

Prove that the integrated concept can operate on a real vessel in a tightly
bounded mission envelope.

### Mission framing

This is not fleet deployment.
This is a bounded pilot operation for the locked reference vessel class.

### Questions this stage should answer

- can the vessel complete bounded harbor missions on the intended architecture
- do dispatch classifications map to real operations
- do crew procedures hold up under actual use
- does the hydrogen plus battery split behave as intended
- do alarms, degraded modes, and return-to-berth logic remain understandable
- are maintenance and berth burdens within the expected concept envelope

### What this stage can prove

- bounded operational plausibility
- crew / HMI interaction value
- real mission-cycle friction
- actual maintenance and procedure burden discovery

### What this stage cannot prove

- universal fleet readiness
- deep-sea applicability
- universal economic advantage
- universal regulatory acceptance

### Minimum pass logic

Stage 5 passes only if:

- the vessel can complete the bounded mission profile safely
- major alarms and degraded modes remain understandable to crew
- no uncontrolled unsafe state appears during routine operation or scripted
  fault drills
- post-run logs support clear review
- maintenance and berth realities remain inside the repo’s stated honesty bounds

## Verification categories by subsystem

### Intake & Water Treatment Module
Must verify:
- intake restriction detection
- pretreatment differential-pressure visibility
- water-quality out-of-spec lockout
- clean-water reserve threshold logic
- maintenance-required visibility

### Hydrogen Generation Module
Must verify:
- startup permissives
- bad-water stop or inhibit
- loss-of-ventilation inhibit
- safe stop on downstream-path loss
- no casual restart after trip
- energy-use logging

### Gas Conditioning & Storage Module
Must verify:
- compressor fault response
- charge-path isolation
- discharge-path permissives
- storage isolation logic
- vent / relief path awareness
- inventory estimation visibility

### Fuel Cell / Power Conversion Module
Must verify:
- split-module degraded operation
- battery reserve protection
- main bus visibility
- load-shed behavior
- black-start entry and recovery logic
- dispatch-class recalculation after module loss

### Safety & Ventilation Module
Must verify:
- gas alarm ingestion
- detector fault behavior
- ventilation proving and loss response
- ESD escalation
- purge failure behavior
- ingress alarm handling
- no automatic restart after major event

### Housekeeping Energy Module
Must verify:
- H-1 load continuity
- reserve hold-up function
- helper-source accounting isolation
- no-backfeed behavior
- load-priority shedding
- black-start support continuity

### Monitoring & Controls Module
Must verify:
- blocked-start reason visibility
- event sequence logging
- trend generation
- dispatch classification
- degraded-state clarity
- maintenance-state handling
- HMI readability for fault states

## Measurement-first expectations

Every meaningful verification stage should capture actual measurements for at
least one of the following categories:

- pressure
- flow
- conductivity / water-quality state
- power
- energy
- temperature
- detector / ventilation status
- valve or contactor state
- time-to-trip or time-to-stop
- event order

The repo is not allowed to pass a major verification stage on vague narrative
alone.

## Pass / fail posture

The repo uses four concept-stage verification outcomes:

### V-1 — Pass
Expected behavior occurred and was visible.

### V-2 — Pass with limitation
Behavior was acceptable, but one or more bounded limitations were exposed and
must remain visible in documentation.

### V-3 — Needs redesign
The architecture or logic did not behave acceptably and needs correction before
claiming progression.

### V-4 — Invalid test or insufficient instrumentation
The test setup or logging was too weak to support the conclusion.

A repo that confuses V-4 with V-1 is not serious.

## Kill criteria

The repo should treat the following as concept-stage kill criteria unless the
architecture is redesigned:

- inability to reliably block electrolysis on bad-water condition
- inability to isolate hydrogen path on confirmed major gas event
- inability to preserve critical controls visibility through blackout recovery
- inability to distinguish green / amber / red dispatch meaningfully
- arrangement that destroys routine maintenance access
- helper-source logic that contaminates main-energy accounting with fake claims

## Evidence packaging expectations

Each future test package in this repo should include, at minimum:

- test ID
- objective
- setup
- instrumentation
- preconditions
- procedure
- expected result
- observed result
- pass / limitation / redesign outcome
- raw or summarized measurement evidence
- linked requirement and hazard references

That makes the repo reviewable.

## What this file can and cannot solve

### What it can solve now
It can lock:
- the order proof should happen
- the minimum questions each stage must answer
- what counts as a meaningful pass
- what the architecture must measure rather than assume

### What it cannot honestly solve now
It cannot finalize:
- vendor-specific acceptance test procedures
- final class witness requirements
- final vessel trial plan
- final authority-approved commissioning sequence

## Explicit non-claims

This file does **not** claim:

- verification is already complete
- passing a bench test proves commercial readiness
- passing a dockside test proves class approval
- a bounded harbor pilot proves deep-sea viability
- every future test will use identical instrumentation

It defines the proof discipline the repo must follow.

## Summary

The verification strategy for IX-Marine-H2-Retrofit is deliberately staged:

first prove the architecture is coherent, then prove subsystems, then prove the
integrated skid logic, then prove dockside realism, then prove bounded vessel
operation.

At every stage, the repo must test bad inputs, bad states, shutdown behavior,
degraded modes, and recovery logic—not just the happy path.

That is the only honest way this repo becomes worth taking seriously.
