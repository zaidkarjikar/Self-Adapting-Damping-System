# Objective
The primary objective of the experiment is to generate a comprehensive data-driven foundation regarding the dynamic behavior of the driver during the grinding process.
Specifically, the experiment aims to:
1. Characterize the Amplitude (A) and Frequency (f) of continuous vibrations.
2. Quantify the Amplitude (A) and Duration (d) of sudden force impacts (shocks) acting on the cylindrical roller.
3. Analyze thermal loads and high-frequency noise in the grinding zone.

This data is prerequisite for developing the control algorithms for the Self-Adapting Damping System.

# Experimental Setup

### Sensor Configuration
The following sensor array will be installed to capture multi-physical signal data:

| Sensor Type | Location | Metric | Purpose |
|-------------|----------|--------|---------|
| Force       | Driver   |Force Amplitude (F), Impact Duration (d)| To detect and quantify sudden mechanical shocks transferred to the roller.|
| Acceleration | Driver   |Vibration Amplitude (A), Frequency (f)| To map the vibrational spectrum of the driver during operation. |
| Structure-Borne Sound | Grinding Zone   |Acoustic Emission (High Frequency)| To detect high-frequency micro-vibrations and loads where stress is highest.|
| Temperature     | Grinding Zone |Temperature (T)| To monitor local heat generation, which influences MR fluid viscosity requirements.|

### Experimental Variables
To ensure the damping system is robust, the experiments will follow a full factorial design variation based on the following process parameters:
* __Variable 1 - Cutting Speed (Vc):__
  Variation of the grinding wheel rotational speed.
* __Variable 2 - Feed Rate (Vf):__
  Variation of the in-feed velocity of the workpiece.
* __Variable 3 - Coolant Volume Flow (Vkss):__
  Variation of the lubricant flow rate
* __Variable 4 - Tool Condition:__
  Comparative tests between a newly dressed grinding wheel and a worn grinding wheel (defined by specific wear degree).

# Procedure
## Phase I: System Calibration & Baseline
### Phase Objectives
1. __Sensor Verification:__ Ensure all installed sensors (force, acceleration, acoustic emission, temperature) are functioning and correctly calibrated.
2. __Thermal Equilibrium:__ Establish a steady thermal state for the machine before testing begins to account for thermal drift.
3. __Noise Floor Determination:__ Quantify the inherent vibration Amplitude (A0) and Frequency (f0) of the rotating driver without process loads (air cutting).
4. __Interference Check:__ Confirm that no "false positives" (phantom shocks) are detected by the force sensors during idle rotation.

### Instrumentation Setup
Before calibration, verify physical installation

1. __Sensor Calibration:__ Zeroing of force and acceleration sensors.
2. __Idle Measurement:__ Recording of "noise floor" data (vibration and acoustic emission) with the spindle running but no contact between wheel and workpiece.
   
### Phase II: Parametric Variation (Grinding Cycles)
Execute the following sequence for each combination of variables defined in Section 3:
1. __Setup:__ Install cylindrical roller and align with driver.
2. __Process Start:__ Initiate grinding cycle at define Vc and Vf.
3. __Data Acquisition:__ Continuous logging of:
   * Vibration frequency spectra (f)
   * Peak amplitudes (A)
   * Temperature rise (delta T)
4. __Shock Provocation:__ Specific monitoring for sudden force spikes (simulating mechanical shocks or face runout). Measure the exact duration (d) of these impulse events.
### Phase III: Environmental Stress Testing
1. __Thermal Loading:__ Run extended cycles with reduced Cooland Volume Flow (Vkss) to generate maximum process heat.
2. __Measurement:__ Record the correlation between local Temperature (T0) and vibration characteristics to determine thermal drift in the driver.
### Phase IV: Wear Simulation
1. __Tool Change:__ Replace the dressed wheel with a pre-worn grinding wheel.
2. __Repetition:__ Repeat Phase II to determine how tool wear alters the frequency signature (f) and amplitude (A) of the shocks.

# Data Analysis
The collected raw data will be processed to extract:
* __Frequency Resonance Function (FRF):__ To identify the resonant frequencies of the driver.
* __Shock Envelope:__ Defining the maximum expected force (Fmax) and the rise time of shocks.
* __Thermal Correlation:__ Mapping temperature rise vs. operation time.
