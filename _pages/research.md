---
layout: archive
title: "Research Projects"
permalink: /research/
author_profile: true
---

{% include base_path %}

<center>
  <img src="/images/research_schematic.png" alt="Research Methodology Schematic" style="width: 100%; max-width: 900px; border: 1px solid #ddd; padding: 5px;">
  <br>
  <em><strong>Figure 1:</strong> Overview of my framework for Scalable Stability & Robustness Verification of Neural Feedback Systems.</em>
</center>
<br>
## 1. Neural Network Bounding
A critical step in verifying neural feedback loops is creating accurate, tractable mathematical models of the neural network's non-linear behavior. My research focuses on deriving linear "Sector Bounds" that enclose the network's output.

### Global Sector Bounds
For global stability analysis, I derived a method to calculate **Global Sector Bounds** for fully connected Feedforward Neural Networks (FFNNs).
* **Method:** We propagate the sector properties of individual activation functions (like ReLU or Tanh) layer-by-layer through the weight matrices.
* **Result:** This yields a global linear envelope \\(\Gamma_1 x \leq NN(x) \leq \Gamma_2 x\\) valid for the entire state space.

### Local Sector Bounds
Global bounds can be conservative. To address this, I developed a novel **Local Sector Bound** formulation.
* **Innovation:** By restricting the analysis to a specific compact set of inputs, we calculate tighter, input-dependent slope matrices.
* **Advantage:** These bounds are significantly tighter than norm-based approximations and avoid the affine offsets used in methods like CROWN, making them compatible with robust control frameworks.

---

## 2. Stability Verification & Safety
Once the neural network is bounded, I use **Control Theory** to certify that the closed-loop system (the robot or plant + the neural network) is stable.

### Positive Aizerman Framework
My verification pipeline relies on the **Positive Aizerman Conjecture**. By embedding the bounded neural network into a "Positive Lur'e System" framework, we reduce the complex stability problem to simple linear algebra checks.
* **Efficiency:** Instead of solving computationally expensive Linear Matrix Inequalities (LMIs), we simply check if the resulting system matrices are **Metzler** and **Hurwitz**.
* **Scalability:** This approach achieves up to \\(\approx 10^4\times\\) speedup over state-of-the-art methods, enabling verification of larger systems.

### Region of Attraction (ROA) Analysis
For systems that are not globally stable, I use the Local Sector Bounds to estimate the **Region of Attraction** (ROA).
* **Guarantee:** We identify a safe set of initial conditions from which the system is guaranteed to converge to equilibrium.
* **Performance:** Our method certifies larger ROAs than standard IQC-based approaches.

---

## 3. Risk-Aware Safety Verification (Delays & Uncertainty)
Autonomous systems in the real world face two critical risks: **Time Delays** (from communication or computation) and **Parametric Uncertainty** (modeling errors). My research addresses these challenges using two distinct frameworks.

### Method A: Positivity-Based Certificates (Scalable)
To address the computational bottlenecks of traditional methods, I developed a delay-independent verification framework based on **Positive Systems Theory**.
* **Approach:** We model the system with interval matrix uncertainty and time delays. By wrapping the neural network in our **Local Sector Bounds** and enforcing a "Metzler" structure on the system matrices, we can certify stability without solving complex optimizations.
* **Key Result:** If the lower-bound matrix is Metzler and the upper-bound matrix is Hurwitz, the system is robustly stable for *any* non-negative time delay.
* **Performance:** This method runs orders of magnitude faster than SDP-based approaches.

### Method B: IQC-Based Framework (High-Fidelity)
As a rigorous benchmark, I also developed a comprehensive **Integral Quadratic Constraint (IQC)** pipeline tailored for neural networks with delays and uncertainty.
* **LFT Modeling:** We model the discrete delays and element-wise interval uncertainty as a **Linear Fractional Transformation (LFT)**. This separates the "troublesome" components (uncertainty blocks) from the nominal plant.
* **Composite IQCs:** We construct a composite IQC filter that combines:
    1.  **Delay IQCs:** Using a delay-line filter to bound the energy of the delay operator.
    2.  **Uncertainty IQCs:** Using symmetric box multipliers to bound parametric variations.
    3.  **Neural Network IQCs:** Using sector constraints to bound the nonlinearity.
* **Verification:** Stability is certified by solving a large-scale **Semi-Definite Program (SDP)**. While computationally heavier, this framework provides a standard robust control baseline for AI-enabled systems.

---

## 4. Crowd Dynamics & Emergency Evacuation
In addition to neural network verification, I research **multi-agent systems** applied to public safety. Specifically, I develop dynamical models to simulate and optimize crowd behavior during active shooter incidents.

### The Predator-Swarm-Guide (PSG) Model
We introduced the **Predator-Swarm-Guide (PSG)** model, a hybrid framework that models the complex interactions between three distinct entities:
1.  **The Predator (Shooter):** An agent tracking and repelling the crowd.
2.  **The Swarm (Crowd):** Agents exhibiting pairwise repulsive/attractive forces (social friction) and wall interactions.
3.  **The Guide (Leader):** A trusted agent attempting to steer the swarm to a "Safe Zone".

### Key Contributions
* **Dynamic Guidance Strategy:** We modeled a guiding agent whose movement is governed by a weighting parameter \\(\lambda\\), optimizing the trade-off between "moving toward safety" and "evading the shooter".
* **Casualty Minimization:** We formulated an optimization problem to tune crowd cohesion \\(\alpha_1\\) and guidance strategy \\(\lambda\\), demonstrating that rational cooperation between the guide and crowd significantly reduces casualties.
* **Equilibrium Analysis:** By analyzing the continuum-limit version of the model, we derived theoretical predictions for the crowd's steady-state configuration (e.g., forming annular shapes around the predator).

---

### Related Publications
1. **H. Montazeri Hedesh**, M. Siami. "Delay-Independent Safe Control with Neural Networks: Positive Lur'e Certificates for Risk-Aware Autonomy," *arXiv*, 2025. [[PDF]](/publication/2025-10-08-delay-paper)
2. **H. Montazeri Hedesh**, M. Wafi, M. Siami. "Local Stability and Region of Attraction Analysis for Neural Network Feedback Systems under Positivity Constraints," *IEEE CDC*, 2025. [[PDF]](/publication/2025-12-01-cdc-local)
3. **A. Darabi, H. M. Hedesh**, M. Siami, M. Sznaier. "Predator-Swarm-Guide Dynamics: A Hybrid Approach to Crowd Modeling and Guidance in Mass Shooting Scenarios," *American Control Conference (ACC)*, 2024. [[PDF]](/publication/2024-07-01-acc-predator)
4. **H. Montazeri Hedesh**, M. Siami. "Ensuring Both Positivity and Stability Using Sector-Bounded Nonlinearity for Systems With Neural Network Controllers," *IEEE Control Systems Letters*, 2024. [[PDF]](/publication/2024-01-01-lcss-positivity)
