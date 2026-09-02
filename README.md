# 5.8-GHz LC-VCO Design in 180-nm CMOS | Cadence Virtuoso

> **Ongoing RFIC Design Project**  
> Design and characterization of a low-power 5.8-GHz differential LC Voltage-Controlled Oscillator (LC-VCO) in 180-nm CMOS using Cadence Virtuoso.

---

##  Project Overview

This project focuses on the design, simulation, RF characterization, and physical implementation of a **5.8-GHz differential LC-VCO** in a 180-nm CMOS technology.

The oscillator uses a **complementary NMOS-PMOS cross-coupled architecture**, a differential LC resonant tank, and **PMOS accumulation-mode varactors** for frequency tuning.

A key part of the design is the integration of an **LC resonator at the common-source/tail node of the NMOS cross-coupled pair**. The resonator is designed close to the second harmonic of the fundamental oscillation frequency (~11.6 GHz), with the objective of suppressing second-harmonic components and their contribution to oscillator noise.

The project follows a complete RFIC design flow, from theoretical design and schematic-level simulation to layout verification. **Parasitic extraction (PEX) and post-layout RF simulations remain as the next stage of the work.**

---

##  Design Objectives

The primary objectives of the project are:

- Design a differential LC-VCO operating near **5.8 GHz**.
- Target operation within the **5.8-GHz ISM band**.
- Achieve low DC power consumption.
- Obtain low phase noise at 1-MHz offset.
- Provide frequency tuning using an integrated PMOS accumulation-mode varactor.
- Design the LC resonator for the required oscillation frequency.
- Ensure sufficient negative resistance for reliable startup.
- Investigate second-harmonic suppression using a tail LC resonator.
- Characterize the RF behavior of the oscillator and resonator.
- Implement a symmetric RFIC layout.
- Verify the physical implementation using DRC and LVS.
- Evaluate layout-induced parasitic effects through PEX and post-layout simulation.

---

##  Circuit Architecture

The proposed LC-VCO consists of the following major blocks:

```text
                    VDD
                     │
              ┌──────┴──────┐
              │             │
            PMOS          PMOS
              │             │
              └─────┬───────┘
                    │
              LC Resonant Tank
            + PMOS Varactors
                    │
              ┌─────┴─────┐
              │           │
            NMOS        NMOS
              │           │
              └─────┬─────┘
                    │
             Common Source Node
                    │
              LC Tail Resonator
                    │
                   GND
```

### Main Components

| Component | Purpose |
|---|---|
| Differential LC Tank | Determines the fundamental oscillation frequency |
| PMOS Varactors | Provides voltage-controlled frequency tuning |
| NMOS Cross-Coupled Pair | Generates negative transconductance |
| PMOS Cross-Coupled Pair | Complements the NMOS pair and contributes to negative resistance |
| Tail LC Resonator | Provides frequency-selective impedance near the second harmonic |
| Differential Output | Provides the RF oscillation signal |

---

##  Design Methodology

The design follows the sequence below:

```text
Design Specifications
        ↓
LC Tank Design
        ↓
PMOS Varactor Characterization
        ↓
Cross-Coupled Pair Design
        ↓
Startup / Negative Resistance Analysis
        ↓
Tail LC Resonator Design
        ↓
S-Parameter / RF Characterization
        ↓
Transient Simulation
        ↓
PSS Analysis
        ↓
PNoise Analysis
        ↓
Layout Implementation
        ↓
DRC / LVS Verification
        ↓
PEX
        ↓
Post-Layout RF Simulation
```

### 1. LC Tank Design

The fundamental oscillation frequency is determined primarily by the LC resonator:

$$
f_0 = \frac{1}{2\pi\sqrt{LC}}
$$

For the target frequency:

$$
f_0 \approx 5.8\text{ GHz}
$$

The effective tank capacitance includes the intentional and parasitic capacitances:

$$
C_{tank} = C_{MIM} + C_{varactor} + C_{parasitic}
$$

An inductor of approximately:

$$
L = 1.01\text{ nH}
$$

was selected during the design process.

The effect of active-device parasitic capacitance was also considered during resonator validation. A parasitic capacitance of approximately:

$$
C_{parasitic} = 90.6\text{ fF}
$$

was incorporated into an equivalent passive resonator. The resulting passive resonator exhibited a resonance near:

$$
f_r \approx 5.82\text{ GHz}
$$

which closely corresponds to the intended 5.8-GHz operating frequency.

### 2. PMOS Varactor-Based Frequency Tuning

A PMOS accumulation-mode varactor is used as the voltage-controlled tuning element. Changing the varactor control voltage modifies its effective capacitance:

$$
C_{varactor} = C(V_{ctrl})
$$

and consequently changes the resonant frequency:

$$
f_0(V_{ctrl}) = \frac{1}{2\pi\sqrt{LC_{tank}(V_{ctrl})}}
$$

The tuning characteristic is evaluated by sweeping the control voltage and observing the resulting oscillation frequency. The VCO gain is defined as:

$$
K_{VCO} = \frac{df}{dV_{ctrl}}
$$

and can be approximated from simulation data as:

$$
K_{VCO} \approx \frac{\Delta f}{\Delta V_{ctrl}}
$$

### 3. Complementary Cross-Coupled Pair

The oscillator uses complementary NMOS and PMOS cross-coupled pairs to generate the negative transconductance required to compensate for losses in the LC resonator.

The simulated DC operating point provided approximately:

| Parameter | Value |
|---|---|
| NMOS $g_m$ | 4.76 mS |
| PMOS $g_m$ | 3.40 mS |
| Total $g_m$ | 8.16 mS |

The effective negative resistance is approximated by:

$$
R_{neg} = -\frac{2}{g_{mn}+g_{mp}}
$$

giving:

$$
R_{neg} \approx -245\Omega
$$

The transistor dimensions and operating points were selected to provide sufficient negative resistance for reliable oscillator startup while maintaining the desired power budget.

### 4. Second-Harmonic Tail Resonator

A major feature investigated in this design is the use of an LC resonator connected at the common-source node of the NMOS cross-coupled pair.

The oscillator generates harmonic components because of the nonlinear switching behavior of the active devices. For a fundamental frequency of approximately 5.8 GHz, the second harmonic occurs near:

$$
2f_0 \approx 11.6\text{ GHz}
$$

The tail LC resonator is therefore designed to resonate close to:

$$
f_{tail} \approx 11.6\text{ GHz}
$$

using:

$$
f_{tail} = \frac{1}{2\pi\sqrt{L_{tail}C_{tail}}}
$$

The purpose of this resonator is to provide a frequency-selective impedance at the common-source node and investigate the suppression of second-harmonic components. The effect of this harmonic suppression on oscillator phase noise is evaluated through RF noise simulations.

### 5. RF Characterization

RF characterization was performed to investigate the behavior of the resonator and the loading introduced by the active oscillator core.

Differential S-parameter analysis was used to extract the RF impedance of the oscillator. High-impedance RF ports were used to minimize direct loading of the resonator during characterization. The extracted differential impedance was approximately:

$$
|Z_{diff}| \approx 134.5\Omega
$$

This extracted impedance was incorporated into an equivalent passive resonator model for further validation.

#### Equivalent Passive Resonator Validation

The passive resonator model includes:

- Designed inductance
- Tank capacitance
- Extracted parasitic capacitance
- Equivalent RF loading impedance

The resulting resonance was observed near:

$$
f_r \approx 5.82\text{ GHz}
$$

This provides a practical validation of the LC tank model while accounting for active-device loading and parasitic capacitance.

### 6. Loaded Quality Factor

The loaded quality factor was estimated from the resonance bandwidth:

$$
Q_L = \frac{f_r}{BW_{3dB}}
$$

The current extracted value is approximately:

$$
Q_L \approx 6.1
$$

This parameter is subsequently used in the analytical evaluation of oscillator phase noise.

### 7. Simulation Methodology

The oscillator has been evaluated using Cadence SpectreRF analyses.

#### Transient Analysis

Used to investigate:

- Oscillator startup
- Steady-state oscillation
- Output waveform
- Oscillation amplitude
- Fundamental frequency

#### PSS Analysis

Periodic Steady-State analysis is used to determine the periodic operating solution of the oscillator and provide the steady-state solution required for RF noise analysis.

#### PNoise Analysis

Periodic Noise analysis is used to evaluate the phase-noise spectrum around the steady-state oscillation. The current simulated phase-noise result is approximately:

$$
L(1\text{ MHz}) \approx -129.7\text{ dBc/Hz}
$$

### 8. Power Consumption

The DC power consumption is determined from:

$$
P_{DC} = V_{DD}I_{DD}
$$

The current design operates at approximately:

$$
P_{DC} \approx 4\text{ mW}
$$

The power consumption is treated separately from the RF voltage developed across the resonator.

### 9. Oscillator Figure of Merit

The oscillator Figure of Merit can be evaluated using:

$$
FoM = L(\Delta f) - 20\log_{10}\left(\frac{f_0}{\Delta f}\right) + 10\log_{10}\left(\frac{P_{DC}}{1\text{ mW}}\right)
$$

where:

- $L(\Delta f)$ is the phase noise at the specified offset.
- $f_0$ is the oscillation frequency.
- $\Delta f$ is the frequency offset.
- $P_{DC}$ is the DC power consumption.

The final FoM will be reported after the operating point and performance values are finalized.

### 10. Layout Implementation

The complete LC-VCO layout has been implemented with emphasis on RF-aware physical design. The layout strategy includes:

- Differential symmetry
- Symmetric placement of active devices
- Appropriate placement of the LC tank
- Compact RF routing
- Controlled interconnects
- Device matching considerations
- Reduced unnecessary routing
- Dedicated physical implementation of the tail resonator

The layout is intended to maintain the electrical symmetry of the schematic while minimizing avoidable parasitic effects.

### 11. Physical Verification

The completed layout has been verified using:

#### DRC — Design Rule Check

**Status: CLEAN**

The layout satisfies the applicable physical design rules.

#### LVS — Layout Versus Schematic

**Status: CLEAN**

The extracted connectivity of the layout matches the intended schematic implementation.

### 12. Parasitic Extraction & Post-Layout Analysis

**Status: Pending**

The next stage of the project is parasitic extraction (PEX) from the verified layout. The extracted netlist will include physical parasitic elements introduced by:

- Metal interconnects
- Device connections
- Routing
- Junctions
- Layout-dependent capacitances and resistances

The extracted design will then be simulated using the same RF analysis flow.

#### Planned Post-Layout Analyses

- Transient analysis
- PSS analysis
- PNoise analysis
- Frequency tuning analysis
- DC power analysis
- Oscillation amplitude analysis
- Phase-noise comparison
- Pre-layout vs. post-layout comparison

The primary objective is to determine how physical parasitics affect:

- Resonant frequency
- Tuning range
- $K_{VCO}$
- Phase noise
- Oscillation amplitude
- Power consumption
- Overall oscillator FoM

---

##  Current Design Status

| Parameter | Current Status / Value |
|---|---|
| Technology | 180-nm CMOS |
| Target Frequency | 5.8 GHz |
| Inductor | 1.01 nH |
| Passive Resonator Frequency | 5.82 GHz |
| Extracted Parasitic Capacitance | 90.6 fF |
| Differential Impedance | 134.5 Ω |
| Loaded Q | 6.1 |
| NMOS $g_m$ | 4.76 mS |
| PMOS $g_m$ | 3.40 mS |
| Total $g_m$ | 8.16 mS |
| Equivalent $R_{neg}$ | ≈ −245 Ω |
| DC Power | ≈ 4 mW |
| Phase Noise @ 1 MHz | ≈ −129.7 dBc/Hz |
| Layout | Completed |
| DRC | Clean |
| LVS | Clean |
| PEX | Pending |
| Post-Layout Simulation | Pending |

*Note: Tuning-range and $K_{VCO}$ values will be added after the final tuning sweep is established.*

---

##  Tools & Technologies

- Cadence Virtuoso
- Cadence Spectre / SpectreRF
- GPDK 180-nm CMOS
- S-Parameter Analysis
- PSS Analysis
- PNoise Analysis
- Transient Analysis
- DRC
- LVS
- PEX (planned)

---

##  Suggested Repository Structure

```text
5.8GHz-LC-VCO/
│
├── README.md
│
├── schematic/
│   ├── lc_vco_schematic/
│   └── testbenches/
│
├── simulations/
│   ├── transient/
│   ├── pss/
│   ├── pnoise/
│   ├── s_parameters/
│   └── tuning/
│
├── rf_characterization/
│   ├── impedance/
│   ├── resonator/
│   └── varactor/
│
├── layout/
│   ├── layout/
│   ├── drc/
│   └── lvs/
│
├── post_layout/
│   ├── pex/
│   ├── extracted_netlist/
│   └── simulations/
│
├── documentation/
│   ├── calculations/
│   ├── figures/
│   └── paper/
│
└── results/
    ├── pre_layout/
    └── post_layout/
```

---

##  Project Status

### Completed

- [x] 5.8-GHz LC tank design
- [x] Complementary NMOS-PMOS cross-coupled oscillator
- [x] PMOS varactor integration
- [x] Second-harmonic tail LC resonator
- [x] Negative-resistance analysis
- [x] RF S-parameter characterization
- [x] Differential impedance extraction
- [x] Passive resonator validation
- [x] Transient simulation
- [x] PSS analysis
- [x] PNoise analysis
- [x] Frequency tuning analysis
- [x] Layout implementation
- [x] DRC verification
- [x] LVS verification

### In Progress / Planned

- [ ] Final tuning-range extraction
- [ ] Final $K_{VCO}$ extraction
- [ ] PEX
- [ ] Post-layout transient simulation
- [ ] Post-layout PSS
- [ ] Post-layout PNoise
- [ ] Pre-layout vs. post-layout comparison
- [ ] Final FoM evaluation
- [ ] Final performance comparison with published designs

---

##  Research Direction

The ongoing work investigates the relationship between:

`LC tank design → active-device parasitics → harmonic behavior → phase noise → physical layout parasitics`

with particular focus on the use of a second-harmonic tail resonator in a low-power 5.8-GHz LC-VCO.

The final version of the project will evaluate whether the proposed architecture maintains its RF performance after physical parasitic extraction and post-layout simulation.

---

##  Team

**Institution:** RNS Institute of Technology, Bengaluru

**Author:** Animesh  
**Co-authors:** Aayush Mishra, Pavan U Shanbhogue, S Manu Rakshith  
**Project Guide:** Ohileshwari M S

---

##  Project Disclaimer

This repository documents an ongoing academic RFIC design project.

The reported values represent the current simulation and design status. Post-layout results are not yet available and will be added after parasitic extraction and extracted-netlist simulations are completed.

No post-layout performance is claimed until it has been verified through simulation.
