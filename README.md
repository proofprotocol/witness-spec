> **Zenodo DOI:** [10.5281/zenodo.21379780](https://doi.org/10.5281/zenodo.21379780) — Published 2026-07-15

# PP-SPEC-005 · Witness Protocol Specification

**Document ID:** PP-SPEC-005  
**Version:** 0.1 - Draft  
**Status:** Draft  
**License:** CC BY 4.0  
**Maintained by:** Proof Economy™ Standards Alliance (PESA)  
**Repository:** https://github.com/proofprotocol/witness-spec  
**Published:** 2026-07-13  

---

## Abstract

This specification defines the Witness Protocol: the requirements for independent observation and attestation of a Proof Protocol™ benchmark run. A valid Certified Run requires an independent witness. This specification defines who qualifies as a witness, what they must observe, and what they must attest.

The witness is the answer to the question: who watched the watcher?

---

## Status of This Document

Draft. Subject to change before v1.0.

---

## Table of Contents

1. [Motivation](#1-motivation)
2. [Witness Eligibility](#2-witness-eligibility)
3. [Witness Obligations](#3-witness-obligations)
4. [Witness Attestation Record](#4-witness-attestation-record)
5. [AgenTwin™ as Automated Witness](#5-agentwin-as-automated-witness)
6. [Disqualifying Conditions](#6-disqualifying-conditions)
7. [Conformance](#7-conformance)
8. [Authors](#8-authors)

---

## 1. Motivation

A benchmark run without an independent witness is a demonstration. The vendor controls the environment, selects the cases, runs the tool, and reports the results. Every step is inside the vendor trust boundary.

Cryptographic receipts make the evidence tamper-evident after the fact. They do not make the run independent. A compromised or cherry-picked run can produce perfectly valid cryptographic receipts.

The witness requirement closes this gap. An independent witness observes the execution conditions, confirms the pre-commitment was honored, and attests that the run was conducted as claimed. Without a witness, a Certified Run is not certified.

---

## 2. Witness Eligibility

A witness must satisfy all of the following:

- No commercial relationship with the vendor under test at the time of the run
- No financial interest in the outcome of the run
- No governance role in any body that sets conformance criteria for the category being tested
- Sufficient technical competence to observe and understand the execution conditions
- Willing to disclose identity and affiliation in the witness attestation record

HACKERverse serving as witness for a run it administers satisfies the independence requirement provided HACKERverse has no commercial relationship with the vendor under test. HACKERverse's structural independence as a disinterested certifying authority is the foundational moat of the Proof Economy™.

---

## 3. Witness Obligations

During a Certified Run the witness must:

1. Confirm the NIST Beacon pulse used for pre-execution commitment was retrieved before execution began
2. Confirm the benchmark corpus used matches the declared corpus reference
3. Observe that the vendor had no access to test cases before the pre-commitment pulse was published
4. Confirm the execution environment matches the declared posture in the ProofBundle™
5. Confirm the verifier was run against the unmodified receipt chain
6. Sign and submit the witness attestation record

---

## 4. Witness Attestation Record

```json
{
  "witness_identity": "string",
  "witness_affiliation": "string",
  "commercial_relationship_to_vendor": "none",
  "financial_interest_in_outcome": false,
  "governance_role_in_category_body": false,
  "observations": {
    "nist_pulse_confirmed_pre_execution": true,
    "corpus_reference_confirmed": "URI",
    "vendor_had_no_pre_run_case_access": true,
    "execution_posture_matches_declaration": true,
    "verifier_run_on_unmodified_chain": true
  },
  "attestation_timestamp": "RFC 3339 UTC",
  "attestation_statement": "I observed the execution of this benchmark run and attest that the conditions described above were satisfied.",
  "witness_signature": "Ed25519 hex signature over canonical JSON of this record"
}
```

The `witness_signature` is optional in v0.1 but required for ProofStamp™ certification.

---

## 5. AgenTwin™ as Automated Witness

AgenTwin™ is the automated witness layer for continuous agent behavioral attestation. In the context of the Witness Protocol:

- AgenTwin™ operates outside the agent trust boundary
- It observes agent actions in real time without access to the agent's credentials or signing keys
- It assembles ProofBundles from receipts, pubkeys, and verifier outputs
- It produces a machine-generated witness attestation record for each bundle

AgenTwin™ automated witness attestation satisfies the witness requirement for T2 trust tier verification under PP-A2P™. T3 ProofStamp™ certification requires a human witness for the initial Certified Run.

---

## 6. Disqualifying Conditions

A witness is disqualified if any of the following are true at the time of the run:

- The witness is employed by or under contract with the vendor under test
- The witness holds equity in the vendor under test
- The witness holds a voting seat on a standards body that governs the category being certified
- The witness reviewed or had access to the benchmark cases before the pre-commitment pulse

A disqualified witness makes the run non-conformant regardless of the cryptographic validity of the receipts.

---

## 7. Conformance

A Certified Run is conformant with the Witness Protocol if:

- The witness satisfies all eligibility requirements in Section 2
- The witness fulfilled all obligations in Section 3
- A complete witness attestation record is included in the ProofBundle™
- The witness has no disqualifying conditions under Section 6

---

## 8. Authors

Craig Ellrod, Founder & CEO, Nebulonium, Inc. (d/b/a HACKERverse)  
Castle Rock, Colorado  
2026-07-13

---

*CC BY 4.0 - Attribution to Craig Ellrod / Nebulonium, Inc. required.*
