# Alternative Pathway Decision Basis

## Purpose

This file locks the alternative-fuel and propulsion-pathway decision basis for
IX-Marine-H2-Retrofit.

It exists because the repo would be weaker if it only said "hydrogen" without
showing that other obvious pathways were considered and deliberately rejected,
deferred, or bounded.

This file answers the practical question:

**Why is this repo centered on hydrogen plus battery hybrid for the reference
vessel, and what else, if anything, should the architecture intentionally
support?**

## Scope

This file covers concept-stage comparison and lock decisions for:

- battery-electric only
- hydrogen plus battery hybrid
- methanol retrofit
- ammonia retrofit
- drop-in biofuel / HVO use
- generic fuel-ready conversion posture

This file does **not** attempt to turn IX-Marine-H2-Retrofit into a
multi-fuel-all-at-once repo.

## Requirements traceability

This file directly supports:

- **R-010** hydrogen plus battery hybrid architecture
- **R-011** battery supports transient maneuvering, black-start, and degraded
  return-to-berth operation
- **R-070** define when hydrogen is made onboard versus loaded onboard
- **R-100** present decision variables, not just a hardware sketch
- **R-101** avoid universal claims
- **R-102** make the real justification visible instead of forcing one answer
  onto every vessel

It also operates under:

- **A-002** harbor / port utility vessel focus
- **A-003** hydrogen is not the only electrical source onboard
- **A-008** operator values local emissions reduction and strategic value
- **A-011** hazard visibility over simplicity theater
- **C-002** no universal vessel applicability
- **C-005** no strong green claim without source-boundary clarity
- **C-009** no fake economic certainty

## Locked pathway decision

The repo is locked to the following decision:

### Primary architecture
**Hydrogen plus battery hybrid**

### Supported supporting path
**Shore-powered replenishment plus optional backup loaded hydrogen**

### Limited fallback support
**Optional HVO / renewable-diesel-compatible emergency auxiliary interface only,
if an operator chooses to retain one outside the core zero-emission operating
path**

### Explicitly not included as first-class design paths in this repo
- methanol retrofit architecture
- ammonia retrofit architecture
- full multi-fuel-ready architecture
- battery-only architecture as the main repo outcome
- biofuel-as-main-solution framing

This is a deliberate scope lock, not an omission by accident.

## Why the repo is not trying to support everything

Trying to make this repo equally ready for hydrogen, methanol, ammonia, battery,
and every backup liquid fuel would damage the repo in five ways:

1. it would blur the hazard model
2. it would bloat the arrangement logic
3. it would weaken the controls and shutdown clarity
4. it would hide the real vessel penalties
5. it would make the repo feel broad but technically soft

A tight architecture with explicit boundaries is stronger than a vague
everything-ready promise.

## Comparison basis

The pathways are judged here against the locked reference vessel:

- harbor / port utility workboat
- daily return to berth
- short-sea / bounded mission profile
- strong local emissions and noise sensitivity
- tolerance for higher procedure burden if the technical value is real
- physical space available for meaningful integration

The comparison categories below are qualitative on purpose.
This repo does not have vessel-specific procurement quotes or a final operator
economic model.

## Comparison matrix

| Pathway | Best-fit strengths | Main weaknesses for this repo | Repo decision |
|---|---|---|---|
| Battery-electric only | simple local-emissions story, quiet operation, strong for short duty | charging-time dependence, heavy battery mass for full mission flexibility, weaker fit if duty has sharp peaks and long service windows between full charge are not guaranteed | not the main repo, but battery remains essential as hybrid support |
| Hydrogen + battery hybrid | stronger zero-emission harbor fit, better steady-load/peak-load split, strategic decarbonization value, allows berth-generated fuel concept | storage volume penalty, safety burden, port dependence, capex burden, procedure burden | **selected primary architecture** |
| Methanol retrofit | easier liquid-fuel logistics in some contexts, simpler storage than compressed H2 | changes repo into a very different fuel and machinery problem, weakens the onboard seawater-to-fuel concept, different emissions/safety/control story | excluded from this repo |
| Ammonia retrofit | serious long-term maritime interest in some contexts, carbon-free at fuel level | toxic handling burden, very different hazard model, not aligned to harbor proof-of-concept simplicity, would radically change crew and safety basis | excluded from this repo |
| Biofuel / HVO | easiest legacy operational continuity, lower change burden, familiar liquid-fuel operations | does not justify the hydrogen architecture, weaker as a transformative retrofit repo, easier operationally but not the same strategic system | allowed only as optional emergency auxiliary compatibility idea |
| Generic fuel-ready conversion | broad future optionality | usually vague, often hides real design tradeoffs, encourages under-specified architecture | rejected for this repo |

## Path-by-path decision logic

### 1) Battery-electric only

#### Why it was considered
Battery-electric is an obvious competitor for short-sea or harbor use because it
offers:
- quiet operation
- strong local emissions reduction
- no hydrogen-process complexity
- relatively understandable charging logic

#### Why it was not selected as the main repo
Battery-only becomes weaker for this repo's intended framing because:

- the repo is specifically built around seawater-derived process water and
  hydrogen generation at berth
- the concept wants a vessel that can use hydrogen as stored energy, not only as
  direct shore-power transfer through batteries
- very large battery-only scaling can create serious mass and charging-time
  pressure depending on duty rhythm
- the hybrid path gives a better split between:
  - battery for peaks and black-start
  - hydrogen for steady sustained electrical supply

#### What survives from the battery-only idea
A lot survives:
- battery remains core to the architecture
- black-start remains battery-first
- degraded return remains battery-supported
- maneuvering peaks remain battery-buffered

So battery-electric was not rejected as useless.
It was rejected as the **sole** architecture.

### 2) Hydrogen plus battery hybrid

#### Why it was selected
This path fits the repo best because it supports all of the following at once:

- a real role for onboard seawater-to-process-water treatment
- berth-oriented hydrogen generation
- explicit storage and fuel-cell architecture
- battery support for dynamic marine loads
- a strong local-emissions and technology-demonstration story
- a bounded harbor / short-sea use case where port dependence is acceptable

#### Why the hybrid split matters
Hydrogen plus battery hybrid is stronger than hydrogen-only because:

- batteries handle fast transients better
- batteries support black-start
- batteries preserve degraded harbor return potential
- fuel cells can carry the steadier base load
- the system becomes more fault-tolerant than a pure hydrogen-only story

#### Locked repo meaning
This is the primary path.
Everything else in this repo is subordinate to making this one path coherent.

### 3) Methanol retrofit

#### Why it was considered
Methanol matters in maritime discussion because it is:
- a liquid fuel
- more familiar logistically than compressed hydrogen in some cases
- often discussed as a retrofit path

#### Why it was excluded from this repo
Methanol is excluded because it would distort the repo away from its actual
mission:

- it does not fit the seawater-to-hydrogen architecture
- it changes the fueling, storage, combustion or conversion, and hazard logic
- it creates a second major fuel identity that this repo does not need
- it would encourage vague "maybe hydrogen, maybe methanol" positioning

That would weaken the repo badly.

### 4) Ammonia retrofit

#### Why it was considered
Ammonia is relevant in maritime decarbonization conversation because it is often
discussed as a future carbon-free shipping fuel.

#### Why it was excluded from this repo
Ammonia is excluded because:

- the toxicity and hazard model are materially different
- the crew-safety posture becomes much heavier and different
- the reference harbor-vessel proof-of-concept gets more complicated instead of
  cleaner
- it would derail the architecture from hydrogen-generation discipline into a
  different marine-fuel program

This repo is not the place to mix that in.

### 5) Biofuel / HVO

#### Why it was considered
Biofuel / HVO matters because it is often the easiest low-disruption path for
existing vessels.

#### Why it is not the main repo path
It is not the main path because:

- it does not justify the electrolyzer, hydrogen storage, or fuel-cell
  architecture
- it does not create the same systems-learning value
- it would turn the repo into a lower-ambition drop-in fuel transition study

#### What is allowed
The repo may acknowledge an **optional HVO-compatible emergency auxiliary
interface** as a bounded owner choice outside the core zero-emission operating
path.

That means:
- not the main propulsion claim
- not the main repo identity
- not a second full architecture

Just a bounded resilience option if later included.

### 6) Generic fuel-ready conversion

#### Why it was considered
"Fuel-ready" language sounds attractive because it suggests future flexibility.

#### Why it was rejected
It was rejected because generic fuel-ready framing often means:

- weak hazard specificity
- vague layout decisions
- fake optionality
- controls and shutdown logic that never get fully disciplined
- a repo that sounds flexible but is not actually decision-grade

This repo is stronger by being explicit.

## Final inclusion and exclusion rules

### Included as core
- hydrogen generation at berth
- compressed hydrogen storage
- fuel-cell power path
- battery power path
- shore-power dependence
- backup loaded hydrogen path

### Included as bounded support
- HVO / renewable-diesel-compatible emergency auxiliary interface only if later
  needed by operator concept
- battery-dominant degraded return mode
- non-mission-critical helper-source contribution to housekeeping functions

### Excluded
- methanol systems
- ammonia systems
- broad fuel-ready boilerplate
- liquid-fuel multimode architecture
- battery-only repo reframing
- “supports everything” wording

## Architecture consequences of the decision

Because hydrogen plus battery hybrid is selected and the rest are not, the repo
must stay consistent with these consequences:

1. hydrogen safety remains the dominant hazard basis
2. battery remains mandatory, not optional
3. berth power remains central
4. water treatment remains a first-class subsystem
5. storage volume penalty remains visible
6. fuel-cell and purge logic remain core
7. methanol- or ammonia-specific design baggage stays out

That clarity is part of the repo's value.

## Best-fit justification for the selected path

The selected path is strongest when the operator needs:

- lower local emissions at port
- quieter operation
- strategic hydrogen-learning value
- a bounded pilot platform
- daily berth access
- a vessel class that can tolerate added integration burden

It is not strongest when the operator wants:
- minimum change
- minimum training burden
- immediate easy payback
- universal deep-sea applicability

## What this file can and cannot solve

### What it can solve now
It can lock:
- which pathways are in and out
- why battery remains core
- why methanol and ammonia stay out
- why HVO is only a bounded fallback option
- why generic fuel-ready language is rejected

### What it cannot honestly solve now
It cannot finalize:
- operator-specific fleet strategy
- local fuel availability
- real-vessel comparative ROI across all fuel options
- future regulation outcomes
- future commodity-price advantage of one fuel over another

## Verification intent

Later repo files should make it obvious that:

- the architecture truly behaves like hydrogen plus battery hybrid
- battery is structurally and operationally central
- no methanol/ammonia design baggage appears by accident
- any emergency auxiliary fallback is clearly bounded and not confused with the
  main architecture
- the repo does not drift into fake “fuel-ready for everything” language

## Explicit non-claims

This file does **not** claim:

- hydrogen is the best answer for all marine retrofits
- methanol or ammonia are bad technologies in general
- battery-only is wrong for all harbor vessels
- HVO has no place in maritime transition
- one pathway wins under all regulatory and electricity-price scenarios

It only claims what is locked for **this repo**.

## Summary

IX-Marine-H2-Retrofit is intentionally **not** a multi-fuel repo.

The locked design choice is:

- **hydrogen plus battery hybrid** as the main architecture
- **shore-powered berth generation plus optional backup loaded hydrogen**
- **optional HVO-compatible emergency auxiliary interface only if later
  bounded**
- **no methanol**
- **no ammonia**
- **no vague fuel-ready-everything posture**

That is the tightest and strongest frame for the project.
