# RVPF: Responsive Virtual Production Framework 🎬🚀
**The Semantic Middleware Architecture for Responsive Environments, ICVFX, and Location-Based Experiences.**

[![Status: Architecture & Prototyping](https://img.shields.io/badge/Status-Architecture_%26_Prototyping-blue)](#)
[![Target: Unreal Engine 5](https://img.shields.io/badge/Target-Unreal_Engine_5-black?logo=unrealengine)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-green)](#)

## 📖 Overview
The **Responsive Virtual Production Framework (RVPF)** is an open-source, domain-driven middleware architecture. It is designed to transform isolated, meaningless technical inputs (from trackers, DMX, MIDI, OSC, etc.) into **context-aware semantic events** for real-time engines. 

While established broadcast standards (like SMPTE 2110) perfectly solve the *transport* of data, RVPF solves the *semantic understanding* of that data within a production environment. 

RVPF completely decouples physical hardware from business logic, making Virtual Production and interactive environments universally scalable, hardware-agnostic, and highly responsive.

---

## 🛑 The Problem: Hardware-Coupling in Real-Time Engines
In current Virtual Production setups, real-time engines process inputs directly. A MIDI fader movement, a DMX signal, or a camera tracking coordinate are just raw data points. 
* A tracking position `(2.31, 1.74, 0.85)` is just a vector. 
* It lacks the **semantic context**: *"The actor just entered the active stage area during Take 4."*

Without context, workflows become hardcoded, device-dependent, and difficult to scale across different studios or interactive installations.

## 💡 The Solution: The RVPF Architecture
RVPF introduces a strict, domain-driven processing pipeline that bridges the physical and virtual worlds:

`Physical World` ➔ `Impulse` ➔ `Context` ➔ `State Transition` ➔ `Semantic Event` ➔ `Rule` ➔ `Action` ➔ `Actuator`

### Key Architectural Concepts
1. **Impulses over Protocols:** The framework does not care about MIDI, OSC, or LiveLink. It only cares about *Impulses*. An impulse has no semantic meaning until interpreted by the current production context.
2. **StudioObjects & Core Capabilities:** Devices are not defined by their hardware type, but by their *Capabilities*. A physical ARRI Skypanel and a virtual Unreal Engine Torch are both represented as a `StudioObject` with the capability `Emit`.
3. **100% Visual Programming (For Now):** The current UE5 reference implementation is built entirely using Unreal's Blueprint visual scripting system (utilizing robust Blueprint Interfaces like `BPI_StudioObject` and internal Event Dispatchers). This ensures maximum accessibility for technical artists while maintaining a clean, scalable architecture ready for future Verse/UE6 porting.

---

## 🌍 Use Cases

### 1. Hybrid Virtual Production (Film & Broadcast)
RVPF seamlessly integrates DMX lighting, camera tracking, and real-time compositing (ICVFX) by evaluating semantic states. E.g., a tracking loss doesn't crash a hardcoded Blueprint; it triggers a semantic `CameraTrackingLost` event, prompting the system to switch to a safe fallback camera automatically.

### 2. Location-Based Experiences (LBE) & Interactive Museums
Because RVPF abstracts hardware, it is the perfect framework for interactive stages, theme parks, and immersive exhibitions. A visitor triggering a physical sensor creates an impulse, which the Context Engine translates into a synchronized reaction across Unreal Engine Niagara systems, MetaSounds, and physical DMX room lighting.

---

## 📂 Repository Structure (Documentation & Specs)
Currently, this repository hosts the core specifications, architecture decision records (ADRs), and domain models. The **Unreal Engine Reference Implementation** is in active development.

* 📄 **[`/docs/VSN-001_Vision.pdf`](#)** - The RVPF Architecture Manifesto.
* 📄 **[`/docs/CS-001_Core_Specification.pdf`](#)** - The normative principles of semantic information processing.
* 📄 **[`/docs/GOV-001_Governance.pdf`](#)** - Open Source lifecycle and artifact governance.
* 📐 **[`/architecture_models/`](#)** - Visual representations of the Context Model, State Model, and StudioObject Pipeline.
* 💻 **[`/implementation/`](#)** - *(WIP)* Modular Blueprint framework for Unreal Engine 5.

---

## 🚀 Roadmap & Next Steps
We are currently transitioning from the formal architecture specification to the **Unreal Engine Reference Implementation**.

- [x] **Phase 1:** Core Specification & Domain Models (StudioObject, Context, Event).
- [x] **Phase 2:** Capability Mapping & Hardware Abstraction (DMX, MIDI, OSC).
- [ ] **Phase 3:** Unreal Engine 5 Blueprint Implementation (`BPI_StudioObject`, Context Resolver).
- [ ] **Phase 4:** Device Adapters & LiveLink Integration.
- [ ] **Phase 5:** Open Source Release & Educational Templates for Universities.
- [ ] **Phase 6:** Future-proofing for Unreal Engine 6 (Verse implementation).

---

## 🤝 Contributing & Education
RVPF is built to give back to the 3D, filmmaking, and educational communities. We believe in teaching students *systemic architecture for real-time environments* rather than just software operation. If you are a developer, technical artist, or researcher interested in cyber-physical systems and Virtual Production, we welcome your contributions!