# 1. Objective
To generate a proper data driven foundation of the dynamic behavior of the driver during the grinding process.
Specifically,
1. Amplitude ($A$) and Frequency ($f$) of continuous vibrations
2. Amplitude ($A$) and Duration ($d$) of sudden force impacts (shocks) acting on the roller.
3. Thermal loads and high frequency noise in the grinding zone.

This data is prerequisite for developing the control algorithms for the self adapting damping system.

# 2. Experimental Setup

### 2.1. Sensor Configuration

| Sensor Type           | Metric                                   | Purpose                                                                             |
|-----------------------|------------------------------------------|-------------------------------------------------------------------------------------|
| Force                 | Force Amplitude (F), Impact Duration (d) | To detect and quantify sudden mechanical shocks transferred to the roller.          |
| Acceleration          | Vibration Amplitude (A), Frequency (f)   | To map the vibrational spectrum of the driver during operation.                     |
| Structure-Borne Sound | Acoustic Emission                        | To detect high-frequency micro-vibrations and loads where stress is highest.        |
| Temperature           | Temperature (T)                          | To monitor local heat generation, which influences MR fluid viscosity requirements. |

### 2.2. Experimental Variables
* __Variable 1 - Cutting Speed ($V_c$):__
  Variation of the grinding wheel rotational speed.
* __Variable 2 - Feed Rate ($V_f$):__
  Variation of the in-feed velocity of the workpiece.
* __Variable 3 - Coolant Volume Flow ($V_Kss$):__
  Variation of the lubricant flow rate.
* __Variable 4 - Tool Condition:__
  Comparative tests between a newly dressed grinding wheel and a worn grinding wheel.

# 3. Procedure
## 3.1. Phase I: System Calibration & Baseline
### 3.1.1. Phase I Objectives
1. Ensure all installed sensors are functioning and correctly calibrated.
2. Establish a steady thermal state for the machine before testing begins to account for thermal drift.
3. Determine the internal vibration Amplitude and Frequency of the rotating driver without any loads.
4. Confirm that no false positives (ghost shocks) are detected by the force sensors during idle rotation.

### 3.1.2. Calibration
__Zero-Point Calibration__
1. Set all Force sensors to 0N.
2. Eliminate bias in Acceleration sensors.
3. Record ambient temperature.

__Thermal Baseline__
1. Run the spindle at nominal speed for a specified duration without grinding.
2. Record temperature at regular intervals until $\Delta T$ / $\Delta t\$ = 0 (temperature variation with time tends to be equal to zero).

   __Purpose:__ As temperature affects the MR fluid viscosity and damping properties, we must stabilize the machine's own temperature first.

### 3.1.3 __Experimental Matrix:__

Perform the following runs without a workpiece or with a dummy workpiece.

| Run ID | Cutting Speed $V_c$ | Feed Rate $V_f$ | Coolant $V_{kss}$ | Purpose                                  |
|--------|---------------------|-----------------|-------------------|------------------------------------------|
|  A-01  | Low                 | 0               | Off               | Low-speed unbalance check                |
|  A-02  | High                | 0               | Off               | High-speed unbalance check               |
|  A-03  | High                | Simulated       | Maximum           | Noise impact of coolant flow turbulence. |

### 3.1.4. Process
1. Set the driver to the target speed.
2. Activate coolant flow $V_{kss}$ (for Run A-03) to measure noise introduced by fluid pressure.
3. Record a 60-second sample of:
   * Vibration spectrum to identify eigenfrequencies of the driver.
   * Background acoustic emission levels.

### 3.1.5. Data Analysis
1. Compare the Eigenfrequencies found here with the expected process frequencies.
2. If the eigenfrequency matches the expected shock frequency, resonance will occur. This basline confirms if the system is naturally prone to resonance before grinding starts.

### 3.1.6. Success Criteria
Phase 1 is considered complete when:
1. All sensors provide stable, non-drifting signals.
2. The Noise Floor Amplitude is defined. This determines the threshold for the control algorithm: $\text{Signals} > \text{Noise Floor Amplitude}$ will be treated as shocks requiring damping.
3. The resonant frequencies of the driver assembly are mapped and documented.
   
## 3.2. Phase II: Parametric Variation

### 3.2.1 Phase II Objectives
1. Correlate cutting speed $V_c$ and feed rate $V_f$ with vibration amplitude and frequency.
2. Measure the peak amplitude and shock duration of sudden force impacts.
3. Determine how coolant volume flow ($V_{kss}$) influences temperature rise in the driver, which in turn could affect MR fluid viscosity.

### 3.2.2. Experimental Matrix
Perform the following runs to cover the full operating range.

__Variables:__
1. Cutting Speed ($V_c$): Low vs High
2. Feed Rate ($V_f$): Low vs High
3. Coolant Flow ($V_{kss}$): Standard vs Reduced (to test thermal limits)

__Test Run Definitions:__

| Run ID | Cutting Speed $V_c$ | Feed Rate $V_f$ | Coolant $V_{kss}$ | Purpose                                                                  |
|--------|---------------------|-----------------|-------------------|--------------------------------------------------------------------------|
|  B-01  | Low                 | Low             | Standard          | __Base reference:__ Minimal load, cleanest signal                            |
|  B-02  | High                | Low             | Standard          | __Frequency Check:__ Impact of high rotational speeds on vibration frequency |
|  B-03  | Low                 | High            | Standard          | __Force Check:__ Impact of aggressive feed on Force Amplitude ($A$).         |
|  B-04  | High                | High            | Standard          | __Max Load:__ Worst-case steady-state scenario.                              |
|  B-05  | High                | High            | Reduced           | __Thermal Stress:__ Provoke temperature rise to test sensor drift.           |

### 3.2.3 Process
1. Load a cylindrical roller into the clamping system.
2. Initiate grinding cycle according to the parameters (B-01 to B-05).
3. Log high frequency sampling on Force and Acceleration sensors to capture start-up shocks.
4. The system has to measure the duration $d$ of sudden impacts:
   * Identify time required from the initial force spike to signal stabilization. (This duration $d$ determines how fast the MR fluid's magnetic field must react.)
5. For Run B-05, monitor temperature sensor values for extended cycle duration, terminate upon stabilization.

### 3.2.4 Data Analysis
From the raw data, the following metrics must be extracted for the control logic:
1. __Trigger Threshold__ ($A_{thresh}$) - The vibration amplitude level that distinguishes normal grinding from a shock event.
2. __Reaction Window__ ($t_{react}$) - Based on the shock duration, how much time does the control unit have to energize the electromagnets?
3. __Damping Map__ - A lookup table correlating Cutting Speed ($V_c$) to the dominant Vibration Frequency ($f$), allowing the controller to predict unwanted resonance.

### 3.2.5 Success Criterion
Phase 2 is complete when:
1. A clear distinction between steady vibration and shock impact is visible in the data.
2. The duration ($d$) of shocks is quantified.
3. Data exists for both high-load and thermal-stress scenarios.

## 3.3. Phase III: Environmental Stress Testing

### 3.3.1. Phase Objectives
1. Measure how the driver assembly heats up over time and how this temperature rise affects MR fluid's viscosity.
2. Verify that acceleration and force sensors do not drift or fail under high heat and high humidity conditions.

Since the MR fluid's viscosity drops as temperature rises, does the viscosity change enough to require active compensation?


### 3.3.2 Setup Modifications
Use a standard grinding wheel to keep vibration consistent.

### 3.3.3 Experimental Matrix (Stress Factors)

| Run ID | Cycle Duration     | Coolant $V_{kss}$ | Grinding Load       | Purpose                                                                       |
|--------|--------------------|-------------------|---------------------|-------------------------------------------------------------------------------|
|  C-01  | Extended           | Normal            | Medium (Continuous) | Find the max steady-state temperature ($\vartheta_{max}$) the driver reaches. |
|  C-02  | Standard           | Reduced (50%)     | High                | Provoke rapid heating to test sensor response speed.                          |
|  C-03  | Standard           | Off (Dry Run)     | Low (Short Bursts)  | Simulate coolant failure.                                                     |

### 3.3.4 Process
___C-01___
1. Run a continuous grinding operation for predecided extended duration.
2. Plot Temperature ($T$) vs. Time ($t$).
3. Identify how long does it take for the driver temperature to stabilize?

(The MR fluid's viscosity might drop significantly till around $60^\circ$ C. The control unit should know this warm-up curve.)

___C-02___
1. Reduce coolant flow to 50% while maintaining high grinding load.
2. Monitor the structure-borne Sound (AE) sensor.

(Less coolant = more friction = more heat = potentially higher noise/vibration?)

3. Observe signal drifts in the force sensors.

(If the sensors are sensitive to temperature gradients, false shocks might be recorded?)

### 3.3.5 Data Analysis

The output of Phase 3 is used to calculate a Thermal Compensation Factor ($k_{T}$) for the control algorithm.
1. As Temperature ($T$) $\uparrow$, Fluid Viscosity ($\eta$) $\downarrow$.
2. The control unit must increase the Magnetic Field Current ($I$) to compensate for the thinner fluid .
   $$I_{req} = I_{base} + k_{T} \cdot (\vartheta_{current} - \vartheta_{ref})$$

This provides the data to define $k_{T}$.

### 3.3.6 Success Criterion

Phase 3 is complete when:
1. The maximum operating temperature ($T_{max}$) of the driver is established.
2. The correlation between Driver Temperature and Drift in the sensor signals is mapped.
3. We confirm whether the MR fluid will stay within its functional temperature range or if active cooling is strictly necessary.

## 3.4. Phase IV: Wear Simulation

### 3.4.1 Phase Objectives
1. Determine how the vibration amplitude and frequency change as the grinding wheel degrades.
2. Identify if the worn wheel induces new resonant frequencies that overlap with the driver's eigenfrequencies.

Does the shock trigger threshold defined in Phase II remain valid for a worn tool, or does the control logic require a dynamic threshold that adapts to tool age?

### 3.4.2 Setup Modifications
The standard grinding wheel used in Phase 2 is replaced with a worn grinding wheel.

### 3.4.3 Experimental Matrix
To isolate the wear variable, we repeat the specific test runs from Phase II that represented the "Best Case" (Low Load) and "Worst Case" (High Load) scenarios.

| Run ID | Ref ID | Cutting Speed $V_c$ | Feed Rate $V_f$ | Purpose                                                                                        |
|--------|--------|---------------------|-----------------|------------------------------------------------------------------------------------------------|
| D-01   | B-01   | Low                 | Low             | How much does the noise floor rise just becayse the wheel is worn?                             |
| D-02   | B-02   | High                | High            | Does a worn wheel under high load generate vibration spikes ($A$) that look like false shocks? |

### 3.4.4 Process
1. Measure and document the diameter and surface condition of the worn tool before starting.
2. Execute runs D-01 and D-02 using the exact same workpiece geometry as Phase 2
3. Measure the acceleration amplitude.

(The worn wheel would show a higher average amplitude than the fresh wheel?)

4. Verify if sudden impact is still detectable while grinding the worn wheel (higher vibration baseline).

(The Signal-to-Noise Ratio SNR might be worse. The shock might be hidden under the higher vibration noise of the worn wheel.)

5. Calculate the SNR for the shock event using the worn wheel data.

### 3.4.5 Data Analysis
The primary output for Phase 4 is to determine if a Static Threshold or Dynamic Threshold is needed for the control unit.
__Scenario A (Static Threshold Works):__
1. Shock Amplitude ($A_{shock}$) > Worn Wheel Noise ($A_{worn}$).
2. __Logic:__ if Signal > X, trigger damping.

__Scenario B (Dynamic Threshold Needed):__
1. Worn Wheel Noise ($A_{worn}$) approaches or exceeds the original Phase 2 Threshold ($A_{thresh}$).
2. The control unit must learn the new baseline ($A_{worn}$) and only trigger on spikes relative to that new baseline.

### 3.4.6 Success Criterion
Phase 4 is complete when:
1. The vibration increase ($\Delta A$) attributable solely to tool wear is quantified.
2. The frequency spectrum ($f$) of the worn wheel is mapped to check for resonance risks with the driver.
3. A decision is made on whether the MR Damping Control Algorithm needs a Tool Wear Compensation factor.
