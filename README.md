# DAY 1

The RTL to GDSII flow is a crucial process in VLSI design, transforming an RTL description of a digital circuit into a physical layout suitable for fabrication. It encompasses stages such as RTL synthesis, floor planning, placement, routing, and the final generation of the GDSII file format, which contains the detailed layout data. This thorough process ensures that the resulting IC layout faithfully represents the intended functionality and adheres to fabrication requirements.

![flow](https://github.com/user-attachments/assets/334e3541-0fca-49d8-8a1d-16676b413a2c)

## Introduction to IC Design components and terminologies

![ic_inside](https://github.com/user-attachments/assets/a6042840-1fbf-4d74-a44a-29198573933f)

- Core

The core is the region of the chip where the essential logic of the design is implemented. It houses all the combinational circuits, soft and hard IPs, and the connecting nets.

- Die

The die is the section of the chip that encloses the core and IO pads. Multiple copies of the die are imprinted across the silicon wafer to maximize production yield.

- IO Pads

IO pads are the interfaces that facilitate communication between the core and the external environment. Pad cells encompass the rectangular metal patches where external connections are made, including input, output, and power pads.

- IPs

Foundry IPs are typically manually designed or require human intervention to define and create, such as SRAM, ADC, DAC, and PLLs.

- PDKs

PDKs (Process Design Kits) serve as the interface between the foundry and design engineers. They include a set of files that model the fabrication process for design tools, encompassing device models, DRC, LVS, physical extraction, layers, LEF, standard cell libraries, timing libraries, and more. In this workshop, the SkyWater 130nm PDK is used, specifically sky130_fd_sc_hd, with openLANE built around this PDK.

## Simplified RTL to GDS Flow


The simplified RTL to GDS flow begins with an RTL file and, through a series of stages, produces a GDS file, which can be sent to a foundry for fabrication. The steps in the RTL to GDS flow include:


![rtltogds](https://github.com/user-attachments/assets/d192d108-3dc6-4aee-b4f8-a159de31c829)


#Lab 1


Understanding the use of various linux commands
pwd : It displays the present working directory and its path.

cd : Using this command we can move in both ways in the directory tree.

ls : It lists all the sub-directories and files present in the current directory.

mkdir : Using this command, we can create a new directory.

rmdir : Using his command, we can delete an existing directory.

rm : This command is used to delete the files.

help : using this command we can know the working of any command.

clear : This command clears the terminal.

To run in interactive mode (step by step mode)

    bash-4.2$ ./flow.tcl -interactive

![2pic](https://github.com/user-attachments/assets/c9268fd5-824e-4c61-b6a4-3278eb466215)

Package import and check

    % package require openlane
![3pic](https://github.com/user-attachments/assets/3c579bdc-ae67-4ec2-b66d-d6081a2ccd4c)

To prepare and setup the design

    % prep -design picorv32a

![4pic](https://github.com/user-attachments/assets/b5bcd4c7-4068-4e24-86bc-9ac5dd2d38c2)


##Synthesis

     % run_synthesis

![synthesis](https://github.com/user-attachments/assets/76ca6f5e-20f1-40c1-b83e-b7675893e3be)

Calculation:

![calculator](https://github.com/user-attachments/assets/87f6709d-8124-4774-9fb6-1fb1ce267d9a)


# Day 2

## Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells

Chip FloorPlanning Considerations:
![fl1](https://github.com/user-attachments/assets/6a0a9969-5ec0-4592-badd-fe4a1149e1be)


Utilization Factor and Aspect Ratio

To determine the Utilization Factor and Aspect Ratio, it's essential to first understand how the height and width of the core and die areas are defined.

The core is the region within a chip designated for placing all the logic cells and components. It is where the primary logic of the chip resides.

The die is the area surrounding the core, used for placing I/O-related components.
![fl2](https://github.com/user-attachments/assets/056d1340-6a46-408d-bfe3-d1a16f209785)


The height and width of the core area are determined by the design’s netlist, which is based on the number of components required to implement the logic. Consequently, the height and width of the die area will depend on the dimensions of the core area.

![fl3](https://github.com/user-attachments/assets/4e2edfe0-f776-43ef-9b28-11d797b50a53)


Utilization Factor: The Utilization Factor is defined as "The ratio of the core area occupied by the netlist to the total core area." For an optimal FloorPlan, the Utilization Factor should never be '1' because if it reaches '1', there will be no room for adding additional logic if needed, which would result in a poor FloorPlan.

Utilization Factor = (Area occupied by netlist / Total core area)

Aspect Ratio: The Aspect Ratio is defined as "The ratio of the height of the core to the width of the core." If the Aspect Ratio is '1', the core is considered to be square-shaped; if it is other than '1', the core will have a rectangular shape.

Aspect Ratio = (Height of the core / Width of the core)

As a designer, it's crucial to ensure that certain settings, known as switches, are properly configured before initiating the floorplan process. These switches, such as the utilization factor and aspect ratio, can significantly impact the floorplan. Designers should verify that all switches are aligned with the project's requirements to ensure smooth execution. The image below illustrates various types of switches involved in the floorplan stage.

    %run_floorplan 
![floor1](https://github.com/user-attachments/assets/aadda2d1-a19b-49b4-b994-4dbab192d60a)

![floor2](https://github.com/user-attachments/assets/a8483c7e-dab3-4c7e-aa24-be602b88916e)

![floor3](https://github.com/user-attachments/assets/a2ab9716-5dc8-4b62-8993-c348d884ac8f)

 ### To open the file in Magic run below command
 
![f4](https://github.com/user-attachments/assets/083a4de7-e32f-4b8b-ad6f-4dec0f50a03e)

![f5](https://github.com/user-attachments/assets/5c7e55fd-8dd7-4fc6-9ab8-3c3ae14b8afd)

![f6](https://github.com/user-attachments/assets/989467be-eb43-46f3-b163-d30531e0812f)

### To run Placement run below command
    run_placement

![place1](https://github.com/user-attachments/assets/d5b221bf-053d-4f0b-8519-93853ab3f415)

## Design Steps
1.Circuit Design:
- Develop the logical schematic of the circuit.
- Specify the functionality and interconnections of standard cells.
  
2.Layout Design:
- Utilize layout tools (e.g., MAGIC) to construct the physical layout.
- Adhere to design rules and guidelines for cell placement and routing.

3.Characterization using GUNA:
- Conduct timing, power, and noise characterizations.
- Ensure the design meets the required specifications.

### Outputs
* CDL (Circuit Description Language): A text-based representation of the circuit.
* GDSII: The layout file in GDSII format, ready for fabrication.
* LEF (Library Exchange Format): Provides details on cell sizes, pin locations, and other essential information.
* Spice Extracted Netlist: Includes parasitic components for accurate circuit simulation.
* Timing, Noise, and Power Libraries: Generated during the characterization process.

# Day 3

## Inverter Characterization using Sky130 Model Files

## CMOS Inverter Simulation with ngspice

This tutorial walks you through creating a basic CMOS inverter netlist, performing DC and transient simulations using ngspice, and analyzing key static and dynamic characteristics.

## Static Characteristics

1. **Switching Threshold (Vth):**
   - The voltage at which the inverter switches from a high (logic 1) to a low (logic 0) state.
2. **Input Low Voltage (Vil):**
   - The highest input voltage that is still recognized as logic 0.
3. **Input High Voltage (Vih):**
   - The lowest input voltage that is recognized as logic 1.
4. **Output Low Voltage (Vol):**
   - The voltage at which the output moves from high to low.
5. **Output High Voltage (Voh):**
   - The voltage at which the output shifts from low to high.
6. **Noise Margins:**
   - The range of voltages between Vil and Vol (low noise margin) and between Vih and Voh (high noise margin).

## Dynamic Characteristics

1. **Propagation Delays:**
   - The time it takes for the output to respond to an input change.
2. **Rise Time (tr):**
   - The duration it takes for the output to go from Vol to Voh.
3. **Fall Time (tf):**
   - The duration it takes for the output to drop from Voh to Vol.

# Design Library Cell using Magic Layout and ngspice Characterization

## Creating Standard Cell Layout

1. **Design the Inverter Layout:**
   - Utilize a layout tool (such as MAGIC) to design the inverter layout.
   - Adhere to process-specific design rules and guidelines.
   - Position standard cells (transistors, metal layers, etc.) based on the logical schematic.

2. **Extraction Process:**
   - After completing the layout, extract parasitic capacitances and resistances.
   - In the `tkcon` window, run the command `extract all`.
   - This will produce an extracted file containing parasitic data, such as capacitances and interconnect resistances.
   - The extracted file is saved in the `vsdstdcelldesign` directory.

3. **SPICE Netlist:**
   - Use the extracted data to generate a SPICE-compatible netlist, typically in `.sp` or `.cir` format.
   - Include transistor models, capacitances, and resistances in the netlist.
   - Use this netlist for simulations in tools like ngspice.

## Magic Layout View to CMOS Inverter

To obtain the cell files, refer to  
[vsdstdcelldesign](https://github.com/nickson-jose/vsdstdcelldesign).

To extract the parasitics and characterize the cell design, use the following commands in the `tkcon` window:

    extract all
    
    ext2spice cthresh 0 rthresh 0
    
    ext2spice

![inv1](https://github.com/user-attachments/assets/140b5398-511b-438a-a045-506e3ef2672c)


The next step is to run the SPICE file in the ngspice tool using the following command:

    ngspice sky130_inv.spice
![inv2](https://github.com/user-attachments/assets/8a0aa69f-68d2-4112-be54-0280eccb87c8)

# Inverter Characterization using Sky130 Model Files

In this lab, we will characterize the inverter using ngspice and Sky130 model files. The goal is to extract key parameters from the simulation results.

## Parameters to Characterize

1. **Rise Time:**
   - The time taken for the output waveform to transition from 20% to 80% of its maximum value.
   - Using data points:
     - x0 = 6.26138e-09, y0 = 0.660007
     - x1 = 6.30366e-09, y1 = 2.64009
   - Rise time = x1 - x0 = 0.0423 ns

2. **Fall Time:**
   - The time taken for the output waveform to transition from 80% to 20% of its maximum value.
   - Using data points:
     - x0 = 8.06034e-09, y0 = 2.64003
     - x1 = 8.08818e-09, y1 = 0.659993
   - Fall time = x1 - x0 = 0.0280 ns

3. **Propagation Delay:**
   - The time taken for a 50% transition at the output (0 to 1) corresponding to a 50% transition at the input (1 to 0).
   - Using data points:
     - x0 = 2.17449e-09, y0 = 1.64994
     - x1 = 2.16e-09, y1 = 1.65011
   - Propagation delay = x1 - x0 = 0.045 ns

4. **Cell Fall Delay:**
   - The time taken for a 50% transition at the output (1 to 0) corresponding to a 50% transition at the input (0 to 1).
   - Using data points:
     - x0 = 4.06432e-09, y0 = 1.65
     - x1 = 4.05001e-09, y1 = 1.65
   - Cell fall delay = x1 - x0 = 0.0050 ns
## LEF File Creation

After successfully characterizing the inverter, the next step is to generate a LEF (Library Exchange Format) file.

Use the following command to download the necessary files:

    wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

**VLSI Layout Geometries and DRC Errors**

In this section, we examine independent layout geometries (M3.1, M3.2, M3.5, and M3.6) and identify the specific DRC (Design Rule Check) violations associated with each:

1. **M3.1 (Metal Width DRC):**
   - Issue: The metal trace width in M3.1 is less than the minimum required width.
   - Error: Metal width violation according to design rules.

2. **M3.2 (Metal Spacing DRC):**
   - Issue: The spacing between adjacent metal traces in M3.2 is below the required threshold.
   - Error: Metal spacing does not meet the design rules.

3. **M3.5 (Via Overlapping DRC):**
   - Issue: The vias in M3.5 are overlapping.
   - Error: Overlapping via issue.

4. **M3.6 (Minimum Area DRC):**
   - Issue: The area enclosed within M3.6 is below the minimum specified area.
   - Error: Minimum area requirement not met.

To launch the Magic tool, use the following command:

    magic -d XR

![poly1](https://github.com/user-attachments/assets/3f083aed-39a0-4667-9a45-d955946fef67)

![poly2](https://github.com/user-attachments/assets/bba1bfc3-ee52-49e8-8fa0-db3392ba702f)

![poly3](https://github.com/user-attachments/assets/05deba4f-b92f-47b3-a3c2-f44d89f48b02)

![poly4](https://github.com/user-attachments/assets/a28182c5-78b8-4ee1-9ac8-f17951f3e809)

![poly5](https://github.com/user-attachments/assets/698986a9-5595-409f-8a25-7c3696fe0bf4)

## To Remove errors below changes made in the sky130pdk file

![poly6](https://github.com/user-attachments/assets/695e0c01-1539-4b18-81fd-9d35a5331d7d)


![o6qifyhh](https://github.com/user-attachments/assets/b3abc6d7-f731-477d-b4cf-4bb1569cd473)


## Skywater130nm pdk rules

![rules](https://github.com/user-attachments/assets/257cb006-ac28-45e2-aeae-0426392fe84e)











     
    


