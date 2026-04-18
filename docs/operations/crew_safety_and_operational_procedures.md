# Crew Safety and Operational Procedures Basis

## Purpose

This file defines the concept-stage crew safety basis and operating-procedure
framework for IX-Marine-H2-Retrofit.

It exists because a technically clever architecture is still weak if the human
side is vague.

This file answers the practical questions that follow immediately after the
hardware discussion:

- what the crew is expected to do
- what the crew is not allowed to do
- what minimum procedural gates must exist before startup, berth generation,
  dispatch, maintenance, or restart
- what personal safety posture is required around hydrogen-related operations
- how degraded or emergency states should change crew behavior

This file is concept-stage only.
It does not replace owner procedures, class rules, flag requirements, company
SMS documentation, or local port instructions.

## Scope

This file covers concept-stage treatment of:

- normal operating roles
- startup and pre-departure procedural gates
- berth generation procedure basis
- backup loading / service evolution basis
- maintenance-entry and maintenance-exit basis
- personal protective and personal-monitoring posture
- hot-work restrictions
- degraded-operation rules
- emergency-response interface rules
- training burden and drill expectations

## Requirements traceability

This file directly supports:

- **R-053** layered emergency shutdown states
- **R-054** explicit handling for leak, ignited release, purge failure, sensor
  failure, blackout recovery, flooding or spray ingress, and maintenance error
  states
- **R-070** define when hydrogen is generated onboard versus loaded from shore
- **R-072** include emergency-response interfaces between vessel and shore
- **R-073** strong dependency on port procedures and shore-side coordination
- **R-080** monitoring and controls concept with process, safety, and
  maintenance visibility
- **R-081** alarm prioritization
- **R-082** lockouts tied to maintenance-state conflicts and unresolved safety
  alarms
- **R-100** present training load and operating burden as decision variables

It also operates under:

- **A-008** operator values local emissions reduction and strategic value
- **A-009** maintenance access is first-order
- **A-011** hazard visibility over simplicity theater
- **C-006** no fake class or approval certainty
- **C-009** no fake economic certainty

## Locked crew-safety philosophy

The crew-safety philosophy for this repo is locked as follows:

- no casual hydrogen operation
- no single-person unsupervised maintenance in hydrogen-affected spaces
- no hot work near hydrogen systems without formal isolation and gas-free
  confirmation
- no assumption that "normal day" means low procedure discipline
- no startup or restart on ambiguous alarm state
- no hidden maintenance bypass treated as normal service
- no emergency response based only on memory; state and interfaces must be
  visible

## Operating-role concept

The concept assumes a small professional vessel crew with clearly defined
responsibilities during hydrogen-related operations.

The repo uses the following concept roles:

### Role O-1 — Vessel operator / watchkeeper
Primary responsibilities:
- confirm status on HMI
- acknowledge and interpret operational alarms
- execute startup / shutdown from normal operating interface
- confirm dispatch classification before departure
- enforce operating restrictions in degraded mode

### Role O-2 — Engineering / technical maintainer
Primary responsibilities:
- service treatment, gas, battery, and controls hardware
- enter and clear maintenance state correctly
- perform detector checks and service confirmations
- perform isolation and restoration procedures
- verify post-maintenance readiness

### Role O-3 — Berth-side coordinating crew member
Primary responsibilities:
- coordinate berth power or service readiness
- support restricted-zone discipline during active berth operations
- support communications between vessel and shore during hydrogen-related
  operations
- verify that conflicting berth activities are not active nearby

### Role O-4 — Command authority
Primary responsibilities:
- approve degraded dispatch or block departure
- authorize restart after significant abnormal events within company and
  procedural authority
- coordinate emergency communication and muster decisions

One person may hold more than one role on a small vessel, but the functions
still need to exist.

## Personal safety posture

### Locked personal safety rules

The architecture assumes the following personal safety posture:

1. no casual entry into hydrogen-affected service area during active abnormal
   alarm state
2. no single-person maintenance in hydrogen-affected spaces
3. portable personal hydrogen detector should be used during relevant
   maintenance or troubleshooting work
4. maintenance entry requires system state awareness, not guesswork
5. no assumption that powered-down means gas-free
6. no hot work without formal isolate / gas-free / permit path
7. crew must know the location of:
   - storage zone
   - vent / relief outlet
   - emergency stop concept
   - muster or restricted-zone boundary concept

### Personal protective equipment concept

This repo does not prescribe a final PPE standard, but it assumes at minimum
that hydrogen-related maintenance or abnormal-response work may require:

- basic marine industrial PPE appropriate to the vessel
- portable gas detection where work exposure justifies it
- task-appropriate eye / hand protection for process or maintenance work
- controlled communication path to another crew member

The repo deliberately avoids pretending PPE is the main safety barrier.
It is only one layer.

## Normal startup procedure basis

The concept startup basis is:

1. housekeeping-alive state confirmed
2. no active emergency shutdown state
3. gas detector health normal in affected zones
4. required ventilation proof healthy
5. maintenance state not active
6. required subsystem ready signals valid
7. operator verifies that startup is not blocked by unresolved trip or lockout
8. startup command issued only after status review
9. operator confirms state transition on HMI

### Locked rule
If startup is blocked, the operator must be shown **why** it is blocked.
The crew is not expected to guess.

## Pre-departure / dispatch procedure basis

Before departure, the concept requires the crew to verify at minimum:

- dispatch class is green or amber with accepted limits
- hydrogen inventory is above required threshold for planned mission category
- battery SOC and reserve margin are acceptable
- no unresolved severe gas alarm or shutdown state exists
- no unresolved maintenance lockout exists on mission-critical hardware
- fuel-cell path readiness is valid
- vent / relief area is not in abnormal condition
- recent berth generation or loading session ended in secured state

### Dispatch classes

The crew should see one of:

- **Green** — planned mission permitted
- **Amber** — reduced mission or conditional release only
- **Red** — departure blocked

Amber dispatch must be explained in plain operational language.

## Berth hydrogen-generation procedure basis

The baseline berth-generation procedure is conceptually:

1. vessel secured at berth
2. housekeeping alive
3. berth power interface status known
4. required emergency interface state known
5. active restricted-zone awareness established
6. water-treatment path healthy
7. clean-water reserve sufficient
8. detector and ventilation states healthy
9. electrolysis start permitted
10. charging session supervised through HMI and alarm states
11. session ends through controlled stop
12. storage secured and post-session state reviewed

### Locked procedural rule
Hydrogen generation at berth is not treated as a "background invisible process."
It is a supervised operational state.

## Backup loading / service evolution basis

If backup delivered hydrogen or other hydrogen-service evolution occurs, the
concept procedure is:

1. vessel secured
2. relevant generation path isolated as required
3. detector and controls live
4. temporary restricted zone active
5. conflicting berth operations checked
6. transfer readiness confirmed
7. controlled service evolution performed
8. post-transfer or post-service secure state confirmed
9. dispatch status recomputed

### Locked rule
Service evolution is never treated as casual fueling while routine unrelated
work continues nearby without coordination.

## Maintenance-entry basis

Before maintenance on hydrogen-related or safety-critical equipment, the concept
expects the following:

1. affected subsystem identified
2. maintenance state entered in controls
3. hydrogen source path isolated as required
4. gas-free or purge-related condition confirmed where procedure requires it
5. restart path blocked
6. another qualified person aware of the work
7. portable detection used where task exposure justifies it
8. no hot work unless separately permitted and confirmed safe

### Locked rule
Power-off alone is not treated as proof of gas-free condition.

## Maintenance-exit basis

Before returning equipment to service after maintenance, the concept expects:

1. work area inspected
2. tools / temporary devices removed
3. valves / isolation points restored to intended service state
4. detector or sensor health restored and verified where relevant
5. maintenance lockout cleared deliberately, not implicitly
6. startup permissives re-evaluated from known safe baseline
7. event log reflects maintenance entry and exit
8. post-maintenance functional check completed

### Locked rule
No maintenance bypass may silently remain active and still be interpreted as
normal service by the controls layer.

## Hot-work control basis

The repo is locked to a conservative hot-work posture.

### Hot-work concept rules

- no hot work in hydrogen-affected areas during active hydrogen operation
- no hot work near storage, manifold, or hydrogen-bearing enclosure without
  formal isolate and gas-free confirmation
- no assumption that weather deck automatically makes hot work acceptable
- maintenance state and work permit concept must make the hot-work conflict
  visible

This repo does not define final permit forms.
It does define that the architecture must assume hot-work conflict is real.

## Degraded-operation crew rules

If the vessel enters degraded operation, the crew must not be left guessing what
the new limitations are.

### Locked degraded-operation basis

The HMI and procedures should make clear at minimum:

- whether hydrogen generation is unavailable
- whether one fuel-cell module is unavailable
- whether the vessel is battery-dominant only
- whether dispatch is reduced-speed or reduced-endurance
- whether departure is blocked
- whether restart of affected subsystem is allowed

### Crew response expectation

In degraded mode, the crew should:

- accept reduced mission limits visibly
- avoid trying to "push through" amber or red constraints by habit
- preserve reserve margin more conservatively
- prioritize return-to-berth if required by state logic or alarm condition

## Alarm-response basis

### Advisory alarms
Crew action:
- acknowledge
- review
- continue with awareness unless procedure says otherwise
- schedule service or inspection where needed

### Action-required alarms
Crew action:
- acknowledge
- assess whether dispatch limit or process stop is required
- follow bounded operating restriction
- clear cause before normal release if procedure requires it

### Trip / immediate safety alarms
Crew action:
- do not attempt casual restart
- follow emergency or shutdown procedure
- assess whether vessel is in degraded return or full emergency state
- coordinate with command authority and shore if required
- preserve scene discipline

## Emergency-response basis

The concept assumes emergency response must bridge machine state and crew action.

### Minimum crew emergency expectations

Crew should be able to identify:

- whether hydrogen is isolated
- whether the vessel is in ESD-2 or ESD-3 type state
- whether battery-only safe return remains available
- where not to enter
- whether berth responders need notification or active coordination
- where vent / relief path is located conceptually

### Emergency priorities

The crew concept priority order is:

1. life safety
2. hazard isolation
3. emergency visibility and communication
4. controlled vessel state
5. recovery only after abnormal condition is understood

### Locked rule
A major hydrogen-related event is not followed by casual reset and continuation.

## Training burden basis

This repo does not pretend training burden is low.

### Locked training assumptions

The concept should assume at minimum:

- **3 to 5 days** of operator-focused training for routine use, alarm
  interpretation, dispatch meaning, and berth procedures
- **2 additional days** of maintenance-focused training for service, lockout,
  detector checks, restoration logic, and maintenance-state handling
- recurring emergency drills and refreshers

These are engineering planning assumptions, not regulatory mandates.

### Drill expectations

The concept assumes recurring drills should cover at minimum:

- hydrogen leak response
- ignited-release / major-event recognition
- ventilation-loss response
- blackout and black-start recovery awareness
- maintenance-state conflict recognition
- berth emergency coordination

## Human-factors design rules for the repo

The repo is locked to the following human-factors rules:

- blocked states must explain themselves
- amber dispatch must explain its operational consequence
- serious alarms must not look like minor warnings
- maintenance mode must be visibly different from normal operation
- crew should not have to infer storage or vent location from memory alone
- critical actions should be gated through state visibility and procedure, not
  hope

## What this file can and cannot solve

### What it can solve now
It can lock:
- procedural expectations
- crew role expectations
- degraded-operation posture
- maintenance-entry / maintenance-exit discipline
- hot-work conflict posture
- training burden visibility

### What it cannot finalize now
It cannot finalize:
- company SMS documents
- legal crewing rules
- final permit-to-work forms
- class / flag-approved emergency procedures
- port-authority-specific response doctrine
- exact training syllabus content for a real operator

## Verification intent

Later proof-of-concept and controls artifacts should make it possible to inspect:

- whether the HMI actually supports the crew behaviors assumed here
- whether blocked and degraded states are understandable
- whether maintenance mode is visible and hard to misuse
- whether berth-generation and backup-loading modes are clearly distinct
- whether emergency states produce obvious crew-facing consequences

## Explicit non-claims

This file does **not** claim:

- final legal operating procedure for a real vessel
- final emergency manual content
- final hot-work permit form
- final training certification requirement
- that human error can be eliminated

It defines the minimum operational discipline this repo needs in order to remain
credible.

## Summary

IX-Marine-H2-Retrofit is only believable if the crew side is as disciplined as
the hardware side.

This file locks that posture:

no casual hydrogen operation, no single-person hydrogen maintenance, no hot work
without formal isolation, no ambiguous restart after major events, no hidden
degraded state, and no pretense that the port-supported hydrogen workflow is a
low-procedure activity.
