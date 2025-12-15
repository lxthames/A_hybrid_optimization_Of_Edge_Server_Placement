# Optimizing Edge Server Placement Using Hybrid Metaheuristic Algorithms

![Status](https://img.shields.io/badge/Status-Completed-success)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Institution](https://img.shields.io/badge/Institution-HSE_University-red)

**A Comprehensive Framework for Edge Computing Infrastructure Optimization**

---

## 📋 Table of Contents
- [Abstract](#-abstract)
- [The Problem](#-the-problem)
- [System Architecture](#-system-architecture)
- [Methodology & Algorithms](#-methodology--algorithms)
- [Performance Results](#-performance-results)
- [Setup & Usage](#-setup--usage)
- [Authors](#-authors)

---

## 📖 Abstract

The exponential growth of Internet of Things (IoT) devices has placed immense pressure on traditional cloud computing architectures, necessitating the shift toward **Edge Computing**. However, the efficacy of edge computing relies heavily on the optimal placement of Edge Servers (ES) to minimize latency.



This project addresses the **Edge Server Placement (ESP)** problem, treating it as an **NP-hard optimization challenge**. We developed a framework evaluating over ten metaheuristic algorithms, including novel hybrids like **PSO-WOA** and **TLBO-WOA**. Our results indicate that the hybrid TLBO-WOA approach significantly outperforms standard algorithms, achieving the lowest average response time (**0.00172 ms**) and demonstrating superior stability under high-load conditions.

---

## ⚠️ The Problem

The traditional cloud model struggles with the latency demands of modern applications (e.g., autonomous driving, real-time video analytics). While Edge Computing bridges this gap, deciding where to place servers is a complex balancing act involving:

1.  **Network Constraints:** Limited capacity compared to the cloud.
2.  **Queuing Delays:** Modeled using M/M/1 queuing theory.
3.  **Offloading Penalties:** Handling requests that must be sent to the distant cloud when edge capacity is exceeded.

**Objective:** Determine the optimal subset of candidate sites to deploy edge servers to minimize average system response time.

---

## 🏗 System Architecture

We simulated a realistic network environment structured across three distinct layers:

1.  **Device Layer:** IoT devices generating initial requests.
2.  **Edge Layer:** Base stations and potential Edge Server locations.
3.  **Cloud Layer:** Fallback mechanism for capacity overflow.

The mathematical model minimizes total latency, calculated as the weighted sum of transmission time, processing time (via M/M/1 theory), and network propagation delay.

---

## 🧠 Methodology & Algorithms

We implemented a diverse portfolio of nature-inspired algorithms. To address stagnation issues in standard algorithms, we developed specific **Hybrid Approaches** combining exploration and exploitation capabilities.



### Standard Algorithms
* **Evolutionary:** Genetic Algorithm (GA), Differential Evolution (DE)
* **Swarm-Based:** Particle Swarm Optimization (PSO), Whale Optimization Algorithm (WOA), Grey Wolf Optimizer (GWO), Cuckoo Search (CS)
* **Physics/Social:** Simulated Annealing (SA), Teaching-Learning Based Optimization (TLBO)

### Novel Hybrid Algorithms
| Algorithm | Composition | Strategy |
| :--- | :--- | :--- |
| **PSO-WOA** | Particle Swarm + Whale Optimization | Uses PSO for rapid initial convergence and WOA spiral search to escape local optima (Inertia weight: 0.7). |
| **TLBO-WOA** | Teaching-Learning + Whale Optimization | Leverages TLBO "Teacher Phase" for global guidance and "Learner Phase" + WOA for diversity. |

---

## 📊 Performance Results

We conducted rigid testing on grid-based topologies (20-100 nodes) using a Python-based custom simulator.



### 1. Scale Analysis (100 Nodes)
The **TLBO-WOA hybrid** emerged as the clear winner. Traditional algorithms like PSO struggled significantly in high-dimensional search spaces.

| Algorithm | Avg Response Time (ms) | Performance Note |
| :--- | :--- | :--- |
| **TLBO-WOA** | **0.00172** | 🏆 Best Performance |
| WOA (Standard) | 0.00176 | Runner-up |
| PSO | 3.918 | Slowest / Trapped in local optima |

### 2. Stability & Statistical Validation
* **Runs:** 30 independent runs per algorithm.
* **Stability:** TLBO-WOA standard deviation: **0.00012 ms** (vs PSO: 1.240 ms).
* **Significance:** Paired t-test confirmed significance with p < 0.05.

### 3. Stress Testing (Load Variation)
Under near-congestion loads (0.9 utilization):
* **TLBO-WOA:** Degraded gracefully from 0.00098 ms to 0.00385 ms.
* **Standard WOA:** Suffered a **613% increase** in latency.

---

## ⚙️ Setup & Usage

### Prerequisites
* Python 3.8+
* `numpy`
* `scipy`
* `matplotlib` (for plotting results)
