# Fire, Explosion, and Hazardous-Zone Basis

## Purpose

This file defines the concept-stage fire / explosion protection basis and
hazardous-zone layout discipline for IX-Marine-H2-Retrofit.

It exists because the repo would be weak if it described hydrogen generation,
storage, and use without answering the harder arrangement question:

**Where can hydrogen go, where must people and ignition-capable equipment stay
out of the way, how should abnormal release be vented or relieved, and what
fire / explosion design posture is being assumed before a real vessel-specific
dispersion and class review exists?**

This file is concept-stage only.
It does not claim final hazardous-area classification, final class acceptance,
or final quantitative dispersion-study output for a real hull.

## Scope

This file covers:

- fire and explosion design philosophy
- hazardous-zone layout basis
- weather-deck storage fire / explosion posture
- enclosure and cabinet abnormal-release philosophy
- vent / relief routing discipline
- electrical de-energization basis in affected zones
- temporary restricted zones during berth-side operations
- relationship between design placeholders and later real-vessel study

## Requirements traceability

This file directly supports:

- **R-031** gas drying, isolation, pressure management, and storage control
- **R-032** storage arranged so venting, isolation, and maintenance access are
  addressable
- **R-050** hydrogen-specific gas detection integration
- **R-051** ventilation proving for hydrogen-bearing spaces and enclosures
- **R-052** safe state on loss of required ventilation
- **R-053** layered emergency shutdown states
- **R-054** explicit handling for hydrogen leak and ignited release
- **R-060** concept-level allowances for ventilation space and arrangement
- **R-072** emergency response interfaces between vessel and shore

It also operates under:

- **A-009** maintenance access is first-order
- **A-011** hazard visibility over simplicity theater
- **C-006** no fake class certainty
- **C-008** no single-point safety philosophy

## Locked philosophy

The fire / explosion and zoning basis for this repo is locked to the following
philosophy:

- keep normally occupied and accommodation-adjacent spaces gas-safe where
  practicable
- prefer open-weather hydrogen storage rather than burying high-pressure
  inventory in hard-to-vent enclosed spaces if avoidable
- expect leaks and design venting, relief, detection, and isolation accordingly
- do not rely on a single detector, a single fan, or a single shutdown action
  as the whole answer
- treat hydrogen release and ignited release as different abnormal-event cases
- preserve clear keep-clear logic around venting and service interfaces
- use concept placeholders honestly until real dispersion study and class review
  exist

## Core abnormal-event design posture

The architecture assumes three broad abnormal-event families:

1. **non-ignited release**
2. **ignited release**
3. **secondary fire / exposure event near hydrogen equipment**

Each family needs a different immediate design response.

### Non-ignited release posture
Priority:
- detection
- ventilation / dispersion
- isolation
- ignition prevention
- restart inhibition

### Ignited release posture
Priority:
- isolate hydrogen source
- de-energize nonessential affected-zone equipment
- preserve emergency visibility
- protect personnel and boundaries
- avoid casual re-entry or restart

### Secondary fire / exposure posture
Priority:
- prevent heat exposure from escalating into storage or manifold failure
- preserve relief path function
- provide cooling / boundary protection concept
- isolate process segments if safe

## Hazardous-zone concept classes

This repo uses concept-stage zone descriptions to discipline layout before a
real vessel-specific study exists.

These are **repo-internal concept classes**, not class-approved hazardous-area
labels.

### HZ-1 — Routine gas-safe occupied zone

Intent:
- normal crew occupancy
- no casually exposed hydrogen-bearing equipment
- no vent discharge directed into this area
- should remain outside normal hydrogen hazard condition

Examples:
- bridge / control area
- accommodation-adjacent areas
- routine workstations not part of hydrogen handling

### HZ-2 — Gas-managed machinery-adjacent zone

Intent:
- may be near hydrogen systems but arranged to remain non-hazardous in normal
  service through enclosure, ventilation, separation, and shutdown logic

Examples:
- fuel-cell machinery integration area under gas-safe or gas-managed philosophy
- nearby electrical support space separated from hydrogen-bearing equipment

### HZ-3 — Hydrogen-bearing enclosure or cabinet zone

Intent:
- contains equipment where hydrogen release is credible under fault
- requires detector logic, ventilation / extraction discipline where relevant,
  and shutdown / isolation coupling

Examples:
- compressor enclosure
- manifold cabinet
- conditioning cabinet
- hydrogen supply cabinet

### HZ-4 — Open-weather hydrogen equipment zone

Intent:
- external hydrogen storage and related manifold / vent support area
- leak should disperse more readily than in enclosed spaces, but personnel
  separation and ignition control still matter

Examples:
- weather-deck storage rack area
- vent mast root area
- protected manifold access area

### HZ-5 — Temporary active service / transfer zone

Intent:
- temporary restricted zone that exists during active loading, service,
  depressurization, or other hydrogen-handling evolution

Examples:
- backup loading point
- planned controlled service-point use
- temporary offload / defuel interface zone

## Locked hazardous-zone basis

The repo is locked to the following hazardous-zone basis.

### ZB-001 — Accommodation and routine occupied spaces should stay gas-safe
No normal design intent in this repo allows hydrogen-bearing process hardware to
be casually integrated into accommodation or routine occupied spaces.

### ZB-002 — Weather-deck storage is preferred for the reference concept
The reference concept prefers weather-deck storage because it supports:
- clearer venting
- less trapped accumulation risk than deep enclosed placement
- easier emergency visual separation
- more practical heavy-access logistics

### ZB-003 — Critical hydrogen cabinets are treated as local hazard sources
Compressor, manifold, and conditioning enclosures are treated as local hazard
sources that require:
- detection
- ventilation or extraction where relevant
- isolation
- maintainable access
- abnormal-event logic

### ZB-004 — Temporary service operations create temporary restricted zones
Active hydrogen service, loading, or controlled vent-related operations create a
temporary restricted zone even if the surrounding vessel is normally in routine
service state.

### ZB-005 — Placeholder distances are for discipline, not approval
The placeholder keep-clear distances in this repo are only for concept layout
discipline and must not be presented as final approved hazardous-zone
dimensions.

## Placeholder keep-clear basis

### Honest boundary

A real vessel needs:
- leak source definition
- dispersion analysis
- ventilation assessment
- arrangement review
- class and authority input

This repo does **not** have those final results.

### What is locked anyway

For concept-stage layout discipline, the repo uses the following placeholders
unless a later bounded file says otherwise:

- **10 ft horizontal keep-clear** around active vent or service-point concept
- **20 ft vertical keep-clear** above vent outlet concept
- no deliberate HVAC intake, accommodation opening, or routine standing
  position inside those placeholder envelopes
- no casual mooring-operation conflict with those envelopes if avoidable

### Why placeholders still matter

Without placeholders, layout files drift into unrealistic packing.
These values force the repo to preserve space for:
- vent discharge
- emergency access
- separation from normal crew activity
- berth-side operating discipline

## Fire and explosion design basis by area

### Weather-deck storage rack area

#### Locked design basis
The weather-deck storage zone should support:

- protected structural framing
- no casual impact path from normal operations
- deliberate vent / relief routing upward
- no direct venting toward personnel routes or intakes
- visible isolation concept
- no assumption that open weather alone removes all need for detection and
  shutdown logic

#### Fire / explosion posture
If a leak occurs:
- isolate storage or affected branch
- keep area clear
- avoid creating local ignition opportunity
- preserve clear outward vent path

If an ignited release or severe exposure fire occurs:
- escalate to ESD-3
- isolate hydrogen if possible
- support boundary cooling / exposure protection concept
- preserve responder visibility of storage location and vent path

### Compressor / manifold / conditioning enclosure area

#### Locked design basis
These enclosures should support:

- detector coverage
- extraction / ventilation where the safety basis requires it
- local isolation
- no clutter that blocks inspection
- no casual energized-equipment persistence under major gas event
- accessible service and test points

#### Fire / explosion posture
If non-ignited leak:
- alarm
- isolate
- stop affected process
- preserve or command required ventilation

If ignited release:
- ESD-3
- de-energize nonessential affected-zone equipment
- isolate hydrogen
- block restart until formal recovery

### Fuel-cell hydrogen supply area

#### Locked design basis
The fuel-cell supply path should be arranged so that:
- hydrogen-bearing portions are understandable and bounded
- startup depends on purge completion and valid supply state
- leak trip can isolate affected supply path
- gas-safe or gas-managed machinery integration remains the target philosophy

#### Fire / explosion posture
If leak:
- isolate affected supply path
- trip affected fuel-cell module
- preserve battery-backed degraded return only if safe

If ignited release:
- trip all affected fuel-cell paths
- escalate shutdown
- isolate storage as required by the event scope

## Vent and relief philosophy

### Locked philosophy
Venting and relief must be intentional, not improvised.

### Core rules

#### VR-001 — Vent upward and away from routine occupancy
Vent and relief discharge should be routed so that routine personnel presence is
not treated as acceptable under discharge conditions.

#### VR-002 — Do not vent into HVAC intake or enclosed dead space
The concept must avoid routing abnormal hydrogen discharge into:
- air intakes
- semi-enclosed crew work zones
- hidden recesses
- dead-end architectural pockets

#### VR-003 — Relief path should remain unobstructed
The arrangement must not casually place removable gear, line stowage, or other
obstructions where they can compromise relief-path function.

#### VR-004 — Atmosphere venting is not the normal convenience offload method
Controlled venting may exist as an emergency or bounded service action, but it
is not the repo's normal convenient defuel method.

## Fire / explosion protection features expected in the concept

The concept should visibly include or assume the following protection features:

- hydrogen-specific gas detection in relevant enclosures
- flame detection where ignited release detection materially improves response
- emergency shutdown escalation
- de-energization of nonessential equipment in affected zones
- fire boundary separation between hydrogen process spaces and occupied /
  control-adjacent spaces where relevant
- weather-deck separation and protection for storage
- boundary cooling / exposure protection concept where hydrogen inventory could
  be exposed to nearby fire
- visible vent / relief path

This is a concept-basis list, not a final equipment procurement list.

## Electrical equipment posture in affected zones

### Locked philosophy
The repo does not finalize hazardous-area equipment certification selection, but
it does lock the behavior expected of electrical systems in affected zones.

### Required concept posture
The architecture should support:

- separating essential and nonessential electrical loads in hydrogen-affected
  zones
- de-energizing nonessential loads during major gas or fire event
- preserving critical sensing and controls only where safe and deliberately
  justified
- avoiding the assumption that "if it is powered, it may as well stay powered"

## Temporary service / transfer zone basis

### When this zone exists
HZ-5 is active when the vessel is performing:

- backup hydrogen loading
- controlled service transfer
- bounded depressurization action
- other planned hydrogen-handling evolution outside normal steady operation

### Locked rules
During HZ-5 operations, the concept assumes:

- temporary restricted area is enforced
- crew know the operation is in progress
- relevant detectors and controls are alive
- no conflicting hot work or casual nearby ignition activity is accepted
- berth emergency interface state is known
- vent outlets and service hardware remain visible and unobstructed

## Crew and responder visibility requirements

A hazardous zone that exists only in the engineer's head is weak.

The concept therefore expects:

- visible indication when the vessel is in hydrogen process or service state
- visible identification of storage location
- visible knowledge of vent / relief outlet location
- clear restricted-zone concept during active operations
- operator / responder access to emergency status

## What this file can and cannot solve

### What this file can solve now
It can lock:
- arrangement discipline
- placeholder keep-clear logic
- fire / explosion posture by area
- vent / relief routing philosophy
- temporary restricted-zone concept
- de-energization philosophy
- visibility rules for crew and shore responders

### What this file cannot honestly finalize now
It cannot finalize:
- approved hazardous-area classification for a real hull
- exact zone radii for real service
- exact vent dispersion behavior for a specific vessel geometry
- final fire boundary approvals
- final detector count and exact certified equipment set
- final authority-approved berth exclusion doctrine

## Verification intent

Later proof-of-concept, arrangement, and assembly files should prove at concept
stage that:

- hydrogen storage is not arranged inside obviously weak occupied-space logic
- vent paths remain upward and clear
- placeholder keep-clear envelopes are actually respected in layout
- cabinet / enclosure hazard sources are treated as real sources
- active service zones are not treated as business-as-usual walkways
- electrical de-energization philosophy is visible in the controls logic

## Explicit non-claims

This file does **not** claim:

- final class hazardous-area acceptance
- final explosion analysis
- final dispersion-study approval
- final firefighting doctrine
- that placeholder keep-clear values are sufficient for every real vessel
- that weather-deck storage eliminates all explosion or fire risk

## Summary

The fire / explosion and hazardous-zone basis for IX-Marine-H2-Retrofit is
simple but strict:

keep occupied spaces gas-safe where practicable, treat hydrogen enclosures as
local hazard sources, prefer weather-deck storage with deliberate venting, use
placeholder keep-clear distances honestly until a real study exists, and never
pretend that detection alone solves the fire / explosion problem.

This file is the arrangement-discipline bridge between concept and real hazard
review.
