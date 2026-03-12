# IX-ZeroCell-72

Battery-free, supercapacitor-buffered, multi-source edge-power architecture for real low-power systems.

## What this repo is

IX-ZeroCell-72 is the reality-based rebuild of the original ZeroCell concept.

The goal is no longer fantasy wattage or wall-power replacement. The goal is now precise, honest, and technically defensible:

**Harvest small amounts of real ambient energy, buffer it safely, and run low-power electronics for long-duration autonomous operation without a battery.**

This repo is focused on a serious engineering target:

- battery-free power for real low-power systems
- 72-hour autonomous operation target under defined site conditions
- modular energy bins that can operate alone or as part of a larger rack
- source-specific harvesting paths instead of one unrealistic mixed-energy bus
- supercapacitor storage, protection, and energy-aware output control
- reproducible test criteria instead of speculative power claims

---

## What this repo is not

IX-ZeroCell-72 is **not**:

- a perpetual motion machine
- a kilowatt-class ambient generator
- a wall-outlet replacement
- a laptop, appliance, or motor power source
- an excuse to blur measured output with theoretical maximums

If a load exceeds what the harvest conditions can support, the system must either buffer longer, duty-cycle harder, or refuse the load.

That is the engineering line for this repo.

---

## Core mission

The mission of IX-ZeroCell-72 is to produce a credible open architecture for:

- sensor nodes
- telemetry devices
- BLE and LoRa endpoints
- environmental monitoring
- watchdog controllers
- e-paper updates
- ultra-low-duty-cycle edge electronics
- bursty 5V tasks when energy budget permits

This is the correct problem class for ambient energy harvesting.

---

## Design doctrine

The original ZeroCell concept had the right instinct but the wrong scale.

The corrected doctrine is:

1. **Match each source to the right front end**
   - indoor / outdoor light
   - thermal gradient
   - vibration / piezo
   - RF trickle input where viable

2. **Store harvested energy in supercapacitors**
   - no battery required for core mission
   - fast charge acceptance
   - long cycle life
   - safe burst delivery with proper protection and balancing

3. **Separate always-on loads from burst loads**
   - stable low-power rail for sensing and control
   - gated burst rail for intermittent higher draw events

4. **Use firmware to enforce energy truth**
   - no wake event without budget
   - no burst output without threshold
   - no pretending a weak energy day is a strong one

5. **Scale by modularity**
   - one bin is a node
   - many bins form a platform
   - rack-scale architecture is allowed, but honesty about source conditions is mandatory

---

## System concept

IX-ZeroCell-72 is built around a modular “bin” architecture.

Each bin is a self-contained low-power energy appliance that can include:

- source-specific harvest front ends
- local rectification and conditioning
- supercapacitor storage
- health sensing and protection
- microcontroller-based energy management
- regulated low-voltage output rails

Multiple bins can be combined into a larger rack configuration to improve resilience, total harvest area, and burst capability.

### Single-bin role
A single bin is meant to prove:

- cold start behavior
- low-power autonomy
- source integration discipline
- storage and gating logic
- repeatable measurement

### Rack role
A rack of bins is meant to prove:

- modular scaling
- load sharing strategy
- system-level autonomy
- deployment flexibility across real environments

---

## Success criteria

A design in this repo is only considered credible if it can meet measured criteria.

### Minimum credibility standard
- defined load profile
- defined site conditions
- defined storage configuration
- measured startup behavior
- measured steady-state harvest contribution
- measured output duty cycle
- measured failure limits

### IX-ZeroCell-72 target standard
The long-form target for this project is:

**Maintain mission-defined low-power operation for 72 hours without a battery, using only harvested energy plus supercapacitor storage, under named environmental conditions and a documented duty cycle.**

That means the phrase “72” is not decoration. It is the autonomy target.

---

## Power honesty policy

This repo will not use vague phrases like:

- “free energy”
- “self-sustaining unlimited output”
- “device powers itself forever”
- “harvests enough for anything”

Instead, every meaningful claim should eventually tie back to:

- source conditions
- conversion chain
- storage behavior
- duty cycle
- measured output
- thermal and electrical limits

If it is not measurable, it is not finished.

---

## Architecture direction

The corrected IX-ZeroCell-72 architecture moves away from a single mixed-energy intake and toward a source-matched system:

- light harvesting path
- thermal harvesting path
- vibration / piezo path
- optional RF trickle path
- storage and balancing layer
- low-power always-on rail
- gated burst-output rail
- firmware-controlled energy arbitration

This repo will document those paths separately and then integrate them at the system level.

---

## Intended deployment environments

IX-ZeroCell-72 is meant for environments where at least one real harvest source exists:

- indoor spaces with consistent light
- industrial areas with vibration
- warm equipment zones with usable thermal gradients
- structures with periodic motion
- instrumented environments that benefit from battery-free nodes

A dead environment gives dead performance.
This project assumes actual energy availability, not wishful thinking.

---

## Engineering priorities

Priority order for this repo:

1. Credibility
2. Safety
3. Measurability
4. Modularity
5. Serviceability
6. Scalability
7. Aesthetic coherence

This order matters.

---

## What “72” means in the product family

The ZeroCell family name remains intact, but this branch defines a stricter standard.

**IX-ZeroCell-72** means:

- same family
- corrected mission
- corrected claims
- autonomy-centered architecture
- serious low-power target
- build-and-test discipline

It is not a cosmetic rename.
It is the hard reset to a version that can be defended.

---

## Repository status

This repository is being rebuilt commit by commit around the corrected mission.

Planned documentation includes:

- system architecture
- source-path design
- storage topology
- firmware behavior
- mechanical bin layout
- rack-scale topology
- power budget
- validation criteria
- test protocol
- BOM and sourcing
- safety limits
- deployment notes

---

## Licensing

This project is licensed under the **Apache License 2.0**.

---

## Working principle in one sentence

**IX-ZeroCell-72 is a modular, battery-free, low-power energy platform that harvests small real ambient inputs, stores them in supercapacitors, and spends that energy only when the system can honestly afford it.**

---

## Status statement

This is the first commit in the reality-based rebuild.

From this point forward, the repo is anchored to:
- real environments
- real loads
- real storage
- real limits
- real measurements

Anything else gets cut.

---
