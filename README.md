# Veritas – Loop Persistence Manager Blueprint

### Unity C# Architecture Design

## Overview

This repository presents a design-oriented technical blueprint for the **Loop Persistence Manager (LPM)** system created for *Veritas*, a time-loop–based game concept.

The core problem addressed is how to handle **scene reloads on loop reset** while preserving selected player progress (persistent data) and resetting all world and runtime state (ephemeral data).

The focus of this repository is system architecture, data segregation, and loop lifecycle management rather than concrete implementation code.

## Challenge Context

In *Veritas*, gameplay operates on a repeating daily time loop.

- When the player dies or the day ends, the scene reloads.
- Certain progress must persist across loops, such as items stored in a persistent chest or unlocked Fate Nodes.
- All world state resets to its initial condition.

The design goal is to clearly define what persists, what resets, and how the system enforces that separation in a clean and maintainable way.

## Design Goals

- Explicit separation between persistent, ephemeral, and runtime data
- No direct mutation of persistent data during gameplay
- Clear responsibilities at loop start and loop end
- Modular integration of independent minigames
- Scalability for future systems and additional persistence rules

## Core Concepts

- **Persistent Data**  
  Long-term player progression stored in ScriptableObjects

- **Ephemeral Data**  
  Loop-specific world and gameplay state that is reset on each loop

- **Runtime State**  
  A controlled runtime copy used during gameplay to prevent unsafe modification of persistent data

## Documentation

Detailed design explanations can be found in the `Docs` directory:

- `Challenge_Response.md` – Explicit response to the original five-point technical challenge  
- `DataSegregation.md` – Persistent vs ephemeral vs runtime data model  
- `LoopLifecycle.md` – Loop start and loop end flow breakdown  
- `MinigameIntegration.md` – Modular minigame loading and result handling  

## Disclaimer

This repository represents a conceptual system design and does not contain production-ready code or a playable Unity project.

## Author

YuLung Tsai  
Unity Game Developer / Software Engineer
