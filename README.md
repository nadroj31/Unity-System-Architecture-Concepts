# Veritas – Loop Persistence Manager Blueprint

### Unity C# Architecture Design

## Overview

This repository presents a design-oriented technical blueprint for the **Loop Persistence Manager (LPM)** system created for *Veritas*, a time-loop–based game concept.

The core problem addressed is how to support **full scene reloads on loop reset** while selectively preserving player progression and ensuring all loop-specific state is safely reset.

This repository focuses on **system architecture, data ownership, and lifecycle control**, rather than concrete implementation code.

## Challenge Context

In *Veritas*, gameplay operates on a repeating daily time loop.

- When the player dies or the day ends, the scene reloads.
- Certain progress must persist across loops, such as items stored in a persistent chest or unlocked Fate Nodes.
- All world and gameplay states must reset to a clean baseline.

The design goal is to define clearly **what persists**, **what resets**, and **how the system enforces this separation** in a scalable and maintainable manner.

## How to Read This Repository

This repository is structured to allow both quick review and deep inspection.

### Recommended Reading Order

1. **Data Segregation Rules**  
   `Docs/01_Data_Segregation.md`  
   Defines ownership and lifecycle rules for all data categories.

2. **Persistent Data Structure**  
   `Docs/02_PersistentPlayerData_SO_Structure.md`  
   Details the schema and responsibilities of persistent player data.

3. **Loop Lifecycle Flows**  
   - `Docs/03_LPM_Flow_Loop_Start.md`  
   - `Docs/04_LPM_Flow_Loop_End.md`  
   Visual and step-by-step breakdown of loop initialization and reset.

4. **Minigame Integration**  
   `Docs/05_Minigame_Integration.md`  
   Explains how minigames are loaded, isolated, and how permanent results are applied.

5. **Overall System Overview**  
   `Docs/06_Overall_UML_Overview.md`  
   High-level UML diagram summarizing component relationships.

For reviewers interested in the original technical challenge requirements and their explicit responses, see:  
`Docs/Challenge_Response.md`.

## Design Principles

- Persistent data is never mutated during active gameplay
- Runtime state acts as a controlled buffer for all gameplay changes
- Ephemeral state is fully discarded on each loop reset
- Loop lifecycle responsibilities are centralized and explicit
- Independent systems communicate through well-defined boundaries

## Disclaimer

This repository represents a **conceptual system design**.  
It does not contain production-ready code or a playable Unity project.

## Author

YuLung Tsai  
Unity Game Developer / Software Engineer
