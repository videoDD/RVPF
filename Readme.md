# Responsive Virtual Production Framework (RVPF) 🎬⚡
**The Domain-Driven Semantic Middleware Architecture for Cyber-Physical Studio Environments, ICVFX, and Responsive Real-Time Systems.**

## 📖 Overview
The Responsive Virtual Production Framework (RVPF) is an open, technology-agnostic middleware specification and reference architecture designed to transform isolated, semantically neutral technical telemetry (trackers, DMX, MIDI, OSC, Live Link, etc.) into context-aware production events and deterministic real-time reactions.

While broadcast standards (e.g., SMPTE 2110) address data transport, RVPF solves the semantic understanding and orchestration of telemetry within the dramatic and temporal reality of a production. It strictly decouples domain business logic from underlying hardware communication protocols, making interactive sets, ICVFX stages, and location-based experiences (LBE) modular, deterministic, and hardware-agnostic.

---

## 🛑 The Problem: Hardware Coupling & Lack of Context
In contemporary real-time productions, engines frequently process raw hardware signals directly within device scripts or actors:
* A continuous spatial coordinate `(2.31, 1.74, 0.85)` is merely a numeric measurement vector lacking domain meaning.
* A MIDI button press or DMX packet is processed as an immediate hardcoded command rather than a contextual trigger.
* Workflows become brittle, device-dependent, and non-deterministic, making hardware swapping or reproducible playback across takes difficult.

---

## 💡 The Solution: Closed-Loop Information Processing
RVPF enforces a deterministic causality pipeline and closed-loop control cycle:

$$\text{Physical World} \longrightarrow \text{Impulse} \longrightarrow \text{Context} \longrightarrow \text{State Transition} \longrightarrow \text{Event} \longrightarrow \text{Rule} \longrightarrow \text{Action} \longrightarrow \text{Actuator} \longrightarrow \text{Physical World}$$

```mermaid
flowchart LR
    HW[1. Physical/Virtual Sensor] -->|Raw Signal| ADP[2. Protocol Adapter]
    ADP -->|Normalize| IMP["3. FStudioImpulse (DTO)"]
    IMP -->|HandleImpulse| SO["4. StudioObject (Aggregate Root)"]
    SO -->|Telemetry| CR["5. Context Resolver (Evaluator)"]
    CR -->|State Transition| EV((6. Domain Event))
    EV -->|Evaluate| RE[7. Rule Engine]
    RE -->|Decision| CAP["8. Target Capability (Contract)"]
    CAP -->|Actuation Payload| ACT[9. Actuator / Device Output]
```
### Core Architectural Pillars

1. **Semantic Neutrality of Impulses (ADR-002):** Incoming signals are ingested as raw, normalized `FStudioImpulse` packages carrying zero inherent domain logic.
    
2. **Context Determines Meaning (DM-PRD-001, DM-CTX-001):** Telemetry acquires meaning exclusively when evaluated against the active dramatic state (Scene, Shot, Take) and spatial/environmental context.
    
3. **Events Arise from State Transitions (ADR-003, DM-STM-001):** High-frequency data streams update state metrics; formal domain events fire strictly upon discrete state boundary crossings, eliminating event flooding.
    
4. **StudioObject Aggregate Root & Capabilities (ADR-001, DM-OBJ-001, DM-CAP-001):** Entities model _what they can do_ (Emit, Capture, Track, Interact) rather than _what they are_, while protocol adapters (`StudioComponent`) handle hardware I/O.
    
5. **Master Timeline Authority (ADR-004, DM-PRD-001):** Execution is anchored to the engine timeline (Sequencer/Take Recorder), ensuring identical processing logic for live performance, recording, and replay.
    

## 📊 Current Status: Alpha Release

The RVPF is currently in **Alpha Status**. The core architecture is fully specified, and we are actively validating the framework via our Unreal Engine 5 Reference Implementation.

**Currently Working Implementations:**

- ✅ **Core Architecture:** Domain Models, Event Dispatching, and Context Engine are established.
    
- ✅ **MIDI Integration:** Fully functional `MidiInputAdapter` allowing dynamic orchestration of multiple MIDI inputs (e.g., triggering Niagara particle systems and virtual states).
    
- ✅ **DMX Integration:** Fully functional 16-bit DMX output routing to physical studio fixtures (e.g., ARRI SkyPanels), allowing the physical studio to mirror virtual scene lighting deterministically.
    

## 🚀 Development Roadmap (2026 / 2027)

- **Phase 1: DMX Finalization (Current Focus)**
    
    Finalizing the bidirectional lighting synchronization. Isolating static greenscreen illumination from dynamic scene lighting via contextual rule sets and deploying custom GDTF fixtures.
    
- **Phase 2: 6DoF Tracking Integration**
    
    Implementing robust adapters for positional tracking (e.g., HTC Vive Mars, OptiTrack) to drive `StudioObject` telemetry without hardcoding LiveLink streams into actors.
    
- **Phase 3: Virtual Camera (VCam) Rigs**
    
    Developing generalized VCam capabilities bridging Joypad/Smartphone inputs with custom, physical Arduino/ESP32-based camera rigs and field recorder telemetry.
    
- **Phase 4: Advanced LBE & Physical Interactivity**
    
    Scaling capabilities to orchestrate complex Location-Based Experiences (e.g., physical spaceship cockpits where buttons/potentiometers trigger synchronized SFX, VFX, and DMX lighting changes).
    
- **Phase 5: Audio & NPC Integration**
    
    Expanding the pipeline to ingest voice/audio capture and output via MetaSounds. Integrating Non-Player Characters (NPCs) via Behavior Trees/State Trees that react naturally to RVPF semantic events.
    
- **Phase 6: The Digital Twin**
    
    Completing a permanent, high-fidelity Digital Twin of the physical studio. This will serve as the ultimate reference environment for all generated projects to guarantee real-world fidelity and testability.
    

## 📂 Repository Structure & Artifact Inventory

Plaintext

```
RVPF/
├── adrs/                                      # Architecture Decision Records
│   ├── ADR-001_SeparationOfBusinessStateAndHardwareCommunication.md
│   ├── ADR-002_SemanticNeutralityOfIncomingImpulses.md
│   ├── ADR-003_EventGenerationViaContextTransitions.md
│   └── ADR-004_TimeBasedExecutionViaMasterTimeline.md
│
├── docs/                                      # Normative Specifications & Architecture
│   ├── CS-001_CoreSpecification.md            # Foundational Normative Principles
│   ├── GOV-001_RVPF_Governance.md             # Lifecycle & Process Specification
│   ├── RA-001_RVPF_referenceArchitecture.md   # 5-Tier System Topology
│   ├── RA-002_RVPF_layerModellInformationProcessingPipeline.md # Flow & Causality
│   ├── TMP-001_RVPF_ArtifactTemplate.md       # Standardized Artifact Schema
│   └── VSN-001_RVPF_Vision.md                 # Strategic Manifesto & Scope
│
├── models/                                    # Domain Models & Formal Taxonomy
│   ├── DM-CAP-001_capabilityModel.md          # Abstract Functional Contracts
│   ├── DM-CTX-001_contextModel.md             # Semantic Context Resolution
│   ├── DM-IMP-001_impulseModel.md             # Normalized Ingestion Vector
│   ├── DM-OBJ-001_StudioObjectSpecification.md# Aggregate Root Composition
│   ├── DM-PRD-001_ProductionModel.md          # Production Hierarchy & Master Timeline
│   ├── DM-SID-001_studioIdentity.md           # Immutable Identity Value Object
│   ├── DM-STM-001_stateModel.md               # Deterministic Lifecycle State Machine
│   └── GLS-001_glossary.md                    # Single Source of Semantic Truth
│
├── implementation/                            # Hardware Abstraction & Driver Tier
│   └── IL-001_ImplementationLayer.md          # Device Inventory & Protocol Adapters
│
├── diagrams/                                  # Visual Architecture & Sequence Schemes
│
└── RVPF_UE/                                   # Unreal Engine 5 Reference Implementation
    └── RRI-001_UnrealReferenceImplementation.md                              # UE5 Architecture, Structs & Blueprint APIs
```

## 🛠️ Implementation Mapping (Unreal Engine 5 Reference)

The RVPF specification is platform-agnostic, with Unreal Engine 5 serving as the primary reference implementation:

|**RVPF Concept**|**Unreal Engine 5 Reference Construct**|**Pattern / DDD Role**|
|---|---|---|
|**StudioObject**|`AActor` / `BP_StudioObjectBase`|Aggregate Root|
|**StudioIdentity**|`FStudioIdentity` (`USTRUCT`)|Value Object|
|**StudioLifecycle**|`UStudioLifecycleComponent`|State Pattern|
|**StudioCapability**|`UBPI_Capability` / `UStudioCapabilityComponent`|Strategy / Contract Interface|
|**StudioImpulse**|`FStudioImpulse` (`USTRUCT`)|Data Transfer Object (DTO)|
|**Public Interface**|`UBPI_StudioObject` (`UInterface`)|Facade / Port Interface|
|**Context Resolver**|`UContextManagerSubsystem`|Mediator / Broker Pattern|
|**Master Timeline Authority**|`ULevelSequencePlayer` & `UTakeRecorder`|Temporal Master Clock|
|**Protocol Adapters**|`UDMXComponent`, `ULiveLinkComponent`, `UMidiComponent`|Adapter Pattern|

## 🔬 Reference Production Validation (UC-001: The Cave Torch)

The framework architecture is formally validated via the canonical end-to-end reference production scenario:

Plaintext

```
[Vive Mars Rover Pose] ───► Ingestion (IL-001) ───► FStudioImpulse ───► BP_StudioObject (Torch)
                                                                             │
                                                                       Forward Telemetry
                                                                             ▼
[Take Recorder: Take 01] ────────────────────────────────────────► Context Resolver (DM-CTX-001)
                                                                             │
                                                                   Evaluates Cave Boundary
                                                                             ▼
                                                                 State: OFF ──► IGNITED
                                                                             │
                                                                 Event: TorchIgnited (DM-STM-001)
                                                                             │
                                                                  Dispatches Action Directives
                                                                             ▼
                                                                ┌────────────┴────────────┐
                                                                ▼                         ▼
                                                        [ARRI SkyPanel DMX]      [Niagara / MetaSound]
                                                        (Physical Actuation)     (Virtual Environment)
```

## 🤝 Research, Governance & Community

RVPF is developed as an open research and educational platform at the intersection of media engineering, computer science, and virtual production.

- **Governance:** Specification changes follow strict semantic versioning and artifact lifecycle rules defined in `GOV-001`.
    
- **Traceability:** Every domain entity directly traces back to the normative Core Principles in `CS-001` and formal ADRs.
    
- **Contributions:** Inquiries, academic collaborations, and pull requests regarding adapters or target runtimes are warmly welcome.    