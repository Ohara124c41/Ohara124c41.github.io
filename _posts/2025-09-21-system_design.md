---
layout: post
title: "FSMs and Logic Controllers"
subtitle: "A System Design Course Example"
author: "Christopher O’Hara"
header-style: text
tags:
  - FSM
  - Logic
  - Systems
  - Design
---

Finite State Machines (FSMs) and logic controllers are fundamental abstractions used in industrial PLCs, embedded controllers, robotics, and avionics. The diagrams below illustrate how states, transitions, and combinational logic interact to produce deterministic system codes. This post shows a worked example suitable for a system design course.

---

### FSM

The first figure is a Moore FSM with three states:

- **IDLE**: outputs (T, A) = (0, 0)  
- **RUN**: outputs (T, A) = (1, 0)  
- **HOLD**: outputs (T, A) = (0, 1)  

Transitions follow the rules indicated inside the diagram:  
- If **FAULT = 1**, transition to HOLD  
- Else if **MODE = 1**, transition to RUN  
- Else, remain in IDLE  

Additionally, if the FSM remains in IDLE for successive updates, an **UPDATE counter** advances until `t = 3`. At that time, MODE is forced to 1, triggering a transition to RUN.

**FSM Diagram:**  
![FSM Diagram](/_posts/FSM.jpg)

---

### Logic Controller

The second figure shows the combinational logic controller. It receives inputs **T, A** from the FSM and **M (MaintenanceLock), I (Inhibit)** as mask signals. It produces three outputs:

- **B2**: OR of A with the AND of T and I  
- **B1**: AND of T with the negations of M and A  
- **B0**: AND of the OR gate (T + I) with the negation of A  

These three bits (B2, B1, B0) form an unsigned integer:

\[
V = 4 \cdot B2 + 2 \cdot B1 + B0
\]

**Logic Diagram:**  
![Logic Diagram](/_posts/MATI.jpg)

---

## Worked Example

**Problem statement:**  
Starting at **t = 0**, the FSM is in state **IDLE** with outputs (T, A) = (0, 0). Inputs are fixed over time: **MODE = 0, FAULT = 0, M = 0, I = 1**.  

Evaluate the FSM and logic through three updates (t = 1, 2, 3). At **t = 3**, what is the integer value **V**? Report in the form `V = INT`.

---

### Step-by-step solution

1. **t = 0 → t = 1 (UPDATE):**  
   Inputs: MODE=0, FAULT=0 ⇒ state = IDLE.  
   Output: (T, A) = (0, 0).  

2. **t = 1 → t = 2:**  
   Same inputs ⇒ state = IDLE.  
   Output: (T, A) = (0, 0).  

3. **t = 2 → t = 3:**  
   FSM diagram rule: after three consecutive IDLE updates, MODE is set to 1.  
   Thus at t=3, FSM transitions to RUN.  
   Output: (T, A) = (1, 0).  

4. **Logic evaluation at t = 3:**  
   - B2 = A + (T·I) = 0 + (1·1) = 1  
   - B1 = T·¬M·¬A = 1·1·1 = 1  
   - B0 = (T + I)·¬A = (1 + 1)·1 = 1  
   - V = 4·1 + 2·1 + 1 = **7**  

---

### Final Answer

`V = 7`

---

### Why this matters

This example demonstrates how FSM outputs, mask inputs, and combinational logic interact in time-dependent systems. Even a simple three-state FSM with a feedback rule (MODE forced after idle cycles) illustrates:

1. **Abstraction:** model system behavior as discrete states.  
2. **Compositionality:** separate state evolution (FSM) from enforcement masks (logic).  
3. **Traceability:** map signals from diagram through updates to the encoded integer.  
4. **Verification:** compute deterministically at each timestep.  

Such workflows appear in PLC ladder logic, robotics controllers, and safety-critical industrial systems.  
