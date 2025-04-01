# MCRS Specification Overview

This document provides a high-level overview of the Medication Consensus Resolution Squad (MCRS) Data Specification.

## Purpose

The primary goal of MCRS is to standardize the representation and workflow for resolving medication change requests in complex healthcare environments involving multiple caregivers. This enhances patient safety, improves coordination, and ensures interoperability between systems.

## Key Concepts

*   **Medication Change Request (MCR):** The core data object representing a proposed change to a patient's medication regimen.
*   **Proposer:** The caregiver initiating the MCR.
*   **Verifier:** Caregivers responsible for reviewing and approving/rejecting an MCR.
*   **Consensus Workflow:** The defined process for submitting, verifying, resolving conflicts, and finalizing MCRs.
*   **State Management:** Tracking the status of an MCR (e.g., PENDING, APPROVED, REJECTED, CONFLICT, OVERRIDDEN).
*   **FHIR Alignment:** Mapping MCRS concepts to standard HL7 FHIR resources.

## Specification Modules

*   [Core Specification](./modules/mcrs-core.md): Details of the MCR data model.
*   [Workflows](./modules/mcrs-workflows.md): Explanation of the consensus and resolution processes.
*   [FHIR Mappings](./modules/mcrs-fhir-mappings.md): How MCRS aligns with FHIR.
*   [Glossary](./glossary.md): Definitions of key terms.

## Diagrams

*   [Entity Relationship Diagram](./diagrams/entity_relationship_diagram.png)
*   [Workflow Diagram](./diagrams/workflow_diagram.png)

(Diagrams need to be created and added)
