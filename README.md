<img width="1370" height="912" alt="image" src="https://github.com/user-attachments/assets/17739a0e-2dc3-404e-8f14-e03075b55168" />

# ACS37100 Breakout Board 10MHz Ultra Fast Current Sensor
Documentation and schematic reference for the Allegro ACS37100 10MHz TMR Current Sensor Eval Board. Available now on Tindie.

# Allegro ACS37100 10MHz TMR Current Sensor Evaluation Board

[![Get it on Tindie](https://www.tindie.com/products/41742/)]
[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC_BY--NC--ND_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/)

Technical documentation, schematic reference, and application guide for the **ACS37100 Industry's Fastest TMR Current Sense Eval** board, engineered by LogicalEdges.

---

## 🚀 The Problem: Measuring Wide-Bandgap Transients
Standard clamp-on oscilloscope current probes capable of capturing 10 MHz transients cost thousands of dollars. Meanwhile, standard integrated Hall-effect sensors (like the ACS712 or ACS724) typically hit a "bandwidth wall" at around 400 kHz. 

When working with modern **GaN (Gallium Nitride)** or **SiC (Silicon Carbide)**  electronics, switching edges occur in the 50ns range. A 400 kHz sensor acts as a low-pass filter, turning sharp switching transients into sluggish, rounded blobs on your oscilloscope. You cannot optimize what you cannot see.

## 💡 The Solution: 10 MHz TMR Silicon
This evaluation board is built around the **Allegro ACS37100**, the fastest **TMR (Tunnel Magnetoresistance)** silicon on the market. 
* **10 MHz Bandwidth:** See the true shape of your high-speed switching transients.
* **50 ns Response Time:** Capture microsecond peak fault currents before your FETs let out the magic smoke.
* **Coreless Architecture:** Traditional sensors use ferromagnetic cores that suffer from magnetic remanence (getting "magnetized" after a spike). The ACS37100 guarantees **zero magnetic hysteresis**—when the current stops, the waveform drops perfectly back to the baseline.

---

## 📐 Engineered for RF Signal Integrity & Advanced Prototyping
Sending a 10 MHz analog signal across a lab bench requires treating the output like a transmission line. This breakout board is designed strictly for high-fidelity lab measurements:

### 1. 50-Ohm Environment Ready
* Unpopulated SMA edge-mount footprints allow for professional coaxial connections.
* Inline 0805 series resistor pads allow you to populate **50-ohm source termination resistors**. This perfectly drives short (under 1 meter) SMA-to-BNC coaxial cables straight into your scope's 50-ohm terminated inputs, eliminating capacitive ringing and phase margin degradation.

### 2. Differential Math Channel Setup (Common-Mode Rejection)
High dV/dt switching nodes generate massive EMI. Single-ended measurements will often show false ringing. To capture pristine data:
* **VOUT (Signal):** The primary analog output representing the sensed current.
* **VREF (Baseline):** The integrated VREF pin outputs a rock-solid 1.65V reference corresponding exactly to 0 Amps.
* **The Scope Hack:** Route both VOUT and VREF to your scope. Use your oscilloscope's math function **(CH1 - CH2)** to mathematically subtract the reference from the output. This aggressively rejects common-mode noise and shifts your trace to a perfect 0V baseline. *(Sensitivity: 26.4 mV/A for the 50A variant - note: board has not been tested up to 50A).*

### 3. Hardware-Level Fault Customization
Don't rely on microcontroller software to catch a 50ns overcurrent event.
* **FAULT Pin:** Provides an ultra-fast, open-drain overcurrent flag to instantly turn off your gate drivers.
* **Tunable VOC Thresholds:** Populate the unpopulated VOC pin's 0805 resistor divider to set custom hardware-level fault trip points.

---

## 📂 Repository Contents & Open Source Status
This repository serves as the documentation hub for the LogicalEdges evaluation board.
* **`/Schematic`** - Contains the reference PDF schematic detailing the 50-ohm termination topology, VREF/VOUT routing, and fault logic. 
* **`/Docs`** - Link to the Allegro ACS37100 datasheet and related application notes.
* *(Note: The physical PCB layout, via-stitching matrix, and Gerber manufacturing files are proprietary to LogicalEdges and are not included).*

🛒 **Skip the layout work and start testing today:** **[[Get the Pre-Assembled Breakout Board on Tindie](https://www.tindie.com/products/41742/)]**

---

## ⚠️ CRITICAL SAFETY & DERATING WARNING (READ BEFORE USE)
**This board is explicitly classified as an Experimental Evaluation Board designed for lab prototyping by qualified engineers. It is NOT a certified consumer product.**

* **Untested High Current (Derating Required):** The bare ACS37100 IC is theoretically rated by the silicon manufacturer for up to 50 Amps. However, this assembled 1oz copper PCB breakout board has **NOT** been laboratory certified to sustain high continuous DC current. We make **zero claims** regarding its maximum safe continuous current limit. 
* **Usage Recommendation:** We strongly recommend significantly derating the continuous DC current to a safe level (e.g., 15A to 20A). Utilize the IC's higher 50A headroom strictly for microsecond transient peak measurements. 
* **Thermal Management:** We utilized a dense matrix of ~190 thermal vias to stitch the top and bottom copper layers, and removed the soldermask around the high-current bus. If you intend to push higher continuous currents, you must actively monitor thermal limits and add physical mass (e.g., flowing solder or soldering copper braid) to the exposed pads at your own risk.
* **Untested Isolation:** While the bare IC claims 5kV isolation and we have included a physical milled creepage slot in the PCB, this assembly is not certified for high voltage. **DO NOT use this board on AC Mains (120V/240V) or lethal high-voltage systems.**
* **Liability:** The user assumes full responsibility for safe integration, thermal management, and compliance. LogicalEdges' liability is strictly limited to manufacturing defects upon arrival, and shall not exceed the original purchase price. No refunds will be issued for components damaged by user misuse, thermal failure, or improper integration.
