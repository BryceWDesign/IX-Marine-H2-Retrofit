# Concept of Operations (CONOPS)

## Purpose

This file defines how IX-Marine-H2-Retrofit is intended to operate across its
main mission phases.

The goal is not to make the system look smooth or effortless.

The goal is to show:

- when the vessel makes hydrogen
- when it uses stored hydrogen
- when the battery carries the vessel
- when the system is locked out
- what degraded operation still looks like
- where shore support is mandatory

## Operating philosophy

The operating philosophy is simple:

- generate hydrogen mainly while berthed
- use stored hydrogen plus battery while operating
- let the battery absorb fast transients and black-start duties
- never hide interlocks, lockouts, or safety dependencies
- preserve enough low-voltage control power to supervise faults and recovery

This is a berth-supported vessel architecture, not a free-roaming
self-fueling fantasy.

## Mission phases

The reference concept uses nine operational phases.

1. Cold / secured
2. Housekeeping alive
3. Berth connection and readiness checks
4. Water treatment and clean-water readiness
5. Electrolysis and hydrogen replenishment
6. Pre-departure readiness
7. Vessel operation on fuel-cell plus battery hybrid power
8. Degraded operation / return-to-berth mode
9. Shutdown, maintenance, or emergency state

Each phase is described below.

---

## Phase 1 — Cold / secured

### Description

The vessel is not operating. Main propulsion and hydrogen processes are off.
The vessel may be docked, laid up, or between service windows.

### System condition

- main DC bus de-energized or partially isolated
- electrolyzer off
- compressor off
- fuel cells off
- storage isolated per secured-state logic
- battery protected and monitored
- only minimal monitoring may remain alive if selected

### Purpose

This phase exists to:
- hold the vessel in a safe dormant state
- preserve battery health
- prevent unintended hydrogen process startup
- support maintenance or layup preparation

### Entry conditions

- commanded secured shutdown complete
- no unresolved emergency state requiring active response
- vessel not in live hydrogen generation mode

### Exit conditions

- housekeeping system is intentionally brought alive
- startup is authorized by procedure

---

## Phase 2 — Housekeeping alive

### Description

The low-voltage critical control layer is active even though the main hydrogen
process and propulsion path are not yet enabled.

### System condition

- 48V critical controls bus alive
- safety PLC or equivalent logic alive
- data logging alive
- gas detection alive
- selected environmental sensing alive
- communications and state retention alive
- main propulsion loads still inhibited

### Purpose

This phase exists because the vessel needs a supervisory state between "dead"
and "fully active."

It supports:
- safe startup checks
- gas detector status
- ventilation proof checks
- maintenance-state awareness
- black-start sequencing

### Allowed energy sources

Housekeeping power may come from:
- battery-backed DC conversion
- hold-up energy storage
- shore power auxiliary feed
- optional low-power auxiliary harvesters if installed

### Exit conditions

- startup permissives are checked
- berth power or operational power path becomes available
- no critical lockout is active

---

## Phase 3 — Berth connection and readiness checks

### Description

The vessel is berthed and preparing for either hydrogen generation, recharge,
or operational readiness.

### System condition

- shore electrical interface available or being verified
- berth-side power quality check complete or in progress
- vent path status checked
- detector health checked
- maintenance-state conflicts checked
- storage isolation position confirmed
- no hydrogen generation yet

### Core checks in this phase

The system should verify at minimum:

- shore power present and within acceptable bounds
- emergency stop link state known
- no unresolved gas alarm
- ventilation path healthy
- water-treatment path available
- maintenance mode not active
- storage manifold isolation state valid

### Purpose

This phase creates a controlled gateway between a passive vessel and an active
process plant.

### Failure behavior

If berth readiness fails:
- hydrogen generation is blocked
- compressor start is blocked
- fuel-cell start remains blocked or limited based on fault class
- alarm raised to operator

---

## Phase 4 — Water treatment and clean-water readiness

### Description

The intake and treatment train prepares electrolyzer-grade process water from
seawater.

### System condition

- protected intake path active
- pretreatment active
- desalination active or ready
- polishing active or ready
- clean-water day tank filling or ready
- electrolyzer still inhibited until water quality is confirmed

### Purpose

This phase exists to make the water path visible as a first-class subsystem
instead of silently assuming perfect water.

### Required checks

The control layer should confirm:

- intake flow within expected band
- no severe intake blockage indication
- pretreatment differential pressure acceptable
- desalination path healthy
- polished water conductivity within specification
- clean-water reserve above minimum startup threshold

### Failure behavior

If water treatment fails:
- electrolyzer remains locked out
- berth connection may still support battery recharge
- vessel may still depart on stored hydrogen plus battery if dispatch allows
- maintenance action required is logged

---

## Phase 5 — Electrolysis and hydrogen replenishment

### Description

The vessel is berthed, supplied with external power, and actively generating
hydrogen onboard.

### System condition

- electrolyzer active
- gas-liquid separation active
- drying and purity path active
- compressor active when permitted
- storage charging active when permitted
- ventilation proven
- gas detection live
- operator alarms and trends active

### Purpose

This is the main replenishment phase for onboard hydrogen generation.

### Core logic

This phase shall only proceed if all permissives are true:

- clean-water quality valid
- ventilation proven
- no active gas trip
- storage pressure path valid
- compressor healthy
- purge logic healthy
- no maintenance lockout
- shore power sufficient for process demand

### Typical use

This phase is expected to run:
- overnight
- during extended berth windows
- during planned recharge intervals

### Notable non-claim

This phase is not intended to happen mainly while the vessel is underway.

### Failure behavior

If a major fault occurs:
- electrolyzer stops
- compressor stops
- local isolation closes as required
- storage returns to safe isolated configuration
- ventilation remains active if available
- event is logged
- restart is blocked until permissives are restored

---

## Phase 6 — Pre-departure readiness

### Description

The vessel has completed or ended berth-side replenishment and is preparing to
leave berth.

### System condition

- electrolyzer off
- compressor off unless completing post-process stabilization
- storage isolated and confirmed
- fuel-cell path available
- battery charge state confirmed
- alarms reviewed
- dispatch status known

### Required confirmations

Before departure, the system should confirm:

- usable hydrogen inventory above mission minimum
- battery state of charge above dispatch threshold
- no unresolved hydrogen leak alarm
- fuel-cell startup path healthy
- required purge completed
- shutdown valves in correct travel position
- vent path not obstructed
- maintenance barriers cleared

### Dispatch outcome categories

The vessel should be categorized as one of:

- **Green dispatch** — full planned mission allowed
- **Amber dispatch** — limited mission or reduced endurance
- **Red dispatch** — departure blocked

### Purpose

This phase prevents operators from leaving berth with an unresolved process
condition disguised as a minor warning.

---

## Phase 7 — Vessel operation on fuel-cell plus battery hybrid power

### Description

The vessel is underway and using stored hydrogen plus battery support.

### System condition

- fuel-cell modules active
- battery buffering active
- propulsion and hotel loads supplied
- controls, logging, and safety systems active
- electrolysis inactive under normal concept operation
- storage supply regulated to fuel-cell demand

### Power behavior

Typical operating logic:

- fuel cells carry steady base load
- battery handles transient maneuvering peaks
- battery smooths load response
- fuel cells recharge or sustain battery within defined limits during lower-load
  periods where appropriate

### Purpose

This is the main vessel-operating state.

### Required protections

During this phase, the system shall continue to supervise:

- hydrogen leak risk
- enclosure ventilation status
- fuel-cell health
- battery thermal and electrical state
- isolation valve state
- black-start reserve margin
- abnormal pressure or temperature trend

### Failure posture

This phase is built on the assumption that faults can occur underway.

The vessel therefore needs a controlled path into degraded operation.

---

## Phase 8 — Degraded operation / return-to-berth mode

### Description

A fault or subsystem loss has occurred, but enough capability remains for
controlled return or restricted operation.

### Typical triggers

This phase may be entered due to:

- loss of electrolyzer capability while berthed or underway
- compressor fault
- minor non-ignited leak alarm that leads to hydrogen process isolation
- partial fuel-cell module loss
- water-treatment lockout
- partial sensor disagreement
- restricted battery condition
- non-catastrophic ventilation issue in a nonactive process segment

### Possible degraded modes

Examples include:

- battery-dominant harbor return mode
- single-fuel-cell-module mode
- no-electrolysis / no-replenishment mode
- reduced-speed dispatch limitation
- no-hot-restart until berth inspection

### Core principle

A degraded mode is only acceptable if:

- the remaining configuration is understood
- operator limits are explicit
- required protections remain alive
- the vessel can still be supervised safely

### Purpose

This phase protects the project from fake all-or-nothing thinking.

Real vessels need controlled fallback states.

---

## Phase 9 — Shutdown, maintenance, or emergency state

### Description

The vessel is either intentionally shutting down, entering maintenance
configuration, or responding to a significant fault.

### Intentional shutdown path

For controlled shutdown:
- unload fuel cells
- stop nonessential process functions
- secure hydrogen process path
- preserve housekeeping controls as needed
- log final conditions

### Maintenance path

For maintenance:
- isolate hydrogen source paths
- gas-free affected volume where required
- enter maintenance key state
- block restart permissives
- make status visible to crew

### Emergency path

For serious events:
- escalate to defined emergency shutdown level
- isolate hydrogen sources
- de-energize affected equipment as required
- preserve only essential control and alarm functions if safe
- support muster and shore interface procedure

### Purpose

This phase covers the highest-consequence conditions and forces the repo to
treat shutdown as an engineered behavior rather than a hand-wave.

---

## Normal daily cycle summary

A normal concept-day should look roughly like this:

1. vessel completes mission and returns to berth
2. housekeeping remains alive
3. berth power is connected and verified
4. water treatment runs and clean-water reserve is confirmed
5. electrolysis runs overnight or during layover
6. hydrogen inventory is replenished
7. battery is recharged
8. pre-departure checks are completed
9. vessel departs on stored hydrogen plus battery support
10. any faults are handled through degraded mode or return-to-berth logic

This is the operating heartbeat of the architecture.

## Operational truths this CONOPS is enforcing

This file deliberately enforces the following truths:

- the vessel depends on berth access
- electrolysis is a managed process, not a background miracle
- water quality matters
- safety permissives are not optional
- the battery is operationally essential
- degraded modes matter
- dispatch discipline matters
- the system is only credible if failure handling is visible

## What later files must add

This CONOPS does not yet finalize:

- exact alarm thresholds
- exact startup timer values
- exact purge durations
- exact shutdown valve positions
- exact human-machine interface layout
- exact class response logic
- exact port emergency doctrine

Later files should refine those without breaking this operational structure.

## Summary

IX-Marine-H2-Retrofit operates as a berth-supported hydrogen-plus-battery hybrid
vessel architecture in which seawater treatment, onboard electrolysis, hydrogen
storage, fuel-cell power delivery, safety interlocks, and degraded-mode control
are all treated as explicit operational states.

That state visibility is part of the repo's core value.
