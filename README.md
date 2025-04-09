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

## Day 1: Introduction to Open-Source EDA, OpenLane, and Sky130 PDK

### How to Talk to Computers

In this session, we explored the foundational concepts of communicating with computers, focusing on the architecture and components of integrated circuits.



---

### Introduction to QFN-48 Package, Chip, Pads, Core, Die, and IPs

- **QFN-48 Package**: A surface-mount IC package with 48 pins.
- **Chip Layout**:
  - **Pads**: Points for external connection.
  - **Core**: The heart of the IC where computation happens.
  - **Die**: The silicon wafer that holds the chip.
  - **IPs**: Pre-designed modules integrated into SoCs.
 
    <img src="images/Screenshot 2025-03-29 231640.png" width="800"/>

---

### Introduction to RISC-V

- RISC-V is an open-standard ISA based on reduced instruction set computing principles.
- Enables modular, extensible processor designs for SoCs and embedded applications.

---

### OpenLane and RTL to GDSII Flow

**OpenLane** is an open-source automated digital design flow from RTL to GDSII, integrating tools like Yosys, OpenROAD, Magic, Netgen, etc.

- Automates synthesis, floorplanning, placement, CTS, routing, and DRC/LVS checks.
- Uses **Sky130 PDK** for fabrication-compatible design rules.

<img src="images/Screenshot 2025-04-01 110009.png" width="800"/>

---

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
- After the run is complete, you can inspect the runs directory for output data. The results/ folder contains the synthesized netlist, logs/ stores detailed logs for each stage (like synthesis), and reports/ includes all reports generated during the flow. Among the multiple synthesis reports in reports/synthesis/, the one with the latest timestamp is the most accurate and should be referred to for final results.
  
- To calculate the DFF ratio using the following formula:
FlipFlop Ratio = Number of D Flip Flops / Total Number of Cells
Percentage of DFFs = FlipFlop Ratio * 100
Percentage of DFFs = (1613 / 14876) * 100 = 10.84%
<img src="images/Screenshot 2025-04-09 020049.png" alt="D FF Ratio" width="800"/>
- New files i.e. merged,synthesis are now created in the picorv32a folder







---

### 🗓️ Day 2: Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells

- Compared effective vs poor floorplans
- Studied standard cells (inverter, buffer, etc.)
- Gained hands-on experience with floorplanning in OpenLane
  

### 🔲 Preplaced Cells Concept
- The top-level logic is divided into smaller cuts or blocks, which are implemented separately.
- Some parts of the circuit are designed in a reusable, black-boxed format — often used multiple times like an IP block.
- Examples include memory blocks, complex clock gating, muxes, comparators, ALUs, etc.
- These blocks are placed and fixed **before** the standard cell placement. Tools do not alter their positions during placement.
- These are called **pre-placed cells**, and must be surrounded with **decoupling cells** to maintain voltage integrity.

### ⚡ Decoupling Cells
- Help maintain stable supply voltage near pre-placed logic blocks.
- Mitigate voltage drops caused by resistance in the power delivery path.
- Act like capacitors that release charge during voltage dips.

### 🔌 Power (PWR) Planning
- If there's only one power supply point, the voltage drop can cause **signal integrity issues**.
- To mitigate this, **power mesh grids** are spread across the chip to ensure minimal distance from power to logic.

### 📍 Pin Placement
- Requires knowledge of how input/output pins will interact with internal logic.
- Affects routing congestion and final performance of the chip.

---

## LAB: Floorplanning & Placement

To understand configuration hierarchy:

```bash
~/Desktop/work/tools/openlane_working_dir/openlane/configuration < design/runs/config.tcl < design/PDK.tcl
```

- The directory `~/Desktop/work/tools/openlane_working_dir/openlane/configuration` contains the **default configuration files** used by OpenLane.
- Inside this folder, there's a `README.md` file that **documents all available configuration variables**. It's a great reference for understanding and customizing your design flow.

- Configuration Priority Order

OpenLane applies configuration settings in the following **priority order**:

```text
1. ~/Desktop/work/tools/openlane_working_dir/openlane/configuration
2. design/runs/config.tcl
3. design/PDK.tcl
```

```bash
  run_floorplan
  # run floorplan

```
<img src="day2/Screenshot from 2025-04-02 20-57-06.png" alt="Floorplan def" width="800"/>
###  Floorplan Dimensions and Die Area Calculation
In OpenLane, dimensions are expressed in **unit distance**, where:1000 unit distance = 1 micron


Based on the DEF (Design Exchange Format) file:

- **Width in unit distance** = `660685 - 0` = `660685`
- **Height in unit distance** = `671405 - 0` = `671405`

To calculate the **die area in microns²**:

Die Area = (Width × Height) / (1000 × 1000) = (660685 × 671405) / 1,000,000 ≈ 443587.21 µm²

###  Report and Visualization

- After completing the floorplan step, OpenLane generates a report that includes parameters like die area and aspect ratio.
- To visually inspect the floorplan and layout in a GUI, use the **MAGIC** tool.

> Tip: The `magic` GUI helps to debug DRC issues and inspect placement and routing interactively.
```bash
# in a seperate terminal enter the directory with def filr (results folder in recent run stage : floorplan)
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
###  Navigating the Layout in `magic` GUI

When using the `magic` GUI to explore your design, here are some helpful shortcuts and tips:

- **Center the design** for better viewing:
  - Press **`s`** to select the entire design.
  - Then press **`v`** to center the view.

- **Zoom into a specific location**:
  - **Left-click** to select the lower-left corner `(x1, y1)`
  - **Right-click** to set the upper-right corner `(x2, y2)`

- **Get pin or object info** in the layout:
  - Hover your cursor over the desired object.
  - Press **`s`** to select it.
  - In the **tkcon** console, type the following command:
    ```
    what
    ```
    This will display details like pin names, net connections, and more.
    
<img src="day2/Screenshot from 2025-04-03 01-33-48.png" alt="magic gui" width="800"/>

### Library Binding and Placement

- **Library**  
  The library contains multiple **flavors of standard cells**, providing:
  - Functional behavior
  - Timing characteristics
  - Physical layouts  

  These are crucial for synthesis, placement, and routing stages of the flow.

---

- **Placement** refers to the process of positioning the netlist elements (standard cells) **within the core area** defined during the floorplanning stage.

- This placement takes into account:
  - The **pin locations**
  - **Estimated resistance and capacitance** of interconnects
  - **Timing constraints**

- **Signal transition analysis** is performed post-placement to check:
  - Whether the placed cells are receiving signals **within the required timing window**

- If signal transitions are not meeting the required timing:
  - **Buffers are inserted** to reduce delay and improve signal integrity.

> Proper placement is critical for ensuring that the design meets timing and power constraints, and it sets the stage for successful routing.

```bash
run_placement
results/placement
#in above dir results present
```

<img src="day2/Screenshot from 2025-04-04 11-13-08.png" width="800"/>

```bash
# enter the directory with def file - results folder in recent run stage : placement
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

<img src="day2/Screenshot from 2025-04-04 11-36-40.png" alt="def generated in magic" width="800"/>


---

### 🗓️ Day 3: Design library cell using Magic Layout and ngspice characterization

- Designed and laid out a basic inverter
- Characterized cell using ngspice
- Extracted parameters for use in synthesis
  
### LAB: Custom Inverter Standard Cell

- Clone the custom inverter standard cell design from the GitHub repository: [nickson-jose/vsdstdcelldesign](https://github.com/nickson-jose/vsdstdcelldesign). 

  ```bash
  #Navigate to the openlane working dir
  cd ~/Desktop/work/tools/openlane_working_dir

  #clone cudtom standard cell from github
  git clone https://github.com/nickson-jose/vsdstdcelldesign.git

  # Move into the cloned inverter design directory
  cd vsdstdcelldesign

  # Copy the required Magic technology file from the PDK directory into the current folder
  cp ../../pdks/sky130A/libs.tech/magic/sky130A.tech .

  # Launch Magic with the custom inverter layout
  magic -T sky130A.tech sky130_inv.mag &

  # In the Magic GUI:
  # - Press "s" to select the component under your cursor.
  # - Pressing "s" repeatedly selects all electrically connected components.
  # - After selecting, use the "tkcon" window to run the command below for detailed info:
  #   what

  #for creating spice file

  #inside the magic tkconsole
  extract all

  # creates cell.ext file
  ext2spice

  # creates spice file

  ```
  
<img src="day3_1/Screenshot from 2025-04-06 18-52-04.png" alt="std cell magic gui" width="800"/>

-Here we identify nmos,pmos,Drain to drain connection of nmos and pmos,Pwr to Pmos connection,Gnd to Nmos connection.

<img src="day3_1/Screenshot from 2025-04-06 19-57-59.png " width="800"/>

  



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





