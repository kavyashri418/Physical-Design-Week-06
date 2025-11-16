# Good Floorplan vs Bad Floorplan and Introduction to Library Cells

## 1 Chip Floor Planning Considerations
a) Define Width and Height of Core and Die
Lets begin with a netlist

```
FF = Flip Flop/Latches/Registers
A1, Q1 = standard cells (AND, OR, Inverter)
```
Consider, a netlist with 2 flops and 2 gates, with above shown connections.
Note: a netlist describes the connectivity of an electronic design.
Now, lets convert the highlighted symbols into physical dimension.

What is 'core' and 'die' section of a chip?
A die, which consists of core, is small semiconductor material specimen on which the fundamental circuit is fabricated.

How to arrive on its dimensions?
Place all logical cells inside the core. The logical cells occupies the complete area of the core

100% Utilization is given by the formula
```
Utilization Factor = (Area occupied by the netlist)/(Total area of the core)
```
b) Define Locations of Preplaced Cells
- Lets consider block 1 and block 2
- Extend IO pins
- Black box the boxes
- Seperate the black boxes as two different IP's or modules

Similarly there are other IP's also available for eg
- The arrangements of these IP's in a chip is referred as floorplanning.
- These IP's/blocks have user-defined locations, and hence are placed in chip before automated placement , routing and are called as pre-placed cells.
- Automated placement and routing tools places in the remaining logical cells in the design onto chip.

c) De-coupling Capacitors
Surround pre-placed cells with decoupling capacitor

Consider the amount of the switching current required for a complex circuit something like below,
- Consider capacitance to be zero for the discussion Rdd, Rss, Ldd and Lss are well defined values.
- During switching operation, the circuit demands switching current ie peak current (Ipeak).
- Now, due to the presence of Rdd and Ldd, there will be a voltage drop across them and voltage at node 'a' would be 'vdd' instead of vdd.
- If 'vdd' goes below the noise margin, due to Rdd and Ldd, the logic 1 at the output of the circuit wont be detected as logic '1' at the input of the circuit following this circuit.

Noise Margin Summary
Noise induced bump characteristics at different noise margin levels.
For any signal to be considered as logic '0' and logic '1' it should be in the NML and NMH ranges respectively.

d) Power Planning
We have taken care of local communication now we consider below scenario

Now let the output of 16-bit bus, is connected to an inverter.

What does this mean?
This means all capacitors which were charged to 'v' volts will have to discharge to '0' volts through single 'gnd' tap point. This will cause a bump in 'gnd' tap point.

Also, all capacitors which were '0' volts will have to charge to 'v' volts through single 'vdd' tap point. This will cause lowering of voltage at 'vdd' tap point.

e) Pin Placement and Logical Cell Placement Blockage
Lets take below design for eg that needs to be implemented

Complete Design

The connectivity information between the gates is coded using verilog language and is called as the netlist.

Logical Cell Placement Blockage

Floorplan is ready for placement and routing step

## 2 Library Binding and Placement
- Netlist binding and initial place design
- Bind netlist with physical cells
- Placement
- Optimize Placement
  This is the stage where we estimate wire length and capacitance and based, on that insert repeaters.

Stage 1
Stage 2
Stage 3
Stage 4

Need for Libraries and Characterization
Library Characterization and Modelling
PART-1 Concepts and theory = NLDM, CCS timing, Power and Noise Characterization
