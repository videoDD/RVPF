# RVPF Domain Model: StudioObject Specification
**Document ID:** DM-OBJ-001  
**Status:** Stable  

## 1. Concept and Purpose
The `StudioObject` is the central semantic entity (Aggregate Root) of the RVPF. It is the digital representation of a physical or virtual entity within the studio ecosystem. A `StudioObject` abstracts real-world hardware and virtual systems into a unified object model, defining their identity, capabilities, and states completely independent of their technical implementation (e.g., DMX, MIDI, OSC).

## 2. Core Composition
A `StudioObject` is composed of the following core domains, strictly separating generic properties from hardware-specific logic:

* **Identity (`StudioIdentity`):** The immutable description of the object, acting as a Value Object. It contains properties such as ID, Name, Manufacturer, Model, and a Physical/Virtual flag.
* **Role (`StudioRole`):** Categorizes the object both by Device Family (e.g., Sensor, Actuator, Gateway) and Studio Role (e.g., Camera, Light, Tracking, Audio).
* **Lifecycle (`StudioLifecycle`):** A state machine tracking the object's operational readiness. States include Created, Initialized, Available, Connected, Configured, Ready, Active, Busy, Paused, Offline, Error, and Destroyed.
* **Capabilities (`StudioCapabilitySet`):** An array of abstract contracts defining what the object can do, rather than what it is. Examples include Capture, Emit, Track, Monitor, Synchronize, and Configure.
* **Relationships (`StudioRelationships`):** Defines the topology of the studio via Parent, Children, and Dependencies (e.g., a Tracking device attached to a Camera).
* **Components (`StudioComponent`):** Modular components attached to the `StudioObject` that handle the actual hardware communication and protocol parsing (e.g., a `DMXComponent` or `LensComponent`).

## 3. Public Interface (`BPI_StudioObject`)
To ensure loose coupling and universal interaction, every `StudioObject` must implement a minimal, generic Blueprint Interface (`BPI_StudioObject`) consisting of the following operations:

* `Initialize()`: Brings the object into a defined initial state.
* `Shutdown()`: Cleans up resources, network connections, and timers.
* `GetIdentity()`: Returns the immutable `FStudioIdentity` struct.
* `GetLifecycleState()`: Returns the current `EStudioLifecycle` enum value.
* `GetCapabilities()`: Returns an array of supported `ECoreCapability` enum values.
* `HandleImpulse(FStudioImpulse)`: The universal entry point for all incoming data. The `StudioObject` receives a standardized `FStudioImpulse` and evaluates it, without needing to know if the source was MIDI, DMX, or a GUI interaction.