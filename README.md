# 🔧 NASSCOM - VSD SoC Design Program

A 5-day learning journey into the world of open-source digital design, focusing on ASIC flow using tools like OpenLANE and the Sky130 process.

---

## 📚 Table of Contents

1. Day 1: Introduction to Open-Source EDA, OpenLane, and Sky130 PDK  
2. Day 2: Floorplanning Fundamentals and Library Cells  
3. Day 3: Magic Layout and SPICE-based Characterization  
4. Day 4: Timing Analysis and Clock Tree Essentials  
5. Day 5: RTL to GDSII Flow - Final Integration  

---

## 📆 Day-wise Summaries

### 🗓️ Day 1: Getting Started with Open Source ASIC Design

- Learned about chip-level components: die, pads, core
- Explored RISC-V ISA and its role in hardware-software interaction
- Understood open-source flow: RTL design → GDSII using EDA tools
- Breakdown of RTL2GDS stages:
  - Synthesis
  - Floorplanning & Power Planning
  - Placement
  - CTS (Clock Tree Synthesis)
  - Routing
  - Sign-off (DRC, LVS, STA)

## LAB : SKY130_D1_SK4 - Synthesis using Yosys

- First, navigate to the design directory:`cd ~/Desktop/work/tools/openlane_working_dir/openlane`.To open the openlane instance:

```bash
docker
# calls the docker instance for the openlane
./flow.tcl -interactive
# opens openlane terminal
package require openlane 0.9
# calls openlane 0.9
prep -design picorv32a
# prepares Picorv32a design for implementation
designs/picorv32a/runs/<run_id>/


run_synthesis
# runs synthesis and abc's
```

<img src="images/openlaneterminal.png" alt="OpenLane Terminal Screenshot" width="800"/>
- In runs/<run_id>/ folder, there's a config.tcl file that shows the actual configuration parameters used during the run, which may differ from the original `designs/picorv32a/config.tcl` file. This allows inspection of what defaults were applied during flow execution.
- After the run is complete, you can inspect the runs directory for output data. The results/ folder contains the synthesized netlist, logs/ stores detailed logs for each stage (like synthesis), and reports/ includes all reports generated during the flow. Among the multiple synthesis reports in reports/synthesis/, the one with the latest timestamp is the most accurate and should be referred to for final results
- To calculate the DFF ratio using the following formula:
FlipFlop Ratio = Number of D Flip Flops / Total Number of Cells
Percentage of DFFs = FlipFlop Ratio * 100
Percentage of DFFs = (1613 / 14876) * 100 = 10.84%
<img src="images/Screenshot 2025-04-09 020049.png" alt="D FF Ratio" width="800"/>







---

### 🗓️ Day 2: Floorplan Strategies and Library Components

- Compared effective vs poor floorplans
- Studied standard cells (inverter, buffer, etc.)
- Gained hands-on experience with floorplanning in OpenLane

📷 *[Add your Day 2 image here]*

---

### 🗓️ Day 3: Designing Cells with Magic and Running SPICE Simulations

- Designed and laid out a basic inverter
- Characterized cell using ngspice
- Extracted parameters for use in synthesis

📷 *[Add your Day 3 image here]*

---

### 🗓️ Day 4: Timing Analysis and Clock Distribution

- Pre-layout vs post-layout timing
- Importance of CTS and reducing clock skew
- Worked with OpenSTA to analyze slack and critical paths

📷 *[Add your Day 4 image here]*

---

### 🗓️ Day 5: Integration and Final Tape-Out

- Used TritonRoute and Magic to complete routing
- Ran DRC and LVS checks
- Generated GDSII file for submission

📷 *[Add your Day 5 image here]*

---

## 🧰 Tools Used

- **OpenLane**
- **Sky130 PDK**
- **Magic VLSI**
- **ngspice**
- **KLayout**
- **Yosys**
- **OpenSTA**

---





