# IX-ZeroCell-72 System Architecture

## Purpose

This document defines the top-level architecture for IX-ZeroCell-72.

It describes how a single bin works, how multiple bins scale into a rack, and how the system maintains battery-free operation for real low-power loads by using:

- source-specific harvesting paths
- supercapacitor storage
- energy-aware control logic
- strict rail separation
- modular expansion

This is the governing architecture document for the repo.

---

## Architectural intent

IX-ZeroCell-72 is designed as a **battery-free, modular edge-power system**.

The architecture is built around four truths:

1. Different harvest sources behave differently and cannot be treated as one generic input.
2. Harvested energy is small and intermittent, so storage and scheduling matter more than raw peak claims.
3. The control rail must survive even when burst loads are denied.
4. Scaling must happen through modular bins, not by pretending one bin can do everything.

---

## Top-level block view

```text
[ LIGHT INPUT ] ----------\
[ THERMAL INPUT ] ---------\
[ VIBRATION / PIEZO ] ------> [ SOURCE-SPECIFIC FRONT ENDS ] --> [ LOCAL ENERGY MERGE ] --> [ SUPERCAP STORAGE ]
[ OPTIONAL RF TRICKLE ] ---/                                                |                          |
                                                                          [ SENSE ]                  [ BALANCING / PROTECTION ]
                                                                                                      |
                                                                                                      v
                                                                                          [ POWER POLICY CONTROLLER ]
                                                                                                      |
                                                                                     +----------------+----------------+
                                                                                     |                                 |
                                                                                     v                                 v
                                                                           [ ALWAYS-ON 3.3V RAIL ]            [ GATED BURST RAIL ]
                                                                                     |                                 |
                                                                                     v                                 v
                                                                           MCU / sensors / sleep logic       radios / short 5V tasks / pulses


Single-bin architecture

A single IX-ZeroCell-72 bin is the smallest complete system unit.

Each bin contains the following major layers:

1. Harvest layer

The harvest layer receives ambient energy from one or more source classes.

Typical source classes:

light

thermal gradient

vibration / piezo

optional RF trickle

Each source enters through its own path.
There is no assumption that all sources are always present.

2. Front-end conversion layer

Each source path has conversion logic matched to its behavior.

Examples of required behaviors:

high-impedance source handling

low-voltage startup behavior

rectification for AC-like inputs

source-specific protection and clamping

local reservoir buffering where appropriate

This layer is the key architectural correction over the earlier ZeroCell form.

3. Local merge layer

After source-specific conditioning, usable energy is merged into a common storage-facing path.

The merge layer must:

prevent backfeed from one source into another

isolate weak sources from stronger bus disturbances

tolerate intermittent source appearance

protect the storage stage from unstable source behavior

This merge point is downstream of source conditioning, not upstream.

4. Storage layer

The storage layer is a supercapacitor bank.

It exists to:

absorb small intermittent harvest events

support cold-start recovery behavior

maintain the always-on rail through weak-input periods

enable burst output events without collapsing the control domain

Storage is central to the system.
Harvest without disciplined storage is not enough.

5. Protection and balancing layer

The storage stage requires electrical discipline.

This layer covers:

overvoltage protection

undervoltage lockout

current limiting

balancing across the supercap stack

thermal protection where applicable

fault isolation

A battery-free system still needs serious protection design.

6. Control layer

A low-power MCU or equivalent controller monitors system state.

The control layer is responsible for:

reading storage voltage

tracking source availability signals

estimating energy budget state

permitting or denying burst loads

managing duty cycle timing

enforcing deep low-power policy when energy is scarce

The controller is not optional.
Without energy-aware control, the system will waste stored charge and fail the autonomy mission.

7. Output layer

The output layer is intentionally split into two classes:

Always-on rail

Used for:

MCU

sensor baseline operation

low-rate monitoring

wake scheduling

persistent low-power logic

This rail must be stable and protected from impulsive loads.

Gated burst rail

Used for:

radio transmission

short communication events

e-paper refresh

LED or alert pulse

limited short 5V support

small task-specific events

This rail is not continuously available.
It is enabled only when storage state and policy allow.

Source-path doctrine

The architecture depends on treating each source class correctly.

Light path

The light path is often the most practical steady contributor in real deployments.

Design priorities:

low-loss harvesting

good low-light behavior

storage-friendly output conditioning

serviceable panel routing

support for indoor or outdoor variants

The light path is a candidate primary source in many installations.

Thermal path

The thermal path uses real temperature differentials only.

Design priorities:

effective coupling to hot and cold sides

startup behavior under weak delta-T

avoidance of self-defeating thermal packaging

realistic expectations when thermal delta is small

The thermal path should never be assumed strong without a named site condition.

Vibration / piezo path

The vibration path can be very good in the right environment and almost useless in the wrong one.

Design priorities:

resonance tuning for the target environment

mechanical mounting integrity

proper rectification and clamping

isolation from damaging shock events

serviceable tuning access where required

The original tube-array identity belongs here, not as a universal source but as a site-tuned vibration subsystem.

RF trickle path

The RF path is optional and conservative.

Design priorities:

low-loss rectification

no reliance on RF as a core mission source

useful only as a supplemental input

no exaggerated range or output claims

This path may be omitted entirely in some builds.

Energy-state model

The architecture assumes the system moves through defined energy states.

State A: Cold start

Characteristics:

storage is near empty

only essential harvest capture is active

controller may be in minimal or delayed startup mode

burst rail is disabled

Goal:

accumulate enough energy to bring up control logic safely

State B: Recovery

Characteristics:

storage is rising

always-on rail becomes available

controller begins monitoring and scheduling

burst rail remains locked or highly restricted

Goal:

stabilize the platform before spending anything nonessential

State C: Sustainable operation

Characteristics:

storage is healthy

always-on rail is stable

burst events are allowed according to policy

duty cycle is managed in response to energy state

Goal:

maintain mission-defined operation while preserving margin

State D: Energy scarcity

Characteristics:

source input weakens

storage falls toward protection threshold

nonessential tasks are denied

sensing and timing become more conservative

Goal:

protect autonomy and preserve minimum service level

State E: Protective shutdown / survival mode

Characteristics:

storage near survival floor

only essential retention or wake logic remains active

burst rail hard-off

aggressive low-power posture

Goal:

survive until harvest conditions improve

Control-policy doctrine

The firmware or supervisory controller must follow a strict policy model.

Rules

Never enable burst output below the storage threshold.

Never assume a source is present just because it was present earlier.

Never let burst activity collapse the control rail.

Always preserve the ability to recover from weak-input periods.

Treat energy margin as a first-class system resource.

Policy outcomes

low energy = reduced duty cycle

healthy storage = normal mission cycle

strong harvest period = opportunistic task execution

weak harvest period = survival-first behavior

This is how the system closes the gap between harvested energy and useful work.

Bin internal subsystems

Each bin should be partitioned into the following physical subsystems:

Input panel / connector zone

source entry points

source identification

fuse / clamp / ESD considerations

Front-end board area

source-specific converter circuits

local reservoir elements

isolation and routing discipline

Storage core

supercap bank

balancing hardware

protection hardware

voltage sensing

Control board

MCU

ADC / telemetry

load gating logic

local status interface

Output section

always-on rail regulator

burst rail switch and regulator

output connectors

Mechanical support

source mounting structure

thermal path hardware

vibration module frame

service access

Rack-scale architecture

Multiple bins can be assembled into one coordinated system.

The rack architecture exists to improve:

aggregate harvest capacity

resilience through modular redundancy

mission flexibility

total buffered burst capability

servicing and replacement

Rack principles

each bin remains independently valid

bins should fail gracefully without killing the rack

rack coordination must not erase bin autonomy

energy sharing, if used, must be controlled and limited

common bus design must not create cross-coupled instability

Rack coordination options

There are two valid rack styles.

1. Federated rack

Each bin powers its own mission load.
A supervisory layer only monitors health and status.

Best for:

resilience

modular testing

easier fault isolation

2. Coordinated rack

Bins feed a managed shared service layer through controlled aggregation.

Best for:

larger burst events

shared communication infrastructure

centralized telemetry or gateway loads

The repo will document both, but the single-bin design remains the foundation.

What the architecture deliberately avoids

This design deliberately avoids:

one universal harvest bus at the input

undefined source interactions

continuous exposure of the control rail to burst loads

battery dependency hidden inside the system story

architecture language that outruns measured reality

Avoiding those errors is part of the architecture.

Design constraints

All downstream design work must stay inside these constraints:

battery-free core mission

supercapacitor-based storage

source-specific front ends

two-class output policy

energy-aware control

modular single-bin validity

defensible rack scaling

measurable 72-hour autonomy under named conditions

Any design choice that breaks one of those constraints must be challenged.

Completion standard for architecture

The system architecture is only complete when the repo also includes:

source-path documents

storage topology document

control-policy document

power-budget method

mechanical bin layout

rack topology

test and validation plan

This file defines the structure those later documents must follow.

Summary

IX-ZeroCell-72 is a modular battery-free energy system made credible by architecture discipline.

Its core form is:

source-specific intake

protected merge

supercap-centered storage

energy-aware control

always-on low-power rail

gated burst rail

modular bin scaling

rack-capable deployment

That is the correct system architecture for the ZeroCell family.
