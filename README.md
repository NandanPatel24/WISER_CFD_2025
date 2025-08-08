# Quantum Simulation of the 1D Burgers’ Equation — WISER 2025

## Team Information
- Team name: EntangledAngle
- Team members: - Nandan Patel (Enrollment ID - gst-wM5uVX3ux7Ly44Y), Isshaan Singh (Enrollment ID - gst-RarLsdWbYJyKeFe)

## Overview

This repository contains our final submission for the **Womanium WISER 2025 Program**, focused on **hybrid quantum-classical simulation of nonlinear fluid dynamics**. We solve the **1D viscous Burgers’ equation**, a fundamental nonlinear PDE modeling shock waves and turbulence, using a quantum-enhanced algorithm built for current noisy quantum hardware.

>  The core objective: Demonstrate that quantum simulation techniques — when combined with classical preprocessing and noise mitigation — can effectively solve nonlinear PDEs like Burgers’ equation with modest quantum resources.

##  Problem Formulation

We solve the **1D Burgers’ equation**:

$$
\partial_t u + u \partial_x u = \nu \partial^2_x u, \quad x \in [0, 1], \quad t \in [0, 0.01]
$$

with:
- Boundary conditions:  
  $u(0, t) = 1$, $u(1, t) = 0$
- Initial condition (smooth):  
  $u(x, 0) = \sin(\pi x)$  
> 💡 *Note: The original step function initial condition*
> 
> $$
> u(x,0) = 
> \begin{cases}
> 1 & \text{if } x < 0.5 \\
> 0 & \text{otherwise}
> \end{cases}
> $$
>
> *is smoothed here to avoid numerical instability.*
  
## 🔬 Methodology

We employ a **hybrid quantum-classical framework** that transforms the nonlinear PDE into a solvable form for quantum circuits.

###  1. Cole–Hopf Transform  
Linearizes Burgers’ equation to a **diffusion (heat) equation** using:

$$
u(x,t) = -2\nu \frac{\partial_x \psi}{\psi}
\Rightarrow \partial_t \psi = \nu \\partial_x^2 \psi
$$

### 2. Quantum Simulation via Trotterization  
We discretize the heat equation and simulate it quantumly:
- **Laplacian Hamiltonian $\( H = -i\nu L \)$** created from finite differences
- **Trotterized time evolution**:
  $e^{-iHt} \approx \prod_i R_{XX}^{(i, i+1)}(\theta)$
- Implemented using **Qiskit** with 4 qubits (for 16 grid points)

### 3. Zero-Noise Extrapolation (ZNE)  
To mitigate quantum noise:
- Simulate circuits at **scales 1 and 3**
- Perform extrapolation:
  $u_{\text{ZNE}} = 1.5 \cdot u_{1} - 0.5 \cdot u_{3}$

### 4. Classical Benchmarks  
Validated results against:  
- **QuTiP Krylov solver**

All classical simulations done using **NumPy**, **SciPy**, and **QuTiP**.

## Metrics & Results

We validate quantum simulation results using:

| Metric               | Description |
|----------------------|-------------|
| L2 Errors          | Compare quantum vs classical u(x,t) |
| Shock Position     | $\( x \)$ where $\( u \approx 0.5 \)$ |
| Dissipation Rate   | $\( \nu \sum (\partial_x u)^2 \cdot dx \)$ |
| Circuit Complexity | Gate count, depth, Trotter steps |
| ZNE Improvement    | Reduction in L2 error from extrapolated results |

Visualization includes:
- **u(x, t) vs x** for 6 timesteps
- **Circuit depth vs time**
- **Dissipation rate curves**
- **L2 Error curves**
- **Shock front position curve**

## Tools & Libraries

- [Qiskit](https://qiskit.org/) — quantum circuit simulation, noise modeling, Rxx gate-based Trotter evolution  
- [QuTiP](https://qutip.org/) — Krylov evolution on Hamiltonian  
- [NumPy, SciPy] — grid discretization, integration, gradient calculation  
- [Matplotlib] — plotting simulation outputs  
- [IBM AerSimulator] — noise-aware circuit execution

##  Folder Structure

```bash
WISER_CFD_2025/
│
├── README.md                                  # Project overview and documentation
├── LICENSE                                    # License for use and distribution
│
├── Prototype_Code_WISER_CFD.ipynb             # Main prototype code for solving 1D Burgers' equation using quantum methods
│
├── Quantum Simulation of the 1D Burgers Equation.pptx   # Final presentation deck used to summarize and pitch the project
├── WISER_EntangledAngle(1) (1).mp4                   # Project demonstration video showing quantum entanglement behavior or results
│
├── Algo_Design_WISER_CFD.pdf                  # Detailed algorithmic design of the proposed quantum solvers
├── Algo_Comparison_WISER_CFD.pdf              # Comparative study of QTN, HSE, and hybrid methods
├── Quantum_Hardware_Run_WISER_CFD.pdf         # Results and observations from real quantum hardware runs
├── Resource_and_Noise_Analysis_WISER_CFD.pdf  # Analysis of quantum resource requirements and noise effects
├── Scalability_Study_WISER_CFD.pdf            # Study on how the methods scale with system size
├── Validation_and_Benchmark_WISER_CFD.pdf     # Validation against classical solvers and benchmark results




