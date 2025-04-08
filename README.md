NASSCOM-VSD SoC Design Program
This repository documents the work done as part of the NASSCOM-VSD open-source SoC design program. The goal was to understand the complete RTL-to-GDSII flow using the Sky130 process node and tools like OpenLane.

Objectives
Learn digital design fundamentals

Understand ASIC design flow from RTL to layout

Use open-source tools for synthesis, floorplanning, placement, routing, and verification

Tapeout a RISC-V based SoC block

Tools Used
OpenLane

Yosys

Magic

KLayout

Netgen

OpenSTA

Sky130 PDK

Design Overview
The project implements a basic RISC-V core and runs it through the full physical design flow. Steps include:

RTL design in Verilog

Functional simulation

Synthesis and gate-level netlist generation

Floorplanning and power planning

Placement and clock tree synthesis

Routing and parasitic extraction

DRC and LVS checks

GDSII generation

Repository Structure
verilog/: RTL design files

openlane/: Physical design project

pdks/: Sky130 PDK setup (not included here)

reports/: Logs and output reports

images/: Flow diagrams and results
