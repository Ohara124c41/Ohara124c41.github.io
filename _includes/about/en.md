> Hic Sunt Automata!

Hi, I am Christopher Aaron O’Hara (_@ohara124c41_), an AI system architect and researcher focused on safety-critical cyber-physical systems, autonomous robotics, and digital-twin platforms. My work spans end-to-end system architecture (requirements to validated deployment), reinforcement learning for decision-making in dynamic environments, and model-based systems engineering for complex, resource-constrained, software-intensive systems. Current interests include human–robot interaction under uncertainty, resilience engineering, certified learning for autonomy, and domain-specific languages for control (IEC 61131-3/PLC) integrated with real-time scheduling and verification.

In recent roles, I have centered my efforts on building the **Space Station OS**, a modular digital-twin ecosystem (ROS 2 + Isaac Sim + URDF validation with Omnigraph) to prototype GNC/ECLSS/EPS/COMM subsystems and to train/control free-flying robots (e.g., Int-Ball/Astrobee) in microgravity scenarios. This includes interface patterns that transform algorithmic outputs (C++/Python/ROS 2 nodes) into simulator actuation while enforcing physical and operational constraints. Complementary work leads industrial AI initiatives: predictive maintenance for high-throughput bottling (fusion of DPCA with BiLSTM-attention; supervised and semi-supervised RUL/health-status pipelines), anomaly detection with strictly separated holdouts to prevent leakage, and dual-head architectures combining unsupervised deviation scoring with labeled anomaly prediction.

Research contributions include dynamic multi-objective reinforcement learning for hazard-aware navigation (**DynaMRPPO**) that integrates global–local planning and information-gain objectives; adaptive sensor/filter management with meta-learning and graph attention for energy- and compute-constrained robots; and risk/awareness metrics aligned with human factors for sociotechnical collaboration. Application domains span space robotics (ISS use cases), industrial inspection (e.g., Boston Dynamics Spot risk-aware navigation), and operations optimization in chemical/nuclear-analog environments. Prior collaborative work includes engagements with **NASA Ames** (airspace separation management), **Siemens** (COGENT generative/concurrent engineering), **ESA**, **CERN**, and **Volvo**. Most recently, I served as a **faculty member/AI researcher at the University of Tokyo (RCAST)**, working projects at the intersection of digital twins, autonomy, and traditional control systems.

Education comprises a **PhD in Aeronautics & Astronautics** (University of Tokyo, AI Lab, 2024), an **EngD in Software Technology** (TU Eindhoven, 2021), MSc degrees in Embedded Systems/Mechatronics/ICT Innovation (TU/e, TU Berlin, NJIT), and an undergraduate background in Philosophy, Science, Technology & Society (Cal Poly Pomona). This interdisciplinary training anchors a practice that unifies formal methods, learning-based control, and human-centered systems engineering.

---

### Selected Projects & Contributions

- **Space Station OS (Digital-Twin Platform):** Modular ROS 2 package ecosystem with Isaac Sim/URDF validation and subsystem interfaces (GNC/ECLSS/EPS/COMM). Emphasizes extensibility, microservice-style boundaries, and CI-ready design for multi-team collaboration.  
- **ISS/Int-Ball Microgravity Simulator:** Low-fidelity but dynamics-faithful environment for safe navigation, task completion, and certified learning under operational constraints (sensor realism, airflow, microgravity).  
- **Adaptive Sensor/Filter Management for Space Robots:** GAT-based fusion with few-shot/meta-learning to reduce energy/CPU usage while maintaining situational awareness; validated on Astrobee-class platforms.  
- **Hazard-Aware Navigation via DynaMRPPO:** Graph-based, multi-reward RL integrating information gain, terrain handling, and hazard avoidance; improved success rates over standard PPO in complex terrains.  
- **Industrial Predictive Maintenance:** Valve-level DPCA features + BiLSTM-attention fusion for anomaly detection and RUL; rigorous holdout by valve, semi-supervised clustering for unlabeled segments, dual-model decision fusion (regressor + classifier).  
- **Risk/Resilience Metrics & Human Factors:** Definitions and metrics aligning robustness/resilience with operator expectations; sociotechnical framing for human–machine teaming in ISS and process-plant analogs.  
- **Generative/Concurrent Engineering (COGENT):** Methods and tooling for large-scale, multi-disciplinary engineering workflows.

---

### Research & Engineering Interests

Programming language design for controls (DSLs for PLCs, static analysis for timing/safety), RL under constraints, multi-agent coordination, certified learning and gray-box hybrid modeling, system identification for digital twins, and MBSE/SysML-inspired architecture artifacts (IBDs, package/object diagrams) to bridge teams across electrical, mechanical, and software disciplines.

---

### Education

- **PhD, Aeronautics & Astronautics (AI Lab)** — University of Tokyo, 2024  
- **EngD, Software Technology** — TU Eindhoven, 2021
- **MEng, Biomedical Engineering** — Colorado State University, 2022  
- **MSc, Mathematics & Theoretical Computer Science (Embedded Systems)** — TU Eindhoven, 2020  
- **MSc, Electrical Engineering & Computer Science (ICT Innovation)** — TU Berlin, 2019  
- **MSc, Electrical Engineering (Mechatronics)** — New Jersey Institute of Technology  
- **BA, Philosophy, Science, Technology & Society** — Cal Poly Pomona, 2015  

---

### Programming Languages Spectrum

Preference increases left→right. Depth increases top→bottom. Versions indicate lower bounds.

|            | Low Preference             | Medium Preference                 | High Preference                         | Very High Preference                 |
|------------|----------------------------|-----------------------------------|-----------------------------------------|--------------------------------------|
| **Expert** |                            |                                   | `MATLAB/Octave`                         | `Python` `C++17+`                    |
| **Proficient** | `LaTeX` `Bash`         | `C11`                             | `Java`                                  |                                      |
| **Working**| `SQL`                      | `JavaScript`                      | `TypeScript` `COBOL`                     | `IEC 61131-3 ST` `Ladder` (PLC)      |
| **Exploring** | `Rust`                  | `Haskell` `OCaml` (DSL prototyping) | `Julia`                                 |                                      |

> *Notes:* ROS 2 is a primary application framework (C++/Python). Familiar with real-time patterns (priority ceiling, rate-monotonic), dataflow models (SDF), and verification-adjacent workflows (tests, property checks) for safety/timing.

---

### Selected Highlights

- **Avatarin (space robotics):** Adaptive sensor-fusion with GAT + meta-learning achieving double-digit reductions in energy/CPU usage on constrained platforms.  
- **Tohoku Enterprise (Spot):** Graph-based, multi-reward navigation increasing success rate over PPO baselines in cluttered, hazard-rich maps.  
- **NEC AIOps:** LLM wrappers and memory-constrained training pipelines on modest hardware.  
- **Shibuya Kogyo (RUL/Anomaly):** 7-feature DPCA + BiLSTM-attention pipeline; strict holdouts by valve; semi-supervised extensions and dual-head modeling (unsupervised deviation + supervised anomaly).  
- **NASA/ESA/CERN/Siemens/Volvo:** Systems-architecture and AI/controls contributions across safety-critical and industrial contexts.  

---

If collaboration involves digital-twin validation, autonomy under constraints, or PLC/DSL-backed controls with verifiable timing and safety, this is the locus of ongoing work.
