# Microwatt + Sensor Fusion Accelerator on OpenFrame

## Overview

This project integrates the **open-source Microwatt POWER CPU core** with a custom **sensor fusion accelerator**, implemented on the **OpenFrame harness**.

Unlike Caravel/Caravan, OpenFrame provides only the essential padframe, power-on-reset, and project ID ROM, giving us a clean slate to implement our custom SoC.

Our design demonstrates how an open-source CPU can be extended with a dedicated hardware accelerator to efficiently process real-time sensor data from IoT and wearable devices.

<img width="256" alt="OpenFrame Layout" src="https://github.com/efabless/openframe_timer_example/assets/67271180/ff58b58b-b9c8-4d5e-b9bc-bf344355fa80">

---

## Motivation

IoT and wearable devices rely heavily on **real-time sensor data processing** (accelerometer, gyroscope, temperature, etc.). Software-only solutions consume significant power and add latency.

By integrating a **hardware accelerator** directly with Microwatt, we enable:

- ⚡ Faster sensor fusion computations
- 🔋 Lower power consumption
- 📉 Reduced latency for event detection
- 🔧 Demonstration of practical **open-source SoC customization** on OpenFrame

This aligns with the hackathon’s theme of **"Microwatt for the open computing era"**, showing how open CPUs can be adapted for edge AI and IoT.

---

## Key Features of Our Design

1. **Microwatt CPU Integration**
    - Lightweight POWER ISA core
    - Acts as the main controller for sensor data management
2. **Custom Sensor Fusion Accelerator**
    - Implements weighted averaging
    - Kalman-filter inspired pre-processing
    - Threshold-based event detection (e.g., fall detection, anomaly alerts)
    - Exposed as memory-mapped peripheral to Microwatt
3. **OpenFrame Harness Advantages**
    - ~15mm² user area for CPU + accelerator
    - 44 configurable GPIOs for sensor connections and debugging
    - Simplified I/O with direct access to padframe

---

## Target Applications

- IoT edge devices
- Wearables (fitness tracking, health monitoring, fall detection)
- Low-power industrial monitoring sensors

---

## Project Structure

```
microwatt_sensorfusion/
│
├── verilog/rtl/        # Microwatt + accelerator RTL
│   ├── microwatt/      # Microwatt CPU core
│   ├── accel/          # Sensor fusion accelerator
│   └── top.v           # Integrated SoC top module
│
├── openlane/           # OpenLane configs
│   └── sensorfusion/   # Design-specific flow configs
│
├── testbench/          # Simulation & verification files
│
├── docs/               # Documentation & block diagrams
│
└── README.md           # Project documentation
```

## Setup Instructions

### 1. Clone Repository

```
git clone <repo_url>
cd microwatt_sensorfusion
make setup
```

### 2. RTL Integration

- Place Microwatt + accelerator Verilog under `verilog/rtl/`
- Update `openlane/sensorfusion/config.json` with:
    - `DESIGN_NAME` = top-level module
    - `VERILOG_FILES` = list of source files
    - `CLOCK_PERIOD` = 25ns (40 MHz target)

### 3. Hardening Flow

```
make sensorfusion
make openframe_project_wrapper
```

**4. Run Precheck**

```
make run-precheck
```

Ensure power connections use `vccd1_connection` and `vssd1_connection` macros.

## Deliverables

- ✅ Open-source RTL (Microwatt + accelerator)
- ✅ Testbenches and verification reports
- ✅ Hardened GDS via OpenLane flow
- ✅ Precheck logs and validation reports
- ✅ Documentation + final video demo
- ✅ MIT/Apache 2.0 licensed GitHub repository

## Team

- **Nidesh Kanna R**
- **Sankar Narayan**
- **Madhavan Shree A**
- **Chezhiyan**
- **Ebinesh**
- **Jhotheeshwar**
- **Ramaprakash**

---

## Future Work ✨

- Adding machine learning accelerators (TinyML integration with Microwatt)
- Expanding to multi-sensor fusion (e.g., heart rate, SpO₂, environmental sensors)
- Integrating with RISC-V peripherals for hybrid open-source SoCs
- Porting to FPGA for live demos before tapeout
---

## Acknowledgments 🙌

This project builds on the amazing work of the **OpenPOWER Foundation**, **Microwatt developers**, and **ChipFoundry** for enabling open-source ASIC design.

Special thanks to the mentors and the Microwatt Momentum Hackathon organizers for making this innovation possible.

---
