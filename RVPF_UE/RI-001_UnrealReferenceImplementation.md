# RVPF Technical Specification: Unreal Engine Reference Implementation
**Document ID:** RI-001  
**Title:** RVPF Unreal Engine 5 Reference Implementation & Folder Structure  
**Version:** 0.1  
**Status:** Stable  
**Artifact Type:** Reference Implementation Guide  
**Author:** Olaf Erler  
**Maintainer:** Olaf Erler  
**Artifact Owner:** Olaf Erler  
**Created:** 2026-08-27  
**Last Modified:** 2026-08-27  
**Depends on:** CS-001, RA-001, RA-002, IL-001, DM-OBJ-001, DM-IMP-001, DM-CAP-001  
**Approval:** Accepted  

---

## 1. Purpose
This document defines the normative Unreal Engine 5 (UE5) project architecture, directory conventions, and asset taxonomy for the official RVPF Reference Implementation (`/RVPF_UE`). It maps the abstract domain entities to concrete Blueprint Interfaces, Actor Components, Structs, and Subsystems.

---

## 2. Directory Structure (`/Content/RVPF/`)
To prevent namespace pollution and ensure modularity, all framework assets reside exclusively within a isolated `/RVPF` root content directory:

```text
Content/
└── RVPF/
    ├── Core/                       # Abstract Framework Core (Engine-independent Domain)
    │   ├── Classes/                # Base Actor & Object implementations (BP_StudioObjectBase)
    │   ├── Components/             # Abstract base components (StudioLifecycle, ComponentManager)
    │   ├── Enums/                  # Core state and category enums (EStudioLifecycle, EStudioRole)
    │   ├── Interfaces/             # Public Contracts (BPI_StudioObject, BPI_Capability)
    │   └── Structs/                # Value Objects & DTOs (FStudioIdentity, FStudioImpulse)
    │
    ├── Capabilities/               # Functional Capability Contracts & Logic
    │   ├── Emit/                   # Light & Visual Emitter Capabilities
    │   ├── Capture/                # Camera & Take Recording Capabilities
    │   ├── Track/                  # Spatial Tracking Capabilities
    │   └── Interact/               # Trigger & Value Interaction Capabilities
    │
    ├── Adapters/                   # Concrete Protocol & Hardware Ingestion Layer (IL-001)
    │   ├── DMX/                    # DMX Fixture Controllers & Output Components
    │   ├── MIDI/                   # MIDI Device Listeners & Normalization Adapters
    │   ├── LiveLink/               # Tracking & Camera Subject Adapters
    │   └── OSC/                    # Open Sound Control Receivers & Normalizers
    │
    ├── Context/                    # Semantic Evaluation & State Machines (DM-CTX-001)
    │   ├── Subsystems/             # UContextManagerSubsystem (Mediator & Timeline Authority)
    │   ├── Rules/                  # Declarative Rule Evaluation Assets
    │   └── Volumes/                # Spatial Trigger Volumes & Zone Contexts
    │
    ├── Library/                    # Concrete Studio Objects & Digital Twins (Device Inventory)
    │   ├── Lighting/               # BP_SkyPanel_S30C, BP_SkyPanel_S60C, BP_L7C
    │   ├── Cameras/                # BP_CineCamera_Rig
    │   └── Trackers/               # BP_ViveMars_Tracker, BP_TrackedProp
    │
    └── Showcase/                   # End-to-End Validation & Test Levels
        ├── Levels/                 # LVL_RVPF_ReferenceStage, LVL_TheCaveTorch (UC-001)
        └── Sequences/              # LevelSequences & Master Timeline Assets
```

	## 3. Core Blueprint Artifact Taxonomy

### 3.1 Data Structures & Enums (`/Content/RVPF/Core/Structs` & `/Enums`)
| Asset Name         | Unreal Type           | Domain Counterpart    | Description                                                                                                          |
| :----------------- | :-------------------- | :-------------------- | :------------------------------------------------------------------------------------------------------------------- |
| `FStudioIdentity`  | `User Defined Struct` | `DM-SID-001` | Encapsulates `ObjectID` (GUID), `DisplayName`, `Role`, and `Tags`.                                          |
| `FStudioImpulse`   | `User Defined Struct` | `DM-IMP-001` | Normalized DTO carrying `ValueNorm` (Float 0.0..1.0), `TransformValue`, `Timestamp`, and `SourceGUID`.   |
| `EStudioLifecycle` | `User Defined Enum`   | `DM-STM-001` | Deterministic lifecycle states (`Uninitialized`, `Initializing`, `Ready`, `Active`, `Error`, `Offline`). |
| `ECoreCapability`  | `User Defined Enum`   | `DM-CAP-001` | High-level capability tags (`Emit`, `Capture`, `Track`, `Interact`, `Synchronize`).                      |

---

### 3.2 Interfaces (`/Content/RVPF/Core/Interfaces`)

#### `BPI_StudioObject`
The mandatory Port interface implemented by every studio actor aggregate root:
* `HandleImpulse(FStudioImpulse Impulse)` $\rightarrow$ Primary ingestion entry point for normalized signals.
* `GetStudioIdentity(FStudioIdentity &OutIdentity)` $\rightarrow$ Returns the immutable domain identity value object.
* `GetLifecycleState(EStudioLifecycle &OutState)` $\rightarrow$ Returns the active operational lifecycle state.
* `QueryCapability(ECoreCapability Capability, bool &bIsSupported)` $\rightarrow$ Verifies supported capability contracts.

#### `BPI_Capability`
The operational contract for executing directives on attached modular capability components:
* `ExecuteCommand(FName CommandName, FInstancedStruct Payload)` $\rightarrow$ Routes action payloads to target actuators.

---

### 3.3 Base Classes & Subsystems
* **`BP_StudioObjectBase` (`AActor`):** Minimal Aggregate Root containing `FStudioIdentity`, `StudioLifecycleComponent`, and the component attachment registry.
* **`UContextManagerSubsystem` (`UWorldSubsystem` / `UGameInstanceSubsystem`):** Central mediator tracking the Master Timeline, active dramatic state (`Shot`/`Take`), and orchestrating event generation upon state transitions.