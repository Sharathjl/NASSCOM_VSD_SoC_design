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


     
    


