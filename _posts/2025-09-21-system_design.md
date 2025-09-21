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

Finite State Machines (FSMs) and logic controllers are core abstractions in system design. They appear everywhere: industrial PLCs, avionics control loops, robotics, automotive ECUs. These structures provide a disciplined way to reason about what the system should do when inputs change over time. This post develops a compact example I use in teaching, where students can see both the state-level abstraction and the low-level logic that enforces decisions.

---

### FSM

**FSM Diagram:**  
![FSM Diagram](https://github.com/Ohara124c41/Ohara124c41.github.io/blob/master/_posts/img/FSM.jpg?raw=true)


The first figure shows a Moore FSM with three states:

- **IDLE**: outputs $(T, A) = (0, 0)$  
- **RUN**: outputs $(T, A) = (1, 0)$  
- **HOLD**: outputs $(T, A) = (0, 1)$  

The transitions follow the rules:

```
if FAULT=1 → HOLD
 else if MODE=1 → RUN
 else → IDLE

if IDLE = 1 → UPDATE
 ++ t
if IDLE = 1 ∧ t = 3
 let MODE = 1 
```

In addition, we model a simple watchdog-like feedback: if the FSM remains in IDLE for three consecutive updates, an **UPDATE counter** increments until $t = 3$. At that point, the FSM forces $MODE = 1$ internally and transitions to RUN. This mechanism is not unlike what one might implement with flip-flops or timers in real circuits—hardware that monitors “excessive idleness” and forces a task ready signal.


---

### Logic Controller

**Logic Diagram:**  
![Logic Diagram](https://github.com/Ohara124c41/Ohara124c41.github.io/blob/master/_posts/img/MATI.jpg?raw=true)

The second figure shows the combinational logic controller. Its job is to enforce mask conditions and produce an encoded system code. It receives $(T, A)$ from the FSM and two mask signals:

- **M (MaintenanceLock)**  
- **I (Inhibit)**  

It produces three outputs:

- **B2**: $A + (T \cdot I)$  
- **B1**: $T \cdot \overline{M} \cdot \overline{A}$  
- **B0**: $(T + I) \cdot \overline{A}$  

The three outputs form a binary-encoded system code:

$$
V = 4 \cdot B2 + 2 \cdot B1 + B0
$$

This “system code” is the kind of integer that might be passed to a higher-level scheduler, bus, or diagnostics module. The structure illustrates how FSMs and combinational logic compose naturally: one block captures abstract behavior, the other enforces masking, priorities, and arithmetic encodings.


---

## Worked Example

**Problem statement:**  
Starting at $t=0$, the FSM is in state IDLE with outputs $(T, A) = (0, 0)$. Inputs remain fixed over time: $MODE = 0, FAULT = 0, M = 0, I = 1$.  

Evaluate the FSM and logic through three updates ($t = 1,2,3$). At $t=3$, what is the integer value $V$?

---

### Step-by-step solution

**Step 1:**  
At $t=0 \to 1$, the FSM sees $MODE=0, FAULT=0$. It stays in IDLE, so $(T, A) = (0, 0)$.  

**Step 2:**  
At $t=1 \to 2$, the same inputs keep the FSM in IDLE again. Output is still $(0, 0)$.  

**Step 3:**  
At $t=2 \to 3$, the FSM has been IDLE for three cycles. The UPDATE counter forces $MODE=1$, which triggers a transition to RUN. The output becomes $(T, A) = (1, 0)$.  

**Step 4:**  
Logic evaluation at $t=3$:  
- $B2 = A + (T \cdot I) = 0 + (1 \cdot 1) = 1$  
- $B1 = T \cdot \overline{M} \cdot \overline{A} = 1 \cdot 1 \cdot 1 = 1$  
- $B0 = (T + I) \cdot \overline{A} = (1 + 1) \cdot 1 = 1$  
- $V = 4 \cdot 1 + 2 \cdot 1 + 1 = 7$  

---

### Final Answer

`V = 7`

---

### Why this matters

This example highlights several principles that graduate students should recognize in system design:

1. **Feedback and history.**  
   FSMs are often enriched with counters, timers, or flip-flops. Our UPDATE counter is a trivial version of a watchdog timer, which prevents indefinite idleness.

2. **Separation of concerns.**  
   The FSM captures high-level mode behavior, while the logic controller enforces masks and computes codes. This separation makes systems analyzable and verifiable.

3. **Encoding and compositionality.**  
   FSM outputs rarely go directly to actuators. They pass through logic that encodes conditions into integer codes or bus values. This bridges state abstraction with low-level enforcement.

4. **Design realism.**  
   While the diagrams shown are minimal, in practice one could implement the IDLE counter with flip-flops, add edge detection for UPDATE, or include reset logic. Those blocks are not drawn here, but they are the natural hardware companions to the abstract diagrams.

---

Even a compact FSM + logic system like this reveals the core of embedded system design: time, feedback, and deterministic translation from abstract states into concrete codes.

---

### Exercise for readers

As an extension, try recomputing the system code if **FAULT were set to 1 at $t=2$** while other inputs remain the same. How does this affect the FSM path, the logic outputs, and the final value $V$ at $t=3$? What assumptions do you need to make and which verification checks are missing?
