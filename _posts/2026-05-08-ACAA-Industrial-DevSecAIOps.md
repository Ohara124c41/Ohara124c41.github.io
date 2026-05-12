---
layout: post
title: "Assurance-Centered Agentic AIOps for Industrial DevSecAIOps"
subtitle: "Contested orchestration, policy gates, and local-cloud OT control planes"
author: "Christopher O'Hara"
date: 2026-05-08
header-style: text
tags:
  - Cybersecurity
  - DevSecAIOps
  - OT
  - AIOps
  - Governance
  - Industrial
  - Agentic AI
---

> **Purpose.** This post summarizes the public-facing architecture behind my integrated industrial application project: an assurance-centered agentic AIOps artifact for IIoT/OT operations. The repository is here: [integrated-industrial-application-acaa](https://github.com/Ohara124c41/integrated-industrial-application-acaa).

---

## From AIOps to Assurance-Centered AIOps

AIOps is usually sold as a speed story: detect incidents faster, generate root-cause narratives faster, route tickets faster, and recover faster. Speed matters, but in industrial and OT environments speed is not enough. A fast recommendation that violates policy, ignores safety context, or hides responsibility is not an improvement. It is a new failure mode.

This project starts from a different assumption: industrial AIOps needs assurance. The system should not only produce a recommendation. It should preserve evidence, respect policy gates, expose competing rationales, and log responsibility. That is the difference between an automation demo and a cyber-physical governance artifact.

The repository integrates several upstream streams:

- vulnerability prior context from KEV/NVD-style signals,
- telemetry risk profiles and prevalence context,
- generated RCA narratives with quality and safety tags,
- policy-gated multi-agent decision orchestration,
- local-cloud plugin contracts and control-plane emulation,
- and explicit interface contracts for integration.

The result is less like a single model and more like an adjudication layer for industrial incidents.

---

## The Industrial Problem: Recommendations Have Consequences

In a typical IT setting, a bad recommendation may cause downtime, ticket churn, or rework. In an OT setting, the recommendation may interact with production safety, physical equipment, maintenance schedules, network segmentation, and operator authority. That changes the architecture.

The question becomes:

> How can an agentic system reason about incidents without silently exceeding its authority?

My answer in this project is contested orchestration. Instead of asking one model or one branch to produce the answer, the system can compare branches, record rationales, and use a meta-adjudication layer constrained by policy. The architecture allows advisory intelligence, but it keeps deterministic selection gates where safety and governance require them.

The hard invariant is simple:

```text
policy-failing incidents are forced to final_recommendation='escalate'
```

That is not glamorous, but it is exactly the kind of rule industrial systems need. If the policy says the system is outside autonomous authority, the agent should not argue its way into action.

---

## Contested Orchestration

The contested-orchestration pattern is useful because incident interpretation is rarely singular. One branch may emphasize vulnerability exposure. Another may emphasize telemetry prevalence. Another may emphasize RCA narrative quality, safety tags, or operational constraints. In a naive agentic workflow, these perspectives can collapse into one fluent answer too early.

In the ACAA design, branch outputs remain inspectable. Meta-selection can compare them, but the process preserves the fact that multiple interpretations existed. That matters for auditability and for human review. If a human-in-the-loop override occurs, the system should know:

- what the original branch recommended,
- why the meta-layer selected or rejected it,
- whether the override stayed inside policy bounds,
- and how responsibility was logged.

This is cyber governance applied to agentic systems. The interesting part is not merely "an LLM was used." The interesting part is whether the orchestration creates a defensible decision record.

---

## Local-Cloud OT Control Plane

The project also includes a local-cloud plugin architecture. That piece matters because industrial systems often live between local constraints and cloud-scale analytics. Edge/local control planes care about latency, availability, data locality, and failure drills. Cloud services may provide richer storage, model execution, or cross-site analysis. The system needs a contract between these layers.

The local-cloud runtime uses plugin contracts, registry patterns, storage materialization, and failure-drill concepts. In practice, that means the architecture can reason about packets, outputs, local summaries, and persistence artifacts without assuming one monolithic platform.

Generated outputs include integrated packets, branch packets, meta decisions, responsibility logs, local-cloud summaries, and local materializations such as SQLite or optional Parquet. That output shape is intentional. Industrial assurance requires more than the final answer. It needs the traces that explain how the final answer came to exist.

---

## Threat Model as Architecture, Not Afterthought

The repository includes a threat-model artifact because agentic AIOps itself becomes part of the attack and failure surface. It can be wrong. It can be overconfident. It can be prompted into unsafe rationale. It can receive incomplete upstream context. It can normalize repeated bad recommendations if the evaluation layer is weak.

For industrial cybersecurity, I think the model should be treated as a participant in the control environment. That means the system should ask:

- What can the agent decide?
- What must be escalated?
- What data contracts are trusted?
- What logs are immutable enough for review?
- What happens if branch rationales disagree?
- What happens if a human override conflicts with policy?

This is where agentic AI starts to resemble classical systems engineering again. You define interfaces, constraints, invariants, logs, failure modes, and authority boundaries.

---

## Why This Matters for Defense-Adjacent Cyber Work

Defense-adjacent cyber work often lives in the uncomfortable space between operational urgency and governance discipline. Systems must respond quickly, but they also need authority boundaries, evidence trails, responsibility, and policy compliance. That is especially true for industrial, logistics, manufacturing, and infrastructure contexts where cyber events can move into physical consequences.

The ACAA project is a public demonstration of the architecture I would want in that kind of environment:

1. Integrate vulnerability and telemetry context.
2. Generate incident narratives, but do not trust narrative fluency alone.
3. Compare contested branches.
4. Enforce policy gates deterministically.
5. Preserve human override boundaries.
6. Log responsibility.
7. Materialize outputs locally for audit, replay, and failure analysis.

The emphasis is not "replace the operator." It is "make machine assistance accountable enough that an operator can use it."

---

## Closing Thought

Agentic systems will keep entering security operations, industrial monitoring, and governance workflows. The question is whether we let them arrive as opaque assistants or engineer them as accountable control-plane participants.

My preference is the second path. If a system touches operational risk, it should leave behind a trail: contracts, packets, decisions, blocked overrides, escalations, and evidence. That is what assurance-centered AIOps is trying to become.
