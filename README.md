# Unive_OpenSource_Project_Oesmita

**Project Title:** Low-Power CCSDS-Inspired Telemetry Frame Encoder with CRC Error Detection

**Field:** Aerospace & Satellite Systems

**One-line pitch:** A digital IP block that packages sensor/telemetry data into a fixed-format frame and appends a CRC checksum, mirroring how CubeSats and small satellites structure downlink data for reliable ground reception.

---

# README.md (for GitHub repository)

## Project Title
Low-Power Telemetry Frame Encoder with CRC Error Detection

## Project Objective
To design and tape out a digital IP block that encodes raw telemetry data (e.g., temperature, battery voltage, status flags) into a structured frame with error-detection capability, modeled after the framing philosophy used in CCSDS (Consultative Committee for Space Data Systems) telemetry standards used by real satellite missions.

*Note: this project uses CCSDS framing as inspiration for structure, not a certified/compliant implementation — worth stating clearly in your report so you're not overclaiming compliance with the actual standard.*

## Problem Statement
Satellites and CubeSats transmit telemetry data over long distances through a noisy RF channel. Bit errors introduced during transmission can corrupt sensor readings, leading to incorrect ground-station decisions. A structured framing + error-detection scheme lets the receiver identify corrupted frames and request retransmission or discard bad data, rather than acting on faulty telemetry.

## Application Domain
Aerospace & Satellite Systems (with relevance to any embedded system needing reliable serial data transmission — also applicable to IoT/industrial telemetry).

## Project Overview
The IP block accepts parallel input data (e.g., an 8-bit or 16-bit telemetry word), wraps it with a sync marker and header, computes a CRC-8 or CRC-16 checksum over the payload, and outputs a serialized frame ready for transmission. A companion decoder path (optional, time permitting) can validate incoming frames and flag CRC mismatches.

## Block Diagram
*(Include a simple diagram with these stages: Telemetry Data Input → Framing FSM → CRC Generator → Frame Assembler → Serial Output. A basic box-and-arrow diagram is enough — draw.io or even a hand sketch photographed works.)*

## Features
- 8-bit (or 16-bit) parallel telemetry data input
- Configurable frame header/sync word
- CRC-8 (or CRC-16) error detection, computed via LFSR-based logic
- Fully synchronous design
- Serial frame output ready for UART/RF transmission
- Parameterizable frame length

## Design Specifications
- **Technology:** IHP SG13G2 (130 nm)
- **Language:** Verilog HDL
- **Flow:** OpenROAD
- **Clock Frequency:** *(pick a modest target, e.g., 50 MHz — leave headroom since this is your first tapeout)*
- **Inputs:** Parallel telemetry data bus + clock + reset + data-valid signal
- **Outputs:** Serial frame output + frame-ready flag

## Suggested Build Order (for your own planning, not part of README)
1. Write a plain CRC-8 calculator module first, verify in simulation with known test vectors.
2. Write the framing FSM that assembles header + payload + CRC into a fixed structure.
3. Combine into a top-level module with a simple serializer.
4. Simulate end-to-end with a testbench feeding sample telemetry values.
5. Only then move to synthesis/PnR.

---

*Draft prepared to help structure your submission — review and adjust wording, clock frequency, and frame format before submitting, since these are your design decisions to finalize.*
