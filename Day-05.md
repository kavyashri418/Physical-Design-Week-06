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

## Inter - Guide Connectivity
- Two guides are connected if:
  - They are on the same metal layer with touching edges, or
  - They are on neighbouring metal layers with a nonzero vertically overlapped area.
- Each unconnected terminal (ie pin of a standard-cell instance should have its pin shape overlapped by a route guide.

## Intra-layer parallel & Inter-layer sequential panel routing
Problem Statement:
 - INPUTS: LEF, DEF, Preprocessed route guides.
 - OUTPUT: Detailed routing solution with optimized wire-length and via count.
 - CONSTRAINTS: Route guide honaring, connectivity constraints and design rules.
   
Handling Connectivity:
 - Access Point (AP): An on-grid point on the metal layer of the route guide, and is used to connect to lower-layer segments, upper-layer segments, pins or IO ports.
 - Access Point Cluster (APC): A union of all Aps derived from same lower-layer segment, upper-layer guide, a pin or an IO port.

## Routing Topology Algorithm

