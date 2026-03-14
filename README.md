# Supersonic Rocket Nozzle Simulation using SU2

This repository contains the configuration and setup for simulating a **compressible turbulent flow in a converging–diverging rocket nozzle** using the **SU2 CFD solver**.

The case models the expansion of high-temperature combustion gases from a combustion chamber through the throat and into a supersonic divergent section designed to generate approximately **600 N thrust**.

The objective of this assignment was to **develop the nozzle simulation from scratch using SU2**, understand the solver configuration, and explore the numerical modeling of compressible turbulent flow.

---

# Author

**Boddu Harshavardhan**
Mechanical Engineering
GVP College of Engineering
India

---

# Project Overview

Rocket engines accelerate high-pressure combustion gases through a **converging–diverging (De Laval) nozzle**.

The flow physics in such nozzles involve:

• Subsonic flow in the converging section
• Sonic flow at the throat
• Supersonic expansion in the divergent section

This simulation captures these phenomena using the **Reynolds-Averaged Navier–Stokes (RANS)** equations.

---

# Turbulence Model

The simulation uses the **Shear Stress Transport (SST) turbulence model**.

Advantages of SST:

• Accurate near-wall behavior
• Good prediction of adverse pressure gradients
• Suitable for high-speed aerodynamic flows

Configuration:

```
SOLVER = RANS
KIND_TURB_MODEL = SST
```

---

# Gas Model

The working fluid is modeled as an **ideal gas** representing hot combustion gases.

Parameters:

| Property            | Value      |
| ------------------- | ---------- |
| Gamma               | 1.22       |
| Gas constant        | 377 J/kg·K |
| Chamber pressure    | 1.5 MPa    |
| Chamber temperature | 3200 K     |

---

# Boundary Conditions

### Inlet (Combustion Chamber)

Total pressure and temperature are specified.

```
1500000 Pa
3200 K
```

### Outlet

Static pressure boundary condition representing atmospheric conditions.

```
101325 Pa
```

### Walls

Adiabatic no-slip walls.

```
MARKER_HEATFLUX = (WALL, 0.0)
```

### Symmetry

Axisymmetric nozzle assumption.

```
MARKER_SYM = (SYMMETRY)
```

---

# Numerical Methods

| Method            | Selection      |
| ----------------- | -------------- |
| Convective Scheme | ROE            |
| Time Integration  | Euler Implicit |
| Gradient Method   | Green–Gauss    |
| Linear Solver     | FGMRES         |
| Preconditioner    | ILU            |

Adaptive CFL is used for faster convergence.

```
CFL_NUMBER = 10
CFL_ADAPT = YES
```

---

# Mesh

The simulation uses a structured nozzle mesh.

```
nozzlemesh600.su2
```

The mesh represents the converging, throat, and diverging sections of the rocket nozzle.

---

# Running the Simulation

Inside the case directory run:

```bash
mpirun -np 1 SU2_CFD config.cfg
```

For parallel simulation:

```bash
mpirun -np 4 SU2_CFD config.cfg
```

---

# Simulation Outputs

SU2 generates several output files during execution.

| File             | Description             |
| ---------------- | ----------------------- |
| history.csv      | Convergence history     |
| flow.vtu         | Flow field solution     |
| restart_flow.dat | Restart file            |
| surface_flow.csv | Surface flow quantities |

These files can be visualized in **ParaView**.

---

# Visualization

Flow results can be visualized using **ParaView**.

Typical plots include:

• Pressure contours
• Mach number distribution
• Velocity magnitude
• Density variation

These help analyze the **supersonic expansion behavior inside the nozzle**.

---

# Repository Structure

```
Assignment-2-From-Scratch-Development-of-a-Supersonic-Nozzle

│
├── config.cfg
├── nozzlemesh600.su2
├── history.csv
├── flow.vtu
└── README.md
```

---

# Learning Outcomes

Through this project the following concepts were explored:

• Compressible CFD simulations
• Rocket nozzle flow physics
• RANS turbulence modeling
• SU2 solver configuration
• Numerical schemes for high-speed flows
• Post-processing using ParaView

---

# References

SU2 Official Repository
https://github.com/su2code/SU2

SU2 Documentation
https://su2code.github.io

Anderson, J. D.
*Modern Compressible Flow with Historical Perspective*
