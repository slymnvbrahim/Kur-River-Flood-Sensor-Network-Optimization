# Kür River Flood Sensor Network Optimization

An algorithmic approach to deploying a cost-effective, hybrid flood monitoring sensor network along the Kür River in the Sabirabad District of Azerbaijan. 

This repository provides a complete computational framework comparing a standard Single-Objective Genetic Algorithm (Weighted-Sum GA) against a Multi-Objective Non-dominated Sorting Genetic Algorithm II (NSGA-II) to find the optimal balance between cost and performance in a resource-constrained environment.

##  Overview

Flood monitoring in resource-constrained environments requires a careful balance between maximizing spatial coverage and minimizing hardware costs. Rather than deploying identical high-end sensors, this project utilizes a **heterogeneous fleet** (a mix of high-precision radar, mid-range ultrasonic, and low-cost water-level switches) to optimize deployment along a real geographic corridor.

The project models the problem using four primary objectives:
1. **Maximize Coverage:** The fraction of the river corridor within sensor detection range.
2. **Maximize Reliability:** Distance-weighted sensor availability, penalizing deployments far from road access nodes to account for maintenance difficulty.
3. **Maximize Redundancy:** Overlapping coverage to ensure fault tolerance.
4. **Minimize Cost:** Keeping the fleet procurement within a strict USD budget constraint.

##  Methodology: NSGA-II vs. Weighted-Sum GA

To demonstrate the superiority of Pareto-based optimization for engineering trade-offs, this notebook implements two distinct approaches from scratch:

### 1. Weighted-Sum GA (Benchmark)
Collapses all four objectives into a single scalar fitness function using predefined weights, heavily penalizing budget violations:
$f_{GA} = w_1 \cdot \text{Coverage} + w_2 \cdot \text{Reliability} + w_3 \cdot \text{Redundancy} - \lambda \cdot \max(0, \text{Cost} - \text{Budget})^2$

### 2. NSGA-II (Proposed Framework)
Simultaneously evaluates all objectives independently, applying constrained-domination rules and crowding distance metrics to generate a diverse **Pareto Front** of non-dominated solutions. This provides decision-makers with a wide array of strategic trade-offs (e.g., "Highest Coverage" vs. "Lowest Cost") rather than a single, rigid solution.

## 🛠️ Technical Features

* **Geospatial Anchoring:** Integrates OpenStreetMap data via `osmnx` (with embedded fallback coordinates) to map the real Kür River polyline and calculate true Haversine distances.
* **Algorithm Implementation:** Custom Python implementations of selection (tournament), crossover (two-point), and mutation (per-gene replacement) tailored for spatial coordinates and categorical sensor types.
* **Advanced Data Visualization:** Extensive interactive plotting using `Plotly`:
  * Mapbox deployment tracking (comparing GA vs NSGA-II configurations).
  * 3D Pareto front scatter plots.
  * Parallel coordinate plots for strategy selection.
  * Hypervolume indicator calculations to mathematically validate the superiority of the NSGA-II algorithm.

##  Tech Stack

* **Language:** Python 3.10+
* **Data Processing & Math:** `numpy`, `pandas`, `math`, `random`
* **Geospatial Analytics:** `osmnx`
* **Visualization:** `plotly` (Graph Objects & Express)

##  Getting Started

### Installation

1. Clone this repository:
   ```bash
   git clone [https://github.com/yourusername/kur-river-sensor-optimization.git](https://github.com/yourusername/kur-river-sensor-optimization.git)
   cd kur-river-sensor-optimization
