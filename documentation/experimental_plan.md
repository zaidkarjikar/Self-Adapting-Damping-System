# 1. Objective
The primary objective of the experiment is to generate a comprehensive data-driven foundation regarding the dynamic behavior of the driver during the grinding process.
Specifically, the experiment aims to:
1. Characterize the Amplitude (A) and Frequency (f) of continuous vibrations.
2. Quantify the Amplitude (A) and Duration (d) of sudden force impacts (shocks) acting on the cylindrical roller.
3. Analyze thermal loads and high-frequency noise in the grinding zone.

This data is prerequisite for developing the control algorithms for the Self-Adapting Damping System.

# 2. Experimental Setup

### 2.1. Sensor Configuration
The following sensor array will be installed to capture multi-physical signal data:

| Sensor Type | Location | Metric | Purpose |
|-------------|----------|--------|---------|
| Force       | Driver   |Force Amplitude (F), Impact Duration (d)| To detect and quantify sudden mechanical shocks transferred to the roller.|
| Acceleration | Driver   |Vibration Amplitude (A), Frequency (f)| To map the vibrational spectrum of the driver during operation. |
| Structure-Borne Sound | Grinding Zone   |Acoustic Emission (High Frequency)| To detect high-frequency micro-vibrations and loads where stress is highest.|
| Temperature     | Grinding Zone |Temperature (T)| To monitor local heat generation, which influences MR fluid viscosity requirements.|

### 2.2. Experimental Variables
To ensure the damping system is robust, the experiments will follow a full factorial design variation based on the following process parameters:
* __Variable 1 - Cutting Speed (Vc):__
  Variation of the grinding wheel rotational speed.
* __Variable 2 - Feed Rate (Vf):__
  Variation of the in-feed velocity of the workpiece.
* __Variable 3 - Coolant Volume Flow (Vkss):__
  Variation of the lubricant flow rate
* __Variable 4 - Tool Condition:__
  Comparative tests between a newly dressed grinding wheel and a worn grinding wheel (defined by specific wear degree).

# 3. Procedure
## 3.1. Phase I: System Calibration & Baseline
### 3.1.1. Phase Objectives
1. __Sensor Verification:__ Ensure all installed sensors (force, acceleration, acoustic emission, temperature) are functioning and correctly calibrated.
2. __Thermal Equilibrium:__ Establish a steady thermal state for the machine before testing begins to account for thermal drift.
3. __Noise Floor Determination:__ Quantify the inherent vibration Amplitude (A0) and Frequency (f0) of the rotating driver without process loads (air cutting).
4. __Interference Check:__ Confirm that no "false positives" (phantom shocks) are detected by the force sensors during idle rotation.

### 3.1.2. Instrumentation Setup
Before calibration, verify physical installation:
1. __Driver Assembly:__
   * __Triaxial Acceleration Sensors:__ Mounted rigidly to the driver housing to detect vibration frequency (f).
   * __Force Sensors:__ Integrated into the driver flux to measure force amplitude (A) and impact duration (d).
2. __Grinding Zone:__
   * __Structure-borne Sound (AE) Sensor:__ Coupled to the machine headstock near the contact zone.
   * __Temperature Sensor:__ Positioned to capture local heat generation near the grinding contact point.

### 3.1.3. Calibration Protocol
__Step 1.1: Zero-Point Calibration (Static)__

With the machine completely turned stopped and cooland off:
1. Tare all Force Sensors to 0N.
2. Tare all Acceleration Sensors to eliminate DC gravity bias (if applicable) or verify 1g orientation.
3. Record ambient temperature (Tamb).

Success Criterion: Signal noise on force sensors must be < +- 0.5 N (or sensor resolution limit).

__Step 1.2: Establishing Thermal Baseline__
1. Run the machine spindle at nominal speed (e.g., mid-range of intended Vc) for 30 minutes without grinding.
2. Record Temperature (T) every 60 seconds until delta T/delta t = 0.
Purpose: As temperature affects the MR fluid viscosity and damping properties, we must stabilize the machine's own temperature first.

### 3.1.4: Dynamic Idle Testing (Air Grinding)
This step isolates the machine's kinematics from the cutting process.

__Experimental Matrix for Phase 1:__

Perform the following runs without a workpiece (or with a dummy workpiece not contacting the wheel).

| Run ID | Cutting Speed (Vc) | Feed Rate(Vf) | Coolant (Vkss) | Purpose |
|--------|--------------------|---------------|----------------|---------|
|  B-01  | Low                | 0             | Off            | Low-speed unbalance check |
|  B-02  | High               | 0             | Off            | High-speed unbalance check (Centrifugal forces) |
|  B-03  | High               | Simulated     | On (Max)       | Noise impact of cooland flow turbulence. |

### 3.1.5. Process
1. Set the driver to the target speed.
2. Activate coolant flow Vkss (for Run B-03) to measure noise introduced by fluid pressure.
3. Record a 60-second sample of:
   * Vibration Spectrum (FFT) to identify Eigenfrequencies (f0) of the driver.
   * Background Acoustic Emission levels.

### 3.1.6. Critical Analysis
1. Compare the Eigenfrequencies (f0) found here with the expected process frequencies.
2. If f0 matches the expected shock frequency, resonance will occur. This basline confirms if the system is naturally prone to resonance before grinding starts.

### 3.1.7. Success Criteria
Phase 1 is considered complete when:
1. All sensors provide stable, non-drifting signals.
2. The Noise Floow Amplitude (Anoise) is defined. This determines the threshold for the control algorithm: Signals > Anoise will be treated as shocks requiring damping.
3. The resonant frequencies (f0) of the driver assembly are mapped and documented.
   
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

# 4. Data Analysis
The collected raw data will be processed to extract:
* __Frequency Resonance Function (FRF):__ To identify the resonant frequencies of the driver.
* __Shock Envelope:__ Defining the maximum expected force (Fmax) and the rise time of shocks.
* __Thermal Correlation:__ Mapping temperature rise vs. operation time.
