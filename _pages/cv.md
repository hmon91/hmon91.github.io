---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

You can download a PDF copy of my complete CV [here](/files/cv.pdf).

## Education
* **Ph.D. in Electrical Engineering**, Northeastern University, Boston, USA (Sep 2021 – Present)
    * **GPA:** 3.81
    * **Thesis:** Scalable Method for Stability and Robustness Verification of Systems with NN Feedback using Positivity Constraints.
* **M.Sc. in Aerospace Engineering**, Sharif University of Technology (Sep 2017 – June 2020)
    * **Control Courses GPA:** 3.75
    * **Thesis:** Coupled Attitude-Orbit Dynamics and Control of a Solar Sail via Center-of-Mass Manipulation.
* **B.Sc. in Aerospace Engineering**, Sharif University of Technology (Sep 2012 – June 2017)
    * **Thesis:** Attitude Control of an Under-Actuated Satellite by Two Reaction Wheels.

## Research & Impact
* **Novel Neural Network Bounding:** Designed global & local NN bounding (depth‑agnostic) methods, enabling ~10× faster bound computation and tight, input‑aware sector envelopes for controllers.
* **Scalable Verification Pipeline:** Built a scalable robust stability verification pipeline for NN‑in‑the‑loop systems under positivity constraints, achieving up to ~10⁴× speedup over state-of-the-art baselines.
* **Sim-to-Real Gap:** Validated learning-enabled control frameworks through extensive simulation and hardware-informed experiments, bridging the gap between theoretical guarantees and real-world robotic performance.
* **Tool Integration:** Implemented state‑of‑the‑art verification (AutoLiRPA, JAX‑Verify) and bridged them with classical control toolchains (MPC/robust analysis) for reproducible experiments using MATLAB/Python integration.
* **Crowd Dynamics & Fluid Analogy:** Modeled large-scale population motion as continuum flow dynamics and designed optimal egress control policies, highlighting transferable techniques for airflow and transport phenomena.
* **Space Robotics Optimization:** Derived coupled attitude–orbit dynamics of a solar sail via center-of-mass manipulation, including interplanetary path optimization using SNOPT.

## Work Experience
* **Graduate Research & Teaching Assistant**, Northeastern University (Sep 2021 – Present)
    * Supported autonomous experimentation environments (Quanser, Franka Emika) and reproducible computational pipelines.
    * Research in control, estimation, and learning-enabled autonomy.
* **Control Systems Engineer**, Safatco (Dec 2019 – Oct 2020)
    * Reverse engineered and developed electromagnetic servo valves for fuel control systems.
    * performed SolidWorks modeling, precision measurement, and tolerance validation.
* **R&D Engineer**, Sharif Technology Services (Satellite-building Project) (Apr 2018 – Oct 2019)
    * Built and configured Hardware-in-the-Loop (HIL) and Software-in-the-Loop (SIL) testbeds to support system integration.
    * Developed digital models for satellite attitude and position estimation using EKF and UKF.
    * Designed and executed sensor calibration procedures for magnetometers, gyroscopes, and magnetorquers.
* **R&D Engineer**, Sharif Technology Services (Aerospace Systems Manufacturing) (Jan 2017 – May 2017)
    * Conducted R&D for a satellite reaction wheel; drafted verification and calibration procedures.

## Selected Projects

### Robotics, AI & Control
* **Safe Control Learning:** Designed learning-based controllers for a network of quadrotors using a scalable NN-in-the-loop verification framework.
* **Autonomous Lab Setup:** Installed and calibrated a Quanser autonomous lab environment with multi-camera sensing for real-time 6-DOF pose estimation of drones and ground vehicles.
* **Imitation Learning for MPC:** Implemented safe imitation learning of a Model Predictive Control (MPC) policy for nonlinear inverted pendulum dynamics.
* **Robotic Manipulation:** Configured two Franka Emika robotic arms and established real-time coordination for interactive tasks (Tic-Tac-Toe).
* **Data-Driven Identification:** Applied Sparse Identification of Nonlinear Dynamics (SINDy) and Sum-of-Squares (SOS) methods to discover governing equations and certify stability from data.
* **Embedded Control:** Designed a controller-observer system for a quadrotor and deployed the closed-loop system on an Arduino platform.

### Aerospace & Dynamics
* **High-Fidelity Spacecraft GNC:** Developed nonlinear spacecraft attitude/orbit dynamics models with integrated state estimation (EKF/UKF) and feedback control; evaluated performance under sensor noise and disturbances.
* **Fluid Dynamics (CFD):** Conducted CFD simulations using Gambit/Fluent to analyze quadrotor ground-effect flows and re-entry vehicle aerodynamics.
* **Structural Dynamics:** Performed finite-element-based analysis of an aircraft wing box using Abaqus to evaluate modal characteristics and structural response.
* **Complex Dynamics Modeling:** Modeled fuel sloshing effects in spacecraft attitude dynamics and analyzed nonlinear momentum transfer control via feedback linearization.
* **Aircraft Control:** Analyzed statistical control of aircraft encountering Clear Air Turbulence (CAT) considering measurement noise effects.
* **Orbital Mechanics:** Modeled satellite ground tracks, eclipse times, and visibility to ground stations.

### Software Development
* **Reversi Game Engine:** Programmed an automatic "Reversi" game in C, including game-state modeling and algorithmic decision logic.

## Technical Skills
* **Robotics & Perception:** 6-DoF rigid-body dynamics, robotic arms, real-time control, multi-camera sensing, sensor calibration, EKF/UKF.
* **Machine Learning:** Imitation Learning, Reinforcement Learning, PyTorch, TensorFlow, AutoLiRPA, JAX-Verify.
* **Control & Optimization:** Nonlinear Control, MPC, Robust Control, Reachability Analysis, Lyapunov Methods, SNOPT, CVX.
* **Programming:** Python, MATLAB, C, Julia.
* **Simulation Tools:** Simulink, Fluent, Gambit, SolidWorks, Abaqus, ANSYS.

## Teaching & Mentorship
* **Teaching Assistant:**
    * *Embedded Design Enabling Robotics* (Spring 2026)
    * *Linear Systems Analysis* (Fall 2025)
    * *Electrical Engineering Class & Lab* (Spring 2025)
    * *Classical Control* (Spring 2023)
* **Mentorship:** Capstone project "Robotic Gloves for Teaching Piano" (Summer 2024).

## Professional Service
* **Leadership:** Founder & President of Northeastern ECE Ph.D. Council.
* **Reviewer:** IEEE CDC, ACC, Control Systems Letters, IFAC CPHS.
* **Memberships:** IEEE, Society for Risk Analysis (SRA).
