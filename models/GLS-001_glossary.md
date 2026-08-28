# RVPF Glossary Specification
**Document ID:** GLS-001  
**Title:** RVPF Glossary  
**Version:** 0.1  
**Status:** Stable  
**Artifact Type:** Glossary  
**Author:** Olaf Erler  
**Maintainer:** Olaf Erler  
**Artifact Owner:** Olaf Erler  
**Created:** 2026-07-30  
**Last Modified:** 2026-07-30  
**Depends on:** CS-001  
**Referenced by:** All RVPF Artifacts  
**Approval:** Accepted  

---

## 1. Purpose
The RVPF Glossary defines the authoritative domain terminology and vocabulary for the Responsive Virtual Production Framework (RVPF). It serves as the single source of semantic truth, ensuring strict terminology consistency across all normative specifications, domain models, architecture decision records, and implementations.

---

## 2. Document Scope
**This document defines:**
* Authoritative domain concepts and terms utilized across RVPF specifications.
* Precise operational and contextual definitions distinguishing data, semantics, and execution tiers.
* Hardware-agnostic classifications for entities, telemetry, and capabilities.

**This document explicitly does not define:**
* Specification lifecycle statuses (See `GOV-001`).
* Concrete behavioral logic or Blueprint execution flows (See `DM-STM-001`, `RA-001`).
* Hardware device registries or communication configurations (See `IL-001`).

---

## 3. Normative References
| ID | Title | Relation / Description |
| :--- | :--- | :--- |
| **CS-001** | RVPF Core Specification | Foundational principles and normative constraints |
| **GOV-001** | RVPF Governance | Process specifications, lifecycle rules, and standards |
| **TMP-001** | RVPF Artifact Template | Structural blueprint for specifications |

---

## 4. Core Domain Terminology

| Term | Domain Category | Authoritative Definition | Contextual Disambiguation / Architectural Boundary |
| :--- | :--- | :--- | :--- |
| **Action** | Execution | An abstract or concrete operation executed by a system in response to an evaluated rule or command. | Differs from an Event; an Action represents intended execution, not a state change occurrence. |
| **Actuator** | Entity / Hardware | A physical or digital component capable of altering the state of the studio environment (e.g., lighting fixture, speaker, motor, virtual parameter). | Contrasts with a Sensor; Actuators produce output effects rather than capturing input data. |
| **Capability** | Interface / Contract | An abstract, hardware-agnostic contract defining a functional operation that a `StudioObject` can provide or execute. | Modeled independently of device types (e.g., `Emit`, `Capture`, `Track`). |
| **Command** | Interaction | An explicit imperative instruction dispatched to an entity to invoke a specific Capability method (e.g., `SetBrightness`, `StartCapture`). | Directly targets a Capability; represents an explicit execution directive. |
| **Context** | Semantic | The semantic interpretation of one or more `StudioObjects` derived by evaluating incoming telemetry within the active production situation. | Context transforms raw data into situational awareness (e.g., `ActorInsideStage`). |
| **Context Resolver** | Middleware | An architectural component that continuously evaluates incoming normalized impulses against active context definitions to derive state. | Acts as the translation bridge between raw telemetry and semantic state. |
| **Digital Twin** | Representation | A real-time virtual simulation model mirroring the kinematics, photometric state, and metadata of a physical counterpart. | Synchronized bidirectionally via telemetry impulses and actuator commands. |
| **Event** | Semantic | A formal semantic notification generated exclusively when an evaluated context undergoes a discrete state transition. | Distinct from an Impulse; an Event carries established production meaning. |
| **Impulse** | Ingestion / Telemetry | An immutable, semantically neutral information vector representing a discrete temporal data occurrence from a sensor or interface. | Ingested without inherent domain logic until contextualized. |
| **Normalization** | Ingestion | The process of scaling and mapping diverse hardware input values into standardized framework ranges (e.g., mapping 0–255 DMX or 0–127 MIDI to 0.0–1.0). | Eliminates protocol dependencies before context evaluation occurs. |
| **Production Context** | Production | The root temporal and dramatic framework defining the global operational boundary (Production, Scene, Shot, Take, Timeline). | Serves as the overarching contextual umbrella for all localized states. |
| **Rule** | Decision | A conditional statement (`IF <Event/Condition> THEN <Action>`) evaluated by the middleware to orchestrate studio behavior. | Decouples event generation from target actuator execution. |
| **Sensor** | Entity / Hardware | A physical or virtual component that measures environmental, spatial, or operational parameters and generates telemetry. | Ingests data into the pipeline as raw impulses. |
| **State** | Dynamic State | The discrete, verified condition of an entity, context, or capability at a specific instant in time. | Persistent until altered by an evaluated impulse or transition. |
| **State Transition** | Dynamic State | A deterministic change of an entity or context from a verified source state to a target state. | The mandatory prerequisite for raising an Event. |
| **StudioIdentity** | Aggregate / Metadata | An immutable Value Object encapsulating all static descriptive identifiers and taxonomies of an entity (ObjectID, UUID, Role, Vendor). | Answers *"Who am I?"*; contains no mutable operational states. |
| **StudioObject** | Aggregate Root | The fundamental domain entity representing any physical, virtual, or hybrid element operating within the studio environment. | Aggregates Identity, Lifecycle, Capabilities, and Device Adapters. |
| **Unreal Asset** | Engine / External | A passive content resource native to the Unreal Engine environment (e.g., StaticMesh, Material, Texture, SoundWave). | Excluded from direct domain representation; instantiated as or attached to a `StudioObject`. |

---

## 5. Traceability Mapping
| Core Principle / Constraint | Realized In / Handled By | Conformance Criteria |
| :--- | :--- | :--- |
| **Principle 1: Impulses have no semantic meaning** | Definition of `Impulse` vs. `Event` | Incoming telemetry is strictly defined as neutral data vectors until contextualized. |
| **Principle 2: Context determines meaning** | Definition of `Context` & `Context Resolver` | Semantic interpretation is decoupled from physical input channels. |
| **Principle 3: Events describe state transitions** | Definition of `Event` & `State Transition` | Events are restricted to discrete state boundary crossings. |
| **Principle 4: Capabilities describe functions** | Definition of `Capability` & `Command` | Operations are modeled via abstract contracts rather than vendor hardware classes. |
| **Principle 5: StudioObjects as core entities** | Definition of `StudioObject` & `StudioIdentity` | All studio elements share a unified aggregate model. |