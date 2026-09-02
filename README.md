Create a professional, technically strong project description for my resume and placement applications, targeting **Analog IC Design, RFIC Design, Mixed-Signal IC Design, and VLSI roles**.

My main project is the **design and implementation of a 5.8-GHz LC VCO in 180-nm CMOS technology using Cadence Virtuoso**. Present it as a complete transistor-level RFIC design flow, not merely as a simulation project.

The project flow and technical work are:

1. LC VCO Architecture and Frequency Tuning**

   * Designed a differential cross-coupled LC VCO in 180-nm CMOS.
   * Designed and optimized the LC tank and varactor-based frequency tuning mechanism.
   * Targeted operation around the 5.8-GHz ISM band with approximately 10% frequency tuning range.
   * Optimized device sizing and bias conditions for reliable oscillation and tuning performance.

2. Tail-Noise Filtering for Phase-Noise Reduction**

   * Implemented an LC-based tail-noise filtering technique to suppress the contribution of tail current-source noise to oscillator phase noise.
   * Optimized the filtering network for improved phase-noise performance while maintaining stable oscillation.

3. DC Power Optimization**

   * Optimized bias current, transistor sizing, and operating point to reduce DC power consumption while maintaining oscillation amplitude, frequency tuning range, and phase-noise performance.

4. RF Characterization of the LC Tank**

   * Performed RF characterization of the LC tank using S/Z-parameter analysis.
   * Extracted the equivalent resistance/impedance of the tank from Z-parameter analysis.
   * Evaluated the tank quality factor (Q) and analyzed its impact on oscillator performance.
   * Used the extracted RF characteristics to guide tank and passive-device optimization.

5. Cadence RF and Transient Analysis**

   * Performed transient simulations to verify startup, steady-state oscillation, output amplitude, and oscillation frequency.
   * Performed PSS analysis for steady-state periodic operation and accurate RF characterization.
   * Evaluated phase noise using RF simulation methodology.

6. PVT Robustness**

   * Verified phase-noise performance across process, voltage, and temperature (PVT) corners.
   * Verified oscillation frequency across PVT corners and optimized the design for robust operation.
   * Emphasize that the final design is PVT-clean with respect to both phase noise and oscillation frequency.

7. Layout and Post-Layout Verification**

   * Designed a symmetric/common-centroid layout considering matching, parasitic reduction, differential symmetry, and RF routing requirements.
   * Performed post-layout parasitic extraction (PEX).
   * Re-simulated the extracted design to evaluate the impact of layout parasitics on oscillation frequency, phase noise, and overall RF performance.
   * Present this as a complete pre-layout to post-layout verification flow.

