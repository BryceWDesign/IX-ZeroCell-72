# IX-ZeroCell-72 Mission Profile

## Purpose

This document defines the operational mission for IX-ZeroCell-72.

It answers five questions:

1. What is the system supposed to do?
2. Under what conditions is it supposed to do it?
3. What kinds of loads are in scope?
4. What counts as mission success?
5. What counts as failure?

This file exists so the repo cannot drift back into vague claims.

---

## Mission statement

**IX-ZeroCell-72 must support a defined low-power electronics mission for 72 hours without a battery, using harvested ambient energy plus supercapacitor storage, under named environmental conditions and a documented duty cycle.**

That is the entire point of the project.

---

## Core mission class

The system is intended for **real low-power autonomous electronics**, not general-purpose consumer power.

### In-scope mission types
- environmental sensing
- temperature / humidity / pressure logging
- BLE advertising or telemetry
- LoRa status bursts
- supervisory control and watchdog logic
- low-rate event counting
- e-paper or low-refresh status display
- wake-and-report edge instrumentation
- fault/status beaconing
- timed relay or pulse events with strict gating

### Out-of-scope mission types
- laptops
- phones as a primary charging target
- desktop computers
- routers with continuous high draw
- motors with meaningful continuous duty
- heaters
- refrigeration
- household appliances
- large lighting loads
- anything that assumes wall-power behavior

The repo must stay inside the in-scope class.

---

## Mission philosophy

The system is not judged by peak bragging rights.
It is judged by **survival and useful work over time**.

The project therefore prioritizes:

- endurance over momentary output spikes
- truthful duty cycle over inflated “can power X” language
- autonomous recovery over fragile demos
- source fit over universal claims
- predictable behavior over dramatic but unstable output

---

## Mission layers

IX-ZeroCell-72 has three mission layers.

### Layer 1: Survival mission
This is the minimum non-negotiable mission.

The system must preserve:
- control logic
- timing base
- storage monitoring
- protection behavior
- recovery capability

If the system cannot preserve its own survival mission, it is not credible.

### Layer 2: Baseline service mission
This is the normal always-on mission.

The system should support:
- sensor sampling
- state logging
- low-rate health telemetry
- periodic status processing
- low-power communication readiness

This layer must be designed to remain active during ordinary weak-input periods.

### Layer 3: Opportunistic burst mission
This is the higher-cost mission layer.

The system may support:
- radio transmissions
- status display refresh
- short alert pulses
- short 5V accessory support
- limited actuator pulses
- higher-rate compute windows

This layer is conditional.
It only runs when the energy budget allows.

---

## Mission durations

The name “72” in IX-ZeroCell-72 refers to the target endurance window.

### Minimum test window
- 72 consecutive hours

### Preferred validation windows
- 24 hours for quick screening
- 72 hours for baseline validation
- 168 hours for extended evaluation
- longer windows for site-specific confidence testing

The repo centers on the 72-hour window because it is long enough to expose weak assumptions without being unrealistic to test.

---

## Operating environments

The system is only meaningful when tied to a real environment.

### Environment class A: indoor light dominant
Characteristics:
- stable indoor light
- weak or negligible vibration
- little or no thermal gradient
- possible RF presence
- quiet mechanical environment

Typical use:
- office or facility monitoring
- shelf-mounted nodes
- near-window instrumentation

Primary expected source:
- light

Secondary possible sources:
- RF trickle
- minor thermal input

### Environment class B: industrial vibration dominant
Characteristics:
- regular structural or machinery vibration
- variable light
- possible thermal gradients
- more aggressive mechanical exposure

Typical use:
- equipment-side monitoring
- machinery health sensing
- structural telemetry

Primary expected source:
- vibration / piezo

Secondary possible sources:
- thermal
- light

### Environment class C: thermal gradient dominant
Characteristics:
- stable hot/cold surface relationship
- moderate or weak light
- limited motion
- consistent equipment heat signature

Typical use:
- ducting
- equipment housings
- machinery surfaces
- enclosed service zones

Primary expected source:
- thermal

Secondary possible sources:
- light
- vibration

### Environment class D: mixed-source deployment
Characteristics:
- moderate light
- periodic vibration
- intermittent thermal gradient
- optional RF contribution

Typical use:
- utility spaces
- transport-adjacent structures
- complex equipment areas

Primary expected source:
- mixed, site-dependent

This is often the most realistic class for a modular bin system.

### Environment class E: dead environment
Characteristics:
- low light
- no meaningful vibration
- no useful thermal gradient
- weak RF
- long quiet periods

Typical result:
- weak or failed mission performance

This class is important because it defines the hard limit.
IX-ZeroCell-72 is not expected to perform well in a dead environment.

---

## Load classes

Mission loads are divided into three categories.

### Class 1: survival loads
Examples:
- MCU sleep-state retention
- RTC or timer maintenance
- voltage monitoring
- wake comparator logic
- essential housekeeping

Requirements:
- lowest possible power draw
- highest reliability
- never exposed to burst instability

### Class 2: baseline mission loads
Examples:
- periodic sensor reads
- local processing
- state logging
- low-rate BLE beacon
- health status updates

Requirements:
- efficient schedule control
- conservative power policy
- stable always-on rail

### Class 3: burst mission loads
Examples:
- LoRa transmission
- e-paper refresh
- alarm pulse
- short relay event
- gated 5V accessory action

Requirements:
- hard enable threshold
- event budgeting
- immediate cutoff when storage margin is inadequate

---

## Example mission profile

The exact mission will vary by build, but a credible demonstration must look something like this in structure:

### Example: low-power telemetry bin
- sensor read every 5 minutes
- health sample every 1 minute
- BLE beacon every 30 seconds or less frequently when energy is scarce
- data log write every 15 minutes
- LoRa transmission every 60 minutes if storage is above burst threshold
- status LED disabled except during test mode
- 5V rail normally off

This is only an example of structure, not a fixed final spec.

The important point is that mission behavior must be explicitly defined.

---

## Mission scheduling doctrine

The scheduler or control policy must classify tasks by energy cost and importance.

### Priority order
1. survival
2. protection
3. sensing
4. logging
5. communications
6. optional burst tasks

When energy is scarce, the system must shed lower-priority tasks first.

### Shedding order
- disable optional indicators
- increase reporting interval
- reduce sensor sampling frequency
- suspend burst output
- retain survival mission only

This is how 72-hour behavior becomes realistic.

---

## Required mission definitions

Any build or test claiming mission success must define the following:

- environment class
- source hardware included
- storage configuration
- always-on rail voltage
- burst rail voltage and policy
- sampling schedule
- communication schedule
- nominal and worst-case load current
- start condition
- pass / fail criteria

If those are not present, the mission is undefined.

---

## Start conditions

A test or deployment must state one of these start conditions.

### Start condition S1: precharged start
Storage begins above a defined threshold.

Use case:
- functional mission validation
- controlled repeatability
- output-policy testing

### Start condition S2: cold start
Storage begins at or near minimum charge.

Use case:
- startup realism
- recovery behavior
- harvest-path validation

### Start condition S3: brown-recovery start
Storage begins above collapse but below normal operation threshold.

Use case:
- resilience testing
- post-disturbance recovery
- threshold tuning

A serious repo should eventually test all three.

---

## Mission pass criteria

A mission passes only if all the following are true over the stated window:

1. no battery is used for core operation
2. survival logic remains intact
3. storage stays inside defined protection limits
4. always-on rail remains stable enough for mission control
5. burst loads only occur when policy permits
6. task execution matches the documented duty cycle or the documented degraded mode
7. system does not require manual intervention to continue
8. measured logs support the claim

A successful mission is documented, not narrated.

---

## Mission fail criteria

A mission fails if any of the following occur:

- hidden battery dependence
- burst output collapses the control rail
- storage falls below safe survival floor without controlled behavior
- claimed tasks are not actually executed
- undefined energy assumptions are used to excuse missing performance
- source conditions are omitted from reporting
- test requires manual resets to continue
- 72-hour target is claimed without data support

The repo should treat these as hard failures.

---

## Autonomy definition

For IX-ZeroCell-72, “autonomy” does not mean infinite power.

It means the system can:

- sense its own energy state
- prioritize tasks
- degrade gracefully
- recover from weak-input periods
- preserve the core mission without human intervention

That is the correct meaning of autonomy here.

---

## The role of modular bins

The modular-bin architecture supports the mission in two ways.

### Single-bin mission role
- prove source-path correctness
- prove control policy
- prove storage integrity
- prove basic 72-hour viability for a named low-power load

### Multi-bin mission role
- improve source coverage
- increase resilience
- increase aggregate buffered burst support
- support shared gateway or supervisory infrastructure
- support larger deployments while keeping each bin individually valid

A rack does not replace mission discipline.
It multiplies it.

---

## Constraints that protect the mission

All design work must stay inside these constraints:

- battery-free core operation
- ambient-source dependence must be named and real
- supercapacitor storage only for the core platform
- survival logic isolated from impulsive loads
- burst tasks are optional, never assumed
- deployment environment matters
- measurement is mandatory

These constraints are what keep the project serious.

---

## Mission completion standard

The mission profile is considered complete only when the repo also includes:

- power budget document
- control policy document
- storage topology document
- test protocol
- pass / fail templates
- deployment scenario notes

This file sets the operational target those documents must serve.

---

## Summary

IX-ZeroCell-72 is complete only when it can do the following:

- harvest real ambient energy
- buffer it in supercapacitors
- run a named low-power mission
- protect itself during weak-input periods
- survive 72 hours without a battery
- prove all of that with documented conditions and measured results

That is the mission.
