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

![q1](https://github.com/britovski/PhyDesign_WS/blob/main/images/l11.PNG)

As we can show in the image above, the answer is: 15420.24 microns.

******

![q2](https://github.com/britovski/PhyDesign_WS/blob/main/images/l12.PNG)

The number of DFF cells divided by total number of cells give us an answer of 12-13.99% 

## Day 2
Second workshop day begins with Chip Floorplanning concept. Some steps are introduced as part of Chip Floorplanning phase:
    1) Define width and height of core and die based on standard cell dimensions
    - Place all standard cells inside the core
    - notions of utilization factor and aspect ratio.
    2) Define location of pre-placed cells
    - separate circuits in to blocks or modules
    - select available IP's
    * The arrangement of the cells (IP's, blocks, modules) is referred as floorplanning.
    * pre-placed cells are placed in user-defined locations before automated place and route.
    3)
    

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
