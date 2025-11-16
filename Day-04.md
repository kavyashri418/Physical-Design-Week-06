## Pre-layout Timing Analysis and Importance of Good Clock Tree

## 1 Introduction to Delay tables

Observations
- 2 levels of buffering
- At every level, each node driving same load
- Idential buffer at same level

Let us assume C1=C2=C3=C4=25fF
How about creating a buffer tree at node 'A'
Let us assume Cbuf1=Cbuf2=30fF
Therefore, total cap at node 'A' => 60fF
Therefore, total cap at node 'B' => 50fF
Therefore, total cap at node 'C' => 50fF

## Delay Table for Cbuf '1'

## Delay Table for Cbuf '2'

## 2 Timing Analysis with Ideal Clock using OpenSTA
- Timing Analysis (with Ideal Clock)
Specifications
```
Clock frequency (F) = 1GHz
Clock period (T) = 1/F
                 = 1/1 GHz
                 = 1ns
```
Hence finite time 'S' required (before clk edge) for 'D' to reach Qm ie internal delay of Mux1 = setup time.

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

Clock Uncertainty
Clock uncertainty represents the overall margin added to the timing analysis to account for all kinds of unknown variations in the clock signal, including jitter, skew, and other unpredictable delays.
It is an intentional design margin used by EDA tools to ensure that the circuit remains functional under worst-case conditions.

Why jitter and uncertainty are critical:
- Static Timing Analysis (A)
- Defining safe setup and hold timing margins
- Ensuring reliable operation of high-speed digital systems
- Avoiding timing violations due to unpredictable clock behavior

Let us Identify timing paths from designs, with single clock

## Clock Tree Routing and Buffering using H-tree Algorithm

What can go wrong, if there's a glitch?
Incorrect data in memory will result in inaccurate functionality

Impact of  Crosstalk Delta Delay-Skew

Timing Analysis with real clocks using OpenSTA setup timing analysis using real clocks

## Introduction to  Maze Routing - Lee's Algorithm Routing and Design Rule Check (DRC)


