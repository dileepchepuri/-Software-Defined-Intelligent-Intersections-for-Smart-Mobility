SDI² — Software-Defined Intelligent Intersections
Hybrid SIMP–AIMP Intelligent Traffic Signal Management Using SUMO & SDN Principles

This repository contains the full implementation and SUMO simulation dataset for SDI² (Software-Defined Intelligent Intersections), a hybrid traffic management framework that switches between:

SIMP — Synchronous Intersection Management Protocol

AIMP — Adaptive Intersection Management Protocol

depending on real-time vehicle density and grouping.

This project is based on the EWGT 2025 research work titled:
“Software-Defined Intelligent Intersections for Smart Mobility”

📂 Project Structure 
📦 final result/
 ├── __pycache__/  
 │     ├── trafficmetrics.cpython-312.pyc
 │     └── trafficsignalcontroller.cpython-312.pyc

 ├── data/
 │     ├── AIMP/                     # Results/snapshots for AIMP evaluation
 │     ├── cross.add                 # SUMO additional elements
 │     ├── cross.det                 # Detector definitions
 │     ├── cross.edg                 # Network edge definitions
 │     ├── cross.flow                # Traffic flow definitions
 │     ├── cross.net                 # Road network
 │     ├── cross.netccfg             # NETCONVERT config
 │     ├── cross.nod                 # Nodes (intersections)
 │     ├── cross.out                 # Output files
 │     ├── cross.rou                 # Route files
 │     ├── cross.src                 # Source lane config
 │     ├── e0_0, e0_1, e1_0 ...      # Network state snapshots
 │     ├── SUMO Configuration File   # Simulation config (.sumocfg)
 │     └── <other SUMO XML assets>

 ├── output/
 │     ├── 0.133                     # Simulation output logs
 │     └── tripinfo                  # SUMO trip-level performance metrics

 └── result.py                       # Main Python script (SIMP/AIMP decision logic)

🚀 SDI² Overview

SDI² is an SDN-inspired traffic control system that:

✔ Reads real-time traffic data from SUMO
✔ Detects isolated vs. grouped vehicles
✔ Dynamically switches between SIMP and AIMP
✔ Adjusts traffic signal phases automatically
✔ Computes performance metrics (stopped delay, emissions, fuel use)
🧠 Core Components
1. SIMP — Synchronous Intersection Management Protocol

Used when:

A single isolated vehicle is approaching the intersection.

Features:

Pre-defined phase timings

Conflict-free directions (CDM-based scheduling)

One vehicle per non-conflicting lane

2. AIMP — Adaptive Intersection Management Protocol

Used when:

Multiple vehicles intend to cross in the same direction

Features:

Dynamic adjustment of green duration

Batch/group serving

Improved throughput

Reduced idle delay

3. SDI² Mode Switching Logic (Inside result.py)

Pseudo-logic reflecting your implementation:

if consecutive_vehicle_count(direction) > 1:
    activate_AIMP()
else:
    activate_SIMP()

🧪 SUMO Simulation Setup (data folder)

data/ folder contains the complete network:

File	Purpose
cross.net, cross.nod, cross.edg	Road network & node geometry
cross.flow	Traffic injection definition
cross.det	Induction loop detectors
cross.rou	Vehicle routes
cross.src	Source lane mapping
cross.out, e0_0, etc.	Output and network state files
*.sumocfg	Main SUMO simulation config file

This structure represents an 8-inflow, 4-arm intersection used in the EWGT evaluation.

📊 Simulation Output (output folder)

The output/ directory stores:

tripinfo → Per-vehicle travel time, delay, stops

0.133 → Aggregated emission/fuel metrics

These files are used to compute:

Stopped delay

Fuel consumption

PMx emissions

As reported in the EWGT 2025 paper.

📈 Performance Summary (from your abstract)

(Backed by SUMO results from the project)
SDI² achieves:

Metric	Improvement vs RR	Improvement vs SIMP
Stopped Delay	89.5% ↓	5% ↓
Fuel Consumption	63.3% ↓	15% ↓
PMx Emissions	76.9% ↓	27% ↓

This is due to efficient SIMP–AIMP switching.

🏃‍♂️ How to Run the Project
1. Install SUMO

Download from:
https://sumo.dlr.de/docs/Downloads.html

Ensure SUMO commands are available:

sumo --version

2. Install Python Dependencies
pip install sumolib traci

3. Run the Simulation

Inside final result/:

python result.py


This script:

Loads the SUMO network from data/

Runs the simulation

Applies SDI² logic

Stores outputs in output/

🧩 What result.py Does

traci connection setup

sensor data extraction

SIMP logic

AIMP phase adjustment

Decision switching

Metrics calculation (linked to trafficmetrics.py)

🎯 Future Enhancements

Multi-intersection SDN coordination

Neural-network–based phase prediction

V2I communication integration

Real-world RSU integration

👤 Developer

CHEPURI DILEEP
Developer & Implementer of the SDI² Simulation Framework
Department of AI, Sree Vidyanikethan Engineering College, India

📜 License

MIT or CC-BY-NC-ND (based on paper)
