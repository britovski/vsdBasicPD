# PhyDesign_WS
Physical Design Workshop repo

## Description
This repository is a summary of the 5-day workshop of VLSI/SoC Physical Design using opensouce EDA tools provided by VSD. It is organized day-by-day as follows:

## Day 1

First day is used to introduce the cloud based structure of the workshop. The learning platform is divided in assessments (MCQs) and learning skills (DXSKXs). Also, a web based linux virtual machine is provided to labs hands-on execution.

Cloud based learning is guided through learning skils as follows:

### Fundamentals
Some concepts introduced:
- Board design x chip design
- packages x chip/die (composed by PADs + core) x IC
- Foundry IP's x IP's x Macros

### RISC-V ISA
An introduction to RISC-V architeture is done.
- Translation from high-level language to machine code is presented: C --> ASM --> binary code (compilator + assembler)
- Implementation of the RISC-V ISA can be performed using HDL in the front-end side and layout in the back-end side. For exemple: picorv32 CPU core.
- (Apps. --> System Softwares --> Hardware) real execution flow.
SoC is introduced by Raven and picoSoC examples (RISC-V based SoCs).
- SoC is related to the synthesizable logic in a chip. Ex: Raven Chip = Raven SoC + RAM blocks + analog IP's.

### Design tools
An introduction to IC Design flow and tools are performed. The goal is to show the RTL2GDS flow using opensource tools.
- Beginning with logic synthesis (using Yosys);
- Floorplanning;
- Placement (graywolf);
- Clock Tree Synthesis - CTS;
- Routing (Qrouter);
- Static Timing Analysis - STA (Opentimer);
* MAGIC layout viewer and editor is presented. Also used for equivalent circuit extraction and DRC;
* ngspice is presented for pré and post-layout simulations;
* eSIM is also presented for SPICE simulations with schematic capture functionality and also with PCB design capabilities;
Last but not least, Qflow is presented as a complete tool chain (using tools as Yosys and graywolf) for complete RTL2GDS flow.

Some examples using qflow gui is presented, as well as vsdflow (that is a script which uses .csv configuration files with the purpose to check if opensource tool flow is ok).
- vsdflow invokes qflow.

### Hands-on Labs
Some labs are performed using web based linux virtual machine with opensource tools.

**First step is to clone vsdflow repo**

    git clone https://github.com/kunalg123/vsdflow.git
 
**Then vsdflow script is used by typing below commands**

    cd vsdflow
    ./vsdflow spi_slave_design_details.csv
    ls -ltr outdir_spi_slave/

**and we can see some files creates.

**entering in the created folder and opening qflow with display option

    cd outdir_spi_slave
    qflow display spi_slave

It will open 2 windows "layout1" and "tkcon"

On "tkcon" window, type "box".

Question: What is the output area in microns?

![q1_1](https://github.com/britovski/PhyDesign_WS/blob/main/images/l11.PNG)

As we can show in the image above, the answer is: '15420.24 microns.'

After that the next labs introduce the picorv32 using qflow.

**typing below commands**

    cd
    cd vsdflow
    mkdir my_picorv32
    cd my_picorv32
    mkdir source synthesis layout
    cp ~/vsdflow/verilog/picorv32.v source/.
    qflow gui &

**Select below options in gui**

    Technology = osu018
    Verilog source file : picorv32.v
    Verilog module : picorv32

**Click on Set Stop**

**Then run labs till synthesis as shown in Labs Video**

Question: What is the % ratio of flipflop/total logic ?

![q2_1](https://github.com/britovski/PhyDesign_WS/blob/main/images/l12.PNG)

The number of DFF cells divided by total number of cells give us the answer of 12-13.99% 

Daily sync calls with zoom platform are used to track workshop progress and clarify questions.  

## Day 2

Second day presents the Chip floorplanning as the preparation before automatic placement and routing. Also presents the requirement of library cells and it design flow.

### Chip Floorplaning
Second workshop day begins with **Chip Floorplanning concept**. Some steps are introduced as part of Chip Floorplanning phase:
1) Define width and height of core and die based on standard cell dimensions
 - Place all standard cells inside the core
 - notions of utilization factor and aspect ratio.
2) Define location of pre-placed cells
 - separate circuits in to blocks or modules
 - select available IP's
 * The arrangement of the cells (IP's, blocks, modules) is referred as floorplanning.
 * pre-placed cells are placed in user-defined locations before automated place and route.
3) Surround pre-placed cells with decoupling capacitors.
 * Noise margin concept is presented (NMh for '1' and NMl for '0')
 - Vdd or Vss could drop without decoupling caps between Vdd and Vss;
 * Decoupling caps. are huge caps between Vdd and Vss and need to be placed near the circuit/block.
4) Power planning
 - If many blocks discharges from '1' to '0' at same time in a single ground cause a bump (Gnd bounce). If from '0' to '1' a voltage droop (for single Vdd).
 - Istead of single supply lines, use multiple arrays of power supply (Vdd and Vss points). See image below (from xyalis).
    
![powergrid](https://www.xyalis.com/wp-content/uploads/PowerGrid-1024x554.jpg)

 5) Pin placement
  - Connectivity is described using VHDL or verilog;
  - try to put pins near blocks;
  - bigger PADs for clock pins.
 6) Logical Cell placement blockage --> add PAD ring blocks.

**After floorplanning. We are ready for placement and routing steps**

Some tips are provided to use 'qflow gui' to setup placement (using pin arrangement UI).

Before introduction of Cell Design flow, some motivation is provided about **Placement** phase.

### Placement 
1) Before placement is required to bind netlist with physical cells. 

So, you need a **library**, that is a collection of blocks/cells with different flavors, sizes, *vt*, etc...).

2) Place the cells

3) Optimize the placement
 - check signal integrity;
 - add buffers for long paths;

4) After optimization, setup the timimg analysis with ideal clock. **we return to this on Day 4**

### Cell Design Flow (standard cells)

**Inputs:** PDKs, rules (DRC e LVS) and tech files, SPICE models, libraries and user defined specifications (supply voltages, layers, cell sizes, etc...).

**Design steps:** circuit design, layout design, characterization (timing, noise, power, .libs, functions, etc...).
- GUNA software for characterization
- timing characterization is based on threshold definitions, propagation delays and transition times.

**Outputs:** CDL, GDSII, LEF, extracted SPICE netlist (.cir)

### Hands-on Labs

Two way hands-on labs are performed in day 2. First one is from learning concepts, to use qflow gui for preparation and placement, as follows:

    Create my_picorv32 directory
    Enter in my_picorv32 directory
    Create source synthesis layout

    cp ../verilog/picorv32.v source/.
    Qflow gui &

    Select technode osu018
    Select verilog module picorv32

    Set stop

    Prep: run
    Synthesis: run

    Placement settings: init. Density 0.7
    Arrange Pins: Auto Group and apply
    Arrange Pins: New Group and create my_pin_grouping for resetn and clk pins. Check only left box, as we can seen in image below. 
    
![q1_2](https://github.com/britovski/PhyDesign_WS/blob/main/images/l22.PNG)

    Then, Run placement. 

After that, is possible to see placement running with graywolf on below image screen

![q2_2](https://github.com/britovski/PhyDesign_WS/blob/main/images/l23.PNG)

Second lab is guided by MCQs, and the goal is to measure layout area, as follows:

Type below command

    cd
    cd vsdflow/my_picorv32
    qflow display picorv32 &
    
This will open layout and tkcon window In the layout window, select whole chip using below steps

    Take cursor to bottom left
    Left mouse click
    Take cursor to top right
    Right mouse click
    Press Shift+i

This will select the whole layout Now in tkcon window, type below command

    box

What is the area of you chip in microns?

![q3_2](https://github.com/britovski/PhyDesign_WS/blob/main/images/l21.PNG)

As we can see on image above, the answer is '812062.19 microns.'


## Day 3

Third day is focused on the design and characterization of one library cell using MAGIC layout tool and ngspice.

### SPICE Simulations (pre-layout)
- SPICE deck / netlisting
- ngspice intro with simulation commands (source, run, setplot, display, plot...)
- 

### Art of Layout - Euler´s path and stick diagram
xxx

### MAGIC Labs
zzz

### Post-layout simulations
xxx

### Hands-on Labs

For the third day labs, the MCQs guide to use ngspice_labs repo @ github.

**First step is to clone ngspice_labs repo**

    git clone https://github.com/kunalg123/ngspice_labs.git
 
After...



## Day 4
xxx

## Day 5
xxx

## Final notes
