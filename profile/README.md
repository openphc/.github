# OpenPHC — Digital Public Infrastructure for Primary Healthcare

> *Data flows. Care doesn't. OpenPHC changes that.*

---

## The Problem

Primary healthcare delivers **80% of essential health services** — yet it remains one of the most fragmented layers of any health system.

Despite strong platforms (OpenMRS, CHT, DHIS2) and interoperability standards (FHIR, OpenHIE), three critical coordination failures persist globally:

| Failure | Reality |
|---|---|
| **Broken care continuum** | 60–70% of high-risk patients identified in communities never receive follow-up at a facility |
| **Fragmented patient data** | Health workers must check 4+ disconnected systems to see a complete picture of one patient |
| **Knowledge lag** | Protocol updates take 18–24 months to reach frontline workers — still propagated via email and PDFs |

The root cause: global digital health has solved *data exchange* but not *care coordination*. Systems can talk. They can't work together.

---

## What is OpenPHC?

**OpenPHC is digital public infrastructure (DPI) purpose-built to close the coordination gap in primary healthcare.**

It is not another EMR. It is not a vertical app. OpenPHC provides the connective tissue between existing systems — transforming disconnected digital tools into unified care delivery engines, built entirely on open standards with no vendor lock-in.

```
OpenPHC = Where Data Flows Become Care Journeys
```

---

## The Three Building Blocks

OpenPHC is modular. Countries can adopt one, two, or all three building blocks based on their specific gaps — each works independently with existing national systems.

### 1. Care Coordination Engine (CCE)
**Orchestrates multi-step care pathways across systems**

The CCE ensures no patient, task, or handoff falls through the cracks. It automates referrals, follow-ups, and escalations using FHIR-native workflows — coordinating care journeys across community health workers, facilities, and program managers.

![CCE Architecture — Fully Distributed, Beckn-Style](./profile/assets/cce-architecture.png)

The CCE uses a fully distributed, Beckn-style architecture: each health system runs its own **Edge Coordinator** that can discover, send, receive, and acknowledge coordination messages directly peer-to-peer over an **Open Coordination Protocol Network** — no central gateway or routing authority. Observability is an optional passive subscriber, never a mediator.

- Executes FHIR `PlanDefinition` and manages `CarePlan`/`Task` resources across systems
- Routes through OpenHIM for authentication and audit logging
- Embeds into partner applications via SDKs
- Adds new disease workflows in days, not weeks

*Example: A CHW screens a diabetic patient → CCE creates a referral task in the facility EMR → notifies the CHW when the visit occurs → schedules follow-up for medication adherence → reports outcomes to DHIS2. Automatically.*

### 2. Primary Health Profile (PHP) Composer
**Gives every provider a complete patient view at the point of care**

A stateless FHIR Composition Service that federates real-time queries across multiple systems — without storing or duplicating data. Health workers see complete patient context in one view instead of switching between systems.

- Queries OpenMRS, DHIS2, SHR, CHT, and other sources simultaneously
- Returns PHC-specific summaries tailored to clinical context
- Configurable minimal data elements by demographics, risk status, or care setting
- Pure composition: no data is stored, no migration required

### 3. Knowledge Libraries (KL)
**Governs and distributes clinical intelligence as infrastructure**

Converts static protocols and PDFs into living, machine-readable intelligence. Think Git for clinical knowledge — versioned, governed, and distributed through standard FHIR APIs.

- Versions and distributes `FHIR Library`/`PlanDefinition` resources via standard APIs
- Tracks adoption, dependencies, and updates across the health ecosystem
- Supports approval workflows and subscription-based automated updates
- Vector-database ready, enabling safe and governed AI application deployment

---

## Architecture Principles

- **FHIR R4** for all clinical data exchange
- **OpenHIE architecture** with OpenHIM as the interoperability layer
- **CQL** for clinical logic
- **Configuration-driven** — workflows, composition rules, and knowledge content are stored externally, not hardcoded
- **No proprietary protocols.** No vendor lock-in. Countries control content; OpenPHC provides infrastructure.

While optimized for primary healthcare, all three building blocks use generic standards that work across all care levels — hospital surgical pathways, emergency coordination, specialty referrals.

---

## SmartCare — Reference Platform

**SmartCare** is the reference implementation that demonstrates how OpenPHC building blocks integrate with a country's existing digital health ecosystem. It provides concrete, adaptable patterns for other implementers.

Current SmartCare deployments are active in **Bangladesh** (in partnership with BRAC and the Ministry of Health), addressing fragmented patient data and AI governance for hypertension and maternal health pilots.

---

## Repositories

The repositories in this org implement the **Care Coordination Engine** — OpenPHC's first building block — as a suite of interoperable microservices:

| Repository | Description |
|---|---|
| [`cce-collector-service`](https://github.com/openphc/cce-collector-service) | Collects events and triggers from connected health systems |
| [`cce-compliance-service`](https://github.com/openphc/cce-compliance-service) | Validates care pathway compliance against FHIR PlanDefinitions |
| [`cce-scheduler-service`](https://github.com/openphc/cce-scheduler-service) | Schedules and manages follow-up tasks across care journeys |
| [`cce-intelligence-service`](https://github.com/openphc/cce-intelligence-service) | Applies clinical intelligence to pathway decisions |
| [`cce-insights-service`](https://github.com/openphc/cce-insights-service) | Aggregates coordination metrics and program outcomes |
| [`cce-insights-ui`](https://github.com/openphc/cce-insights-ui) | Dashboard for care coordination analytics |
| [`cce-data-pipeline`](https://github.com/openphc/cce-data-pipeline) | Data ingestion and transformation pipeline |
| [`fhir-cce-emitter-adaptor`](https://github.com/openphc/fhir-cce-emitter-adaptor) | Emitter adaptor for FHIR-native systems |
| [`openhim-cce-emitter-adaptor`](https://github.com/openphc/openhim-cce-emitter-adaptor) | Emitter adaptor for OpenHIM interoperability layer |
| [`openmrs-cce-emitter-adaptor`](https://github.com/openphc/openmrs-cce-emitter-adaptor) | Emitter adaptor for OpenMRS deployments |
| [`deploy-scripts`](https://github.com/openphc/deploy-scripts) | Scripts for deploying the CCE stack to server environments |

---

## Standards & Governance

OpenPHC contributes back to the global digital health ecosystem:

- **FHIR Implementation Guides** for PHC care coordination patterns
- **OpenHIE community process** contributions for workflow orchestration layer specification
- **CDS Hooks extensions** for PHC-specific clinical decision support

Governance includes a technical steering committee, clinical advisory board (aligned with WHO SMART Guidelines), and a country implementation forum — ensuring OpenPHC serves ecosystem needs through transparent, community-driven development.

---

## Who We Are

OpenPHC is built by **[Medtronic LABS](https://medtroniclabs.org)**, a nonprofit focused on last-mile healthcare delivery. We partner with Ministries of Health, global health organizations, and implementers across Africa and South Asia to deploy OpenPHC where it's needed most.

Active pilots and deployments: **India** · **Bangladesh** · **Kenya** · **Rwanda**

---

## Get Involved

OpenPHC is open infrastructure for the global digital health community.

- Explore the repositories and open issues
- Reach out to collaborate on a country deployment
- Contribute to FHIR Implementation Guides and standards work

*The question isn't whether coordination challenges exist in PHC — every country experiences broken care continuums, fragmented data, and slow knowledge propagation. The question is whether digital public infrastructure can address these gaps while integrating with existing investments rather than creating new fragmentation. We believe it can.*
