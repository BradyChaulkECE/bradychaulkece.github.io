

# Desktop Robotic Arm Project

## Overview

This project involves the design and development of a fully custom robotic arm, built from scratch with a focus on mechanical reliability, precision, and system-level integration.

Unlike previous software-heavy projects, this system emphasizes **physical engineering constraints**, including torque, structural rigidity, and power distribution.

The goal is to produce a **functional prototype within 2–3 months**, capable of lifting a 300g load at full extension while maintaining low backlash and high precision.

---

## Design Constraints

To guide development, the following constraints were defined early:

- **Timeline:** Working prototype within 2–3 months
- **Precision:** Minimize backlash as much as possible
- **Load Capacity:** Lift 300g at maximum reach
- **Budget:** ≤ $300 (including failed iterations)
- **Noise:** Keep volume low, but not a primary constraint
- **Independence:** No tutorials or prebuilt robotic arm systems

These constraints ensured the project remained:

> realistic, challenging, and fully self-driven

---

## System Architecture Decision

### Arm Structure Selection

Two primary robotic arm architectures were evaluated:

1. **Central Column Design**
    - Simpler, cheaper
    - Requires internal routing and gearing
    - Limited flexibility
2. **Segmented Industrial Design (e.g., UR5e)**
    - Modular joints with integrated gearboxes
    - Higher precision and range of motion
    - Significantly higher complexity and cost

### Final Choice

A **linear, double-supported arm design** was selected.

**Reasoning:**

- Higher structural stability
- Lower cost compared to industrial modular joints
- Better suited for external actuation and custom gearing

---

## Actuation System Design

### Motor Selection

Two options were evaluated:

#### Stepper Motors

- Pros:
    - Low backlash
    - High positional control
    - Supports gear reduction systems
- Cons:
    - Lower torque without gearing
    - Requires drivers and external control

#### Servo Motors

- Pros:
    - Integrated system (driver + gearbox)
    - High torque options available
- Cons:
    - Limited range (~180°)
    - Cost increases rapidly with torque

### Final Decision

- **Steppers** → Base roll, base pitch, elbow
- **Servos** → Wrist and gripper (future)

**Reasoning:**

- Keeps heavier components near the base
- Enables high gear ratios for torque-critical joints
- Uses servos where torque requirements are lower

---

## Joint Design Strategy

Three joint architectures were evaluated:

1. **Motor-Supported Joint**
    - Simple, but places stress directly on motor shaft
    - Not suitable for high torque systems
2. **Externally Supported Joint (Bearings + Shaft)**
    - Better load handling
    - Still suffers from poor weight distribution
3. **Remote Actuation (Selected)**
    - Motors remain at base
    - Torque transmitted via belts
    - Joints supported by bearings and shafts

### Final Decision: Remote Actuation

**Why:**

- Significantly improved weight distribution
- Reduced load on moving joints
- Enables higher torque capacity through gearing

---

## Power Transmission: Belts vs Gears

### Initial Plan

- Spur gears (e.g., 20T → 80T for 1:4 ratio)

### Problem

- High gear ratios (1:12–1:16) → very large gear sizes
- Increased width and mechanical complexity

### Final Decision: Belt Drive System

**Why:**

- More compact for high ratios
- Easier to stack and route
- Lower cost and simpler integration

---

## Mechanical Design

### Base System

- Square base (adjustable dimensions)
- Lazy-susan style rotation platform with bearing support
- Wide footprint for stability and load distribution

### Arm Structure

- Dual-sided support arms
- ~100mm spacing for:
    - Pulley systems
    - Future gear integrations
    - Structural stability

### Gear Ratios

- Stacked pulley system:
    - Two 1:4 ratios → compact high reduction

---

## End Effector (Gripper)

Two designs considered:

1. **Extending Dual-Axis Grip**
    - Greater reach
    - Lower force efficiency
2. **Gear-Based Clamp (Selected)**
    - Simpler mechanism
    - Better force transmission

---

## Electrical System & PCB Design

### Control System

- Microcontroller: **Raspberry Pi Pico**
- Stepper Driver: **TMC2209**

### Driver Selection Reasoning

The TMC2209 was selected due to:

- Microstepping capability (up to fine resolution)
- Reduced vibration and noise
- Higher voltage/current handling compared to simpler drivers

---

### Power System Design

- Main Supply: **12V 10A**
- Stepper drivers powered directly from 12V rail
- Capacitors added for voltage stability

### Voltage Regulation

- 5V (Pico): via buck converter
- 6V (Servos): via separate buck converter

---

### PCB Design Decisions

- **1.5mm traces** for power lines  
    → reduce voltage drop and noise
- **0.3mm traces** for signal lines  
    → efficient routing without compromising signal integrity
- **Ground plane (copper backplate)**  
    → improves return paths and reduces electrical noise
- **Fixed microstepping (1/16)**  
    → hardwired via 3.3V/VIO for consistent behavior

---

## Current Project State

- CAD: Complete (optimization ongoing)
- PCB: Designed and finalized
- Components: Selected and acquired
- Assembly: Not yet started

--- 





