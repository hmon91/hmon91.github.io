---
layout: archive
title: "Research Projects"
permalink: /research/
author_profile: true
---

## 1. Neural Network Bounding
A critical step in verifying neural feedback loops is creating accurate, tractable mathematical models of the neural network's non-linear behavior. My research focuses on deriving linear "Sector Bounds" that enclose the network's output.

### Global Sector Bounds
[cite_start]For global stability analysis, I derived a method to calculate **Global Sector Bounds** for fully connected Feedforward Neural Networks (FFNNs)[cite: 108, 148].
* [cite_start]**Method:** We propagate the sector properties of individual activation functions (like ReLU or Tanh) layer-by-layer through the weight matrices[cite: 639, 740].
* [cite_start]**Result:** This yields a global linear envelope $\Gamma_1 x \leq NN(x) \leq \Gamma_2 x$ valid for the entire state space[cite: 305].

### Local Sector Bounds
Global bounds can be conservative. [cite_start]To address this, I developed a novel **Local Sector Bound** formulation[cite: 467].
* [cite_start]**Innovation:** By restricting the analysis to a specific compact set of inputs, we calculate tighter, input-dependent slope matrices[cite: 494].
* [cite_start]**Advantage:** These bounds are significantly tighter than norm-based approximations and avoid the affine offsets used in methods like CROWN, making them compatible with robust control frameworks[cite: 629].

---

## 2. Stability Verification & Safety
Once the neural network is bounded, I use **Control Theory** to certify that the closed-loop system (the robot or plant + the neural network) is stable.

### Positive Aizerman Framework
My verification pipeline relies on the **Positive Aizerman Conjecture**. By embedding the bounded neural network into a "Positive Lur'e System" framework, we reduce the complex stability problem to simple linear algebra checks.
* **Efficiency:** Instead of solving computationally expensive Linear Matrix Inequalities (LMIs), we simply check if the resulting system matrices are **Metzler** and **Hurwitz**.
* **Scalability:** This approach achieves up to **~$10^4\times$ speedup** over state-of-the-art methods, enabling verification of larger systems.

### Region of Attraction (ROA) Analysis
For systems that are not globally stable, I use the Local Sector Bounds to estimate the **Region of Attraction** (ROA).
* **Guarantee:** We identify a safe set of initial conditions from which the system is guaranteed to converge to equilibrium.
* **Performance:** Our method certifies larger ROAs than standard IQC-based approaches.

**Related Publications:**
1. **H. Montazeri Hedesh**, M. Siami. "Ensuring Both Positivity and Stability Using Sector-Bounded Nonlinearity for Systems With Neural Network Controllers," *IEEE Control Systems Letters*, 2024. [[PDF]](/publication/2024-01-01-lcss-positivity)
2. **H. Montazeri Hedesh**, M. Wafi, M. Siami. "Local Stability and Region of Attraction Analysis for Neural Network Feedback Systems under Positivity Constraints," *IEEE CDC*, 2025. [[PDF]](/publication/2025-12-01-cdc-local)

### 2. Local Sector Bounds (Region of Attraction)
While global bounds are powerful, they can be conservative for large inputs. In my recent work on *Local Stability and Region of Attraction Analysis* [[2]](/publication/2025-12-01-cdc-local), we refined this approach to find tighter, **Local Sector Bounds**.

* **The Innovation:** Instead of finding a bound valid for *all* space, we calculate bounds valid within a specific compact set $\Gamma$. We utilize layer-wise linear relaxations of activation functions to propagate tighter constraints.
* **Region of Attraction (ROA):** By applying a localized version of the Positive Aizerman Conjecture, we can certify a specific **Region of Attraction**. Any trajectory starting inside this region is guaranteed to converge to the equilibrium.
* **Performance:** Numerical results show this method yields larger certified ROAs than existing methods like CROWN or IBP while maintaining high computational efficiency.

**Related Publications:**
1. **H. Montazeri Hedesh**, M. Siami. "Ensuring Both Positivity and Stability Using Sector-Bounded Nonlinearity for Systems With Neural Network Controllers," *IEEE Control Systems Letters*, 2024.
2. **H. Montazeri Hedesh**, M. Wafi, M. Siami. "Local Stability and Region of Attraction Analysis for Neural Network Feedback Systems under Positivity Constraints," *IEEE CDC*, 2025.

---

## 2. Crowd Dynamics & Control
---
## Crowd Dynamics & Emergency Evacuation
In addition to neural network verification, I research **multi-agent systems** applied to public safety. Specifically, I develop dynamical models to simulate and optimize crowd behavior during active shooter incidents.

### The Predator-Swarm-Guide (PSG) Model
We introduced the **Predator-Swarm-Guide (PSG)** model, a hybrid framework that models the complex interactions between three distinct entities:
1.  **The Predator (Shooter):** An agent tracking and repelling the crowd.
2.  **The Swarm (Crowd):** Agents exhibiting pairwise repulsive/attractive forces (social friction) and wall interactions.
3.  **The Guide (Leader):** A trusted agent attempting to steer the swarm to a "Safe Zone".

### Key Contributions
* **Dynamic Guidance Strategy:** We modeled a guiding agent whose movement is governed by a weighting parameter ($\lambda$), optimizing the trade-off between "moving toward safety" and "evading the shooter".
* **Casualty Minimization:** We formulated an optimization problem to tune crowd cohesion ($\alpha_1$) and guidance strategy ($\lambda$), demonstrating that rational cooperation between the guide and crowd significantly reduces casualties.
* **Equilibrium Analysis:** By analyzing the continuum-limit version of the model, we derived theoretical predictions for the crowd's steady-state configuration (e.g., forming annular shapes around the predator).

**Related Publications:**
1. **A. Darabi, H. M. Hedesh**, M. Siami, M. Sznaier. "Predator-Swarm-Guide Dynamics: A Hybrid Approach to Crowd Modeling and Guidance in Mass Shooting Scenarios," *American Control Conference (ACC)*, 2024. [[PDF]](/publication/2024-07-01-acc-predator)
