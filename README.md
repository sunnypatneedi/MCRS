# MCRS
Medication Consensus Resolution Squad (MCRS) Data Specification.

## Overview

This repository contains the open-source data specification for the Medication Consensus Resolution Squad (MCRS). The MCRS spec defines a standardized way to represent Medication Change Requests (MCRs) and their associated resolution workflows, particularly in multi-caregiver scenarios.

## Purpose

*   **Standardize Data:** Provide a common format for MCRs and resolution processes.
*   **Improve Interoperability:** Facilitate seamless data exchange between healthcare systems (EHRs, SMART on FHIR apps).
*   **Enhance Safety:** Address conflicting medication instructions via a structured consensus workflow.
*   **Support Compliance & Analytics:** Define schemas for audit logs and notifications.
*   **Align with FHIR:** Integrate with HL7 FHIR standards where applicable.

## Key Components

*   **Documentation (`/docs`):** Human-readable specification details, workflows, and FHIR mappings.
*   **Schemas (`/schemas`):** Machine-readable definitions (JSON Schema, Protobuf).
*   **Examples (`/examples`):** Sample MCR payloads in JSON and YAML.

## Getting Started

Refer to the documentation in the `/docs` directory for detailed information on the specification, data models, and workflows.

## Contributing

We welcome contributions! Please see the `CONTRIBUTING.md` file for guidelines.

A mockup of a provider-facing application built with MCRS.
![image](https://github.com/user-attachments/assets/b2475522-72b0-4bc3-987b-d0ceb4d9de64)

A mockup of a patient-facing application built with MCRS.
![image](https://github.com/user-attachments/assets/01f608ac-e022-4ce5-862c-b274313350ce)

Scenario:
An elderly patient in a longevity care program has been managed for decades by a rotating team of caregivers.
How MCRS Helps:
	•	Transparency Over Time: All medication changes—initiated, reviewed, and approved over many years—are logged with detailed rationales and verifiable digital signatures.
	•	Safe Transitions: When a new care team takes over, MCRS provides a comprehensive history of changes, ensuring that critical updates (e.g., dosage adjustments based on genomic or biomarker data) are clearly understood, reducing the risk of errors in long-term care management.
![image](https://github.com/user-attachments/assets/53b70fca-926e-4953-9f30-bef54c0d9361)

Scenario:
A patient receives personalized, precision care where treatment is continuously adjusted based on genomic profiles and real-time biomarker monitoring.
How MCRS Helps:
	•	Multidisciplinary Consensus: Multiple specialists (e.g., geneticists, oncologists, pharmacists) can propose and verify tailored medication adjustments.
	•	Conflict Resolution: If different experts suggest varying regimens for a targeted therapy, MCRS triggers a consensus process, merging proposals or escalating the conflict until a single, optimized treatment plan is reached.
	•	Traceability: Detailed audit logs capture the rationale behind each change, ensuring that personalized treatments are both safe and accountable.
![image](https://github.com/user-attachments/assets/7c5dc32a-f599-4062-a07a-b1013f4372d7)

Scenario:
Primary care physicians oversee patients with multiple chronic conditions, often coordinating with external specialists and community pharmacists.
How MCRS Helps:
	•	Streamlined Coordination: MCRS centralizes all medication change requests and approvals, ensuring that recommendations from different providers (e.g., adjustments for diabetes or hypertension) are consistently reconciled.
	•	Interoperability: By integrating with diverse EHR systems and mapping to FHIR resources, MCRS maintains a synchronized view of the patient’s medication regimen, reducing the risk of conflicting instructions across platforms.
	•	Efficient Verification: A streamlined verification process allows routine changes to be approved quickly, while still enforcing strict review for high-risk adjustments.
![image](https://github.com/user-attachments/assets/084584c5-af2f-436d-aef9-f951dd8ca086)

Scenario:
In a specialized clinic (e.g., oncology or cardiology), medication changes are high-stakes and require rigorous review.
How MCRS Helps:
	•	Hierarchical Verification: Critical medications (such as chemotherapy agents or high-risk cardiac drugs) require unanimous approval from a designated set of verifiers (lead physician, specialist, pharmacist), ensuring that every change is thoroughly vetted.
	•	Auditability: Each state change—from proposal to final override—is recorded, providing a clear chain-of-custody for decision-making and compliance purposes.
	•	Integrated Communication: Real-time notifications ensure that all stakeholders, including secondary reviewers, are immediately informed of changes, fostering coordinated care even when multiple EHR systems are involved.
![image](https://github.com/user-attachments/assets/336982cf-d852-4cb6-b300-cccc5706a0a9)

Scenario:
A patient presents in an urgent care setting with an acute adverse reaction, necessitating immediate modification of their medication regimen.
How MCRS Helps:
	•	Emergency Override: In critical situations (e.g., anaphylaxis or acute cardiac events), a caregiver can trigger an emergency override that updates the medication instructions immediately while logging the override for later review.
	•	Rapid Notification: The override is broadcast in real time to all relevant caregivers to ensure that every member of the care team is aware of the change.
	•	Post-Event Audit: Once the emergency subsides, the override is reviewed through the standard consensus process, ensuring that the change is reviewed and reconciled appropriately.

## Frequently Asked Questions (FAQ)

**1. Why is the MCRS specification needed? How does it complement existing standards like FHIR or EHR reconciliation tools?**
   - While FHIR provides robust data exchange standards and EHR tools handle internal reconciliation, MCRS specifically addresses the coordination challenge in multi-caregiver environments. It defines a structured consensus protocol with verification and conflict resolution rules to ensure medication changes proposed across different systems or organizations are consistent, transparent, and safe *before* they are finalized.

**2. How does the MCRS specification ensure medication changes are synchronized and conflicts resolved?**
   - The spec defines a state model (`PENDING`, `APPROVED`, `REJECTED`, `CONFLICT`, etc.) and mandates tracking changes via an `audit_log`. It outlines standard workflows for proposing changes, assigning verifiers, checking for consensus based on configurable rules (e.g., quorum, criticality), and escalating detected conflicts (e.g., simultaneous contradictory proposals) for arbitration. Interoperability is achieved through defined mappings to standard resources (like FHIR) and recommending standardized identifiers.

**3. What consensus mechanisms does the MCRS specification define?**
   - The specification proposes a role-based verification system. The exact rules (e.g., unanimous approval for critical medications, majority for non-critical) are intended to be configurable by the implementing system, but the spec provides the framework. It defines verifier statuses (`APPROVED`, `REJECTED`, `NEED_MORE_INFO`) and requires tracking these responses to determine if consensus is reached or if a conflict state exists.

**4. How does the MCRS specification handle different medication terminologies?**
   - To ensure accuracy and interoperability, the specification recommends using standardized medication identifiers (like RxNorm and ATC codes) in the `rxnorm_code` and `atc_code` fields, alongside the human-readable `medication_name`. This allows systems using different local terminologies to map to a common standard for comparison and verification.

**5. What FHIR resources does the MCRS specification map to, and how are extensions handled?**
   - The spec is designed for FHIR interoperability. Core MCRS concepts map naturally to FHIR resources like `MedicationRequest` (the proposed change), `Provenance` (audit trail), `Task` (workflow steps), and `CommunicationRequest` (notifications). The spec includes an `extensions` field and anticipates the need for specific FHIR Profiles (e.g., defining `x-mcrs-criticality` or `x-mcrs-state` extensions on FHIR resources) to capture MCRS-specific details not present in the base FHIR standards. A dedicated `mcrs-fhir-mappings.md` document details these relationships.

**6. How does the MCRS specification support different user roles and permissions?**
   - The spec includes `proposer` and `verifier` objects, each with `user_id` and `role` fields. While defining a basic set (e.g., physician, pharmacist, nurse), the specification is designed to be extensible, allowing implementing systems to define more granular roles (e.g., specialist, arbiter) and implement Role-Based Access Control (RBAC) to govern who can perform specific actions (propose, verify, override) based on role and context (like medication criticality).

**7. How is the MCRS specification designed for integration with EHRs (e.g., via SMART on FHIR)?**
   - The specification focuses on the data model (JSON Schema, Protobuf) and the consensus workflow logic. Integration into EHRs is envisioned via defined mappings (especially to FHIR) and standard protocols. SMART on FHIR is a natural fit, enabling secure, contextual launch of MCRS-aware applications within an EHR to allow users to interact with MCRs (propose, review, approve) directly within their existing workflow, leveraging OAuth2 for security.
