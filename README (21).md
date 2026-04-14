# ADIC Clinical Submission Audit Demo

**Fix the conditions, implementation, and change history used in submission analyses — so audit requests, regulatory queries, and reproduction demands can be answered on the spot.**

→ **[Try the live demo](https://ghostdrifttheory.github.io/adic-clinical-audit)**

---

## Does this sound familiar?

**After NDA/BLA submission, a reviewer asks: "Please re-run the analysis so we can verify the results."**
No record of which model version was running at the time.

**An internal audit discovers that the AI model was updated during the trial — after submission.**
No change control record. No way to determine which analyses were affected.

**A reviewer asks: "Can you confirm the implementation matches what was specified in the SAP?"**
The documentation is scattered. Preparing a response takes weeks.

These are not edge cases. They are structural gaps that appear when AI enters clinical development without an audit trail built for regulatory use.

---

## What ADIC does

ADIC is not an explainability layer. It does not improve model accuracy.

ADIC fixes the **conditions, implementation, and change history** used in submission analyses, and keeps them in a form that can be handed directly to reviewers, auditors, and third-party statisticians.

Specifically, ADIC produces three artifacts for every analysis run:

| Artifact | What it covers | When you use it |
|---|---|---|
| **SAP Correspondence Table** | Line-by-line match between SAP specification and actual implementation | Responding to reviewer queries about SAP compliance |
| **Execution Log** | Model version hash, random seed, library versions, input data hash, lock status | Demonstrating that the same conditions produce the same results |
| **Environment Specification** | Exact reproduction steps for a third-party statistician to re-run independently | Independent statistical review, regulatory submission packages |

The verification engine checks these three artifacts for internal consistency and emits one of two outcomes:

- **Consistency confirmed** — all three artifacts align; the analysis is reproducible under the recorded conditions
- **Deviation detected — analysis halted** — a model version mismatch or unapproved change was found; the analysis is stopped before SAP-deviant results can enter submission documents

The second outcome is the critical one. It means problems surface **at execution time**, not during post-submission review or inspection.

---

## Try the demo

**[→ Open the demo](https://ghostdrifttheory.github.io/adic-clinical-audit)**

Two scenarios are available:

1. **Consistency check** — SAP aligned, model version locked, analysis reproducible
2. **Change detection** — model version changed during the trial period; unapproved change detected; analysis halted automatically

No data is transmitted. The demo runs entirely in-browser.

---

## Formal foundation

The ADIC framework is described in the preprint:

> Maeki, H. (2026). *Deterministic Replay Verification of Interval Programs over a Finite Primitive Core via Quantifier-Free Integer Certificates.* Zenodo. [https://zenodo.org/records/18897322](https://zenodo.org/records/18897322)

The core mathematical claim: for a fixed primitive set {+, −, ×, inv, sqrt, relu}, verifier acceptance implies the existence of a concrete trajectory and enclosure of all certified specification constraints. Verification cost is O((n + s) · C(b)) — linear in ledger size, deterministic, no solver search.

A Lean formalization of the core lemma is available at [ghostdrifttheory.github.io/adic-lean-proof](https://ghostdrifttheory.github.io/adic-lean-proof).

---

## Scope of this repository

This repository demonstrates the **certificate → audit ledger → verifier (consistency / deviation)** flow for clinical submission analyses.

The implementation covers:
- SAP correspondence table generation
- Execution log with model hash, seed, and library fingerprints
- Environment specification for third-party reproduction
- Automated consistency checking and deviation detection

ADIC does not replace regulatory judgment. It fixes the conditions, records, and change history used in analyses in a form that is auditable and reproducible.

---

## About

**GhostDrift Mathematical Institute** develops formal verification infrastructure for numeric computations in safety-critical systems.

[ghostdriftresearch.com](https://ghostdriftresearch.com/) · [GitHub](https://github.com/GhostDriftTheory)

© 2026 GhostDrift Mathematical Institute.
Research and evaluation use permitted without charge. Commercial use requires explicit license.
