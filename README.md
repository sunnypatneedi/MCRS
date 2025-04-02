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
![image](https://github.com/user-attachments/assets/644f3e04-5906-4705-8d20-66ed2c8c11f2)

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
	•	Post-Event Audit: Once the emergency subsides, the override is reviewed through the standard consensus process, ensuring that the change is reconciled with the patient’s overall medication history.
![image](https://github.com/user-attachments/assets/375fcb5d-2d45-4104-914a-f0329f933d97)
