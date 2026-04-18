# IX-Marine-H2-Retrofit

Concept-stage maritime hydrogen retrofit architecture for a harbor / port utility vessel using:

- protected seawater intake
- water treatment to electrolyzer-grade process water
- berth-powered onboard hydrogen generation
- 350-bar compressed hydrogen storage
- split PEM fuel-cell generation
- LFP battery buffering
- layered hydrogen safety, shutdown, and monitoring logic
- proof-of-concept planning
- full concept BOM
- concept-stage assembly and integration walkthrough

Licensed under **Apache-2.0**.

---

## What this repo is

IX-Marine-H2-Retrofit is a **measurement-first, concept-stage engineering repo**
for a **harbor / port utility workboat retrofit**.

It studies a bounded, realistic question:

> Can an existing short-sea / harbor vessel be retrofitted to use a
> **hydrogen + battery hybrid architecture**, with **onboard hydrogen generation
> primarily at berth**, using **treated seawater-derived process water**, while
> keeping the real penalties visible instead of hiding them?

This repo is designed to be read by:

- marine retrofit engineers
- shipyard and systems-integration teams
- port and harbor decarbonization teams
- hydrogen safety and controls reviewers
- fuel-cell / battery hybrid reviewers
- technical decision-makers who want the ugly parts exposed, not blurred

---

## What this repo is not

This repo is **not**:

- a perpetual-motion claim
- a “ship powers itself forever from seawater and waves” claim
- a class-approved vessel package
- a certified installation package
- a ready-to-order commercial design
- a universal retrofit answer for all vessel classes
- a methanol or ammonia architecture repo
- a promise of guaranteed positive ROI
- a claim that hydrogen is always the best marine answer

It is a **decision-grade architecture study** with explicit boundaries.

---

## Final locked concept in one paragraph

The final locked concept is a **harbor-vessel retrofit** that takes seawater
through a **protected, serviceable intake**, treats it through **pretreatment,
desalination, and polishing** into electrolyzer-suitable process water, uses
**external berth power** to run a **450 kW-class PEM electrolyzer**, conditions
and stores hydrogen in a **weather-deck 350-bar storage rack**, then uses
**2 × 125 kW PEM fuel-cell modules** plus a **500 kWh LFP battery** to support
vessel electrical operation. The architecture includes explicit **hydrogen leak,
ventilation, purge, shutdown, black-start, degraded-mode, logging, dispatch,
maintenance, and berth-interface logic**. Small helper harvesters may support
**housekeeping power only** and are never counted as the main propulsion or main
hydrogen-production energy source.

---

## Locked reference vessel

This repo is intentionally bounded to a single reference vessel class:

- **vessel type:** harbor / port utility workboat retrofit
- **length overall:** about 85 to 95 ft
- **beam:** about 24 to 28 ft
- **displacement:** about 130 to 180 tons
- **operating pattern:** daily return to berth
- **mission style:** short-sea / harbor service with predictable berth access

If the use case drifts far outside that envelope, the repo gets weaker.

---

## Locked architecture

### Primary energy architecture
- **Hydrogen + battery hybrid**

### Replenishment model
- **Primary:** onboard hydrogen generation while berthed
- **Backup:** loaded hydrogen from shore when needed

### Explicitly excluded as first-class repo paths
- methanol retrofit
- ammonia retrofit
- generic “fuel-ready for everything” framing
- battery-only as the final repo outcome

### Optional bounded fallback
- HVO-compatible emergency auxiliary interface only if an owner later chooses to
  retain one outside the core hydrogen operating path

---

## Locked reference sizing

### Hydrogen generation
- **PEM electrolyzer:** 450 kW class
- **normal operating role:** berth-side hydrogen production

### Hydrogen storage
- **storage class:** 350 bar compressed hydrogen
- **gross hydrogen target:** about 90 kg
- **usable hydrogen target:** about 80 kg

### Fuel-cell generation
- **Fuel Cell A:** 125 kW PEM
- **Fuel Cell B:** 125 kW PEM
- **total net continuous target:** about 250 kW

### Battery
- **chemistry:** LFP
- **capacity:** 500 kWh

### Mission basis
- **daily energy target:** about 0.9 to 1.1 MWh/day
- **average operating demand:** about 120 to 180 kW
- **peak maneuvering demand:** about 400 to 500 kW

### Berth-side replenishment
- **design electrical demand at berth:** about 500 to 550 kW
- **about 60 kg top-up:** about 8 hours practical berth time
- **about 80 kg top-up:** about 10 to 11 hours practical berth time

These are **concept-stage reference numbers**, not vendor guarantees.

---

## Why the repo is framed this way

Most marine hydrogen concept work gets weaker when it hides one or more of the
following:

- water-treatment burden
- hydrogen storage penalty
- ventilation burden
- compressor burden
- control-system complexity
- black-start dependence
- port and shore-power dependence
- maintenance burden
- training burden
- economics that do not cleanly pay back on fuel savings alone

This repo keeps those burdens visible on purpose.

The point is not to sound easier than reality.  
The point is to be harder to misunderstand.

---

## Final arrangement logic

The architecture is built around six arrangement zones:

### Z-1 — Weather-deck hydrogen storage zone
- compressed hydrogen rack
- protective framing
- manifold enclosure
- vent / relief interface

### Z-2 — Hydrogen process room / process skid zone
- PEM electrolyzer
- immediate gas interface
- process instrumentation
- local shutdown points

### Z-3 — Water treatment zone
- intake path
- pretreatment
- desalination
- polishing
- clean-water reserve

### Z-4 — Fuel-cell and conversion zone
- Fuel Cell A
- Fuel Cell B
- DC distribution
- conversion interfaces
- cooling interfaces

### Z-5 — Low battery zone
- 500 kWh LFP battery
- isolation and monitoring hardware

### Z-6 — Controls / housekeeping / safety core
- safety controller
- process controls
- housekeeping bus
- logging and HMI support

This arrangement exists for one major reason:

> the topside hydrogen-storage penalty is real, so the architecture must fight
> it with low battery placement, low treatment placement, deliberate venting,
> and serviceable zoning.

---

## What the repo solves

At concept stage, this repo solves for:

- **tank volume**
- **electrolyzer footprint**
- **desalination footprint**
- **ventilation space**
- **hazardous-zone layout placeholders**
- **fuel-cell room / machinery integration philosophy**
- **weight-change allowances**
- **center-of-gravity and stability guardrails**
- **maintenance access envelope**
- **hydrogen generator arrangement**
- **ventilation and inerting posture**
- **fire / explosion design basis**
- **hazardous-area discipline**
- **fuel-cell space concept**
- **shutdown logic**
- **crew safety posture**
- **hazard register**
- **FMEA-style failure handling**
- **capex / downtime / maintenance / training framing**
- **berth interface and emergency-response posture**
- **proof-of-concept structure**
- **full concept BOM**
- **concept-stage assembly walkthrough**

---

## Safety posture

The repo is locked to layered protection, not one magic barrier.

### Core safety layers
- arrangement and separation
- enclosure strategy
- detection
- ventilation proving
- purge logic
- shutdown escalation
- isolation
- crew procedure
- maintenance-state control
- event logging and visibility

### Shutdown levels
- **ESD-0:** controlled stop
- **ESD-1:** process isolate
- **ESD-2:** hydrogen isolate
- **ESD-3:** major event emergency shutdown

### Named hazard families handled explicitly
- hydrogen leak
- ignited release
- ventilation failure
- seawater intake blockage
- bad-water lockout
- compressor fault
- purge failure
- sensor failure
- false-negative detection vulnerability
- blackout / black-start failure
- flooding or spray ingress
- maintenance error state

This repo does not pretend those hazards disappear.  
It is built around the idea that they are real and must be treated as normal
design drivers.

---

## Operational posture

This is a **berth-supported** architecture.

### Normal operational rhythm
1. vessel returns to berth
2. housekeeping layer remains alive
3. berth interface is checked
4. water treatment prepares clean process water
5. electrolysis runs during overnight or extended layover
6. hydrogen inventory is replenished
7. battery is recharged
8. pre-departure checks are completed
9. vessel departs on stored hydrogen + battery support

### Dispatch classes
- **Green:** planned mission permitted
- **Amber:** reduced mission / restricted release only
- **Red:** departure blocked

### Crew discipline assumptions
- no casual hydrogen operation
- no single-person hydrogen maintenance
- no hot work near hydrogen systems without formal isolate / gas-free posture
- no ambiguous restart after major event
- no hidden maintenance bypass treated as normal state

---

## Economics posture

This repo is intentionally blunt about economics.

### Concept-stage capex range
**About $5 million to $9 million**

### Concept-stage retrofit downtime
**About 20 to 30 weeks**

### Maintenance burden
**Moderate to high**

### Port dependency
**High**

### Shore-power dependency
**High if onboard electrolysis is the main replenishment path**

### Training burden
At minimum:
- **3 to 5 days** operator-focused training
- **2 additional days** maintenance-focused training
- recurring drills

### Payback posture
This repo is **not** framed as a guaranteed fuel-savings payback retrofit.

Its strongest justifications are:

- lower local emissions in port
- quieter harbor operation
- strategic decarbonization value
- pilot-platform value
- bounded hydrogen-systems learning
- preparation for stricter harbor emissions expectations

---

## Proof-of-concept posture

This repo includes a bounded proof-of-concept path, not a pretend full ship.

### Proof ladder
1. architecture coherence
2. benchtop subsystem verification
3. integrated PoC verification
4. dockside / pier-side verification
5. bounded vessel operational verification

### PoC intent
The PoC is meant to prove that:

- bad-water lockout works
- ventilation-loss lockout works
- gas-trip logic works
- compressor-fault response works
- fuel-cell + battery hybrid control works
- degraded modes are explicit
- black-start logic is real
- event logging preserves cause / effect order
- helper-source accounting stays honest

It is **not** meant to prove unrestricted live-vessel readiness.

---

## Repository map

### Project framing
- `docs/project/repo_scope.md`
- `docs/project/reference_vessel.md`
- `docs/project/requirements_basis.md`
- `docs/project/non_claims.md`
- `docs/project/assumptions_and_constraints.md`

### Architecture
- `docs/architecture/system_overview.md`
- `docs/architecture/conops.md`
- `docs/architecture/layout_and_arrangement.md`

### Module definitions
- `docs/architecture/modules/intake_and_water_treatment.md`
- `docs/architecture/modules/hydrogen_generation.md`
- `docs/architecture/modules/gas_conditioning_and_storage.md`
- `docs/architecture/modules/fuel_cell_and_power_conversion.md`
- `docs/architecture/modules/safety_and_ventilation.md`
- `docs/architecture/modules/housekeeping_energy.md`
- `docs/architecture/modules/monitoring_and_controls.md`

### Operations
- `docs/operations/berth_replenishment_and_port_interface.md`
- `docs/operations/crew_safety_and_operational_procedures.md`

### Safety
- `docs/safety/hazard_register.md`
- `docs/safety/failure_modes_and_effects.md`
- `docs/safety/shutdown_interlocks_and_safe_states.md`
- `docs/safety/fire_explosion_and_hazardous_zone_basis.md`

### Analysis
- `docs/analysis/economics_and_operational_case.md`
- `docs/analysis/alternative_pathway_decision.md`
- `docs/analysis/final_configuration.md`

### Verification and PoC
- `docs/verification/verification_strategy.md`
- `docs/proof_of_concept/proof_of_concept_plan.md`
- `docs/proof_of_concept/test_matrix.md`

### Bill of materials
- `docs/bom/full_concept_bom.csv`

### Assembly / integration
- `docs/assembly/concept_stage_assembly_walkthrough.md`

---

## Recommended reading order

If you want the fastest serious read, start here:

1. `docs/analysis/final_configuration.md`
2. `docs/architecture/system_overview.md`
3. `docs/architecture/layout_and_arrangement.md`
4. `docs/safety/hazard_register.md`
5. `docs/analysis/economics_and_operational_case.md`
6. `docs/proof_of_concept/proof_of_concept_plan.md`
7. `docs/bom/full_concept_bom.csv`
8. `docs/assembly/concept_stage_assembly_walkthrough.md`

---

## Best-fit use case

This repo is strongest for an operator with:

- a harbor / port utility vessel
- daily return to berth
- stable home-berth access
- willingness to accept procedure burden
- willingness to accept a serious retrofit and maintenance burden
- genuine interest in lower local emissions and strategic hydrogen integration

It is weakest if someone tries to read it as:

- a deep-sea cargo answer
- a no-infrastructure-required answer
- a cheap quick retrofit
- a universal marine solution
- a perpetual-motion seawater-fuel machine

---

## Non-claims worth repeating

This repo does **not** claim:

- class approval
- guaranteed positive ROI
- guaranteed universal emissions superiority
- universal vessel applicability
- final hazardous-zone approval
- final intact or damage stability approval
- unrestricted operational readiness
- that waves, ship motion, or intake flow alone can power the whole system

Those are outside the repo lock.

---

## Why this repo may still matter

Even with all the penalties exposed, this repo still has real value because it
does something many concept-stage energy repos avoid:

> it turns a “marine hydrogen idea” into a **disciplined vessel retrofit
> architecture** with arrangement, hazards, shutdowns, operations, economics,
> proof path, BOM, and assembly logic all tied together in one place.

That makes it useful even to a reader who ultimately decides **not** to choose
hydrogen.

---

## Author

**Bryce Lovell**

## License

**Apache-2.0**

See `LICENSE` and `NOTICE`.

## Final statement

IX-Marine-H2-Retrofit is a harbor-vessel hydrogen retrofit concept for people
who want the real engineering burden on the table:

the water path, the gas path, the battery path, the shutdown path, the port
dependency, the weight penalty, the maintenance burden, and the proof burden.

That honesty is the point.
