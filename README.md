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
# prepares Picorv32a design for implementation'''

📷 *[Add your Day 1 image here]*

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

## 📂 Folder Structure

```bash
.
├── day1/
├── day2/
├── day3/
├── day4/
├── day5/
└── README.md

