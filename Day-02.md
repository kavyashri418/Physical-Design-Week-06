# Good Floorplan vs Bad Floorplan and Introduction to Library Cells

## 1 Chip Floor Planning Considerations

Utilization Factor and Aspect Ratio
In order to find out the Utilization Factor and Aspect Ratio, first we need to know how to define height and width of core and die areas.
- Core is an area in a chip which is used to place all the logic cells and components in a chip. It is the place where logic lies in a chip.
- Die is an area that encircles the core area and used for placing I/O related components.

a) Define Width and Height of Core and Die
Lets begin with a netlist The height and width of core area will be decided by the netlist of the design. It will be based on the no.of components required in order to execute the logic and the height and width of the die area will be dependent on the core area height and width.

<img width="1665" height="541" alt="Screenshot 2025-10-29 104048" src="https://github.com/user-attachments/assets/a33cea8b-a8ae-46aa-8e93-ee38483e8deb" />

```
FF = Flip Flop/Latches/Registers
A1, Q1 = standard cells (AND, OR, Inverter)
```
Consider, a netlist with 2 flops and 2 gates, with above shown connections.
Note: a netlist describes the connectivity of an electronic design.
Now, lets convert the highlighted symbols into physical dimension.

<img width="1128" height="637" alt="Screenshot 2025-10-29 105155" src="https://github.com/user-attachments/assets/db5cf65c-43ca-43c3-8058-b62848e9625b" />

<img width="691" height="570" alt="Screenshot 2025-10-29 105216" src="https://github.com/user-attachments/assets/b5442f36-a7a4-4038-9457-b3fb2a865c22" />

What is 'core' and 'die' section of a chip?
A die, which consists of core, is small semiconductor material specimen on which the fundamental circuit is fabricated.

<img width="2681" height="926" alt="Screenshot 2025-10-29 112626" src="https://github.com/user-attachments/assets/497cd409-f63a-46bb-841d-082fd4928438" />

How to arrive on its dimensions?
Place all logical cells inside the core. The logical cells occupies the complete area of the core

100% Utilization is given by the formula
```
Utilization Factor = (Area occupied by the netlist)/(Total area of the core)
```
<img width="2411" height="1142" alt="Screenshot 2025-10-29 113119" src="https://github.com/user-attachments/assets/f1204fc7-966f-44cd-a813-76916b987807" />

b) Define Locations of Preplaced Cells
- Lets consider block 1 and block 2
- Extend IO pins
- Black box the boxes
- Seperate the black boxes as two different IP's or modules

<img width="3186" height="1632" alt="Screenshot 2025-10-29 115756" src="https://github.com/user-attachments/assets/5b63b50e-f746-4328-ba25-13aa6b32936d" />

<img width="1665" height="1994" alt="Screenshot 2025-10-29 120858" src="https://github.com/user-attachments/assets/fe7f6bb9-7867-4470-8c2b-39756d76df19" />

Similarly there are other IP's also available for eg
- The arrangements of these IP's in a chip is referred as floorplanning.
- These IP's/blocks have user-defined locations, and hence are placed in chip before automated placement , routing and are called as pre-placed cells.
- Automated placement and routing tools places in the remaining logical cells in the design onto chip.

<img width="2223" height="626" alt="Screenshot 2025-10-29 121912" src="https://github.com/user-attachments/assets/e3abdf47-8b3e-46f0-a2a1-b3acf3b503b4" />

c) De-coupling Capacitors
Surround pre-placed cells with decoupling capacitor
Decouples the circuit from the VDD rail
Reduce Zpdn for the required frequencies of operation
Serve as a charge reservoir for the switching current demands that the VDD rail cannot satisfy.
Surround pre-placed cells with Decaps to compensate for the switching current demands (di/dt)

<img width="2886" height="1937" alt="Screenshot 2025-10-29 122845" src="https://github.com/user-attachments/assets/83a6faa8-c4ab-4fa2-b1c0-29f0f41e2dc2" />

Consider the amount of the switching current required for a complex circuit something like below,
- Consider capacitance to be zero for the discussion Rdd, Rss, Ldd and Lss are well defined values.
- During switching operation, the circuit demands switching current ie peak current (Ipeak).
- Now, due to the presence of Rdd and Ldd, there will be a voltage drop across them and voltage at node 'a' would be 'vdd' instead of vdd.
- If 'vdd' goes below the noise margin, due to Rdd and Ldd, the logic 1 at the output of the circuit wont be detected as logic '1' at the input of the circuit following this circuit.

<img width="2629" height="1727" alt="Screenshot 2025-10-29 131503" src="https://github.com/user-attachments/assets/7c344b74-d5a5-4db0-88b3-882622442c06" />

Noise Margin Summary
Noise induced bump characteristics at different noise margin levels.
For any signal to be considered as logic '0' and logic '1' it should be in the NML and NMH ranges respectively.

<img width="2815" height="1286" alt="Screenshot 2025-10-29 131617" src="https://github.com/user-attachments/assets/06332c47-9dba-4ef9-b655-4a3ea1a571f4" />

d) Power Planning

In the previous section we used De-cap cells to manage power for different blocks.But Decap cells have some limitations such as Leakage power and increase in the area of chip. To overcome these we use a technique called Powerplanning. In some areas of the chip when there is more switching happening, two tyoes of phenomena can occur.

- L*di/dt
   Discharging : Ground bounce
   Charging : Voltage Droop
- Solution: Reduce the Vdd/ Vss parasitics ->
   Power grid
   Multiple VDD, VSS pins/ balls


<img width="2438" height="1841" alt="Screenshot 2025-10-29 135515" src="https://github.com/user-attachments/assets/ac557b31-d2a5-4a36-9e85-f11b3c430732" />

We have taken care of local communication now we consider below scenario

<img width="2551" height="1793" alt="Screenshot 2025-10-29 135554" src="https://github.com/user-attachments/assets/3432efb7-8c00-4d0b-ba5f-2e7e6bd2184b" />

Now let the output of 16-bit bus, is connected to an inverter.

<img width="1081" height="892" alt="Screenshot 2025-10-29 135628" src="https://github.com/user-attachments/assets/2b88910e-87f3-453e-ab64-6c9cb74af015" />

What does this mean?

This means all capacitors which were charged to 'v' volts will have to discharge to '0' volts through single 'gnd' tap point. This will cause a bump in 'gnd' tap point.

- Voltage drop - When a group of cells are simultaneously switching from 0 to 1, then every cell needs the power and In case the power is supplying from one source, there may occur the shotage of power and drop in the input voltage happens at that place. This is called as "Voltage Drop". The problem occurs only when the voltage level goes below the noise margin.
  
- Ground Bounce : When a group of cells are simultaneoisly switching from 1 to 0, then every cell dumps the power to th ground simultaneously to the same ground pin. In this case the ground instead of being at 0 experiences a short rise in the voltage and this is called as "Ground Bounce".The problem occurs only when the voltage level goes above the noise margin.

<img width="2713" height="581" alt="Screenshot 2025-10-29 135617" src="https://github.com/user-attachments/assets/f2071146-66e7-48a6-b160-bd21990831ce" />

Also, all capacitors which were '0' volts will have to charge to 'v' volts through single 'vdd' tap point. This will cause lowering of voltage at 'vdd' tap point.

<img width="2510" height="1994" alt="Screenshot 2025-10-29 135744" src="https://github.com/user-attachments/assets/18e64f07-ee2d-46aa-b54a-bfb2c1d2d457" />

e) Pin Placement and Logical Cell Placement Blockage

- Lets take below design for eg that needs to be implemented
- Usually: East -> West, North -> South, {East, North} -> {West, South}
- Pin ordering is random (unless we specify explicitly ?)
- Front-End to Back-End team communication/ handshaking needed for optimal pin placement
- CLK ports/ pins are usually bigger to reduce the clk net resistance

<img width="2168" height="1977" alt="Screenshot 2025-10-29 141126" src="https://github.com/user-attachments/assets/3d6f4a2d-e73d-45b6-a3ea-379e30083fc5" />

The connectivity information between the gates is coded using verilog language and is called as the netlist.
Now Floorplan is ready for PnR
<img width="2574" height="1807" alt="Screenshot 2025-10-29 142201" src="https://github.com/user-attachments/assets/abecaf25-5f41-4c1f-8c4b-857eaa85f53d" />

## 2 Library Binding and Placement

i) Netlist binding and initial place design
- Bind netlist with physical cells

<img width="3662" height="967" alt="Screenshot 2025-10-29 143501" src="https://github.com/user-attachments/assets/a085861d-62cf-4f61-87c9-38a9cca1349d" />

- Placement
- 
Placement is a key stage in the VLSI physical design flow where all standard cells, macros, and IP blocks are assigned physical locations on the chip layout after floorplanning and before routing. The goal of placement is to arrange these components optimally so that timing, power, area, and routability constraints are satisfied while minimizing overall wire-length
  
<img width="3812" height="1804" alt="Screenshot 2025-10-29 144826" src="https://github.com/user-attachments/assets/079dd8aa-3cf1-46a4-86a2-56766cf4f783" />
  
- Optimize Placement
  
During physical design, placement optimization involves arranging standard cells on the chip so that timing, power, and routing resources are efficiently utilized. A key part of this optimization is estimating wire-length and interconnect capacitance before actual routing. These early estimates guide placement decisions to minimize delay and congestion
This is the stage where we estimate wire length and capacitance and based, on that insert repeaters.
  
Stage 1

<img width="3807" height="1831" alt="Screenshot 2025-10-29 145936" src="https://github.com/user-attachments/assets/ccd9d4cf-a975-4477-9192-5e754933b1f6" />

Stage 2

<img width="3808" height="1794" alt="Screenshot 2025-10-29 150141" src="https://github.com/user-attachments/assets/d0dafe45-d969-469a-8a8b-849100afe664" />

Stage 3

<img width="3801" height="1830" alt="Screenshot 2025-10-29 150758" src="https://github.com/user-attachments/assets/9aa53b61-3d5d-4b83-82b6-a60376395c33" />

Stage 4

<img width="3796" height="1844" alt="Screenshot 2025-10-29 151130" src="https://github.com/user-attachments/assets/258b832f-6f14-408a-b53c-ef6e544f8b3a" />

Need for Libraries and Characterization
Library Characterization and Modelling
PART-1 Concepts and theory = NLDM, CCS timing, Power and Noise Characterization.

```
Logic Synthesis --> Floorplanning --> Placement --> Clock Tree Synthesis (CTS) --> Routing --> Signoff STA
```
## 3 Cell Design and Characterization Flow

Inputs for Cell Design Flow

<img width="3338" height="1783" alt="Screenshot 2025-10-29 174725" src="https://github.com/user-attachments/assets/339d2db3-2a42-4452-9b4c-33698a3999da" />
<img width="3310" height="1951" alt="Screenshot 2025-10-29 175036" src="https://github.com/user-attachments/assets/52fdc0cc-f1bc-4e37-aa22-808162667232" />
<img width="3369" height="1955" alt="Screenshot 2025-10-29 175655" src="https://github.com/user-attachments/assets/eb8105f7-3fc9-407e-870e-9df600b0aa7e" />

a) Process Design kits (PDK) - is a library of basic photonic components generated by the foundary to give open access to their generic process for fabrication.

b) DRC & LVS

- DRC - design rule checking verifies as to whether a specific design meets the constraints imposed by the process technology to be used for its manufacturing. DRC checking is an essential part of the physical design flow and ensures the design meets manufacturing requirements and will not result in a chip failure. The process technology rules are provided by process engineers and/or fabrication facility.
- LVS - Layout versus schematic (LVS) checking compares the extracted netlist from the layout to the original schematic netlist to determine if they match. The comparison check is considered clean if all the devices and nets of the schematic match the devices and the nets of the layout. Optimally, the device properties can also be compared to determine if they match within a certain tolerance. When properties are compared, all the properties must match as well to achieve a clean comparison.

c) SPICE Models library in VLSI is a collection of test files that contains SPICE models - mathematical descriptions of electronic components like transistor, resistors and capacitors used to simulate a circuits behavior.

<img width="3456" height="1945" alt="Screenshot 2025-10-29 175840" src="https://github.com/user-attachments/assets/20b85a18-1c62-4b29-972a-d4b23bc48606" />

d) Library & User Defined Specs - cell height, supply voltage, metal layer, pin locations, drawn-gate length.

<img width="2113" height="1285" alt="Screenshot 2025-10-29 183707" src="https://github.com/user-attachments/assets/b5c5e330-b9d2-49cd-a021-133b7f0bddde" />

e) Circuit Design 

<img width="3203" height="1864" alt="Screenshot 2025-10-29 183333" src="https://github.com/user-attachments/assets/c04bdcfb-36c2-43b6-8a1b-922c406dbd1f" />

f) Layout Design

<img width="3227" height="1898" alt="Screenshot 2025-10-29 183442" src="https://github.com/user-attachments/assets/a9c8c39d-2377-4493-b5f5-b18597965109" />


## 4 Typical Characterization Flow

a) Read the model files

<img width="2825" height="636" alt="Screenshot 2025-10-29 185843" src="https://github.com/user-attachments/assets/58491b95-5a59-4326-9e8e-81be751a5e74" />

b) Read the extracted SPICE netlist

<img width="1077" height="680" alt="Screenshot 2025-10-29 185904" src="https://github.com/user-attachments/assets/9a7ac3da-89ca-443c-b87f-f9501360d059" />

c) Recognize the behavior of buffer

<img width="3266" height="1733" alt="Screenshot 2025-10-29 185929" src="https://github.com/user-attachments/assets/c733a84a-3b7c-4a82-a44a-3ce4be71f545" />

d) Red the sub circuits of inverter

<img width="1271" height="499" alt="Screenshot 2025-10-29 185958" src="https://github.com/user-attachments/assets/7736c063-bb9f-4c13-8bcd-a955255eaa3c" />

e) Attach necessary power supply

<img width="3244" height="1735" alt="Screenshot 2025-10-29 190039" src="https://github.com/user-attachments/assets/6438a4d5-567e-4cdb-bbf0-af0d16046d33" />

f) Provide necessary output capacitance

<img width="3240" height="1757" alt="Screenshot 2025-10-29 190057" src="https://github.com/user-attachments/assets/367abf2f-6a93-4b07-9153-5b333dc2496b" />

g) Provide necessary transition

<img width="3249" height="1747" alt="Screenshot 2025-10-29 190125" src="https://github.com/user-attachments/assets/3f52ce4c-ffd7-4c5e-9683-ad431f752c60" />

h) Feed all the steps from 1-8 to software GUNA it will generate timing, noise power.libs, function.

<img width="1068" height="676" alt="Screenshot 2025-10-29 190146" src="https://github.com/user-attachments/assets/ece32e89-3a0f-4ada-91d6-325322c0062e" />

<img width="3365" height="957" alt="Screenshot 2025-10-29 190214" src="https://github.com/user-attachments/assets/afe1d5cc-6b5d-48da-a60d-1dceaae498d1" />

It gives an important classfication
- Timing Classfication
- Power Classification
- Noise Classification

## 5 General Timing Characterization Process
Timing Characterization

i) slew_low_rise_thr\

<img width="3292" height="1690" alt="Screenshot 2025-10-29 191525" src="https://github.com/user-attachments/assets/53efccd0-8bc3-44f5-a532-2a91110645f4" />

ii) slew_high_rise_thr

<img width="3312" height="1693" alt="Screenshot 2025-10-29 191627" src="https://github.com/user-attachments/assets/3f62cf7c-afd6-4f9d-a279-229ec3f3300f" />

iii) slew_low_fall_thr

<img width="3292" height="1730" alt="Screenshot 2025-10-29 191756" src="https://github.com/user-attachments/assets/80a7519c-ffb0-4c1f-956c-921c95f3b595" />

iv) slew_high_fall_thr

<img width="3297" height="1709" alt="Screenshot 2025-10-29 191827" src="https://github.com/user-attachments/assets/f3ebd390-b619-403f-a5dd-ed2f628cd9f5" />

v) in_rise_thr

<img width="3335" height="1740" alt="Screenshot 2025-10-29 191942" src="https://github.com/user-attachments/assets/77c40cc6-fd5a-496e-8086-4fe4f6607049" />

vi) in_fall_thr

<img width="3283" height="1701" alt="Screenshot 2025-10-29 192105" src="https://github.com/user-attachments/assets/3cd2bfc3-0df5-428a-accc-1a3f419aba8e" />

vii) out_rise_thr

<img width="3331" height="1716" alt="Screenshot 2025-10-29 192015" src="https://github.com/user-attachments/assets/e489e325-d449-4b03-b019-a2b2cdfc2634" />

viii) out_fall_thr

<img width="3275" height="1701" alt="Screenshot 2025-10-29 192137" src="https://github.com/user-attachments/assets/95d6907e-c01b-4dc5-b1fa-972301738e42" />

## 6 Propagation Delay and Transition Time

To calculate delay the equation is given by
```
time(out_*_thr) - time(in_*_thr)
time(out_fall_thr) - time(in_rise_thr)
```
<img width="3200" height="1775" alt="Screenshot 2025-10-29 193902" src="https://github.com/user-attachments/assets/f19669fe-b5d7-4f54-a337-762c66b8d10c" />

```
time(out_fall_thr) - time(in_rise_thr)
time(in_rise_thr) = 3.207ns
time(out_fall_thr) = 3.230ns
3.230ns - 3.207ns
Delay = 23ps
```

<img width="3316" height="1747" alt="Screenshot 2025-10-29 193928" src="https://github.com/user-attachments/assets/f5c61ca5-37b6-43c1-aba4-59713b6b734d" />

If time(in_rise_thr) is greater than time(out_fall_thr) we get negative delay therefore delay can never be negative value, it indicates poor choosing of threshold point.

```
time(out_fall_thr) - time(in_rise_thr)
time(in_rise_thr) = 3.263ns
time(out_fall_thr) = 3.221ns
3.221ns - 3.263ns
Delay = -42ps
```

<img width="3339" height="1707" alt="Screenshot 2025-10-29 194006" src="https://github.com/user-attachments/assets/f5d95e3b-011c-4917-9950-14811ab7bfa6" />

## Timing Characterization for Transition Time

- time(slew_high_fall_thr) - time(slew_low_fall_thr)

<img width="2646" height="1132" alt="Screenshot 2025-10-29 194052" src="https://github.com/user-attachments/assets/cda1dbbd-26ca-4015-876d-f04b062331f4" />

- time(slew_high_rise_thr) - time(slew_low_rise_thr)
  
<img width="2681" height="1122" alt="Screenshot 2025-10-29 194030" src="https://github.com/user-attachments/assets/26bcebca-2e85-42b5-8567-d1c730efa86f" />

## LAB-02 Run floorplan using OpenLANE and review the layout in Magic

i. Switches for floorplan

```
#open the file
less floorplan.tcl (containing the default parameter for the floorplan stage
```

ii. Run 'picorv32a' design floorplan using OpenLANE flow 

```
run_floorplan
```

iii. Review floorplan files and steps to view floorplan

```
#open the file
less config.tcl
```

iv. Floorplan layout in Magic 

```
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/29-10_08-49/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

## Floorplan view in Magic



Design Alignment Instructions

Centering the Design:
 - Press S to select the entire design.
 - Press V to vertically align it to the middle of the screen.
   
Zooming In on a Specific Area:
 - Left-click and drag to select the desired region.
 - Right-click to bring up the context menu.
 - Press Z to zoom in on the selected area.
  
Getting Details of a Cell:
 - Move your cursor to the cell of interest.
 - Press S to select the cell.
 - In the tkcon window, enter the command "what" to display cell details.

## Horizontal ports metal layers set by the config.tcl

## Vertical ports metal layer set by congig.tcl


## LAB-2.1






