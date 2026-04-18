# Concept-Stage Assembly and Integration Walkthrough

## Purpose

This file provides the concept-stage assembly and integration walkthrough for
IX-Marine-H2-Retrofit.

It exists to answer the practical question that follows the architecture and
BOM:

**If a yard, integrator, or technical reviewer wanted to understand how this
retrofit would be assembled in a disciplined order, what would the sequence look
like, what has to be installed before what, what checks have to happen between
steps, and where are the high-risk integration points?**

This is **not** a certified installation manual.  
This is **not** a shipyard-issued work package.  
This is **not** permission to build without vessel-specific engineering,
hazard review, class review, and qualified execution.

It is the concept-stage assembly backbone for the repo.

## Scope

This walkthrough covers:

- pre-assembly prerequisites
- recommended installation sequence
- subsystem integration order
- inspection and hold points
- startup-readiness checkpoints
- common integration traps
- what must be proven before proceeding to later stages

## Requirements traceability

This file directly supports:

- **R-060** concept-level allowances for volume, footprint, and service
  clearances
- **R-061** center-of-gravity and stability treated as mandatory evaluation
  items
- **R-062** routine service components should be replaceable without major
  teardown
- **R-063** manual isolation devices remain reachable
- **R-090** proof-of-concept path that can be inspected without hidden
  assumptions
- **R-091** full bill of materials at concept stage
- **R-092** concept-stage assembly and integration guidance clearly labeled as
  non-certified
- **R-093** explicit non-claims where proof is incomplete

It also aligns with:

- `docs/architecture/layout_and_arrangement.md`
- `docs/safety/shutdown_interlocks_and_safe_states.md`
- `docs/verification/verification_strategy.md`
- `docs/proof_of_concept/proof_of_concept_plan.md`
- `docs/analysis/final_configuration.md`

## Assembly philosophy

The assembly philosophy for this repo is locked to the following rules:

- install the **structural and routing backbone first**
- install the **low / central heavy compensating mass before topside hydrogen
  hardware where practicable**
- keep **service access visible at every stage**
- do **not** bury manual isolation, detectors, filters, or access points behind
  later-added hardware
- verify **arrangement and clearance** before connecting live process paths
- bring **controls and logging visibility online early**
- prove **interlocks before active hydrogen process operation**
- treat every major subsystem handoff as an inspection gate

## Honest boundary

This walkthrough cannot honestly finalize:

- hull-specific structural reinforcement details
- final welding procedure specifications
- final pipe class / fitting class for a real vessel
- final electrical classification / hazardous-area installation rules
- final class-approved testing or commissioning sequence
- live hydrogen handling procedure for unrestricted service

What it **can** do is give a disciplined, reviewable integration order that
prevents the repo from pretending everything can just be dropped in at once.

## Assembly phases

The concept-stage installation sequence is divided into eleven phases:

1. vessel baseline survey and strip-out
2. structural foundations and route reservation
3. low-zone machinery and battery installation
4. water-intake and treatment installation
5. main electrical backbone and controls installation
6. electrolyzer and process-room installation
7. gas conditioning and storage installation
8. safety, ventilation, and detector installation
9. controls closure and interlock verification
10. cold commissioning and dry functional checks
11. bounded active commissioning and PoC-style integrated verification

Each phase is described below.

---

## Phase 1 — Vessel baseline survey and strip-out

### Objective

Establish what the starting vessel actually is before pretending the retrofit
fits.

### Required actions

- document actual lightship condition and current machinery arrangement
- identify removable legacy machinery, tanks, exhaust paths, and cable trays
- confirm actual access openings and crane / removal paths
- confirm current sea chest or candidate intake location
- confirm usable deck and machinery-zone volumes
- identify spaces that must remain gas-safe and routinely occupied
- identify conflicts with mooring, line handling, and deck work

### Deliverables

- baseline arrangement mark-up
- removal list
- access path map
- protected keep-clear candidate map
- preliminary weight removal credit estimate
- preliminary routing reservation sketch

### Hold point HP-01

Do **not** proceed to fabrication or heavy equipment placement until the vessel
baseline survey confirms that the locked arrangement philosophy still fits the
actual hull.

### Common failure pattern

Trying to install hydrogen hardware before understanding the real removal and
service envelopes creates layout lies that the repo is specifically designed to
avoid.

---

## Phase 2 — Structural foundations and route reservation

### Objective

Create the physical backbone that later equipment depends on.

### Required actions

- define support foundations for:
  - battery installation
  - water-treatment skids
  - electrolyzer skid
  - compressor / conditioning hardware
  - controls and electrical switchgear
  - weather-deck storage rack
- reserve vent / relief mast route
- reserve main hydrogen routing corridor
- reserve main DC bus and critical-controls cable routes
- reserve drainage and cleanout paths for water-treatment hardware
- preserve service aisles and removal paths in structure planning

### Structural priorities

Install or prepare:

- low battery foundations first
- low water-treatment skid supports
- electrolyzer process-zone supports
- storage-rack structural interface
- cable-tray and pipe-support backbone
- vent routing supports

### Deliverables

- support layout verified against equipment envelopes
- route-reservation map
- service-access check against planned aisle widths
- preliminary structural integration review

### Hold point HP-02

No major skid or storage hardware should be landed until:

- service aisles still exist
- vent path still exists
- battery low-placement target is preserved
- manual isolation access is still plausible

### Common failure pattern

Installing supports purely for compactness and then discovering that the
compressor, filters, or isolation valves cannot be serviced.

---

## Phase 3 — Low-zone machinery and battery installation

### Objective

Install the heavy low-placement systems that help the vessel remain physically
credible.

### Sequence

1. install battery containment / structural cradle
2. install battery system
3. install low-zone water-treatment skid supports and major skid hardware
4. install associated low-zone piping stubs and drains
5. install low-zone cooling support hardware where applicable
6. verify access to battery isolation and service points

### Why this phase happens early

Battery and treatment equipment are intentionally low in the vessel because they
help counter the topside hydrogen-storage penalty. If they are delayed until
after upper-zone clutter appears, placement quality usually degrades.

### Mandatory checks

- battery remains low and near centerline
- battery removal / service path still exists
- water-treatment skid can be accessed from the front and service side
- drain routing is not trapped
- no later-installed hydrogen routing will block service access

### Deliverables

- battery installed or battery mock-up installed
- low treatment structure landed
- initial cable / pipe landing zones preserved
- updated weight log for installed low-zone mass

### Hold point HP-03

Do **not** install weather-deck hydrogen storage rack before confirming the low
mass intended to counter it has actually been placed where the configuration
expects it.

---

## Phase 4 — Water-intake and treatment installation

### Objective

Install the seawater-to-clean-water backbone before the hydrogen-generation
process path.

### Sequence

1. install or modify protected intake / sea chest components
2. install coarse debris guard / serviceable strainer path
3. install intake isolation valves
4. install pretreatment hardware
5. install desalination skid
6. install polishing stage
7. install clean-water day tank
8. install conductivity, flow, level, and differential-pressure instrumentation
9. install drain, flush, and sample points
10. verify service removal paths for strainers, elements, and treatment
    consumables

### Integration rules

- no treatment element shall be trapped behind later-added hydrogen hardware
- conductivity instrumentation must remain serviceable
- clean-water tank inspection and drain access must exist
- flush and cleanout hardware must remain reachable

### Required dry checks

- isolation valves operable
- sample points reachable
- filter / strainer removal path demonstrated
- clean-water level instrumentation readable
- treatment skid footprint matches arrangement assumptions

### Deliverables

- water-treatment hardware installed
- instrumentation landed
- service-access photographs or recorded check evidence
- drain / flush route confirmation

### Hold point HP-04

The electrolyzer shall not be landed until the water-treatment system and clean
water reserve path are physically present and verified to be serviceable.

### Common failure pattern

Treating the water path as secondary and then discovering the electrolyzer has
been installed in a way that blocks filter replacement or conductivity probe
service.

---

## Phase 5 — Main electrical backbone and controls installation

### Objective

Install the electrical and controls spine before live process logic is trusted.

### Sequence

1. install main DC distribution backbone
2. install precharge and main isolation hardware
3. install controls cabinet / safety controller cabinet
4. install critical 48V housekeeping bus hardware
5. install hold-up / reserve hardware
6. install controls network and I/O backbone
7. install HMI hardware
8. land main field cabling trays and protected routes
9. verify maintainable access to controls and switchgear

### Why this phase matters

A hydrogen retrofit without a visible controls spine becomes impossible to test
cleanly later. Controls and logging have to exist before meaningful interlock
proof exists.

### Required checks

- battery isolation reachable
- main DC bus isolation reachable
- controls cabinet accessible
- maintenance-mode hardware accessible
- HMI position allows readable operation
- critical-controls bus can be energized independently of full process startup

### Deliverables

- controls hardware installed
- main electrical distribution installed
- field I/O architecture in place
- early power-up path for housekeeping-only state available

### Hold point HP-05

Before landing electrolyzer, compressor, or hydrogen storage equipment, the
project should be able to achieve a bounded **housekeeping alive** state and log
basic subsystem health inputs.

---

## Phase 6 — Electrolyzer and process-room installation

### Objective

Install the berth-generation core in a way that preserves access, ventilation
logic, and clear process layout.

### Sequence

1. land electrolyzer skid on prepared foundations
2. connect clean-water feed path
3. connect power-conditioning interface
4. connect process instrumentation
5. install gas-liquid separation interface hardware
6. install oxygen routing hardware
7. install thermal-management hardware
8. verify front aisle, side access, and top-side or extraction path for service
9. install local E-stop and local status indication

### Integration rules

- water feed shall be traceable and isolatable
- no local manual isolation point may be hidden by later gas hardware
- oxygen routing must remain separate and visible
- process-room access must remain possible with doors, panels, and insulation
  installed

### Required dry checks

- skid footprint matches reserved envelope
- local service clearances preserved
- valve reach confirmed
- detector and ventilation mounting positions still available
- process labeling possible and readable

### Deliverables

- electrolyzer skid installed
- power and water interfaces landed
- local process instrumentation landed
- process-room access check record

### Hold point HP-06

Do **not** connect the active gas-conditioning and storage charge path until:

- electrolyzer skid access is verified
- water-quality instrumentation is landed
- local shutdown and status visibility are installed

---

## Phase 7 — Gas conditioning and storage installation

### Objective

Install the hydrogen conditioning, charging, storage, and supply path in the
most layout-sensitive phase of the retrofit.

### Sequence

1. install compressor package and support cooling
2. install gas drying package
3. install charge manifold
4. install manual isolation valves and visible identification
5. install storage rack and protective framing
6. install storage manifold cabinet
7. install pressure relief devices and vent / relief routing
8. install regulated supply path toward fuel-cell modules
9. confirm weather-deck restricted-area geometry and access path
10. confirm service and crane / extraction path for storage rack

### Integration rules

- storage rack should remain near centerline where practicable
- vent / relief route must remain upward and unobstructed
- manifold access must remain human-reachable
- compressor service path must remain open
- no casual conflict with line handling, walkways, or routine occupancy

### Required dry checks

- storage isolation reachable
- vent mast unobstructed
- cabinet doors / access paths functional
- compressor removal or service envelope demonstrable
- no hydrogen-bearing enclosure lacks reserved detector / ventilation hardware
  space

### Deliverables

- gas-conditioning hardware installed
- storage rack installed
- vent / relief path installed
- storage and supply routing landed
- arrangement check against keep-clear logic

### Hold point HP-07

No active hydrogen introduction should be considered until:

- storage path is complete
- vent / relief path is complete
- detector and ventilation hardware for affected enclosures are installed
- ESD-related isolation actuation paths are verified mechanically

### Common failure pattern

Landing storage cylinders and manifolds first, then discovering that the vent
mast routing or detector positions cannot be installed without rework.

---

## Phase 8 — Safety, ventilation, and detector installation

### Objective

Install the hazard-management layer as hardware, not as theory.

### Sequence

1. install hydrogen gas detectors
2. install flame detectors where planned
3. install dedicated extraction fans
4. install airflow / differential-pressure proving hardware
5. install ingress-detection hardware in critical enclosures
6. install local audible / visual alarm devices
7. install local and remote E-stop stations
8. install maintenance-mode keying hardware
9. install required safety signage and hazard placards

### Integration rules

- detector positions should reflect likely accumulation points, not only cable
  convenience
- fan and proving hardware must remain serviceable
- safety devices must not be trapped behind decorative or secondary hardware
- alarm devices must be visible and audible in their intended use context

### Required dry checks

- every hydrogen-bearing enclosure has the intended detector and ventilation
  hardware provision
- every critical manual E-stop is visible and reachable
- signage and restricted-zone indication is not forgotten until the end

### Deliverables

- safety detection hardware installed
- ventilation hardware installed
- E-stop hardware installed
- hazard placarding installed
- safety-device access check record

### Hold point HP-08

No subsystem may be accepted as “ready for active commissioning” until its
detector, ventilation, and emergency-stop basis are physically present and
addressed in controls.

---

## Phase 9 — Controls closure and interlock verification

### Objective

Close the loop between field hardware and the logic that must supervise it.

### Sequence

1. terminate field I/O to controls
2. verify detector signals
3. verify fan / ventilation proof signals
4. verify valve-state feedbacks
5. verify conductivity, level, flow, and pressure instrumentation
6. verify battery and bus-state inputs
7. verify maintenance-mode state
8. verify alarm outputs
9. verify HMI pages and blocked-start reason visibility
10. verify event logging and sequence-of-events capture

### Required checks

- every critical permissive has a real signal path
- every critical trip cause produces a logged state
- HMI explains blocked states specifically
- maintenance mode blocks startup where intended
- no safety-critical input is missing from the sequence logic

### Deliverables

- I/O checkout record
- interlock mapping record
- blocked-start / trip simulation record
- initial HMI review record

### Hold point HP-09

No active process commissioning is allowed until:

- interlocks are proven to exist
- bad-water lockout works
- ventilation-loss lockout works
- gas-trip handling works
- event log preserves cause / effect order

---

## Phase 10 — Cold commissioning and dry functional checks

### Objective

Prove the system can behave correctly **without** live hydrogen process use.

### Sequence

1. energize housekeeping-only mode
2. prove state transitions:
   - cold / secured
   - housekeeping alive
   - berth readiness
   - maintenance state
3. simulate bad-water condition
4. simulate detector fault
5. simulate gas trip
6. simulate ventilation loss
7. simulate compressor fault
8. simulate purge incomplete
9. simulate battery reserve threshold crossing
10. simulate dead-bus recovery and black-start sequence

### Required outcomes

- correct lockouts appear
- correct ESD depth appears
- correct degraded state appears
- blocked-start reasons are readable
- no serious trip auto-restarts
- event log sequence remains reconstructable

### Deliverables

- cold-commissioning test record
- pass / limitation / redesign list
- unresolved punch list

### Hold point HP-10

No live active hydrogen-process testing should proceed until the dry functional
checks prove that the interlock backbone behaves correctly.

---

## Phase 11 — Bounded active commissioning and PoC-style integrated verification

### Objective

Move from dry logic to bounded active process proof without claiming full vessel
commercial readiness.

### Sequence

1. prove water-treatment function and water-quality gate
2. prove electrolysis permissives and controlled stop
3. prove compressor and charge-path logic
4. prove storage-path supervision
5. prove fuel-cell module startup logic
6. prove split-module degraded mode
7. prove battery reserve protection
8. prove full integrated event logging and dispatch classification

### Active commissioning rules

- test the lockouts, not just the happy path
- inject bad-water state during active generation
- inject ventilation-loss state during relevant active mode
- inject gas-trip logic in safe test conditions
- test black-start after induced bus-loss scenario
- test maintenance-state conflict handling
- keep evidence package tied to requirement and hazard references

### Deliverables

- integrated commissioning record
- test evidence package
- staged proof status against verification strategy
- list of limitations still unresolved before dockside or vessel trial planning

## Integration traps to avoid

The repo is specifically designed to prevent these mistakes:

### Trap 1 — Installing storage before proving the low-mass counterbalance plan
This hides stability risk.

### Trap 2 — Installing electrolyzer before preserving service path to treatment
elements
This hides maintenance reality.

### Trap 3 — Treating vent routing as an afterthought
This destroys the hazard basis.

### Trap 4 — Bringing in live process operation before controls and logging are
proved
This creates blind unsafe states.

### Trap 5 — Allowing maintenance mode to be invisible
This creates restart risk.

### Trap 6 — Treating HMI as decoration
This hides blocked-state and degraded-state meaning from crew.

## Minimum assembly acceptance checklist

The concept-stage installation is only acceptable if all of the following are
true:

1. battery is low and near centerline as intended
2. water-treatment service path exists
3. electrolyzer service aisle exists
4. compressor service path exists
5. storage isolation is reachable
6. vent / relief path is installed and unobstructed
7. detector and ventilation hardware are installed in critical zones
8. controls can enter housekeeping-only state
9. controls can prove bad-water lockout
10. controls can prove ventilation-loss lockout
11. controls can prove gas-trip shutdown path
12. event log can reconstruct injected faults
13. maintenance mode cannot be hidden

If any of those fail, the configuration is not ready to be treated as a serious
PoC or bounded pilot candidate.

## What this walkthrough can and cannot do

### What it can do now
It can lock:
- the installation order
- the integration priorities
- the hold points
- the inspection logic
- the sequence discipline required to keep the project honest

### What it cannot finalize now
It cannot finalize:
- exact yard labor sequence
- exact crane plans
- exact weld packages
- exact pipe-installation specifications
- exact cable schedules
- exact live-gas commissioning permit requirements
- final class witness sequence

## Explicit non-claims

This file does **not** claim:

- that a real yard should build directly from this file
- that the sequence is complete enough for certified installation
- that vessel-specific engineering can be skipped
- that passing these assembly stages proves unrestricted readiness

It is the concept-stage assembly backbone only.

## Summary

The correct assembly logic for IX-Marine-H2-Retrofit is:

- survey first
- build supports and routing second
- place low compensating mass early
- install water and controls before live hydrogen process trust
- install storage with venting and access visible
- install safety hardware before active commissioning
- prove interlocks dry before active process testing
- treat every stage as something that can fail and must be inspected

That is the only honest integration path for this repo.
