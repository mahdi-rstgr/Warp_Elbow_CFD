# Warp Elbow CFD

A 2D incompressible CFD study comparing how obstacle geometry affects wake recovery and pressure drop in channel flow.

This repository contains one notebook:
- rectangle.ipynb

The notebook simulates six obstacle shapes with identical circumradius and compares:
- Wake recovery length
- Pressure drop
- Velocity and streamline fields

## Problem Setup

- Domain: 4.0 m x 1.0 m
- Grid: 160 x 40
- Inlet velocity: 1.0 m/s
- Density: 1.0 kg/m^3
- Dynamic viscosity: 0.02 Pa.s
- Reynolds number: 50
- Obstacle center: (2.0, 0.5)
- Obstacle circumradius: 0.25 m
- Shapes: circle, triangle, square, pentagon, hexagon, dodecagon

## Numerical Method

The solver uses a fractional-step projection method:
1. Advection-diffusion step for intermediate velocity
2. Pressure Poisson solve
3. Velocity correction with pressure gradient

Warp kernels are used for:
- Boundary conditions
- Pressure boundary conditions
- Advection-diffusion update
- Pressure Poisson update
- Velocity correction

## Notebook Workflow

The notebook is organized into these stages:
1. Domain and obstacle geometry setup
2. Warp kernel definitions
3. Simulation pipeline for all shapes
4. Wake recovery analysis
5. Pressure-drop analysis
6. Summary visualization combining all metrics

## Key Metrics

### Recovery metric

At each streamwise location x_i:

E(x_i) = sqrt(<(u(x_i,y)-u_out(y))^2 + (v(x_i,y)-v_out(y))^2>_y) / U_inlet

Recovery length is the distance from obstacle trailing edge to the first sustained location where E(x) stays below tolerance.

### Pressure drop

Delta P = p(x=0, y=H/2) - p(x=L, y=H/2)

## Environment

Recommended:
- Python 3.10+
- NVIDIA Warp
- NumPy
- Matplotlib

If you use conda, a typical setup is:

```bash
conda create -n warp-cfd python=3.10 -y
conda activate warp-cfd
pip install warp-lang numpy matplotlib jupyter
```

## Run

1. Open rectangle.ipynb in Jupyter or VS Code
2. Run cells top to bottom
3. Inspect the final summary figure and printed metrics

## Notes

- The notebook uses a common circumradius and clipping strategy to keep shape comparisons fair.
- The current implementation runs on CPU device in Warp for reproducibility.

## License

Add a license file if you plan public distribution.
