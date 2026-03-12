# IX-ZeroCell-72 Project Summary

## Executive summary

IX-ZeroCell-72 is a battery-free, supercapacitor-buffered, multi-source energy-harvesting platform designed for real low-power electronics.

This project is the corrected engineering evolution of the original ZeroCell concept.

The objective is not high-wattage output.
The objective is controlled, measurable, long-duration autonomous operation for low-power systems under defined environmental conditions.

The core target is simple:

**Support mission-defined low-power operation for 72 hours without a battery by harvesting real ambient energy and buffering it in supercapacitors.**

---

## Why this version exists

The earlier ZeroCell framing mixed valid instincts with invalid scale assumptions.

The valid instincts were:

- modular harvesting
- storage-first architecture
- multi-source intake
- low-voltage control logic
- rack-scale expansion
- visible mechanical identity

The invalid assumptions were:

- exaggerated output expectations
- one mixed intake bus for dissimilar source types
- weak separation between always-on and burst loads
- unclear site-condition dependence
- insufficient measurement discipline

IX-ZeroCell-72 exists to keep the useful architecture and remove the non-defensible claims.

---

## Problem class

IX-ZeroCell-72 is built for the following class of problems:

- battery-free sensing
- low-duty-cycle telemetry
- edge logging
- environmental monitoring
- BLE advertising
- LoRa status transmission
- watchdog controllers
- e-paper status updates
- intermittent 5V support for short events

This is a real and useful engineering space.

It is also the right power class for ambient harvesting.

---

## System philosophy

The system follows one hard rule:

**Energy is only spent when it has actually been harvested, safely stored, and budgeted.**

That rule forces every major design choice:

- separate source front ends
- storage-first thinking
- energy-aware firmware
- hard output gating
- measurable autonomy criteria
- no inflated performance language

---

## Architecture overview

IX-ZeroCell-72 is organized as a modular bin architecture.

Each bin is a self-contained energy node with these layers:

1. **Harvest layer**
   - source-specific inputs
   - local protection
   - local conditioning

2. **Conversion layer**
   - front ends matched to source behavior
   - rectification and regulation where required
   - cold-start-aware energy capture

3. **Storage layer**
   - supercapacitor bank
   - balancing and monitoring
   - undervoltage and overvoltage protection

4. **Control layer**
   - low-power MCU
   - energy-state sensing
   - output arbitration and scheduling

5. **Output layer**
   - always-on low-power rail
   - gated burst rail
   - optional task-specific output modules

6. **Mechanical layer**
   - serviceable enclosure
   - thermal path support
   - mounting and stackability
   - cable and bus management

---

## Source strategy

The corrected design does not combine all harvest sources into one undifferentiated intake path.

Instead, each source class gets treated according to how it behaves electrically.

### Source classes

#### 1. Light harvesting
Best for:
- indoor light
- near-window ambient light
- outdoor exposed installs

Characteristics:
- often the most practical steady source
- predictable in lit environments
- highly deployment-dependent

Role in IX-ZeroCell-72:
- primary or co-primary source in many real installations

#### 2. Thermal harvesting
Best for:
- warm equipment surfaces
- ducts
- machinery housings
- environments with meaningful thermal delta

Characteristics:
- useful when a stable temperature gradient exists
- weak or useless without real delta-T
- often valuable as a background contributor

Role in IX-ZeroCell-72:
- conditional contributor with high deployment value in the right site

#### 3. Vibration / piezo harvesting
Best for:
- machinery environments
- structural vibration
- repeated motion zones
- equipment frames

Characteristics:
- highly site-specific
- can be strong when tuned properly
- weak when untuned or mounted in dead zones

Role in IX-ZeroCell-72:
- deployment-tuned contributor, especially in industrial settings

#### 4. RF trickle harvesting
Best for:
- supplemental contribution only
- controlled demonstration cases
- sites with known strong RF presence

Characteristics:
- usually weak
- not trusted as a core source
- useful only as a small additive path

Role in IX-ZeroCell-72:
- optional micro-input, never primary mission power

---

## The bin model

A bin is the smallest credible working unit in the IX-ZeroCell-72 family.

A single bin must prove:

- cold-start behavior
- source-path correctness
- storage integrity
- protection logic
- output gating discipline
- repeatable test method
- autonomy against a defined low-power load

A bin is not expected to act like a consumer power product.

It is an energy-aware low-power node.

---

## The rack model

Multiple bins can be assembled into a coordinated rack.

The rack exists for:

- modular scaling
- greater total harvest area
- increased resilience
- more flexible deployment
- larger buffered burst capability
- shared system supervision

The rack is not a cheat code.

It still depends on real source availability.
It still must obey measured power truth.
It simply scales the architecture in a defensible way.

---

## Output model

IX-ZeroCell-72 uses a two-class output strategy.

### Always-on rail
Purpose:
- MCU
- sensing
- low-rate monitoring
- sleep-state maintenance
- status logic

Design intent:
- stable
- efficient
- extremely conservative

### Burst rail
Purpose:
- radio transmission
- short communication windows
- actuator pulses
- indicator updates
- limited 5V support when budget allows

Design intent:
- gated
- threshold-controlled
- firmware-approved only

This separation is critical.
It prevents the system from killing its own long-duration mission with one impulsive load event.

---

## What “72” actually means

The “72” in IX-ZeroCell-72 is the autonomy standard for the design family.

It means the system is being engineered around a specific endurance target, not a vague aspiration.

To count as meeting that target, the system must have:

- a named load profile
- a named source environment
- a named storage configuration
- a documented duty cycle
- measured startup behavior
- measured operating survival across 72 hours

The number is only meaningful when tied to those conditions.

---

## Credibility definition

This repo should be considered credible only when it demonstrates all of the following:

- no impossible power claims
- no source ambiguity
- no hidden battery dependency
- no vague load descriptions
- no undefined test environment
- no storage-stage hand-waving
- no “works in theory” language without measurement

Credibility in this project comes from disciplined constraints, not dramatic wording.

---

## What success looks like

A successful IX-ZeroCell-72 implementation does not need to impress with raw wattage.

It needs to prove five things:

1. It starts correctly
2. It harvests honestly
3. It stores safely
4. It spends energy intelligently
5. It survives the mission window without a battery

If it does all five under documented conditions, it is successful.

---

## What failure looks like

Failure is any of the following:

- load target exceeds environment reality
- source paths interfere with each other
- supercap stage is unstable or unsafe
- burst loads collapse the control rail
- 72-hour target is claimed without measured support
- design language outruns test evidence

This repo is specifically being rebuilt to eliminate those failure modes.

---

## Development direction

The project will proceed through these major layers:

1. mission correction
2. system architecture
3. source-path definitions
4. storage topology
5. control logic
6. output policy
7. power budget
8. mechanical packaging
9. validation criteria
10. build and test documentation

Each layer must remain consistent with the battery-free 72-hour mission.

---

## Summary statement

IX-ZeroCell-72 is the disciplined ZeroCell architecture:

- battery-free
- low-power
- source-matched
- supercap-buffered
- firmware-governed
- modular
- measurable
- autonomy-driven

It is not trying to beat the grid.

It is trying to become a serious, testable platform for real low-power autonomous operation.

That is the correct form of ZeroCell.
