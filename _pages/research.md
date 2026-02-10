---
layout: archive
title: "Research Projects"
permalink: /research/
author_profile: true
---

{% include base_path %}

<center>
  <img src="/images/researchschematic.jpg" alt="Research Methodology Schematic" style="width: 100%; max-width: 900px; border: 1px solid #ddd; padding: 5px;">
  <br>
  <em><strong>Figure 1:</strong> Overview of my framework for Scalable Stability & Robustness Verification of Neural Feedback Systems.</em>
</center>
<br>
## 1. Neural Network Bounding
A critical step in verifying neural feedback loops is creating accurate, tractable mathematical models of the neural network's non-linear behavior. My research focuses on deriving linear "Sector Bounds" that enclose the network's output.

### Global Sector Bounds
For global stability analysis, I derived a method to calculate **Global Sector Bounds** for fully connected Feedforward Neural Networks (FFNNs). This method assumes the network has **no bias terms** (or biases are handled separately), ensuring the origin is an equilibrium point.

<center>
  <img src="{{ base_path }}/images/NN_sector_bounds.png" alt="Global Sector Bounds" style="width: 50%; max-width: 600px; border: 1px solid #ddd; padding: 5px;">
  <br>
  <em><strong>Figure 2:</strong> Validation of Global Sector Bounds. The black line represents the neural network output $NN(z)$, which is strictly contained within the linear envelope formed by the lower bound $\Gamma_1 z$ (blue) and upper bound $\Gamma_2 z$ (red) for all 100 random samples.</em>
</center>
<br>

* **Method:** We propagate the sector properties of individual activation functions (like ReLU or Tanh) layer-by-layer through the weight matrices.
* **Result:** This yields a global linear envelope valid for the entire state space:
  $$\Gamma_1 x \le NN(x) \le \Gamma_2 x$$
  where the bounding matrices are defined as:
  $$\Gamma_1 = -c^q \left( \prod_{i=1}^{q+1} |W^i| \right), \quad \Gamma_2 = c^q \left( \prod_{i=1}^{q+1} |W^i| \right)$$

#### Performance Comparison
As shown in **Table 1**, our method computes bounds orders of magnitude faster than IQC-based methods while providing tighter envelopes than standard norm-based approximations.

<table style="width:100%; border-collapse: collapse; text-align: center;">
  <thead>
    <tr style="border-bottom: 2px solid #333; background-color: #f9f9f9;">
      <th style="padding: 10px; border: 1px solid #ddd;">Method</th>
      <th style="padding: 10px; border: 1px solid #ddd;">Network Architecture</th>
      <th style="padding: 10px; border: 1px solid #ddd;">Computation Time (s)</th>
      <th style="padding: 10px; border: 1px solid #ddd;">Bounds</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="padding: 8px; border: 1px solid #ddd;"><strong>Our Method</strong></td>
      <td style="padding: 8px; border: 1px solid #ddd;">10 / 10 / 1</td>
      <td style="padding: 8px; border: 1px solid #ddd;">$2.5 \times 10^{-5}$</td>
      <td style="padding: 8px; border: 1px solid #ddd;">$\pm[2.65, 1.61]$</td>
    </tr>
    <tr style="background-color: #f9f9f9;">
      <td style="padding: 8px; border: 1px solid #ddd;"><strong>Our Method</strong></td>
      <td style="padding: 8px; border: 1px solid #ddd;">10 / 15 / 15 / 1</td>
      <td style="padding: 8px; border: 1px solid #ddd;">$2.6 \times 10^{-5}$</td>
      <td style="padding: 8px; border: 1px solid #ddd;">$\pm[2.75, 1.47]$</td>
    </tr>
    <tr>
      <td style="padding: 8px; border: 1px solid #ddd;"><strong>IQC Method</strong></td>
      <td style="padding: 8px; border: 1px solid #ddd;">10 / 10 / 1</td>
      <td style="padding: 8px; border: 1px solid #ddd;">$0.68$</td>
      <td style="padding: 8px; border: 1px solid #ddd;">—</td>
    </tr>
    <tr style="background-color: #f9f9f9;">
      <td style="padding: 8px; border: 1px solid #ddd;"><strong>Product of Norms</strong></td>
      <td style="padding: 8px; border: 1px solid #ddd;">10 / 10 / 1</td>
      <td style="padding: 8px; border: 1px solid #ddd;">—</td>
      <td style="padding: 8px; border: 1px solid #ddd;">$5.83$</td>
    </tr>
    <tr>
      <td style="padding: 8px; border: 1px solid #ddd;"><strong>Product of Norms</strong></td>
      <td style="padding: 8px; border: 1px solid #ddd;">10 / 15 / 15 / 1</td>
      <td style="padding: 8px; border: 1px solid #ddd;">—</td>
      <td style="padding: 8px; border: 1px solid #ddd;">$6.45$</td>
    </tr>
  </tbody>
</table>

<br>
<em><strong>Table 1:</strong> Comparison of computation time and bound tightness. (10/10/1 denotes a 3-layer NN with 10, 10, and 1 neurons). Note that IQC does not explicitly provide bounds for the entire NN, and Product of Norms is used only for bound comparison, not stability verification.</em>

### Local Sector Bounds
Global bounds can be conservative. To address this, I developed a novel **Local Sector Bound** formulation.

The construction contains the iteration of two stages as shown in **Figure 3**. This is the standard procedure used in calculating other NN bounds like CROWN (Wang et al., 2021).

* **S1:** *Propagate sector bounds through the weight matrix and bias.*
* **S2:** *Sector-bounding the activations $\phi$ over their input interval.*

Iterating **S1–S2** from the input to the output yields constant matrices $\gamma_1, \gamma_2$ such that $\gamma_1 y \le \pi(y) \le \gamma_2 y$ for all $y \in \Lambda$.

<center>
  <img src="{{ base_path }}/images/local_schematic.svg" alt="Local Bound Schematic" style="width: 100%; max-width: 600px; border: 1px solid #ddd; padding: 5px;">
  <br>
  <em><strong>Figure 3:</strong> Schematic illustration of the recursive procedure for computing local sector bounds. We propagate interval bounds layer-by-layer to determine the precise slope matrices $\gamma_1$ and $\gamma_2$.</em>
</center>
<br>

* **Innovation:** By restricting the analysis to a specific compact set of inputs, we calculate tighter, input-dependent slope matrices.
* **Advantage:** These bounds are significantly tighter than norm-based approximations and avoid the affine offsets used in methods like CROWN, making them compatible with robust control frameworks.

<div style="display: flex; flex-wrap: wrap; gap: 20px; justify-content: center; margin-top: 20px;">
  
  <div style="flex: 1; min-width: 300px; max-width: 500px; text-align: center;">
    <img src="{{ base_path }}/images/difbounds.png" alt="Comparison with CROWN" style="width: 100%; border: 1px solid #ddd; padding: 5px;">
    <br>
    <em style="font-size: 0.9em;"><strong>Figure 4a:</strong> Comparison of bound tightness. Our "Local Sector Bound" (yellow) is significantly tighter than the standard interval-based bounds used in CROWN/IBP (light blue), reducing conservatism in stability verification.</em>
  </div>

  <div style="flex: 1; min-width: 300px; max-width: 500px; text-align: center;">
    <img src="{{ base_path }}/images/local_plots.jpg" alt="Local Stability Plots" style="width: 100%; border: 1px solid #ddd; padding: 5px;">
    <br>
    <em style="font-size: 0.9em;"><strong>Figure 4b:</strong> Visualization of Local Sector Bounds for different input intervals. The yellow region indicates the computed sector, which tightly encloses the neural network's nonlinearity (black line).</em>
  </div>

</div>
<br>

---

## 2. Stability Verification & Safety
Once the neural network is bounded, I use **Control Theory** to certify that the closed-loop system (the robot or plant + the neural network) is stable.

### Positive Aizerman Framework
My verification pipeline relies on the **Positive Aizerman Conjecture**. By embedding the bounded neural network into a "Positive Lur'e System" framework, we reduce the complex stability problem to simple linear algebra checks.

<center>
  <img src="{{ base_path }}/images/aizerman_concept.png" alt="Positive Aizerman Concept" style="width: 100%; max-width: 600px; border: 1px solid #ddd; padding: 5px;">
  <br>
  <em><strong>Figure 5:</strong> Conceptual overview of the Aizerman Framework. We replace the nonlinear feedback $\Phi$ with linear surrogates $k x$ bounded within the sector $[k_1, k_2]$. If the system is stable for these linear bounds, it guarantees stability for the nonlinear system.</em>
</center>
<br>

* **Efficiency:** Instead of solving computationally expensive Linear Matrix Inequalities (LMIs), we simply check if the resulting system matrices are **Metzler** and **Hurwitz**.
* **Scalability:** This approach achieves up to $\approx 10^4\times$ speedup over state-of-the-art methods, enabling verification of larger systems.

<center>
  <img src="{{ base_path }}/images/stability_check.png" alt="Stability Check Diagram" style="width: 100%; max-width: 600px; border: 1px solid #ddd; padding: 5px;">
  <br>
  <em><strong>Figure 6:</strong> The simplified verification condition. By constructing lower and upper linear bounds using our novel sector method, stability is certified by checking if the lower bound is Metzler and the upper bound is Hurwitz.</em>
</center>
<br>

### Region of Attraction (ROA) Analysis
For systems that are not globally stable, I use the Local Sector Bounds to estimate the **Region of Attraction** (ROA).

<center>
  <img src="{{ base_path }}/images/roa_plots.png" alt="ROA Analysis Plots" style="width: 100%; max-width: 600px; border: 1px solid #ddd; padding: 5px;">
  <br>
  <em><strong>Figure 7:</strong> Estimation of the Region of Attraction (ROA). The yellow areas represent the certified safe sets of initial conditions from which the system is guaranteed to converge to the origin, calculated using our local sector bounds.</em>
</center>
<br>

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
