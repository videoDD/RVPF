# RVPF Glossary Specification
**Document ID:** GLS-001[cite: 1]  
**Title:** RVPF Glossary[cite: 1]  
**Version:** 0.1[cite: 1]  
**Status:** Stable[cite: 1]  
**Artifact Type:** Glossary[cite: 1]  
**Author:** Olaf Erler[cite: 1]  
**Maintainer:** Olaf Erler[cite: 1]  
**Artifact Owner:** Olaf Erler[cite: 1]  
**Created:** 2026-07-30[cite: 1]  
**Last Modified:** 2026-07-30[cite: 1]  
**Depends on:** CS-001[cite: 1]  
**Referenced by:** All RVPF Artifacts[cite: 1]  
**Approval:** Accepted[cite: 1]  

---

## 1. Purpose
The RVPF Glossary defines the authoritative domain terminology and vocabulary for the Responsive Virtual Production Framework (RVPF)[cite: 1]. It serves as the single source of semantic truth, ensuring strict terminology consistency across all normative specifications, domain models, architecture decision records, and implementations[cite: 1].

---

## 2. Document Scope
**This document defines:**
* Authoritative domain concepts and terms utilized across RVPF specifications[cite: 1].
* Precise operational and contextual definitions distinguishing data, semantics, and execution tiers[cite: 1].
* Hardware-agnostic classifications for entities, telemetry, and capabilities[cite: 1, 2].

**This document explicitly does not define:**
* Specification lifecycle statuses (See `GOV-001`)[cite: 1].
* Concrete behavioral logic or Blueprint execution flows (See `DM-STM-001`, `RA-001`)[cite: 1].
* Hardware device registries or communication configurations (See `IL-001`)[cite: 1].

---

## 3. Normative References
| ID | Title | Relation / Description |
| :--- | :--- | :--- |
| **CS-001** | RVPF Core Specification | Foundational principles and normative constraints[cite: 1] |
| **GOV-001** | RVPF Governance | Process specifications, lifecycle rules, and standards[cite: 1] |
| **TMP-001** | RVPF Artifact Template | Structural blueprint for specifications[cite: 1] |

---

## 4. Core Domain Terminology

| Term | Domain Category | Authoritative Definition | Contextual Disambiguation / Architectural Boundary |
| :--- | :--- | :--- | :--- |
| **Action** | Execution | An abstract or concrete operation executed by a system in response to an evaluated rule or command[cite: 1, 2]. | Differs from an Event; an Action represents intended execution, not a state change occurrence[cite: 1, 2]. |
| **Actuator** | Entity / Hardware | A physical or digital component capable of altering the state of the studio environment (e.g., lighting fixture, speaker, motor, virtual parameter)[cite: 1, 2]. | Contrasts with a Sensor; Actuators produce output effects rather than capturing input data[cite: 1, 2]. |
| **Capability** | Interface / Contract | An abstract, hardware-agnostic contract defining a functional operation that a `StudioObject` can provide or execute[cite: 1, 2]. | Modeled independently of device types (e.g., `Emit`, `Capture`, `Track`)[cite: 1, 2]. |
| **Command** | Interaction | An explicit imperative instruction dispatched to an entity to invoke a specific Capability method (e.g., `SetBrightness`, `StartCapture`)[cite: 1, 2]. | Directly targets a Capability; represents an explicit execution directive[cite: 1, 2]. |
| **Context** | Semantic | The semantic interpretation of one or more `StudioObjects` derived by evaluating incoming telemetry within the active production situation[cite: 1, 2]. | Context transforms raw data into situational awareness (e.g., `ActorInsideStage`)[cite: 1, 2]. |
| **Context Resolver** | Middleware | An architectural component that continuously evaluates incoming normalized impulses against active context definitions to derive state[cite: 1, 2]. | Acts as the translation bridge between raw telemetry and semantic state[cite: 1, 2]. |
| **Digital Twin** | Representation | A real-time virtual simulation model mirroring the kinematics, photometric state, and metadata of a physical counterpart[cite: 1, 2]. | Synchronized bidirectionally via telemetry impulses and actuator commands[cite: 1, 2]. |
| **Event** | Semantic | A formal semantic notification generated exclusively when an evaluated context undergoes a discrete state transition[cite: 1, 2]. | Distinct from an Impulse; an Event carries established production meaning[cite: 1, 2]. |
| **Impulse** | Ingestion / Telemetry | An immutable, semantically neutral information vector representing a discrete temporal data occurrence from a sensor or interface[cite: 1, 2]. | Ingested without inherent domain logic until contextualized[cite: 1, 2]. |
| **Normalization** | Ingestion | The process of scaling and mapping diverse hardware input values into standardized framework ranges (e.g., mapping 0–255 DMX or 0–127 MIDI to 0.0–1.0)[cite: 1, 2]. | Eliminates protocol dependencies before context evaluation occurs[cite: 1, 2]. |
| **Production Context** | Production | The root temporal and dramatic framework defining the global operational boundary (Production, Scene, Shot, Take, Timeline)[cite: 1]. | Serves as the overarching contextual umbrella for all localized states[cite: 1]. |
| **Rule** | Decision | A conditional statement (`IF <Event/Condition> THEN <Action>`) evaluated by the middleware to orchestrate studio behavior[cite: 1, 2]. | Decouples event generation from target actuator execution[cite: 1, 2]. |
| **Sensor** | Entity / Hardware | A physical or virtual component that measures environmental, spatial, or operational parameters and generates telemetry[cite: 1, 2]. | Ingests data into the pipeline as raw impulses[cite: 1, 2]. |
| **State** | Dynamic State | The discrete, verified condition of an entity, context, or capability at a specific instant in time[cite: 1, 2]. | Persistent until altered by an evaluated impulse or transition[cite: 1, 2]. |
| **State Transition** | Dynamic State | A deterministic change of an entity or context from a verified source state to a target state[cite: 1, 2]. | The mandatory prerequisite for raising an Event[cite: 1, 2]. |
| **StudioIdentity** | Aggregate / Metadata | An immutable Value Object encapsulating all static descriptive identifiers and taxonomies of an entity (ObjectID, UUID, Role, Vendor)[cite: 1]. | Answers *"Who am I?"*; contains no mutable operational states[cite: 1]. |
| **StudioObject** | Aggregate Root | The fundamental domain entity representing any physical, virtual, or hybrid element operating within the studio environment[cite: 1, 2]. | Aggregates Identity, Lifecycle, Capabilities, and Device Adapters[cite: 1, 2]. |
| **Unreal Asset** | Engine / External | A passive content resource native to the Unreal Engine environment (e.g., StaticMesh, Material, Texture, SoundWave)[cite: 2]. | Excluded from direct domain representation; instantiated as or attached to a `StudioObject`[cite: 2]. |

---

## 5. Traceability Mapping
| Core Principle / Constraint | Realized In / Handled By | Conformance Criteria |
| :--- | :--- | :--- |
| **Principle 1: Impulses have no semantic meaning**[cite: 1] | Definition of `Impulse` vs. `Event`[cite: 1, 2] | Incoming telemetry is strictly defined as neutral data vectors until contextualized[cite: 1, 2]. |
| **Principle 2: Context determines meaning**[cite: 1] | Definition of `Context` & `Context Resolver`[cite: 1, 2] | Semantic interpretation is decoupled from physical input channels[cite: 1, 2]. |
| **Principle 3: Events describe state transitions**[cite: 1] | Definition of `Event` & `State Transition`[cite: 1, 2] | Events are restricted to discrete state boundary crossings[cite: 1, 2]. |
| **Principle 4: Capabilities describe functions**[cite: 1] | Definition of `Capability` & `Command`[cite: 1, 2] | Operations are modeled via abstract contracts rather than vendor hardware classes[cite: 1, 2]. |
| **Principle 5: StudioObjects as core entities**[cite: 1] | Definition of `StudioObject` & `StudioIdentity`[cite: 1, 2] | All studio elements share a unified aggregate model[cite: 1, 2]. |