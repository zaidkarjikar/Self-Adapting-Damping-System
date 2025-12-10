# 1. Objective
The primary objective of the experiment is to generate a comprehensive data-driven foundation regarding the dynamic behavior of the driver during the grinding process.
Specifically, the experiment aims to:
1. Characterize the Amplitude (A) and Frequency (f) of continuous vibrations.
2. Quantify the Amplitude (A) and Duration (d) of sudden force impacts (shocks) acting on the cylindrical roller.
3. Analyze thermal loads and high-frequency noise in the grinding zone.

This data is prerequisite for developing the control algorithms for the Self-Adapting Damping System.

# 2. Experimental Setup

### 2.1. Sensor Configuration

| Sensor Type | Location | Metric | Purpose |
|-------------|----------|--------|---------|
| Force       | Driver   |Force Amplitude (F), Impact Duration (d)| To detect and quantify sudden mechanical shocks transferred to the roller.|
| Acceleration | Driver   |Vibration Amplitude (A), Frequency (f)| To map the vibrational spectrum of the driver during operation. |
| Structure-Borne Sound | Grinding Zone   |Acoustic Emission (High Frequency)| To detect high-frequency micro-vibrations and loads where stress is highest.|
| Temperature     | Grinding Zone |Temperature (T)| To monitor local heat generation, which influences MR fluid viscosity requirements.|

### 2.2. Experimental Variables
* __Variable 1 - Cutting Speed ($V_c$):__
  Variation of the grinding wheel rotational speed.
* __Variable 2 - Feed Rate ($V_f$):__
  Variation of the in-feed velocity of the workpiece.
* __Variable 3 - Coolant Volume Flow ($V_Kss$):__
  Variation of the lubricant flow rate
* __Variable 4 - Tool Condition:__
  Comparative tests between a newly dressed grinding wheel and a worn grinding wheel (defined by specific wear degree).

# 3. Procedure
## 3.1. Phase I: System Calibration & Baseline
### 3.1.1. Phase Objectives
1. __Sensor Verification:__ Ensure all installed sensors (force, acceleration, acoustic emission, temperature) are functioning and correctly calibrated.
2. __Thermal Equilibrium:__ Establish a steady thermal state for the machine before testing begins to account for thermal drift.
3. __Noise Floor Determination:__ Quantify the inherent vibration Amplitude ($A_0$) and Frequency ($f_0$) of the rotating driver without process loads.
4. __Interference Check:__ Confirm that no false positives (ghost shocks) are detected by the force sensors during idle rotation.

### 3.1.2. Instrumentation Setup
Before calibration, verify physical installation:
1. __Driver Assembly:__
   * __Acceleration Sensors:__ Mounted rigidly to the driver housing to detect vibration frequency ($f$).
   * __Force Sensors:__ Integrated into the driver flux to measure force amplitude ($A$) and impact duration ($d$).
2. __Grinding Zone:__
   * __Structure-borne Sound (AE) Sensor:__ Coupled to the machine headstock near the contact zone.
   * __Temperature Sensor:__ Positioned to capture local heat generation near the grinding contact point.

### 3.1.3. Calibration Protocol
__Step 1.1: Zero-Point Calibration (Static)__

With the machine completely stopped and coolant off:
1. Set all Force Sensors to 0N.
2. Set all Acceleration Sensors to eliminate DC gravity bias if it is applicable.
3. Record ambient temperature ($T_{amb}$).

__Step 1.2: Establishing Thermal Baseline__
1. Run the machine spindle at nominal speed for 30 minutes without grinding.
2. Record Temperature (T) at regular intervals until $\Delta T$ / $\Delta t\$ = 0.
Purpose: As temperature affects the MR fluid viscosity and damping properties, we must stabilize the machine's own temperature first.

### 3.1.4: Dynamic Idle Testing (Air Grinding)
This step isolates the machine's kinematics from the cutting process.

__Experimental Matrix for Phase 1:__

Perform the following runs without a workpiece or with a dummy workpiece.

| Run ID | Cutting Speed $V_c$ | Feed Rate $V_f$ | Coolant $V_{kss}$ | Purpose |
|--------|--------------------|---------------|----------------|---------|
|  B-01  | Low                | 0             | Off            | Low-speed unbalance check |
|  B-02  | High               | 0             | Off            | High-speed unbalance check (Centrifugal forces) |
|  B-03  | High               | Simulated     | On (Max)       | Noise impact of coolant flow turbulence. |

### 3.1.5. Process
1. Set the driver to the target speed.
2. Activate coolant flow $V_{kss}$ (for Run B-03) to measure noise introduced by fluid pressure.
3. Record a 60-second sample of:
   * Vibration Spectrum (FFT) to identify Eigenfrequencies ($f_0$) of the driver.
   * Background Acoustic Emission levels.

### 3.1.6. Critical Analysis
1. Compare the Eigenfrequencies ($f_0$) found here with the expected process frequencies.
2. If $f_0$ matches the expected shock frequency, resonance will occur. This basline confirms if the system is naturally prone to resonance before grinding starts.

### 3.1.7. Success Criteria
Phase 1 is considered complete when:
1. All sensors provide stable, non-drifting signals.
2. The Noise Floor Amplitude ($A_{noise}$) is defined. This determines the threshold for the control algorithm: Signals > $A_{noise}$ will be treated as shocks requiring damping.
3. The resonant frequencies ($f_0$) of the driver assembly are mapped and documented.
   
## 3.2. Phase II: Parametric Variation (Grinding Cycles)

1. __Process Mapping:__
   Correlate specific operating parameters ($V_c$, $V_f$) with Vibration Amplitude ($A$) and Frequency ($f$).
3. __Shock Characterization:__
   Quantify the sudden force impacts by measuring their Peak Amplitude ($A_peak$) and Pulse Duration ($d$).
5. __Thermal Impact:__
   Determine how the Coolant Volume Flow ($V_{kss}$) influences the temperature rise in the driver, which affects MR fluid viscosity.

### 3.2.2. Experimental Matrix (DoE)
To cover the full operating range, a full factorial test matrix will be executed.

__Variables:__
1. Cutting Speed ($V_c$): Low vs High
2. Feed Rate ($V_f$): Low vs High
3. Coolant Flow ($V_{kss}$): Standard vs Reduced (to test thermal limits)

__Test Run Definitions:__

| Run ID | Cutting Speed $V_c$ | Feed Rate $V_f$ | Coolant $V_{kss}$ | Purpose                                                                  |
|--------|---------------------|-----------------|-------------------|--------------------------------------------------------------------------|
|  P-01  | Low                 | Low             | Standard          | Base reference. Minimal load, cleanest signal                            |
|  P-02  | High                | Low             | Standard          | Frequency Check. Impact of high rotational speeds on vibration frequency |
|  P-03  | Low                 | High            | Standard          | Force Check: Impact of aggressive feed on Force Amplitude ($A$).         |
|  P-04  | High                | High            | Standard          | Max Load: Worst-case steady-state scenario.                              |
|  P-05  | High                | High            | Reduced           | Thermal Stress: Provoke temperature rise to test sensor drift.           |

### 3.2.3 Execution Procedure
__Step 2.1: Workpiece Setup__
1. Load a cylindrical roller into the clamping system.
2. To ensure runout shocks are present for measurement, use rollers with known geometric deviations if available, or rely on the inherent process dynamics described in the problem statement.

__Step 2.2: Grinding Cycle Execution__
1. Initiate grinding cycle according to the parameters in the Test Run table (P-01 to P-05).
2. Log high frequency sampling on Force and Acceleration sensors to capture transient start-up shocks.

__Step 2.3: Shock Capture__
1. The system has to measure the duration ($d$) of sudden impacts.
2. During the transition phase (when the wheel first touches the roller face), trigger a burst mode recording.
3. Identify the time delta ($\Delta t$) from the initial force spike to signal stabilization. This value d determines how fast the MR fluid's magnetic field must react.

__Step 2.4: Thermal Logging__
1. For Run P-05, extend the cycle duration.
2. Monitor the temperature (T) sensor near the grinding zone.
3. Terminate if temperature sensor exceeds safety limits or stabilizes.

### 3.2.4 Data Analysis
From the raw data, the following metrics must be extracted for the control logic:
1. __Trigger Threshold__ ($A_{thresh}$) - The vibration amplitude level that distinguishes normal grinding from a shock event.
2. __Reaction Window__ ($t_{react}$) - Based on the shock duration, how much time does the control unit have to energize the electromagnets?
3. __Damping Map__ - A lookup table correlating Cutting Speed $V_c$ to the dominant Vibration Frequency ($f$), allowing the controller to predict unwanted resonance.

### 3.2.5 Success Criterion
Phase 2 is complete when:
1. A clear distinction between "steady vibration" and "shock impact" is visible in the data.
2. The duration (d) of shocks is quantified.
3. Data exists for both high-load and thermal-stress scenarios.

## 3.3. Phase III: Environmental Stress Testing

### 3.3.1. Phase Objectives
1. __Thermal Characterization:__ Quantify how the driver assembly heats up over time ($t$) and how this temperature rise ($\Delta \vartheta$) affects the MR fluid's container and coil resistance.
2. __Viscosity Drift Simulation:__ Since MR fluid viscosity $\eta$ drops as temperature rises, we must determine if the "passive" viscosity changes enough to require active compensation from the controller.
3. __Sensor Resilience:__ Verify that the acceleration and force sensors do not drift or fail under high-heat and high-humidity (coolant mist) conditions .

### 3.3.2 Setup Modifications
1. Tooling: Use a standard (dressed) grinding wheel to keep vibration consistent.
2. Instrumentation:
   * Focus: High-priority monitoring of the Temperature Sensors near the grinding zone and on the driver housing.
   * Environment: Ensure the coolant delivery system is fully active to simulate the "wet" environment that creates humidity and mist.

### 3.3.3 Experimental Matrix (Stress Factors)
This phase pushes the system to its environmental limits rather than its mechanical limits.

| Run ID | Cycle Duration     | Coolant $V_{kss}$ | Grinding Load       | Purpose |
|--------|--------------------|-------------------|---------------------|---------|
|  E-01  | Extended (60 min)  | Standard          | Medium (Continuous) | Saturation Test: Find the max steady-state temperature ($\vartheta_{max}$) the driver reaches. |
|  E-02  | Standard           | Reduced (50%)     | High                | Heat Spike: Provoke rapid heating to test sensor response speed. |
|  E-03  | Standard           | Off (Dry Run)     | Low (Short Bursts)  | worst-Case Thermal: Simulate coolant failure scenario (optional safety test). |

### 3.3.4 Execution Procedure
__Step 4.1: The "Saturation" Run (Run E-01)__
1. Run a continuous grinding operation (or simulated load) for 60 minutes.
2. Plot Temperature ($\vartheta$) vs. Time ($t$).
3. Identify the time constant ($\tau$)—how long does it take for the driver temperature to stabilize?
4. If the driver reaches $60^\circ$C after 20 minutes, the MR fluid's base viscosity might drop significantly. The control unit needs to know this "warm-up curve."

__Step 4.2: The "Coolant Stress" Run (Run E-02)__
1. Reduce coolant flow to 50% while maintaining high grinding parameters.
2. Monitor the Structure-borne Sound (AE) sensor.
3. Hypothesis: Less coolant = more friction = more heat = potentially higher noise/vibration.
4. Watch for signal drift in the force sensors. If the sensors are sensitive to temperature gradients (pyroelectric effect), false shocks might be recorded.

### 3.3.5 Data Analysis

The output of Phase 3 is used to calculate a Thermal Compensation Factor ($k_{\vartheta}$) for the control algorithm.
1. As Temperature ($\vartheta$) $\uparrow$, Fluid Viscosity ($\eta$) $\downarrow$.
2. The control unit must increase the Magnetic Field Current ($I$) to compensate for the thinner fluid .
   $$I_{req} = I_{base} + k_{\vartheta} \cdot (\vartheta_{current} - \vartheta_{ref})$$

This experiment provides the data to define $k_{\vartheta}$.

### 3.3.6 Success Criterion

Phase 3 is complete when:
1. The maximum operating temperature ($\vartheta_{max}$) of the driver is established.
2. The correlation between Driver Temperature and "Drift" in the sensor signals is mapped.
3. We confirm whether the MR fluid will stay within its functional temperature range or if active cooling (or current compensation) is strictly necessary.

## 3.4. Phase IV: Wear Simulation

### 3.3.1 Phase Objectives
1. __Wear Characterization:__ Determine how the vibration amplitude ($A$) and frequency ($f$) change as the grinding wheel degrades.
2. __Threshold Validation:__ Verify if the shock trigger threshold defined in Phase 2 remains valid for a worn tool, or if the control logic requires a dynamic threshold that adapts to tool age.
3. __Frequency Shift Analysis:__ Identify if the worn wheel induces new resonant frequencies that overlap with the driver's eigenfrequencies ($f_0$).

### 3.3.2 Setup Modifications
1. __Tool Change:__ The standard grinding wheel used in Phase 2 is replaced with a worn grinding wheel.
2. __Instrumentation:__ Maintain the exact sensor configuration from Phase 2 to ensure data comparability.

### 3.3.3 Experimental Matrix
To isolate the wear variable, we repeat the specific test runs from Phase 2 that represented the "Best Case" (Low Load) and "Worst Case" (High Load) scenarios.

| Run ID | Ref ID | Cutting Speed $v_c$ | Feed Rate $v_f$ | Purpose |
|--------|--------|---------------------|-----------------|---------|
| W-01   | P-01   | Low                 | Low             | Baseline Drift: How much does the noise floor rise just becayse the wheel is worn? |
| W-02   | P-02   | High                | High            | Max Stress: Does a worn wheel under high load generate vibration spikes ($A$) that look like false shocks? |





1. __Tool Change:__ Replace the dressed wheel with a pre-worn grinding wheel.
2. __Repetition:__ Repeat Phase II to determine how tool wear alters the frequency signature (f) and amplitude (A) of the shocks.

# 4. Data Analysis
The collected raw data will be processed to extract:
* __Frequency Resonance Function (FRF):__ To identify the resonant frequencies of the driver.
* __Shock Envelope:__ Defining the maximum expected force (Fmax) and the rise time of shocks.
* __Thermal Correlation:__ Mapping temperature rise vs. operation time.
