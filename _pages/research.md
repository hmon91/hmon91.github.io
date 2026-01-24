---
layout: archive
title: "Research Projects"
permalink: /research/
author_profile: true
---

## Scalable Stability Verification via Sector Bounds
One of the primary challenges in deploying Neural Networks (NNs) in safety-critical control loops is certifying stability. Traditional methods like Integral Quadratic Constraints (IQCs) or Sum-of-Squares (SOS) often struggle with scalability as the network depth increases.

My research introduces a scalable alternative rooted in **Positive Systems Theory** and the **Positive Aizerman Conjecture**. By enclosing the non-linear neural network within linear "Sector Bounds," we can reduce the stability verification problem to simple linear algebra checks (checking if matrices are Metzler and Hurwitz).

### 1. Global Sector Bounds (Global Stability)
In my work on *Ensuring Both Positivity and Stability* [[1]](/publication/2024-01-01-lcss-positivity), we derived a method to calculate **Global Sector Bounds** for fully connected Feedforward Neural Networks (FFNNs).

* **The Concept:** We prove that a ReLU or Tanh neural network $NN(x)$ can be bounded globally by two linear functions: $\Gamma_1 x \leq NN(x) \leq \Gamma_2 x$.
* **The Method:** We propagate the sector bounds of individual activation functions layer-by-layer through the weight matrices.
* **The Result:** If the system matrices formed by these bounds ($A+B\Gamma_1 C$ and $A+B\Gamma_2 C$) satisfy the Metzler and Hurwitz conditions, the **entire** closed-loop system is globally exponentially stable.
* **Impact:** This method achieves up to **~$10^4\times$ speedup** compared to IQC-based methods and handles continuous-time systems efficiently.

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
In this track of research, I model how crowds move in emergency scenarios...
