## Final Steps for RTL2GDS using Tritonroute and OpenSTA

## TritonRoute
- Performs initial detail route.
- Honors the preprocessed route guides (obtained after fast route ) ie attempts as much as possible to route within route guides.
- Assumes route guides for each net satisfy inter-guide connectivity.
- Works on proposed MILP based panel routing scheme with intra-layer parallel and inter-layer sequential routing framework.

## Preprocessed route guides
Requirements of preprocessed guides:
- Should have until width.
- Should be in the preferred direction.

<img width="954" height="297" alt="Screenshot 2025-11-15 220751" src="https://github.com/user-attachments/assets/1df4e244-d179-40e0-b0e4-dc562c89c9f1" />

## Inter-Guide Connectivity
- Two guides are connected if:
  - They are on the same metal layer with touching edges, or
  - They are on neighbouring metal layers with a nonzero vertically overlapped area.
- Each unconnected terminal (ie pin of a standard-cell instance should have its pin shape overlapped by a route guide.

## Intra-layer parallel & Inter-layer sequential panel routing
Problem Statement:
 - INPUTS: LEF, DEF, Preprocessed route guides.
 - OUTPUT: Detailed routing solution with optimized wire-length and via count.
 - CONSTRAINTS: Route guide honaring, connectivity constraints and design rules.

<img width="896" height="262" alt="Screenshot 2025-11-15 221154" src="https://github.com/user-attachments/assets/2cd124d8-4ad3-4bb2-bafa-26add43132d7" />
   
Handling Connectivity:
 - Access Point (AP): An on-grid point on the metal layer of the route guide, and is used to connect to lower-layer segments, upper-layer segments, pins or IO ports.
 - Access Point Cluster (APC): A union of all Aps derived from same lower-layer segment, upper-layer guide, a pin or an IO port.

<img width="1169" height="378" alt="Screenshot 2025-11-15 221311" src="https://github.com/user-attachments/assets/2e5f8741-0286-4a07-be49-a6c3cf245283" />

## Routing Topology Algorithm

A routing topology algorithm determines the structural pattern or layout followed by interconnects while connecting a set of source and sink nodes on a chip. Its goal is to minimize wirelength, reduce delay, balance load, and improve overall routing quality. Different routing topologies are used depending on design goals such as low skew, minimal RC delay, or congestion reduction.

```
Algorithm 1 Optimization of Routinh Topology
for all i = 1 to n-1 do
  for all j = 1+1 to n do
     cost i,j <--- dist(APCi,APCj)
  end for
end for
T <--- MST(APCs,COSTs)
Return ei,j
```

## LAB-05: Steps to build Power Distribution Network

```
# Add all LEF files, including the merged one, into the OpenLANE environment
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Select a timing-centric synthesis strategy
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Enable sizing during synthesis
set ::env(SYNTH_SIZING) 1

# Run the synthesis stage after preparation
run_synthesis
```

<img width="980" height="237" alt="Screenshot 2025-11-18 222342" src="https://github.com/user-attachments/assets/c303695f-5c5d-4c6b-a73d-e441d5b9329c" />
<img width="984" height="274" alt="Screenshot 2025-11-18 221727" src="https://github.com/user-attachments/assets/bb1ab73d-3d64-43b8-a101-94f8a4666414" />

```
# Commands are internally executed when 'run_floorplan' is called
init_floorplan
place_io
tap_decap_or

# Proceed with placement
run_placement

# If a CTS-related library issue appears, clear the variable
unset ::env(LIB_CTS)

# Generate the clock tree for the design
run_cts

# After CTS is completed, create the power distribution network
gen_pdn
```

Command to generate PDN in openLANE: ```run_power_grid_generation ```

```
# Navigate to the directory where the PDN DEF file was generated
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_13_13/tmp/floorplan/

# Launch Magic and load the PDN DEF along with the technology and LEF files
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech \
      lef read ../../tmp/merged.lef \
      def read 14-pdn.def &
```

<img width="430" height="436" alt="Screenshot 2025-11-18 221045" src="https://github.com/user-attachments/assets/5de4a398-a215-405f-9ef0-a850986dd356" />

Zoomed Layout

<img width="881" height="504" alt="Screenshot 2025-11-18 221225" src="https://github.com/user-attachments/assets/4666a869-6a70-4565-ad41-3fe4a8371917" />

## LAB-5.1: Steps to perform routing

Command to run the routing in OpenLANE: ```run_routing```
```
# Check value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Check value of 'ROUTING_STRATEGY'
echo $::env(ROUTING_STRATEGY)

```

Layout after routing

<img width="393" height="395" alt="Screenshot 2025-11-18 221106" src="https://github.com/user-attachments/assets/d57df914-883a-42df-a839-c79d2bf99c1a" />

Zoomed Layout after routing

<img width="974" height="439" alt="Screenshot 2025-11-18 223546" src="https://github.com/user-attachments/assets/003e6590-24f1-49ee-b92d-606efc1ee283" />

Post routing STA

```
Commands to run post routing STA
read_lef /openLANE_flow/designs/picorv32a/runs/latest_25-03/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/latest_25-03/results/routing/picorv32a.def
read_spef /openLANE_flow/designs/picorv32a/runs/latest_25-03/results/routing/picorv32a.spef

write_db picorv32a_routing.db

read_db picorv32a_routing.db
read_verilog /openLANE_flow/designs/picorv32a/runs/latest_25-03/results/synthesis/picorv32a.synthesis_preroute.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
##read_liberty -max $::env(LIB_SLOWEST)
##read_liberty -min $::env(LIB_FASTEST)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -format full_clock_expanded -digits 4 -fields {net cap slew input_pins fanout}
```




