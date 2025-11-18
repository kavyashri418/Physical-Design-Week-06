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

