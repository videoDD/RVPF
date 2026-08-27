# RVPF Domain Model: Production Context
**Document ID:** DM-PRD-001  
**Status:** Stable  

## 1. Concept and Purpose
The Production Model defines the overarching dramatic and temporal framework of the Responsive Virtual Production Framework (RVPF). While sensors and devices provide raw data, this data only acquires semantic meaning within the specific context of a production. An identical technical impulse can have entirely different consequences depending on the current scene, shot, or take.

## 2. The Role of the Sequencer
In traditional workflows, the Unreal Engine Sequencer is primarily viewed as an animation tool. In the RVPF, the Sequencer (and Take Recorder) serves a more fundamental role: it is the "temporal truth" of the entire production. 
* All impulses occur within this temporal framework.
* Instead of a signal merely triggering an action (e.g., "MIDI triggers explosion"), the framework contextualizes the event: "During Take 14, Shot 6, at Timecode xx:xx:xx:xx, an impulse occurs".

## 3. Production Hierarchy
The Production Model is structured top-down into the following hierarchical layers:

* **Production:** The highest-level container representing the entire project.
* **Session:** A specific working period or day within the production.
* **Scene:** The dramatic or narrative unit currently being executed.
* **Shot:** A specific camera angle or framing setup within the scene.
* **Take:** A single continuous recorded performance of a shot.
* **Timeline / Playback State:** The continuous temporal reference, typically driven by Timecode and the Sequencer's playback status.