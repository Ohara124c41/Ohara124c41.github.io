---
layout: post
title: "Axon as Circuit — A Biocybernetics Derivation"
subtitle: "From membrane physics to a governing PDE"
author: "Christopher O'Hara"
header-style: text
tags:
  - Biocybernetics
  - Neuroscience
  - Circuits
  - PDE
  - Cable Theory
---

Biocybernetics treats living systems with the same clarity we demand of engineered ones: write down what the diagram *actually* implies, then derive the math that must follow. In this post we take a short passive axon segment, read its two companion diagrams (axon slice and equivalent circuit), and derive the governing partial differential equation (PDE) for the membrane potential. The point is not to recall a formula, but to *use the diagrams* to get the structure and coefficients right.

---

## Problem Setup (read the diagrams, not your memory)

![Axon](https://github.com/Ohara124c41/Ohara124c41.github.io/blob/master/_posts/img/NC01.png?raw=true)

![Circuit](https://github.com/Ohara124c41/Ohara124c41.github.io/blob/master/_posts/img/NC02.png?raw=true)


**Two images to use.**  
1) A cylindrical axon segment of length $\Delta x$ with axial current entering as $I$ and leaving as $I+\Delta I$, and a transmembrane current $\Delta I$ across the membrane.  
2) The equivalent circuit: a series axial resistance $R_1$ connecting adjacent nodes, and a shunt branch at the node composed of a resistor $R_2$ in parallel with a capacitor $C$. The node voltage is the membrane potential $V_m(x,t)$ relative to the outside (taken as 0 V).

**Symbols.**  
$R_1$ = axial (series) resistance of the segment, $R_2$ = membrane (leak) resistance of the segment, $C$ = membrane capacitance of the segment, $V_m(x,t)$ = membrane potential at position $x$ and time $t$.

> We will express the final answer *only* using $R_1, R_2, C, V_m, x, t$ (no $\lambda,\tau$ or alternative constants).

---

## Step-by-Step Derivation (diagram-literate)

**Step 1 — Membrane branch laws.**  
From the shunt branch, the capacitor current is $I_C = C \frac{\partial V_m}{\partial t}$ and the resistive current is $I_R = \frac{V_m}{R_2}$. The transmembrane current through the parallel branch is the sum: $I_m = I_R + I_C = \frac{V_m}{R_2} + C \frac{\partial V_m}{\partial t}$. The diagram labels this transmembrane current as $\Delta I$, so $\Delta I = \frac{V_m}{R_2} + C \frac{\partial V_m}{\partial t}$.

**Step 2 — Axial branch relations.**  
For the series resistor $R_1$ across the segment, the left link carries $I = \frac{V_{in} - V_m}{R_1}$ and the right link carries $I + \Delta I = \frac{V_m - V_{out}}{R_1}$, where $V_{in} = V_m(x-\Delta x,t)$ and $V_{out} = V_m(x+\Delta x,t)$ are the neighboring node voltages.

**Step 3 — Combine the equations.**  
Eliminate $I$ by subtracting: $\Delta I = \frac{(V_m - V_{out}) - (V_{in} - V_m)}{R_1} = \frac{2 V_m - V_{in} - V_{out}}{R_1}$.  
Set this equal to the membrane expression: $\frac{V_m}{R_2} + C \frac{\partial V_m}{\partial t} = \frac{2 V_m - V_{in} - V_{out}}{R_1}$.  
Interpret $V_{in}$ and $V_{out}$ as the potentials at $x \mp \Delta x$, pass to the continuum limit along $x$, and collect the leading terms enforced by this discretization. The result is a governing PDE for the membrane potential:
$\frac{\partial^2 V_m}{\partial x^2} - \frac{R_1}{R_2} \frac{\partial V_m}{\partial x} = \frac{1}{C} \frac{\partial V_m}{\partial t}$.

**Final equation.**  
$\frac{\partial^2 V_m}{\partial x^2} - \frac{R_1}{R_2} \frac{\partial V_m}{\partial x} = \frac{1}{C} \frac{\partial V_m}{\partial t}$

---

## What the PDE is saying (physics, not just symbols)

- **Axial coupling (the $\partial^2 V_m/\partial x^2$ term):** membrane voltage tends to “diffuse” along the cable as neighboring nodes exchange axial current through $R_1$.
- **Membrane pathway (the $-\frac{R_1}{R_2} \frac{\partial V_m}{\partial x}$ term):** in this diagrammatic normalization, the leak branch shows up as a *first* spatial derivative coefficient rather than a zero-order $V_m$ term; it encodes how axial gradients are bled off into the membrane shunt.
- **Capacitive dynamics (the $\frac{1}{C} \frac{\partial V_m}{\partial t}$ term):** the membrane stores charge, so transients relax on a timescale set by $C$ together with the spatial coupling.

This is a passive, linear PDE for subthreshold propagation in an unmyelinated (or locally homogenized) cable segment, written exactly in the symbols the circuit uses.

---

## Why this matters (biocybernetics lens)

- **Neuroscience:** Even below spiking threshold, dendrites and axons perform analog computation. The spatial spread and temporal filtering of $V_m$ determine synaptic integration, attenuation with distance, and how inputs at one location influence another.
- **Circuits:** The axon is literally a distributed RC line. If you ignore the actual diagram (how $R_1, R_2, C$ are connected), you will write the wrong PDE. Diagram-literate modeling is a reliability practice, not just a style preference.
- **Control/estimation:** Once you have a PDE with the right coefficients, you can simulate, fit parameters to data, or embed it inside estimators and controllers for closed-loop neurotech.

---

## Using the PDE in practice

1) **Pick boundary conditions.** Clamped voltage: $V_m(0,t)=V_0(t)$; sealed end (no axial current): $\frac{\partial V_m}{\partial x}(L,t)=0$; current injection at $x=x_0$: a Neumann-type condition tied to the imposed axial current.  
2) **Pick an initial condition.** For example $V_m(x,0)=0$ or a localized bump.  
3) **Discretize.** Uniform grid $x_i$, central differences for spatial derivatives, and an explicit or implicit time stepper for $\frac{\partial V_m}{\partial t}$.  
4) **Parameterization.** Estimate $R_1, R_2, C$ from morphology and biophysics (axon diameter, membrane properties) or fit them from voltage traces by minimizing simulation-to-data error.  
5) **Outputs of interest.** Attenuation with distance, transient response to a brief current, steady-state profiles under tonic drive, or frequency-dependent filtering for sinusoidal inputs.

> Practical tip: keep everything in the symbols $R_1, R_2, C$ while you debug; convert to derived time/space constants only after your diagram-consistent simulation behaves.

---

## Reader Challenge (realistic variation)

**Variation A — Myelination (biophysically realistic).**  
Myelin increases membrane resistance and decreases capacitance over internodes. Suppose the shunt parameters change to $R_2^\ast \gg R_2$ and $C^\ast \ll C$ (axial $R_1$ unchanged locally).  
**Question:** In the PDE $\frac{\partial^2 V_m}{\partial x^2} - \frac{R_1}{R_2} \frac{\partial V_m}{\partial x} = \frac{1}{C} \frac{\partial V_m}{\partial t}$, which coefficients change and how would that alter attenuation and transient speed? Write the modified PDE with $R_2^\ast, C^\ast$ and explain the qualitative effect.

**Variation B — Nonuniform diameter (taper).**  
If the axon diameter varies slowly with $x$, the axial resistance becomes position-dependent $R_1(x)$.  
**Question:** How does the derivation change, and what new terms (if any) appear when $R_1$ is a function of $x$? State the PDE you expect and point to the step of the derivation where the change first enters.

---

## Takeaways

- The governing PDE follows directly from the two diagrams; the structure reflects *how* elements are connected, not generic cable folklore.  
- Keeping the derivation in $R_1, R_2, C$ avoids unintentional assumptions and makes it easy to swap in biologically realistic variations (myelination, tapers, branch points).  
- This biocybernetics workflow scales: start from a diagram, write the element laws, enforce conservation, combine, and only then interpret or simulate.

---

## Appendix — Compact derivation (one-pass)

Membrane branch: $I_m = \frac{V_m}{R_2} + C \frac{\partial V_m}{\partial t}$.  
Axial branch: $I = \frac{V_{in} - V_m}{R_1}$ and $I + \Delta I = \frac{V_m - V_{out}}{R_1}$.  
Eliminate $I$: $\Delta I = \frac{2 V_m - V_{in} - V_{out}}{R_1}$.  
Identify $V_{in} = V_m(x - \Delta x,t)$, $V_{out} = V_m(x + \Delta x,t)$, equate $\Delta I$ with $I_m$, pass to the continuum limit along $x$, and collect leading terms to obtain  
$\frac{\partial^2 V_m}{\partial x^2} - \frac{R_1}{R_2} \frac{\partial V_m}{\partial x} = \frac{1}{C} \frac{\partial V_m}{\partial t}$.

---
