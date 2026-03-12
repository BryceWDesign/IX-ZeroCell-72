# IX-ZeroCell-72 Source Path Strategy

## Purpose

This document defines how IX-ZeroCell-72 handles ambient energy sources.

It exists to prevent the project from collapsing different source types into one vague energy story.

Each source must be evaluated, captured, conditioned, and scored on its own terms.

This is one of the core corrections in IX-ZeroCell-72.

---

## Core rule

**Different energy sources are not interchangeable.**

They differ in:

- voltage behavior
- current capability
- impedance
- intermittency
- startup conditions
- mechanical coupling needs
- environmental dependence
- controllability

Because of that, each source must have its own path strategy.

---

## Source classes in IX-ZeroCell-72

IX-ZeroCell-72 organizes harvest sources into four classes:

1. light
2. thermal
3. vibration / piezo
4. RF trickle

These are not equal contributors.
They have different practical value.

---

## Practical source ranking

For the ZeroCell family, the honest practical ranking is usually:

### Tier 1 — primary candidate sources
These are the sources most likely to matter in real deployments.

- light
- thermal
- tuned vibration

### Tier 2 — conditional contributors
These can matter a lot in the right environment, but are not universal.

- tuned vibration
- thermal in stable hot/cold sites
- indoor light in predictable illuminated sites

### Tier 3 — supplemental sources
These help at the margin but should not carry the mission.

- RF trickle
- opportunistic weak ambient effects
- non-dominant secondary source fragments

The system should be designed so the mission still makes sense if Tier 3 contributes almost nothing.

---

## Source acceptance doctrine

A source belongs in IX-ZeroCell-72 only if it can answer all of the following:

1. Is the source physically present in the target environment?
2. Is its contribution likely to be measurable?
3. Can it be conditioned without wasting most of what it provides?
4. Does it improve mission endurance or resilience in a meaningful way?
5. Can it be integrated without destabilizing stronger paths?

If the answer to most of these is no, that source is decorative, not functional.

---

## Source path structure

Every source path in IX-ZeroCell-72 should include these stages:

1. **capture interface**
2. **protection / clamp behavior**
3. **local conditioning**
4. **front-end conversion**
5. **optional local reservoir**
6. **merge isolation**
7. **telemetry visibility**

This structure may be implemented with different circuits depending on the source, but the stages should remain conceptually consistent.

---

## Source path scoring model

Each source should eventually be scored across the following dimensions:

### 1. availability
How often is the source present?

### 2. density
How much usable energy exists at the site?

### 3. regularity
Is the source predictable or sporadic?

### 4. integration cost
How much mechanical and electrical effort is required?

### 5. startup usefulness
Can the source help the system recover from a low-energy state?

### 6. storage compatibility
Can the source be turned into something the storage stage can accept efficiently?

### 7. mission relevance
Does the source materially help the actual 72-hour mission?

This scoring model should later inform build variants and deployment decisions.

---

## Light path strategy

## Why light matters

In many real deployments, light is the most honest ambient source available.

It has several advantages:
- predictable in occupied or illuminated spaces
- easy to understand
- straightforward to scale with area
- often easier to integrate than mechanical harvesters
- useful for both indoor and outdoor variants

For many IX-ZeroCell-72 deployments, light is the best candidate for the primary source.

## Light path goals

The light path should aim to:
- harvest at low illumination levels where possible
- preserve efficiency at low power
- avoid needlessly complex routing
- support serviceable panel placement
- keep shading and cable loss low

## Light path risks

The light path can be overestimated when:
- panel area is too small
- assumed lux level is unrealistic
- installation spends long periods in darkness
- mounting orientation is poor
- packaging blocks light access

The light path must be tied to a real lighting condition, not generic optimism.

---

## Thermal path strategy

## Why thermal matters

Thermal harvesting becomes meaningful only when there is a real and sustained temperature differential.

In the right place, it can be valuable.
In the wrong place, it adds complexity and almost no useful energy.

Thermal is often strongest when installed near:
- warm equipment surfaces
- ducts
- machinery housings
- enclosed systems with repeatable heat gradients

## Thermal path goals

The thermal path should aim to:
- couple properly to the heat source
- preserve cold-side opportunity where possible
- avoid self-insulating the gradient away
- support low-voltage startup conditions
- provide stable contribution over time

## Thermal path risks

The thermal path fails when:
- delta-T is too small
- packaging equalizes both sides
- mechanical mounting is poor
- the design assumes heat where none actually exists
- startup burden exceeds what the path can provide

Thermal harvesting is useful only when the installation is honest about temperature reality.

---

## Vibration / piezo path strategy

## Why vibration matters

Vibration is where the original ZeroCell visual identity can remain technically meaningful.

A vibration harvester can be useful when:
- the environment actually vibrates
- the harvester is tuned for that environment
- the mechanical mounting is correct
- the conditioning path does not waste the output

Untuned vibration harvesting is usually weak.
Site-tuned harvesting is where the value is.

## Vibration path goals

The vibration path should aim to:
- match mechanical resonance to site conditions
- survive shock and fatigue
- capture repeatable motion energy
- isolate fragile front-end electronics from harmful transients
- allow tuning or retuning where practical

## Role of the tube array

The tube array should no longer be treated as a universal power miracle.

Its proper role is:
- a modular vibration-harvesting subsystem
- a site-tuned mechanical energy intake
- a visually distinctive but physically constrained contributor

This is the right way to preserve the old identity without preserving the old exaggeration.

## Vibration path risks

The vibration path underperforms when:
- resonance is mismatched
- mounting is loose or deadened
- motion is intermittent but assumed continuous
- the source is too weak for the mechanical design
- the site is quiet but the design assumes machinery-level motion

A vibration path must be tuned to a named environment, not imagined in the abstract.

---

## RF trickle path strategy

## Why RF is limited

RF harvesting is real, but usually small.

In IX-ZeroCell-72, RF must be treated as:
- optional
- supplemental
- low-priority
- highly site-dependent

RF should never be the basis of the 72-hour mission unless the environment is explicitly controlled and documented for that purpose.

## RF path goals

The RF path should aim to:
- capture micro-input efficiently
- avoid dragging down the rest of the system
- add small background contribution where present
- remain electrically isolated enough that it cannot become a liability

## RF path risks

RF becomes misleading when:
- its output is verbally inflated
- the source field strength is unknown
- the environment is assumed richer than it is
- the path complexity costs more than the energy benefit

RF is garnish, not the meal.

---

## Source coexistence doctrine

Multiple sources can live in one bin, but only if they coexist cleanly.

That means:
- no backfeeding between paths
- no weak source exposed to strong source disturbances
- no shared intake node before conditioning
- no path that creates avoidable losses for another
- no control logic that assumes all paths behave alike

The merge happens after source-specific conditioning.
This is non-negotiable.

---

## Source priority policy

When multiple sources are present, IX-ZeroCell-72 should prefer them in this order:

### 1. dependable source first
Use the source most likely to provide stable useful contribution.

### 2. efficient source second
Prefer the path with lower effective conversion waste.

### 3. supplemental source third
Add secondary paths that improve margin without destabilizing the system.

### 4. decorative source last
If a source does not materially improve the mission, it should be dropped.

The project should not keep a source path just because it sounds futuristic.

---

## Single-bin source recommendations

A single bin does not need every source class.

The most credible single-bin variants are:

### Variant A — light-first bin
Use when:
- predictable indoor or outdoor light exists

Best for:
- office
- facility
- window-adjacent
- shelf-mounted instrumentation

### Variant B — thermal-first bin
Use when:
- stable equipment heat and usable delta-T exist

Best for:
- machinery
- ducting
- service spaces
- thermal monitoring zones

### Variant C — vibration-first bin
Use when:
- repeatable structural or machine vibration exists

Best for:
- industrial telemetry
- rotating equipment environments
- structural motion monitoring

### Variant D — mixed-source bin
Use when:
- more than one source is meaningfully present

Best for:
- complex deployment spaces
- rack demonstrations
- resilience-focused builds

A bin should be configured for its site, not overloaded with every possible source by default.

---

## Rack-level source strategy

At rack scale, the smartest move is often **source diversity by bin**, not maximum source clutter inside each bin.

Examples:
- one light-optimized bin
- one thermal-optimized bin
- one vibration-optimized bin
- repeated across a rack depending on the environment

This can improve:
- serviceability
- tuning clarity
- fault isolation
- source-specific measurement
- deployment flexibility

The rack should scale good source usage, not multiply confusion.

---

## What the source strategy rejects

This source strategy explicitly rejects:
- one universal mixed-source input node
- mission claims based on unknown source conditions
- equal weighting of all source types
- RF-centered mission narratives
- treating vibration as strong without tuning
- treating thermal as useful without real delta-T
- treating light as meaningful without actual illumination conditions

These are all failure patterns the repo is trying to leave behind.

---

## Source qualification checklist

Before including a source in a build, answer these questions:

- What environment class is this source tied to?
- What makes it present at this site?
- What makes it useful at this site?
- What front-end path will it use?
- What local protection does it need?
- Does it help cold start, steady state, or burst margin?
- What evidence will show it is helping?
- Would the build be cleaner without it?

If that checklist is weak, the source path is not ready.

---

## Summary

IX-ZeroCell-72 becomes credible when each source is treated as what it really is.

That means:
- light as a practical primary source where available
- thermal as a conditional but valuable source where delta-T is real
- vibration as a site-tuned mechanical contributor
- RF as a small supplemental trickle only

The design must select, condition, isolate, and measure each source honestly.

That is the source path strategy for the ZeroCell family.
