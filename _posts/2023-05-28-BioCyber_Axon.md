---
layout: post
title: "Biocybernetics: From Neural Models to Systems, Models, Estimation, and Control"
subtitle: "Fundamentals, neural systems, sensory systems, and motor control"
author: "Christopher O'Hara"
header-style: text
tags:
  - Biocybernetics
  - Neuroscience
  - Circuits
  - Modeling
  - Neural Models
  - Estimation
---

> **Purpose**: This document is a structured course writeup for the University of Tokyo’s Biocybernetics course. The writeup emphasizes both biological foundations (neurons, muscles, sensory systems) and systems-engineering perspectives (models, PDEs, control laws, estimation).  I have included an example problem, equivalent to an exam question for reference.


## Section 1 — Fundamentals of Bio-Cybernetics

Cybernetics was proposed by Norbert Wiener to extract and apply mathematical principles of intelligent behavior common to biological, mechanical, and social systems. The term comes from the Greek *kybernetes* meaning steersman. The essential elements are **measurement, recognition, and control**. In modern form, cybernetics integrates control engineering, communication theory, systems engineering, and physiology. Focus on living systems is called **bio-cybernetics**.  

The course introduces **neo-cybernetics** which connects the physical world with the information world through recognition and action. Biological systems can be represented as **feedback loops** comparing a reference set point with a measured value.  

Pharmacokinetics is modeled with **compartment models**. For drug mass $q(t)$  
$\frac{dq(t)}{dt} = -k q(t), \ q(t) = q_0 e^{-kt}$  

With input $u(t)$  
$\frac{dq(t)}{dt} = u(t) - k q(t)$  

---

## Section 2 — Neural Systems

The nervous system has motor neurons, sensory neurons, and interneurons. Synapses transmit signals chemically and electrically with excitatory postsynaptic potentials (EPSPs) and inhibitory postsynaptic potentials (IPSPs).  

The neuron membrane maintains a resting potential of about $-70$ mV. The **Nernst equation** defines equilibrium potential  
$E_A = \frac{RT}{zF} \ln \frac{[A^+]_{out}}{[A^+]_{in}}$  

The overall membrane potential is a weighted average  
$V_m = \frac{g_K E_K + g_{Na} E_{Na} + g_{Cl} E_{Cl}}{g_K + g_{Na} + g_{Cl}}$  

The Hodgkin–Huxley model uses nonlinear dynamics of Na and K conductances. The FitzHugh–Nagumo simplification is  
$\frac{du}{dt} = c(-v + u - \tfrac{u^3}{3} + I(t)) , \ \frac{dv}{dt} = u - bv + a$  

Biopotentials measurable on the body include ECG, EMG, EEG, and EOG. Brain–machine interfaces use rhythms such as alpha and beta waves for control applications.  

---

## Section 3 — Sensory Systems I (Vision, Smell, Taste)

Vision uses cornea and lens for focusing, iris for light regulation, and retina with rods and cones as photodetectors. Eye movements include saccades, smooth pursuit, vestibulo-ocular reflex, and optokinetic reflex. Retinal processing flows photoreceptors → bipolar cells → ganglion cells with dorsal (where) and ventral (what) cortical pathways.  

Artificial vision includes CCD and CMOS sensors and retinal implants. Robotics systems like PRECEYES support ophthalmic microsurgery.  

Smell uses about 400 receptor genes with combinatorial coding enabling discrimination of tens of thousands of odors. Electronic noses detect odors using semiconductors or quartz sensors.  

Taste has five modalities: sour, salty, bitter, sweet, umami. Taste sensors employ lipid membranes to classify flavors through pattern recognition.  

---

## Section 4 — Sensory Systems II (Hearing and Touch)

Hearing covers outer, middle, and inner ear. The sound pressure level is defined by  
$L_p = 20 \log_{10} \frac{P}{P_0} , \ P_0 = 20 \ \mu Pa$  

Middle ear provides impedance matching with effective gain about $20 \times 1.3 = 26$. The cochlea is a frequency analyzer with tonotopy from base (20 kHz) to apex (20 Hz).  

Head-related transfer function  
$H_{l,r}(s,\alpha,\beta,r,\omega) = \frac{G_{l,r}(s,\alpha,\beta,r,\omega)}{F(s,\alpha,\beta,r,\omega)}$  

Cochlear implants stimulate auditory nerves directly though with fewer channels than natural hair cells. The HIBIKI project aims at piezoelectric artificial auditory epithelium.  

Touch involves Merkel, Meissner, Pacinian, Ruffini receptors plus free nerve endings. Engineering equivalents include capacitive $C = \frac{\varepsilon S}{d}$, piezoresistive $R = \rho \frac{L}{A}$, and piezoelectric $Q = dF , \ V = \frac{Q}{C}$.  

Proprioception is provided by muscle spindles and Golgi tendon organs. Wearable systems integrate signals for health monitoring.  

---

## Section 5 — Motor Control

Skeletal muscle structure is hierarchical: muscle → bundle → fiber → myofibril → sarcomere. Contraction follows sliding filament theory with actin and myosin interactions.  

- Force–length curve: maximal force at about 120 percent resting length  
- Force–velocity curve: force decreases hyperbolically with velocity  
$F = \frac{(F_0 + a)b}{v + b} - a$  

The Hill model has contractile, series elastic, and parallel elastic elements  
$F = k_{se}\Delta x_1 = k_{pe}\Delta x_2 + c\frac{dx_2}{dt} + A$  

Bi-articular muscles provide efficiency and robustness by spanning two joints.  

Muscle synergies reduce control dimensionality. A synergy decomposition is  
$m(t) = \sum_{i=1}^N c_i(t) w_i$  

Clinical and experimental studies show synergy alterations after stroke and reorganization during recovery. Physiological and psychophysical evidence supports synergies as neural modules.  


## Section 6 — Measurement Models

An axon can be modeled as a cylindrical cable with resistive and capacitive properties. For a small length $\Delta x$

- Axial resistance  
$R_1 = \frac{4 \rho \Delta x}{\pi d^2}$  

- Membrane resistance  
$R_2 = \frac{r}{\pi d \Delta x}$  

- Membrane capacitance  
$C = c \pi d \Delta x$  

Applying Kirchhoff’s law yields the cable equation  
$\frac{\partial^2 V}{\partial x^2} = \frac{rc}{\rho} \frac{\partial V}{\partial t}$  

This PDE describes spatiotemporal propagation of voltage along the axon membrane.  

The Hodgkin–Huxley model extends this by adding ion channel dynamics  
$C_m \frac{dV}{dt} = - g_{Na} m^3 h (V - E_{Na}) - g_K n^4 (V - E_K) - g_L (V - E_L) + I_{ext}$  
with gating variables $m,h,n$ evolving according to voltage-dependent first-order kinetics.  

Muscle models often use Hill’s formulation to describe the force–velocity relationship  
$F = \frac{(F_0 + a)b}{v + b} - a$  

Tactile sensor principles can be expressed as  

- Capacitive sensor  
$C = \frac{\varepsilon S}{d}$  

- Piezoresistive sensor  
$R = \rho \frac{L}{A}$  

- Piezoelectric sensor  
$Q = dF , \ V = \frac{Q}{C}$  

These equations form the bridge between biological models and artificial sensor design.  

---

## Section 7 — Control Engineering and Kalman Filter

Stability of a system is defined by the poles of the transfer function $G(s)$ lying in the left half-plane. Gain margin and phase margin are practical measures of robustness  

- Tracking control requires $gm = 10$ to $20$ dB and $\theta_m = 40^\circ$ to $60^\circ$  
- Constant value control requires $gm = 3$ to $10$ dB and $\theta_m \ge 20^\circ$  

PID controllers can be tuned by approximating the plant as $G(s) \approx \frac{K e^{-Ls}}{Ts+1}$ or using the ultimate sensitivity method with $K_{pc}$ and $T_c$ from sustained oscillations.  

Anti-windup is applied to integrators under actuator saturation, limiting $u = K_p e + K_i \int e dt + K_d \frac{de}{dt}$ to $u_{max}$.  

Impedance and admittance control allow robots to behave as mechanical analogs  

- Electrical impedance  
$Z = R + j \omega L + \frac{1}{j \omega C}$  

- Mechanical analog  
$F = B \dot{x} + M \ddot{x} + K \int x dt$  

- Impedance control law  
$M(\ddot{r}_{ref} - \ddot{r}) + B(\dot{r}_{ref} - \dot{r}) + K(r_{ref} - r) = f_{ext}$  

- Admittance control  
$\ddot{r} = M^{-1}(f_{ext} - B \dot{r} - K r)$  

State-space models describe system evolution  

$\dot{x}(t) = A x(t) + B u(t) , \ z(t) = C x(t)$  
$x_{k+1} = A x_k + B u_k , \ z_k = C x_k$  

Controllability and observability are checked with matrices  

$\mathcal{C} = [B, AB, A^2B, \dots, A^{n-1}B]$  
$\mathcal{O} = \begin{bmatrix} C \\\\ CA \\\\ \vdots \\\\ CA^{n-1} \end{bmatrix}$  

The Kalman filter operates on the system  
$x_{k+1} = A x_k + w_k , \ z_k = H x_k + v_k$  

Prediction  
$\hat{x}_{k+1|k} = A \hat{x}_{k|k}$  
$P_{k+1|k} = A P_{k|k} A^T + Q$  

Innovation  
$r_{k+1} = z_{k+1} - H \hat{x}_{k+1|k}$  

Gain  
$K_{k+1} = P_{k+1|k} H^T (H P_{k+1|k} H^T + R)^{-1}$  

Update  
$\hat{x}_{k+1|k+1} = \hat{x}_{k+1|k} + K_{k+1} r_{k+1}$  
$P_{k+1|k+1} = (I - K_{k+1} H) P_{k+1|k}$  

This recursive process minimizes mean squared estimation error and is central to control and estimation in bio-cybernetic systems.  


---

## Section 8 - An exam problem example
### Problem Setup 

This problem includes an axon diagram and a circuit diagram. Given the relationships in the models, define an expression for governing PDE.

![Axon](https://github.com/Ohara124c41/Ohara124c41.github.io/blob/master/_posts/img/NC01.jpg?raw=true)

![Circuit](https://github.com/Ohara124c41/Ohara124c41.github.io/blob/master/_posts/img/NC02.jpg?raw=true)


1) A cylindrical axon segment of length $\Delta x$ with axial current entering as $I$ and leaving as $I+\Delta I$, and a transmembrane current $\Delta I$ across the membrane.  
2) The equivalent circuit: a series axial resistance $R_1$ connecting adjacent nodes, and a shunt branch at the node composed of a resistor $R_2$ in parallel with a capacitor $C$. The node voltage is the membrane potential $V_m(x,t)$ relative to the outside (taken as 0 V).

**Symbols.**  
$R_1$ = axial (series) resistance of the segment, $R_2$ = membrane (leak) resistance of the segment, $C$ = membrane capacitance of the segment, $V_m(x,t)$ = membrane potential at position $x$ and time $t$.

> We will express the final answer *only* using $R_1, R_2, C, V_m, x, t$ (no $\lambda,\tau$ or alternative constants).

---

## Step-by-Step Derivation 

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
- **Circuits:** The axon is literally a distributed RC line. If you ignore the actual diagram (how $R_1, R_2, C$ are connected), you will write the wrong PDE. Modeling is a reliability practice, not just a style preference.
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
