---
layout: post
title: "SOX ITGC Control Assurance as a Cybersecurity System"
subtitle: "Evidence, exceptions, threat intelligence, and audit-ready control health"
author: "Christopher O'Hara"
date: 2026-04-18
header-style: text
tags:
  - Cybersecurity
  - GRC
  - SOX
  - ITGC
  - Control Assurance
  - NIST
  - ISO27001
---

> **Purpose.** This post documents a public lab I built to make SOX IT general controls concrete: a simulated financial-systems control environment with evidence packets, deterministic tests, risk scoring, anomaly detection, CISA KEV enrichment, and dashboard-ready reporting. The repository is here: [SOX ITGC Control Assurance Lab](https://github.com/Ohara124c41/sox-itgc-control-assurance-lab).

---

## Why a SOX Lab Belongs in Cybersecurity

SOX is often introduced as an audit or finance topic, but the practical boundary between SOX ITGC and cybersecurity is not clean. Access management, privileged access review, change approval, logging, backup monitoring, and remediation tracking are all cyber-control problems when the systems in scope support internal control over financial reporting.

The interesting engineering question is not simply whether a checklist exists. The useful question is whether the organization can produce evidence that connects:

- risk,
- control objective,
- control activity,
- evidence,
- test result,
- exception,
- deficiency,
- remediation,
- retest,
- and management reporting.

That chain is where control assurance becomes a system. It has data models, workflow states, evidence artifacts, queryable exceptions, severity classifications, dashboards, and increasingly, security enrichment from public threat intelligence. The lab exists because most real audit datasets are protected by confidentiality rules. A simulated substitute lets the architecture be public without pretending to disclose client evidence.

---

## The Control Assurance View

The lab models common ITGC domains for financial systems:

- access provisioning and approval,
- privileged access review,
- terminated-user deprovisioning,
- production change approval,
- independent code review,
- emergency-change retrospective review,
- critical backup monitoring,
- failed-job investigation,
- privileged-action logging,
- and segregation of duties.

The main point is translation. A control objective is not operational until it becomes a data shape that can be tested. For example, "terminated users lose access promptly" needs identity records, employment status, termination dates, access records, system scope, timing thresholds, and a rule that produces pass/fail evidence. Without that translation, assurance remains prose.

![SOX readiness and control risk dashboard](https://github.com/Ohara124c41/sox-itgc-control-assurance-lab/blob/main/screenshots/dashboard.jpg?raw=true)

The dashboard is not a claim of compliance. It is a representation of control health. That distinction matters. A dashboard can help management see readiness, open findings, overdue remediation, or control domains with repeated exceptions. It cannot replace professional judgment, materiality analysis, or an audit opinion.

---

## Risk Model: Transparent Before Fancy

The project deliberately uses a transparent scoring model:

```text
risk_score = inherent_risk * control_criticality * observed_failure_rate
readiness_score = weighted_average(control_pass_rate by control_criticality)
```

This is not a quantitative loss model like FAIR, and it is not a legal conclusion. It is a control-health screening model. In practice, that is often what teams need first: a way to decide where to look, what to retest, and where remediation ownership is lagging.

There is a temptation in governance tooling to make the scoring model mysterious. I prefer the opposite. If a control-risk score cannot be explained to the engineer, auditor, manager, and system owner, then it will not guide behavior reliably. The scoring should be inspectable enough that someone can challenge it.

---

## Deterministic Rules plus Anomaly Detection

SOX evidence needs deterministic rules because audit evidence must be reproducible. If a deployment lacked approval before production release, the test should say so plainly. If a terminated identity still had access beyond the policy threshold, the result should not depend on a model's mood.

But deterministic rules do not answer every question. A strange pattern of access events may be worth investigating even if each individual event passes a narrow rule. A deployment burst, an unusual privilege pattern, or abnormal timing may be an early sign of process drift.

So the lab keeps the two ideas separate:

- deterministic control tests produce auditable evidence,
- lightweight anomaly detection produces investigation hints.

![Deficiency, anomaly, and vulnerability exposure dashboard](https://github.com/Ohara124c41/sox-itgc-control-assurance-lab/blob/main/screenshots/dashboard02.jpg?raw=true)

That separation is important. Machine-learning-style anomaly flags should not quietly become SOX conclusions. They can prioritize investigation, enrich continuous monitoring, or help security teams decide where to ask the next question. The authoritative control result remains the rule-backed evidence path.

---

## Framework Mapping without Losing the Primary Risk

The lab maps SOX ITGC domains to NIST CSF 2.0 and ISO 27001. This is useful because real organizations rarely operate one framework at a time. The same access-control weakness may matter for SOX, NIST, ISO, privacy, and operational resilience.

![NIST and ISO control mapping dashboard](https://github.com/Ohara124c41/sox-itgc-control-assurance-lab/blob/main/screenshots/dashboard03.jpg?raw=true)

The mapping does not mean all frameworks ask the same question. SOX centers on the reliability of financial reporting. NIST and ISO emphasize security governance, protection, detection, response, and continual improvement. GDPR asks a different set of questions about lawful processing, transparency, security, and rights. Mapping is helpful only if the differences stay visible.

This is why the lab treats SOX/ICFR as the primary risk context and uses NIST/ISO as overlays. The result is not a flattened compliance spreadsheet. It is a structured view of how one evidence object may support multiple governance conversations.

---

## Why This Matters for Public-Sector and Defense-Adjacent Work

For public-sector and defense-adjacent environments, the control problem is not just "do we have controls?" It is whether the organization can show that controls operate, exceptions are handled, remediation is tracked, and risk ownership is visible. That is especially important when systems are distributed across cloud services, identity providers, CI/CD pipelines, financial applications, and operational platforms.

The lab is intentionally modest, but the architecture scales:

1. Build a normalized evidence model.
2. Encode deterministic tests.
3. Preserve exception and remediation state.
4. Add public threat-intelligence context.
5. Separate audit conclusions from anomaly triage.
6. Report control health in language that engineering, audit, and management can all understand.

That is the real artifact: not the dashboard alone, but the discipline of turning governance into inspectable system behavior.

---

## Closing Thought

Cybersecurity is often framed around incidents, adversaries, tools, and response. Control assurance asks the quieter question: can the organization prove that its ordinary processes are trustworthy before the incident? For financial systems and regulated environments, that proof has to be engineered.

This project is my attempt to make that engineering visible in a public, reusable form.
