## Pre-layout Timing Analysis and Importance of Good Clock Tree

## 1 Introduction to Delay tables



<img width="782" height="452" alt="Screenshot 2025-11-15 201554" src="https://github.com/user-attachments/assets/b387faa0-3ca0-4e0c-bf17-eab0dd7cff56" />

Observations
- 2 levels of buffering
- At every level, each node driving same load
- Idential buffer at same level

<img width="588" height="523" alt="Screenshot 2025-11-15 202805" src="https://github.com/user-attachments/assets/d0dcd334-2d76-4c76-b951-a678bd0a02a2" />

Let us assume C1=C2=C3=C4=25fF
How about creating a buffer tree at node 'A'
Let us assume Cbuf1=Cbuf2=30fF
Therefore, total cap at node 'A' => 60fF
Therefore, total cap at node 'B' => 50fF
Therefore, total cap at node 'C' => 50fF

## Delay Table for Cbuf '1' & Cbuf '2'

<img width="1901" height="520" alt="Screenshot 2025-11-15 203439" src="https://github.com/user-attachments/assets/3ce7f773-cf51-4cda-87e8-8c8321466c8b" />

## 2 Timing Analysis with Ideal Clock using OpenSTA
- Timing Analysis (with Ideal Clock)

<img width="1613" height="931" alt="Screenshot 2025-11-15 204947" src="https://github.com/user-attachments/assets/e1d74def-a830-4e3a-b79c-d12c2272a7f2" />

Specifications
```
Clock frequency (F) = 1GHz
Clock period (T) = 1/F
                 = 1/1 GHz
                 = 1ns
```
Hence finite time 'S' required (before clk edge) for 'D' to reach Qm ie internal delay of Mux1 = setup time.

<img width="1605" height="609" alt="Screenshot 2025-11-15 205247" src="https://github.com/user-attachments/assets/da0949da-4552-46ec-90dc-a45e77bd8d6c" />

## 3 Introduction to Clock Jitter and Uncertainity

In digital circuits, especially synchronous systems, the clock signal plays a critical role in coordinating data movement between registers. Ideally, the clock edges should arrive at precisely predictable times. However, real hardware introduces variations that affect the timing of these edges. Two important concepts associated with these variations are clock jitter and clock uncertainty.

Clock Jitter
Clock jitter refers to the short-term, random or systematic variation in the arrival time of clock edges compared to their ideal positions.
These variations can be caused by:
- Power supply noise
- Temperature fluctuations
- Electromagnetic interference
- Imperfect clock generation circuits (PLLs, oscillators)
Jitter effectively reduces the time available for signal propagation, which may lead to timing violations if not accounted for during design.

<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/ace047ae-2e55-484d-9348-92ebbd0578c6" />

Clock Uncertainty
Clock uncertainty represents the overall margin added to the timing analysis to account for all kinds of unknown variations in the clock signal, including jitter, skew, and other unpredictable delays.
It is an intentional design margin used by EDA tools to ensure that the circuit remains functional under worst-case conditions.

Why jitter and uncertainty are critical:
- Static Timing Analysis (A)
- Defining safe setup and hold timing margins
- Ensuring reliable operation of high-speed digital systems
- Avoiding timing violations due to unpredictable clock behavior

## 4 Clock Tree Routing and Buffering using H-tree Algorithm

The H-tree clock routing method reduces clock skew by creating a perfectly balanced routing structure where every flop receives the clock through paths of equal length. The process begins by collecting all flip-flops driven by the given clock and calculating the geometric midpoint of their positions. The clock source is then routed from its port to this midpoint. Next, the layout is split into two symmetric halves, and the routing extends from the midpoint to the midpoint of each half. Each half is again subdivided, and new connections are drawn to the centers of these smaller regions, forming H-shaped routing segments at every level. This recursive partitioning and routing continues until the clock reaches the exact clock pin of every flop, ensuring uniform wire lengths and minimal skew across the entire design.

<img width="695" height="690" alt="image" src="https://github.com/user-attachments/assets/711db3e2-b30e-4c43-9762-5cc81b34f2de" />

Clock Buffering - is the process of inserting dedicated buffer cells into the clock distribution network to ensure that the clock signal reaches all sequential elements (like flip-flops) with sufficient strength, minimal delay, and balanced arrival times. As a clock signal travels across a chip, the load increases due to long interconnects and large numbers of clocked elements. This loading can degrade signal quality, slow down transitions, and introduce clock skew. To prevent this, clock buffers—special low-skew, high-drive cells—are strategically inserted in the clock tree to amplify the signal and divide the load. By organizing these buffers hierarchically, the clock tree maintains uniform propagation delay, reduces insertion delay, stabilizes edge transition times, and ensures synchronous operation across the entire design.

## 5 Clock Signal Integrity: Crosstalk and Clock Net Shielding

Clock Crosstalk - refers to unwanted interference induced on the clock net due to capacitive or inductive coupling with neighboring switching signals (aggressor nets). Since the clock is a high-frequency, always-active signal with strict timing requirements, even small disturbances can cause significant timing violations.

Clock Net Shielding - is a physical-design technique that protects the clock from crosstalk by routing shield wires (usually VDD or VSS) parallel to the clock trace. These shields act as electrostatic and electromagnetic barriers, reducing the amount of noise coupled from aggressor nets.

## 6 Introduction to  Maze Routing - Lee's Algorithm Routing and Design Rule Check (DRC)

Lee’s algorithm is a grid-based, breadth-first search (BFS) routing method used to find a path between two points (source and target) while avoiding obstacles. It guarantees finding the shortest path (if one exists), making it a classic routing algorithm in PCB and IC physical design.

<img width="474" height="269" alt="image" src="https://github.com/user-attachments/assets/2f297229-0852-4bd2-bbee-500fa56ddc78" />

| Concept  | Maze Routing (Lee’s)              | DRC                                  |
| -------- | --------------------------------- | ------------------------------------ |
| Purpose  | Find shortest routing path        | Ensure physical design rules are met |
| Method   | BFS wave + backtrack              | Geometric rule checking              |
| Outcome  | A valid routed path               | Pass/Fail for layout validity        |
| Relation | Router avoids DRC-violating cells | Defines obstacles for router         |

## Routing and Design Rule Check (DRC)

![Web_Photo_Editor](https://github.com/user-attachments/assets/74bb4d84-aaba-49ff-935d-a61aee14e9e1)

![Web_Photo_Editor (1)](https://github.com/user-attachments/assets/81e9d4b6-9d01-4536-923e-d036c6428669)

DRC Check

![Web_Photo_Editor (2)](https://github.com/user-attachments/assets/578b3d09-3654-4549-afd9-aa7ec491eaba)

## LAB-04 Convert grid info to track info 

### Port Configuration

1.Define Ports: Create boxes on the relevant layers and add labels with the layer names for A, Y, VPWR, and VGND.

2. Set Port Attributes:
    - For A and Y, set CLASS to input and USE to signal.
    - For VPWR and VGND, set CLASS to inout and USE to power.
      
3. Layout Requirements:
    - Ensure input/output ports are located at the intersection of vertical and horizontal tracks.
    - Verify the width of the standard cell is an odd multiple of the track pitch.
    - Verify the height of the standard cell is a multiple of the track vertical pitch.


LEF File Generation

1. Track Information: Refer to the track information in pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd/tracks.info for the routing stage.
2. Generate LEF File: Use the lef write command in the console window to generate the LEF file.

The LEF file will contain essential information for Place-and-Route (PnR), including:

- PnR boundary of the standard cell
- Power and ground rails
- Input and output ports

Extract the '.lef' file from the '.mag' file.

```
#open the layout
magic -T sky130A.tech sky130_inv.mag

#Open the track info
cd pdks/sky130A/livs.tech/openlane
less track.info
```

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/86cd5daf-6554-49a6-945e-0dbabd926bd0" />
<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/767b5a5a-386e-4503-a065-d5cb497e1b12" />

```
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

Tracks are essentially predefined paths on metal layers (like metal 1, metal 2) used during the routing stage to guide automated Place-and-Route (PNR) tools. To visualize the grid, press 'g' in the layout environment.

Commands for tkcon window to set grid as tracks of locali layer
```
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```
<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/e77ff10a-c9ef-48f1-8795-a2a1602f6621" />

- Place input/output ports at grid intersections to align with routing tracks.
- Ensure the cell width is an odd multiple of the horizontal track spacing.
- Ensure the cell height is an odd multiple of the vertical track spacing.

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/335f5062-d314-4d2f-8929-bb83ea0db490" />

## LAB-4.1 Convert magic layout to standard cell LEF

- Assign port names and values:
    - Input/Output ports: set CLASS and USE attributes accordingly
    - Power and Ground ports (VPWR, VGND):
        - Set CLASS to inout and USE to power
        - Attach to Metal1 layer

<img width="835" height="572" alt="Screenshot 2025-11-18 195719" src="https://github.com/user-attachments/assets/eb81e311-cffa-416a-992e-313f68e2dc90" />

set ports class and port use attributes

```
#in tckon
what
port class output
port use signal
```
<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/53b0d8a3-dd6a-49c6-b849-c82a90cff99b" />

Extract the lef file

```
#in tkcon
save sky130_vsdinv.mag

#in the directory vsdcellstddesign
magic -T sky130A.tech sky130_vsdinv.mag

#in tckon
lef write

#open the lef file
less
```

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/bdf9fe4f-89bf-4115-9d4a-f4d40d5eb8b0" />

<img width="1010" height="768" alt="Screenshot 2025-11-18 200235" src="https://github.com/user-attachments/assets/f8fbb560-a811-40d7-8e2a-00d280461f95" />

Execute the following commands in openlane directory

```
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]      
add_lefs -src $lefs
run_synthesis
```

<img width="1280" height="768" alt="image" src="https://github.com/user-attachments/assets/1ce78aae-a85e-453f-a68a-9263c81853bc" />

<img width="1774" height="240" alt="image" src="https://github.com/user-attachments/assets/91a835c3-2084-4bf8-b7fe-42e7997f00fe" />

To verify if your custom cell is placed in the design, navigate to the placement directory and use the following command:
```
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
This will launch the OpenDB viewer, which allows you to visualize the placement of your design, including your custom cell.

<img width="987" height="788" alt="Screenshot 2025-11-18 220723" src="https://github.com/user-attachments/assets/7663abb3-0cc0-4681-9e81-691747a5d9f6" />

Command for tkcon window to view internal layers of cell
```
#Command to view internal connectivity layers
expand
```

<img width="695" height="523" alt="Screenshot 2025-11-18 230344" src="https://github.com/user-attachments/assets/6098fba3-319a-406e-8e20-132e2d3b80e9" />

## LAB-4.2 Configure OpenSTA for Post-synth timing analysis

- The PnR process can lead to changes in timing violations, including new ones, improved ones, and worsened ones.
- Usually, a dedicated timing tool (like PrimeTime) is run separately from the automated flow for timing analysis and ECO generation.
- In OpenLANE, OpenSTA is employed for analyzing timing after synthesis.

Commands to invoke the OpenLANE flow include new lef and to perform synthesis:

```
#Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a

#Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

#Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

run_synthesis
```

OpenSTA config file: pre_sta.conf:
```
set_cmd_units -time ns -capacitance fF -current uA -voltage V -resistance kOhm -distance um

read_liberty -max ./designs/picorv32a/src/sky130_fd_sc_hd__slow.lib
read_liberty -min ./designs/picorv32a/src/sky130_fd_sc_hd__fast.lib

#read_verilog ./designs/picorv32a/src/picorv32a.v
read_verilog ./designs/picorv32a/runs/latest_21-03/results/synthesis/picorv32a.synthesis.v

link_design picorv32a
read_sdc ./designs/picorv32a/src/my_base.sdc

check_setup -verbose

report_checks -path_delay min_max -fields {nets cap slew trans input_pins}
report_tns
report_wns
```

## LAB-4.3 Optimize Synthesis to reduce setup violations

```
# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a -tag 17-11_17-33 -overwrite

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to set new value for SYNTH_MAX_FANOUT
set ::env(SYNTH_MAX_FANOUT) 4

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

run_synthesis
```

## LAB-4.4 Steps to do basic Timing ECO

- Analyzing setup violations in OpenSTA helps identify reasons for timing issues.
- Common reasons include large output slew due to high capacitance load or fanout that the synthesis tool couldn't optimize.

Fixing Timing Violations

1. Upsizing Cells: Replace a cell instance with a higher drive strength version to reduce delay.
    - Use the replace_cell command: replace_cell instance lib_cell
    - Example: replace_cell _44195_ sky130_fd_sc_hd__inv_4
      
2. Verify Fix: Check if the violation is resolved using report_checks
    - Example: report_checks -from <instance or pin> -to <instance or pin> -through _44195_ -path_delay min_max

Updating the Netlist- After fixing timing violations, update the netlist file using write_verilog
    - Example: write_verilog $OPENLANE_HOME/designs/picorv32a/runs/latest_21-03/results/synthesis/picorv32a.synthesis.v

Iterative Timing Fixing Process- Fixing timing violations is an iterative process involving STA engineers and PnR engineers.
- STA engineers modify the design (e.g., upsize cells, replace cells, insert buffers) and provide ECOs to PnR engineers.
- PnR engineers update the design, perform post-route timing analysis, and provide feedback to STA engineers.
- This process repeats until all timing violations are resolved.

## LAB-4.5 Steps to run CTS using TritonCTS

- Replace previous design with improved design using write_verilog command.
- Specify path of previous design to overwrite with improved version.
- Floorplan: Use same commands as before to start floorplanning
- Placement: Run placement using run_placement command
- CTS (Clock Tree Synthesis): Perform CTS using run_cts command
-  After CTS completion, a new .cts file is added to synthesis results directory
- This file contains:
    - Previous netlist
    - Clock buffers added during CTS stage

<img width="977" height="152" alt="Screenshot 2025-11-18 232531" src="https://github.com/user-attachments/assets/809c5846-a0af-4bb2-af52-2277140417df" />

## LAB-4.6 Steps to analyze timing with real clocks using OpenSTA

```
1. Enter OpenROAD- Enter OpenROAD using the command: openroad

2. Load Design Data- Load LEF (Library Exchange Format) file: read_lef /openLANE_flow/designs/picorv32a/runs/04-05_21-50/tmp/merged.lef
- Load DEF (Design Exchange Format) file: read_def /openLANE_flow/designs/picorv32a/runs/04-05_21-50/results/cts/picorv32a.cts.def

3. Save Database- Save the database: write_db pico_cts.db

4. Load Database- Load the saved database: read_db pico_cts.db

5. Load Design Files- Load Verilog file: read_verilog /openLANE_flow/designs/picorv32a/runs/04-05_21-50/results/synthesis/picorv32a.synthesis_cts.v
 Load Liberty file: read_liberty $::env(LIB_SYNTH_COMPLETE)
 Load SDC (Synopsys Design Constraints) file: read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

6. Set Propagated Clock- Set propagated clock: set_propagated_clock [all_clocks]

7. Report Timing- Report timing: report_checks -path_delay min_max -format full_clock_expanded -digits 4
```

<img width="957" height="338" alt="Screenshot 2025-11-18 233132" src="https://github.com/user-attachments/assets/8053d98a-bd6d-4624-91e7-dfb77fd2438b" />

## LAB-4.7 Steps to execute OpenSTA with right timing libraries and CTS assignment

Remove Cell from CTS Buffer List
```
Remove sky130_fd_sc_hd__clkbuf_1 from CTS_CLK_BUFFER_LIST:

tcl
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]
```

Check Environment Variables
```
Check current value of CTS_CLK_BUFFER_LIST: echo $::env(CTS_CLK_BUFFER_LIST)
Check current value of CURRENT_DEF: echo $::env(CURRENT_DEF)
```

Set Placement DEF
```
Set CURRENT_DEF to placement DEF:
tcl
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/04-05_21-50/results/placement/picorv32a.placement.def
```

Run CTS
```
Run CTS: run_cts
```
Verify Changes
```
Check updated CTS_CLK_BUFFER_LIST: echo $::env(CTS_CLK_BUFFER_LIST)
```

## LAB-4.8 Observing Impact of Bigger CTS Buffers on Setup and Hold Timing

Load Design Data
```
Load LEF file: read_lef /openLANE_flow/designs/picorv32a/runs/04-05_21-50/tmp/merged.lef
Load DEF file: read_def /openLANE_flow/designs/picorv32a/runs/04-05_21-50/results/cts/picorv32a.cts.def
```

Save and Load Database
```
Save database: write_db pico_cts1.db
Load database: read_db pico_cts1.db
```

Load Design Files
```
Load Verilog file: read_verilog /openLANE_flow/designs/picorv32a/runs/04-05_21-50/results/synthesis/picorv32a.synthesis_cts.v
Load Liberty file: read_liberty $::env(LIB_SYNTH_COMPLETE)
Link design: link_design picorv32a
Load SDC file: read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
```

Analyze Timing
```
 Set propagated clock: set_propagated_clock [all_clocks]
 Report timing: report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
 Report clock skew:
     Hold: report_clock_skew -hold
     Setup: report_clock_skew -setup
```




