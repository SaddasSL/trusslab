# TrussLab 2D

A browser based 2D finite element truss solver. Build a pin jointed truss, apply supports and loads, then solve for nodal displacements, member forces, axial stresses and support reactions. Everything runs client side in a single HTML file.

**Live demo:** https://saddassl.github.io/trusslab/

## Features

* Interactive viewport (Three.js, orthographic) with grid snapping, pan, wheel and pinch zoom
* Tools: select and move, add node, add member, apply support (pin, roller in X or Y), apply load (magnitude and direction), delete
* Solver runs in a Web Worker, so the interface stays responsive
* Stress colouring through a custom shader with per vertex stress attributes: blue for compression, green for zero, red for tension
* Animated, scalable deformed shape with optional undeformed overlay
* Results: max displacement, peak tension and compression, member forces, support reactions, equilibrium residual and static determinacy
* Undo and redo, JSON import and export, four example models

## Method

Direct stiffness method, linear elastic, small displacements.

1. Each member stiffness is assembled as `k = (EA/L) BᵀB` with `B = [-c, -s, c, s]`, where `c` and `s` are the direction cosines.
2. Restrained degrees of freedom are partitioned out and `K_ff u_f = F_f` is solved by Gaussian elimination with partial pivoting.
3. A collapsing pivot is reported as a mechanism, naming the node and direction.
4. Reactions come from `R = K u - F`, and member stress from `σ = (E/L) B u_e`.

Check: a 6 m by 3 m triangle with a 40 kN apex load gives +20.000 kN in the tie and −28.284 kN in each rafter, matching the hand calculation.

## Units

Length in m, force in kN, E in GPa, A in mm². Stress is reported in MPa and displacement in mm. Positive axial force is tension.

## Run locally

Open `index.html` in a modern browser. No build step or install is needed.

## Licence

MIT
