# AI Disclosure & Transparency Statement

**Project:** Responsive Virtual Production Framework (RVPF)

**Author & Principal Investigator:** Olaf Erler


**Context:** Academic Research, Open-Source Middleware & Higher Education (HAW NRW)

**Normative Compliance:** Conforming to Committee on Publication Ethics (COPE), IEEE, ACM, and DFG Guidelines on Generative Artificial Intelligence in Research and Software Engineering

## 1. Scope & Purpose of Generative AI Usage

During the conceptualization, formalization, and documentation phases of the Responsive Virtual Production Framework (RVPF), Generative Pre-trained Transformers and Large Language Models (LLMs)—specifically OpenAI ChatGPT and Google Gemini —were utilized as cognitive, structural, and linguistic research tooling.

The application of LLMs was strictly limited to non-autonomous assistive workflows:

- **Linguistic Translation & Tone Standardization:** Translating initial German working drafts, research notes, and conceptual notes into academic, domain-standard British/Oxford English suitable for international peer review (IEEE/ACM SIGGRAPH conventions).

- **Document Refactoring & Formatting:** Structuring technical documentation into standardized Markdown schemas (`TMP-001`), tabular taxonomic matrices, and validating syntactic compliance for diagram generation via Mermaid.js.

- **Cross-Reference Auditing & Traceability Verification:** Assisting in identifying cross-document reference inconsistencies between the Core Specification (`CS-001`), Domain Models (`DM-*`), Glossary (`GLS-001`), and Architecture Decision Records (`ADR-*`).

- **Synthesis of External State-of-the-Art Literature:** Summarizing and categorizing technical documentation, whitepapers (e.g., SMPTE, BBC, Epic Games, ARRI), and academic papers to support bibliography assembly.
## 2. Authorship, Ownership & Epistemic Accountability

In strict adherence to international academic integrity standards, LLMs are not recognized as co-authors and bear no legal, moral, or intellectual accountability:

  

- **Sole Human Authorship:** The entirety of the domain models, ontological taxonomy (`StudioObject`, `Capability`, `Context`, `Impulse`, `State`, `Event`), architectural patterns (Ports and Adapters, Aggregate Roots, Mediator), and systems engineering trade-offs were exclusively formulated, verified, and directed by the human author and project maintainer, Olaf Erler.

- **Human-in-the-Loop Governance:** No AI-generated text, diagram, or programmatic abstraction was adopted into the normative specification baseline without critical evaluation, formal technical peer review, and verification against the fundamental principles outlined in `CS-001` and `GOV-001`.

- **Critical Correction & Verification of AI Hallucinations:** Conceptual errors, syntactic hallucinations (such as syntax collisions in nested Mermaid tokens), or domain-inaccurate structural classifications produced by AI instances were systematically caught, corrected, and rejected during the human review process.

## 3. Methodological Rigor & Architecture Traceability

To maintain reproducible and verifiable scientific software development:

- **Empirical Grounding:** Every fundamental architectural decision is backed by established domain literature (Cyber-Physical Systems, Software Engineering, Real-Time Graphics) and codified in formal Architecture Decision Records (`ADR-001` through `ADR-004`) situated at repository root level.

- **Determinism & Conformance:** The operational behavior of the framework is governed by unambiguous conformance and non-conformance boundaries (`CS-001`, Section 6), preventing unverified, generative code patterns from compromising real-time safety, deterministic timing, or hardware agnosticism.


## 4. IP, License & Security Conformance

- All prompts and contextual exchanges conducted with conversational LLMs were reviewed to ensure that no proprietary, third-party confidential, or copyrighted material was compromised. 
- The resulting RVPF documentation, formal models, and Unreal Engine Blueprint/C++ reference implementations are open, transparent, and distributed under the declared repository open-source license.