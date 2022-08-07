# <p align="center">**Physical-Design-Workshop**</p>

In this repository, you will find the experience lived in the Workshop in VLSI in where We have used the tools Open Source with the technology Skywater130.

### Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK
----

#### **How to talk to computers**

A chip like that of an embedded system, in which it must internally communicate with elements such as SRAM, SPI, ADC DAC, PLL, and other devices that make up the chip, must have their respective pads, which are the internal connections with the external pins.

To be able to represent the general flow of a CPU, it must be passed through what is known as RISC-V, where a set of complex instructions are carried out that are based on computer principles, which for the tools to be used, is an easily compiled program that incorporates machine learning which allows the flow to be generated without the need for human manipulation. In summary, for the general flow, you must go through the ISA that is part of the RISC, implementation (RTL), and then layout.

</p>

#### **SoC design and OpenLANE**

What is known as ASIC, is defined as an integrated Circuit for specific applications, which consists of RTL IP's, EDA Tools, PDK data, which is known as the kit design process, which for this case is the one that comes from skywater130, which allows you to shut off the flow of design, as it delivers all the libraries with this technology, despite the fact that when compared with state of the art technology, it is a technology quite fast with that have already been implemented processors such as the Intel P4EE - Pentium 4.


<p align="center">
  <img src="https://i.imgur.com/t9lCyb6.jpg?style=centerme" />
</p>

##### **EDA Tools**
These tools are so important to due, are open source, and all use the library's skywater 130:

- Fill insertion, HDL Simulation, Global Placemenet
- LVS, Floor Planning, DFM, Logic Synthesis
- RC Extraction, RTL Synthesis, HD2 Design Entry
- DFT, Detailed Routing, Power Planning
- IR Droop Analysis, Static code analysis, DRC
- Static timing analysis, Logic equivalence checkin, Clock tree synthesis

##### **ASIC Flow Design**

Within the digital flow that is carried out to perform an ASIC, the Synthesis, Floor and Power planning, Placement, CTS, Routing and the Sign off intervene.

<p align="center">
  <img src="https://i.imgur.com/jDsYC4R.jpg" />
</p>

##### **Synth**

<p align="center">
  <img src="https://i.imgur.com/W1P2V8m.jpg" />
</p>

##### **FP + PP (Floor and Power planning)**
- **Floorplanning**
The floorplanning consists of defining how the different blocks that make up the main chip will be located, the frame of this is also located where the dimensions, the location of pins, and the rows of this should be defined.

<p align="center">
  <img src="https://siliconvlsi.com/wp-content/uploads/2021/09/Floorplan-1.jpg" />
</p>

- **Powe Planning**

In power planning, the energy that is going to be delivered to all the blocks that are inside the chip is planned.

<p align="center">
  <img src="https://i.imgur.com/fQgNPV5.jpg" />
</p>

##### **Place**

In the place the designed cells are located, which could go within the designated rows in the floorplanning, in such a way that it is in the grid.

<p align="center">
  <img src="https://vlsi-backend-adventure.com/images/placement/global.JPG" />
</p>

##### **CTS**

In the CTS, the distribution of how the clock signal will arrive for all sequential blocks is created and generally it has the shape of a tree.

<p align="center">
  <img src="https://vlsi.pro/wp-content/uploads/2013/08/clocktree.png" />
</p>

##### **Route**

In routing, the different blocks connected in the floorplanning are interconnected, for which the different masks provided by skywater130 are used.

<p align="center">
  <img src="https://vlsi-backend-adventure.com/images/routing/manhattan.JPG" />
</p>

##### **Sign off**

In the Sign off, all the physical verification tests are carried out which includes the DRC and LVS and also the timing verification for which Static Timing analysis (STA) is used.

##### **Open Source ASIC Flow - OPENLANE**

OpenLane is one of the most important tools, which is open source and is mainly used to generate GDSll without the need for human help, in which there should not be any type of violations by DRC, LVS and timing for which he has been trained with multiple design spaces, design examples and has the possibility of adding more in the future.

###### **OPENLANE ASIC flow**

<p align="center">
  <img src="https://i.imgur.com/3u4vQbd.png" />
</p>

1. **Synthesis exploration**
In this section, multiple solutions with delay and area are reviewed, which based on this analysis choose the best synthesis.

2.  **Design exploration - Openlane Regression Testing**
In this section, approximately 70 designs are run that are used to compare with the result and know which is the best.

3. **Designf for test (DFT)**
In this section, scanning inserts are made that allows generating test patterns pra then perform fault simulations, this is done with the Fault program.

4. **Place and Route**
In this section we follow some steps mentioned in the flow mentioned in ASIC Flow Design, where it intervenes: Floor Planning, And Decoupling Capacitors and Tap cell insertion, Placement, Post placement optimization, CTS and routing.

5. **Logic equivalence check (LEC)**
In this section it is formally verified that by making modifications to the CTS or in the previous optimizations that modify the netlist they have not caused the main function not to have changed.

6. **Dealing with antenna tules violations**
It is important to consider that when manufacturing the metal masks, antennas could be generated that could damage the transistor gates, for which false diode antennas are added to then run the magic antenna tester, and in case antennas are found, the false diodes antennas should be changed for a real one.

7. **Physical Verification DRC & LVS**
For the verification of DRC, magic is used and then also using magic, it is to extract the SPICE of the layout that would be used in conjunction with netgeny so that an LVS can be executed.

#### **Get familiar to open-source EDA tools**

To start working, it is important to go to the following route.

`$ cd/Desktop/work/tools/openlane/openlane_working_dir/openlane`

And here We should to type:

`$ docker`

`$ ./flow.tcl -interactive`

<p align="center">
  <img src="https://i.imgur.com/r2TyWJW.jpg" />
</p>

After that We can to type `$ package require openlane 0.9` which gets all dependencies for version 0.9 of openlane.

Now We're going to prepare our project with the next command

`$ prep - design openlane 0.9` and you will can see the next image

<p align="center">
  <img src="https://i.imgur.com/0bs80k0.jpg" />
</p>


`$cd/Desktop/work/tools/openlane/openlane_working_dir/openlane/designs/picorv32a/runs`

<p align="center">
  <img src="https://i.imgur.com/u7bSC6N.jpg" />
</p>

Now ready to run the synthesis with the following command

`$ run_synthesis` and after that You will can see the next image

<p align="center">
  <img src="https://i.imgur.com/gVrNN0O.jpg" />
</p>

After that We will can go to the path and to see that We have the file report.

`$cd/Desktop/work/tools/openlane/openlane_working_dir/openlane/designs/picorv32a/runs/report/synthesis`

And here We could  have information about all the synthesis

<p align="center">
  <img src="https://i.imgur.com/Nw96PVN.jpg" />
</p>

Finally from here we can obtain that we have a ratio of 0.1084 flops and 0.1118 buffers.

----

### Day 2 - Good floorplan vs bad floorplan and introduction to library cells
----

#### **Chip Floor planning considerations**

In order to carry out a good floorplan, different aspects must be taken into account, such as:

- **Define width and weight of core and die**

It starts from the idea of having a combinational circuit with its conventional symbols, to then obtain a circuit where the symbols are replaced by boxes, which are to be represented by the standard cell that will have a fixed height and width according to the type of standard cell.

These circuits are put together to be able to optimize the available area, said circuit would be located in the core of the chip that is inside the die.

With these data, we could calculate the utilization factor which is the ratio of the area occupied by the netlist over the total area of the core, and also the aspect ratio the ratio of height over width.

<p align="center">
  <img src="https://i.imgur.com/IC2uZCg.jpg" />
</p>

-  **Define the location of preplaced cells**

Como habia mencionado antes, el circuito principal si es lo suficientemente grande podria dividirse en varios bloques que al final se convertiran en cajas negras con sus respectivas entradas y salidas que se ubican en el core de acuerdo a como el usuario quiera, antes de ejecutar la herramienta automatizada.

<p align="center">
  <img src="https://i.imgur.com/nu4UbXg.jpg" />
</p>

-  **De-coupling capacitors**

Because locally there may be multiple sequential circuits and logic that are connected to the same vdd, so that when it does happen commutation, it is going to require quite current, which could generate you fall in the levels of tenión, what cause have levels logical undefined, by using capacitors of decoupling, so that the voltage is kept constant and when change has enough time to recover.

And globally, all the circuits are going to require them to be powered, so if both the vdd and the Gnd are linked to a single point, it could cause there to be voltage bumps in Vdd and Gnd, so the way to solve it is to generate a type of grid for Vdd and Gnd. 

<p align="center">
  <img src="https://i.imgur.com/njT3euI.jpgg" />
</p>

- ** Pin placement**

Finally, if in a large circuit there are pins that are repeated, what is done is to unify them to be able to take them to the ends of the die, they must also be strategically located according to the direction from which the signal comes and where it goes.

<p align="center">
  <img src="https://i.imgur.com/63xz0ak.jpg" />
</p>

-  **Using OpenLane for floorplanning**

Let's to type the next command for generate floorplanning with OpenLane

`$ run_floorplan` After that, you will can see the next image

<p align="center">
  <img src="https://i.imgur.com/FYJLESC.jpg" />
</p>

And if You go the next path you can see more information about floorplanning

`$~~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-08_18-44/logs/floorplan$`

So You will can see the next image

<p align="center">
  <img src="https://i.imgur.com/Mlv41f1.jpg" />
</p>

Finally we can see the floorplaning with magic, for that we must execute the following line.

`magic -T /home/juan.andres.lopez491/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../temp/merged.lef def read picorv32a.floorplan.def`

After that You will can see the next image

<p align="center">
  <img src="https://i.imgur.com/mU77Ag4.jpg" />
</p>

#### **Library Binding and Placement**

In this part is passed to generate the netlist that then be represented by the standard cell, however, these should be located strategic, which at this stage is calculated by the length and capacitance that can keep the cables connection and, based on that, insert repeaters, for this reason, the program checks the integrity of the signal from block to block, to turn the program to run it optimizes the position of the elements, in order that they do not violate different parameters of interest.

Let's to type the next command for generate floorplanning with OpenLane

`$ run_placement` After that, you will can see the next image

<p align="center">
  <img src="https://i.imgur.com/V15nnGh.jpg" />
</p>

And after that you can type the next command

`$ magic -T /home/juan.andres.lopez491/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`

 After that, you will can see the next image

<p align="center">
  <img src="https://i.imgur.com/UKm5QYg.jpg" />
</p>

#### **Cell design and characterization flows**

Because all design processes revolve in the vast majority concerning the Standard Cell, it becomes important to be able to characterize them, for this process three stages are involved, the inputs, the design step and the output.

<p align="center">
  <img src="https://i.imgur.com/vuZwIiX.jpg" />
</p>

One of the most common ways to characterize the Standard Cell is directly from the netlist that can be obtained from the Spice, something that is done when the netlist is extracted .Spice of magic. Another way is to directly consult the model that the manufacturer delivers. Another characterization method is to run simulations in spice and obtain the information from there, something that can be done with a fixed or time-varying voltage source, that is, through stimuli.

Finally, there is a mode that incorporates the use of GUNA, which allows calculating the timing, noise, power libs. function.

#### **General timing characterization parameters**

Another characterization important in a Standard Cell has to do with the times of propagation of each, depending on the reference to continue the percentages to locate the level low or high, it may be of 10%-90% or 20%-80%, in addition, the propagation time can be a fact of utility to the design of the standard cell,  it is also a data to take into account when wanting to avoid or correct metastability.

<p align="center">
  <img src="https://i.imgur.com/jf1U5NS.jpg" />
</p>

### Day 3 - Design library cell using Magic Layout and ngspice characterization
----

To work in this section the following code was executed, which copies the working folder in our directory

`https://github.com/nickson-jose/vsdstdcelldesign.git`

<p align="center">
  <img src="https://i.imgur.com/WgGcyBy.jpg" />
</p>

By downloading the folder, we will be able to work on the files, but we will have to bring the sky130A.tech file from the pdk, then we will execute the following code

`magic -T sky130A.tech sky130_inv.mag &` 

After that you can will the next image

<p align="center">
  <img src="https://i.imgur.com/0L20IH5.jpg" />
</p>

After that, We will get the file .spice of magic, We need to type the next command in the box of magic.

`extract all`

`ext2spice cthresh 0 rthresh 0`

`ext2spice`

After that, We will have a file with name sky130_inv.sipce

<p align="center">
  <img src="https://i.imgur.com/vDeHBhR.jpg" />
</p>

After that, Let's go to modified the file for create the simulation file, here We need to add the libraries, the type of simulation and the elements additionals.
<p align="center">
  <img src="https://i.imgur.com/y00AyC9.jpg" />
</p>

After that Let's go run the file in ngspice

`ngspice sky130_inv.sipce `

<p align="center">
  <img src="https://i.imgur.com/tsvdESa.jpg" />
</p>

Here finally, we write in the commands box, 'plot y vs time a' and we will see the graph of the output and input in time, here we could see at the simulation level the different delays of the inverter.

<p align="center">
  <img src="https://i.imgur.com/U8N8rwv.jpg" />
</p>

To end day 3, some DRC exercises were done

<p align="center">
  <img src="https://i.imgur.com/txkENNp.jpg" />
</p>

<p align="center">
  <img src="https://i.imgur.com/eZ47tdK.jpg" />
</p>

----
### Day 4 - Pre-layout timing analysis and importance of good clock tree
----


In this section, a post layout of the clock is made and the importance of correcting it is learned.

#### Timing modelling using delay tables

Before going into details about the timing on the circuit, it is important to know the information about the Tracks and pitchs that the standard cell of skywater 130 provides us.

We will be able to consult that information in the next path.

`$/home/juan.andres.lopez491/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd/tracks.info`

<p align="center">
  <img src="https://i.imgur.com/scMkMSu.jpg" />
</p>

Additionally, we could change the size of the grid to leave it depending on the Tracks.

For skywater130, Let's go type the next command in magic.

`$grid 0.46u, 0.34um 0.23um 0.17um`

<p align="center">
  <img src="https://i.imgur.com/86UryTD.jpg" />
</p>

Now we are going to introduce our standard cell to the picorv32a design folder to then be able to generate the entire implementation using this standard cell.

For this, the LEF file of the magic layout must first be generated.

`$lef write`

<p align="center">
  <img src="https://i.imgur.com/LAkx5F8.jpg" />
</p>

Before generating the floorplan, the libraries used in the standard cell must be copied to the src folder.

<p align="center">
  <img src="https://i.imgur.com/En0jSvw.jpg" />
</p>

we also need to modify the config file.tcl

<p align="center">
  <img src="https://i.imgur.com/u2J2R5G.jpg" />
</p>

Now we open openlane again and let's go prepare our project, and type the next commands

`$./flow.tcl 'interactive`

`$package require openlane 0.9`

`$prep 'design picorv32a -tag 03-18_18-44 -overwrite`

`$set lefs [glob $::env(DESIGN_DIR)/src/*.lef]`

`$add_lefs -src $lefs`

We run the synthesis and floorplan

<p align="center">
  <img src="https://i.imgur.com/61zsd7R.jpg" />
</p>

And we open with magic our design

`magic -T /home/juan.andres.lopez491/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def `

<p align="center">
  <img src="https://i.imgur.com/3TqCTCN.jpg" />
</p>

And if we get closer, we can see our standard cell

<p align="center">
  <img src="https://i.imgur.com/SKe6r18.jpg" />
</p>

#### Timing analysis with ideal clocks using openSTA

In order to generate the timing reports, we need to create two files, the pre_staf.inf my_basic.sdc

In the next image you will can see the file pre_staf.inf

<p align="center">
  <img src="https://i.imgur.com/yW34T2o.jpg" />
</p>

In the next image you will can see the file my_basic.sdc

<p align="center">
  <img src="https://i.imgur.com/pH4zJy4.jpg" />
</p>

se ejecuta el codigo

<p align="center">
  <img src="https://i.imgur.com/HNHRduL.jpg" />
</p>

we try again to correct our slack, for that we run the following code, then we run the synthesis and generate the report with STA.

`set ::env(SYNTH_MAX_FANOUT) 4`

`run_synthesis`

`se ejecuta el sta pre_sta.conf`

<p align="center">
  <img src="https://i.imgur.com/HNHRduL.jpg" />
</p>

en este punto se deben hacer ajustes en el timing ECO con el fin de disminuir el slack, sin embargo, a mi no me funcionó, al finalizar este paso se corre el flloplan y cts.

#### Clock tree synthesis TritonCTS and signal integrity

here the arbon clock with triton CTS is used and in turn the signal integrity, Let'go run the cts.

<p align="center">
  <img src="https://i.imgur.com/dWqnZgU.jpg" />
</p>

Here it gave us error run_floorplan, that's why we must execute it in a different way

`init_floorplan`

`place_io`

`global_placemenet_or`

`detailed_placement`

`tap_decap_or`

`detailed_placement`

`gen_pdn`

To be able to run OpenSTA, we need to make the following configs in openlane.

`echo $::env(LIB_SYNTH_COMPLETE)`

`echo $::env(LIB_TYPICAL)`

`echo $::env(CURRENT_DEF)`

`echo $::env(SYNTH_MAX_TRAN)`

`echo $::env(CTS_MAX_CAP)`

`echo $::env(CTS_CLK_BUFFER_LIST)`

`echo $::env(CTS_ROOT_BUFFER)`

#### Timing analysis with real clocks using openSTA

In order to generate the new analysis with the real clock, we will enter Opentoad.

`openroad`

`read_lef /openLANE_flow/designs/picorv32a/runs/03-18_18-44/tmp/merged.lef`

`read_def /openLANE_flow/designs/picorv32a/runs/03-18_18-44/results/cts/picorv32a.cts.def`

`write_db pico_cts.db`

This will generate the file in openlane

<p align="center">
  <img src="https://i.imgur.com/fKxgHLm.jpg" />
</p>

`read_db pico_cts.db`

`read_verilog /openLANE_flow/designs/picorv32a/runs/03-18_18-44/results/synthesis/picorv32a.synthesis_cts.v`

`read_liberty -max $::env(LIB_SLOWEST)`

`read_liberty -min $::env(LIB_FASTEST)`

`read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc`

`set_propagated_clock [all_clocks]`

`report_checks -path_delay min_max -format full_clock_expanded -digits 4 `

Here let's go generate our report

<p align="center">
  <img src="https://i.imgur.com/vlYHnMW.jpg" />
</p>

Now we are going to run the following commands to fix the timing, which incorporates the buffer configuration, We need to go to openroad again.

`exit`

`openroad`

`read_db pico_cts.db`

`read_verilog /openLANE_flow/designs/picorv32a/runs/03-18_18-44/results/synthesis/picorv32a.synthesis_cts.v`

`read_liberty -max $::env(LIB_SYNTH_COMPLETE)`

`link_design picorv32a`

`read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc``

`set_propagated_clock [all_clocks]`

`exit`

We check the buffers again, replace and define the routes again

`echo $::env(CTS_CLK_BUFFER_LIST)`

`lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0`

`set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]`

`echo $::env(CTS_CLK_BUFFER_LIST)`

To see the effect of the timing correction, the old values are noted separately.

<p align="center">
  <img src="https://i.imgur.com/hIfHDLv.jpg" />
</p>

We let's go to run the next command `run_cts` but we will have a error.

<p align="center">
  <img src="https://i.imgur.com/1p3olPk.jpg" />
</p>

We run the following commands to redefine the path, and we try again.

`$echo $::env(CURRENT_DEF)`

`$set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/03-18_18-44/results/placement/picorv32a.placement.def`

`$echo $::env(CURRENT_DEF)`

`$echo $::env(CTS_CLK_BUFFER_LIST)`

`$run__cts`

Now we see that it runs without problem

<p align="center">
  <img src="https://i.imgur.com/AjPjIpD.jpg" />
</p>

We return to openroad to generate the final report of this section.

openroad


`read_lef /openLANE_flow/designs/picorv32a/runs/03-18_18-44/tmp/merged.lef`

`read_def /openLANE_flow/designs/picorv32a/runs/03-18_18-44/results/cts/picorv32a.cts.def`

`write_db pico.ctsl.db`

`read_db pico.ctsl.db`

`read_verilog /openLANE_flow/designs/picorv32a/runs/03-18_18-44/results/synthesis/picorv32a.synthesis_cts.v`

`read_liberty $::env(LIB_SYNTH_COMPLETE)`

`link_design picorv32a`

`read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc`

`set_propagated_clock [all_clocks]`

`report_checks -path_delay min_max -format full_clock_expanded -digits 4`

When the report is generated, we will see that the slack time was corrected.

<p align="center">
  <img src="https://i.imgur.com/QVtS43U.jpg" />
</p>

Now we can generate the two reports of the clock skew

`report_clock_skew -hold`

<p align="center">
  <img src="https://i.imgur.com/5U7ary9.jpg" />
</p>

`report_clock_skew -setup`

<p align="center">
  <img src="https://i.imgur.com/jbRNaqB.jpg" />
</p>

we exit and re-enable the buffer that was previously disabled and we are ready for the final part of the course.

`echo $::env(CTS_CLK_BUFFER_LIST)`

`set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1`


----
## Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA
----

This section corresponds to the final part of the course, in which we finish learning very important things such as the DRC rules and how they are taken into account by the routing algorithm, it is noteworthy that the DRC rules are caused by lithography in manufacturing.

3 typical DRC rules are known:

- Wire width : 
This rule tells us the minimum or maximum thickness of the mask.

<p align="center">
  <img src="https://i.imgur.com/SYfXjCb.jpg" />
</p>

- Wire spacing
This rule tells us the minimum or maximum separation of two masks

<p align="center">
  <img src="https://i.imgur.com/PskfVll.jpg" />
</p>

- Wite pitch
This rule tells us the minimum distance between the center of the metals, it is commonly used to separate tracks.

<p align="center">
  <img src="https://i.imgur.com/DticMdZ.jpg" />
</p>

On the vias there are also two drc rules

- Via wire:
This rule indicates the width of the track of the via

<p align="center">
  <img src="https://i.imgur.com/5yWL0E5.jpg" />
</p>

- Via spacing:
This rule indicates the space there may be between vias

<p align="center">
  <img src="https://i.imgur.com/wWo4f9y.jpg" />
</p>

For the routing, an intelligent algorithm is used that generates a grid and on each block generates a numerical pattern that expands to the other block, and once it has arrived evaluates the best way to get.

<p align="center">
  <img src="https://i.imgur.com/ltkthZv.jpg" />
</p>

Para rutear se cuenta con principalmente dos modos, fast route which executes a routing globally, and detaile route it is as the name implies, a routing that is done in greater depth, for which the iterates to reduce the drc errors by a smaller amount, it may take too long.

to be able to energize the devices that are inside the chip, as mentioned in the activities of previous days, they must be taken from different vdd and gnd lines, otherwise there are drops or increases in gnd and vdd, for this a vdd and gnd grid with routing is generated.

<p align="center">
  <img src="https://i.imgur.com/qDIHVu0.jpg" />
</p>

Now let's start the routing, for this we write the following commands.

`echo $::env(CURRENT_DEF)`

`gen_pdn`

Now we are going to start the routing, for this we write the following commands, which will define the rules for the power management.

<p align="center">
  <img src="https://i.imgur.com/61zsd7R.jpg" />
</p>

Now we need to run these two to start routing

`echo $::env(CURRENT_DEF)`

`run_routing`

however, We have a error

<p align="center">
  <img src="https://i.imgur.com/k7OX14L.jpg" />
</p>

For fix it, I have wrote the next command

`set ::env(GLB_RT_ADJUSTMENT) 0`
`run_routing`

There I had many DRC errors, so I ran a synthesis explorer to know the best configuration of the tcl.

`flow.tcl -design picorv32a 'synth_explore`

<p align="center">
  <img src="https://i.imgur.com/GndWinO.jpg" />
</p>

<p align="center">
  <img src="https://i.imgur.com/h3g1yns.jpg" />
</p>

We configure the config.tcl 

`set ::env(SYNTH_STRATEGY) "AREA 2"`

And we run the commands for routing again

`run_routing`

Here we can see iteration 52, where it removed all the DRC errors.

<p align="center">
  <img src="https://i.imgur.com/YEVCwXX.jpg" />
</p>

And here we can already see that the routing ended without a problem

<p align="center">
  <img src="https://i.imgur.com/hGtu2IT.jpg" />
</p>

In the next path, you can see the file .spef

<p align="center">
  <img src="https://i.imgur.com/gOGlJvy.jpg" />
</p>

<p align="center">
  <img src="https://i.imgur.com/kMrKaCg.jpg" />
</p>

Now we go back to openlane and run the following command to generate the GDS file and the MAG

`run_magic`

<p align="center">
  <img src="https://i.imgur.com/ACWdCrp.jpg" />
</p>

In the next path, you can see the file .gds and .mag

<p align="center">
  <img src="https://i.imgur.com/qm1F31Q.jpg" />
</p>

Now we open to be able to the routing, and we can see that it was a success

<p align="center">
  <img src="https://i.imgur.com/Zxy2Rwg.jpg" />
</p>

<p align="center">
  <img src="https://i.imgur.com/X3QU5O8.jpg" />
</p>


Finally we can see the photograph taken by the run_magic command, where we see our finished chip.

<p align="center">
  <img src="https://i.imgur.com/wGcrLPp.png" />
</p>



------------
#REFERENCE

-  All images were added to imgr: https://imgur.com/
- https://github.com/nickson-jose/vsdstdcelldesign
- Worshop VSD-IAT
------------

