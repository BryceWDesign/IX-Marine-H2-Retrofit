# Economics and Operational Case

## Purpose

This file defines the concept-stage economics, downtime, training, dependency,
and justification basis for IX-Marine-H2-Retrofit.

It exists to answer the part that weak concept repos usually avoid:

- what this likely costs
- how long the retrofit may take
- what the maintenance burden really looks like
- how dependent the vessel becomes on port and shore support
- whether this is likely to pay back on fuel savings alone
- what the actual justification is if fuel savings do not carry the case

This file is intentionally blunt.
It does not sell the architecture as a universal financial win.

## Scope

This file covers concept-stage treatment of:

- capex range
- retrofit downtime
- maintenance burden
- crew training load
- port dependency
- shore-power dependency
- expected fuel-cost sensitivity
- emissions delta framing
- payback logic or non-payback justification
- decision posture for the reference vessel class

## Requirements traceability

This file directly supports:

- **R-070** define when hydrogen is generated onboard versus loaded onboard
- **R-071** define berth-side demand and replenishment timing
- **R-073** strong dependency on port procedures and shore-side coordination
- **R-100** present capex, downtime, maintenance burden, training load, and
  operating dependency as decision variables
- **R-101** do not present universal payback claims
- **R-102** make strategic and operational justification visible rather than
  pretending direct short-term fuel savings always carry the project

It also operates under:

- **A-008** operator values local emissions reduction and strategic benefit
- **A-011** hazard visibility over simplicity theater
- **C-005** no strong green claim without source-boundary clarity
- **C-009** no fake economic certainty

## Locked economic philosophy

The economics posture for this repo is locked as follows:

- this is **not** presented as a guaranteed low-cost retrofit
- this is **not** presented as a universal fuel-savings winner
- the value case is strongest where:
  - local emissions matter
  - quiet operation matters
  - demonstration or strategic decarbonization value matters
  - port-supported operating rhythm is already normal
- cost, downtime, and training burden are part of the architecture and must stay
  visible

## Reference-vessel economic basis

This file is tied to the locked reference vessel:

- harbor / port utility workboat
- daily return to berth
- approximately 0.9 to 1.1 MWh/day mission basis
- hydrogen plus battery hybrid
- berth-oriented electrolysis
- weather-deck hydrogen storage
- 2 × 125 kW fuel-cell modules
- 500 kWh LFP battery
- 450 kW-class PEM electrolyzer

All estimates in this file are reference-vessel concept estimates only.

## Capex range

### Locked concept estimate

For the reference vessel, the total retrofit concept range is:

**about $5 million to $9 million**

### What this range is intended to cover

This concept-stage range is intended to include the major architecture blocks:

- seawater intake and treatment hardware
- PEM electrolyzer package
- compression and gas-conditioning hardware
- compressed hydrogen storage rack and manifold system
- 2 × fuel-cell modules
- 500 kWh-class battery system
- controls, safety, gas detection, ventilation, and ESD hardware
- integration engineering
- structural and installation work
- test / commissioning burden at concept level

### Why the range is wide

The range is wide because final cost moves with:

- vessel arrangement difficulty
- legacy-equipment removal scope
- yard rate
- vendor packaging choices
- degree of redundancy
- extent of structural reinforcement
- controls and safety implementation depth
- level of port-interface preparation required

### Honest boundary

This is an engineering planning estimate, not a vendor quote and not a purchase
commitment.

## Capex breakdown posture

The repo does not lock a single cost number for each subsystem, but it does
assume the largest cost pressure comes from the following buckets:

### High-pressure cost buckets
- electrolyzer package
- fuel-cell modules
- battery system
- hydrogen storage package
- compressor / conditioning package
- marine integration and yard labor

### Medium-pressure cost buckets
- water treatment
- ventilation and gas detection
- controls and HMI
- structural supports and routing

### Lower but still real cost buckets
- housekeeping energy hardware
- signage / placarding / local interface hardware
- service tooling and local maintenance provisions

## Retrofit downtime

### Locked concept estimate

Expected retrofit downtime for the reference vessel is:

**about 20 to 30 weeks**

### What this duration includes conceptually

- engineering and design freeze
- vessel survey and arrangement confirmation
- procurement lead time overlap
- legacy equipment removal where needed
- structural and support modifications
- machinery installation
- electrical integration
- controls and safety integration
- dockside testing
- harbor trial / bounded commissioning logic

### Why it matters

This is a serious operational penalty.
The architecture cannot be sold as a "quick bolt-on upgrade."

### What can make downtime worse

- difficult legacy machinery removal
- tight vessel arrangement
- unexpected stability / structure issues
- long-lead hydrogen or FC vendor items
- controls integration surprises
- port / authority coordination delays

## Maintenance burden

### Locked concept judgment

The maintenance burden is:

**moderate to high**

especially in early pilot or first-of-class use.

### Major recurring maintenance families

The concept expects recurring attention on:

- intake strainer and sea chest condition
- pretreatment elements
- desalination and polishing elements
- conductivity instrumentation
- gas detectors and bump testing
- compressor service
- fuel-cell stack hour tracking and balance-of-plant checks
- ventilation fan and proving checks
- vent / relief path inspections
- battery health and thermal-system checks

### Maintenance burden posture

This repo does not pretend the architecture is "low-maintenance because electric."

It is lower in some combustion-related areas but higher in:
- process discipline
- detector discipline
- water treatment
- hydrogen-specific service
- controls and safety-state verification

### Maintenance benefit trade

The likely trade is:

- **less** diesel-style exhaust and combustion complexity
- **more** hydrogen / process / instrumentation / water-quality discipline

## Crew training load

### Locked concept estimate

The architecture assumes at minimum:

- **3 to 5 days** operator-focused training
- **2 additional days** maintenance-focused training
- recurring emergency and degraded-mode drills

### Why this burden exists

The crew must understand:

- berth generation state
- dispatch classification meaning
- alarm classes
- hydrogen isolation and restart logic
- maintenance-state discipline
- blackout / black-start posture
- restricted-zone behavior during service operations

### Honest posture

Training is a real adoption burden.
It is not optional overhead.

## Port dependency

### Locked concept judgment

Port dependency is:

**high**

### Why dependency is high

The reference architecture depends on the port or home berth for:

- sustained electrical capacity for onboard generation
- controlled operating window
- emergency coordination
- restricted-zone discipline during hydrogen-related operations
- practical support when onboard generation is unavailable
- known berth geometry relative to venting and occupancy

### Strategic consequence

This architecture makes the most sense where the operator has:

- a reliable home berth
- predictable return-to-port rhythm
- willingness to coordinate procedures
- meaningful interest in emissions reduction in that operating area

## Shore-power dependency

### Locked concept judgment

Shore-power dependency is:

**high if onboard electrolysis is the primary replenishment path**

### Meaning

Without shore power, the vessel must rely on one of the following:

- stored hydrogen already onboard
- backup delivered hydrogen loading
- reduced mission
- fallback non-hydrogen support path if the operator chose to keep one outside
  the repo's core framing

### Consequence

The repo cannot honestly frame onboard electrolysis as infrastructure-light.

## Fuel-cost sensitivity

### Locked concept judgment

Fuel-cost sensitivity is:

**highly sensitive to electricity price and hydrogen-production efficiency**

### Why

The biggest recurring energy cost driver is not seawater treatment.
It is:

- electrolysis power
- compression and support parasitics
- berth electricity pricing and availability

### Operating-cost implication

If electricity is expensive or carbon-intensive:

- operating hydrogen cost becomes weaker
- emissions argument can weaken
- operator may prefer backup loading or alternative strategies in some cases

### What the repo must keep visible

The architecture only looks strong on operating-cost grounds if the berth
electricity environment is at least somewhat favorable.

## Concept operating-cost posture

The repo does **not** lock a universal per-day cost, because that would be fake
precision without:

- local electricity price
- local demand charges
- operator duty cycle
- actual vendor efficiency
- actual maintenance program cost

Instead, the repo locks this operational truth:

- hydrogen made by electrolysis is cost-sensitive to electricity
- compressed storage and conditioning are not free
- maintenance and inspection burden are real contributors
- direct fuel-cost advantage is not guaranteed

## Emissions delta

### Locked emissions posture

The repo separates emissions into two frames:

#### Tank-to-wake
Very strong improvement versus diesel-like operation because:
- fuel-cell operation avoids direct CO2 exhaust from the vessel
- local port-area air quality improves materially
- noise and vibration profile may improve

#### Source-boundary / electricity-dependent view
The full climate case depends on:
- where berth electricity comes from
- how low-carbon that electricity actually is
- how much backup delivered hydrogen is used
- how often the system operates on stored hydrogen generated from clean power
  versus other supply conditions

### What this means

The repo may claim:
- strong local emissions benefit
- strong port-area cleanliness benefit

The repo must **not** imply:
- automatic best-case lifecycle decarbonization in every port and grid context

## Payback logic

### Locked conclusion

**Fuel savings alone are not a reliable universal justification for this
retrofit.**

### What that means

This architecture should not be sold as:
- a simple spreadsheet payback play
- a universal lower-fuel-cost answer
- a slam-dunk replacement on pure operating cost

### Stronger justifications

The concept becomes more defensible when justified by one or more of these:

1. **port and near-shore emissions reduction**
2. **noise and vibration reduction**
3. **strategic decarbonization positioning**
4. **technology demonstration / pilot value**
5. **preparedness for stricter harbor emissions rules**
6. **owner desire for hydrogen-process learning in a bounded vessel class**

### Weak justifications

The concept is weaker when justified only by:
- "hydrogen must be cheaper"
- "the retrofit will obviously pay back fast"
- "shore power will always be favorable"
- "all ports will support this soon anyway"

Those are weak claims.

## Best-fit operator profile

The architecture is strongest for operators who match most of the following:

- home-berth based
- short-sea / harbor duty
- predictable operating rhythm
- real interest in lower local emissions
- willing to accept training and procedure burden
- willing to treat the vessel as a pilot / strategic platform rather than only
  a near-term cost reducer
- able to support maintenance and port coordination discipline

## Weak-fit operator profile

The architecture is weak for operators who need:

- deep-sea endurance
- minimal training burden
- fuel savings as the only decision variable
- infrastructure independence
- high-frequency ultra-short turnaround with little berth time
- no appetite for added procedure and service discipline

## Downtime and adoption penalty summary

The main adoption penalties for the reference concept are:

- high capex
- 20 to 30 week downtime
- moderate-to-high maintenance burden
- high shore and port dependency
- nontrivial training burden
- substantial arrangement and stability evaluation burden
- significant operating-procedure overhead

These penalties are part of the concept.
They are not temporary annoyances to hide.

## Why the repo still has value

Even with those penalties, the repo has serious value if framed correctly.

### Value as a decision-grade architecture
It helps readers understand:
- what a bounded marine hydrogen retrofit actually takes
- what the real penalties are
- where the architecture could work
- where it probably should not be attempted

### Value as an R&D reference
It can help:
- ports
- yards
- pilot-vessel programs
- technology teams
- owner technical groups

reason through hydrogen retrofit burden without pretending the answer is simple.

### Value as a strategic decarbonization concept
For the right operator, the value is:
- strategic positioning
- local emissions leadership
- bounded real-world hydrogen integration experience
- proof-of-concept pathway for future fleet decisions

## Decision framing

The repo is locked to this decision framing:

### Green-light conditions
The concept becomes interesting when:
- harbor / short-sea vessel class is a fit
- predictable berth window exists
- shore power is available
- operator values local emissions reduction
- operator accepts procedure and maintenance burden
- owner sees pilot / strategic value beyond immediate fuel savings

### Amber conditions
The concept becomes difficult when:
- berth windows are inconsistent
- electricity pricing is poor
- layout margin is tight
- maintenance culture is weak
- training burden is unwelcome

### Red-light conditions
The concept is a weak fit when:
- deep-sea range dominates the mission
- no reliable berth power exists
- only fast payback matters
- owner expects low-procedure operation
- the vessel cannot tolerate the arrangement and weight penalties

## What this file can and cannot solve

### What it can solve now
It can lock:
- capex range
- downtime range
- burden framing
- dependency framing
- non-payback honesty
- best-fit and weak-fit operator profiles

### What it cannot honestly finalize now
It cannot finalize:
- exact vendor quotes
- exact lifecycle cost model for a real operator
- exact electricity tariffs
- actual future maintenance contract pricing
- owner-specific ROI
- local grant / subsidy effects
- real fleet-level financial optimization

## Verification intent

Later proof-of-concept and README-level positioning should prove that the repo:

- does not oversell short-term economics
- keeps downtime visible
- keeps maintenance and training visible
- presents the strongest-fit use case honestly
- makes non-payback strategic justification explicit

## Explicit non-claims

This file does **not** claim:

- guaranteed positive ROI
- universal fuel-cost savings
- universal emissions superiority in all power contexts
- trivial retrofit effort
- rapid turnaround adoption
- final market price for hardware or yard labor

It defines the honest economic and operational posture of the repo.

## Summary

IX-Marine-H2-Retrofit is not a "cheap green upgrade" repo.

It is a serious, berth-dependent harbor-vessel hydrogen retrofit concept with:

- about **$5 million to $9 million** concept-stage capex
- about **20 to 30 weeks** concept-stage downtime
- **moderate to high** maintenance burden
- **high** port and shore-power dependency
- real training and procedure burden
- strong local-emissions and strategic value in the right use case
- weak universal payback claims

That is the correct economic frame for the project.
