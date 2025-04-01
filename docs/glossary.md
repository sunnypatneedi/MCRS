# MCRS Glossary

This document defines key terms used throughout the MCRS specification.

*   **Medication Change Request (MCR):** The primary data object representing a proposed change to a medication, including details like dosage, frequency, or route.
*   **Proposer:** The individual (e.g., physician, nurse) initiating an MCR.
*   **Verifier:** An individual or role responsible for reviewing an MCR and providing a response (Approve/Reject).
*   **Arbiter/Medication Manager:** A designated individual or role with the authority to resolve conflicts or make final decisions on escalated MCRs.
*   **Consensus:** The state achieved when the required verifiers have responded according to the defined quorum rules (e.g., unanimous approval, majority).
*   **Quorum:** The minimum number and type (role-based) of verifier responses required to reach a decision (Approve/Reject) on an MCR.
*   **State:** The current status of an MCR within its lifecycle (e.g., `PENDING`, `APPROVED`, `REJECTED`, `CONFLICT`, `OVERRIDDEN`).
*   **Conflict:** A state where an MCR cannot be straightforwardly approved or rejected due to contradictory proposals or verifier responses.
*   **Escalation:** The process of forwarding an MCR (often in a `CONFLICT` state) to an arbiter or higher authority for resolution.
*   **Override:** An action taken, typically in emergencies or by authorized personnel, to bypass the standard verification workflow and implement a change immediately.
*   **Criticality Level:** A classification (`critical`, `semi-critical`, `non-critical`) indicating the potential risk associated with the medication change, often influencing the required verification rigor.
*   **Audit Log:** A chronological record of all actions, state changes, and decisions related to an MCR.
*   **FHIR (Fast Healthcare Interoperability Resources):** A standard for exchanging healthcare information electronically.
*   **SMART on FHIR:** An open, standards-based technology platform that enables developers to create apps that can securely run across different healthcare systems.
*   **RxNorm:** A standardized nomenclature for clinical drugs produced by the U.S. National Library of Medicine (NLM).
*   **ATC (Anatomical Therapeutic Chemical):** A drug classification system controlled by the World Health Organization Collaborating Centre for Drug Statistics Methodology (WHOCC).
