# Technical Challenge Response

This document provides a structured response to a technical design challenge focused on building a **Loop Persistence Manager (LPM)** for a time-loop–based game concept.

The challenge required designing a system that supports full scene reloads while selectively preserving player progression across loops.  
The following sections explicitly address the five requested areas of the challenge.

## 1. Data Segregation

Game data is divided into three clearly defined categories to ensure predictable behavior across loop resets.

- **Persistent Data**  
  Data that must survive across loops and scene reloads.

- **Ephemeral Data**  
  Data that exists only for the duration of the current loop and is reset on reload.

- **Runtime State**  
  A runtime-only copy of relevant persistent data used during gameplay to prevent unsafe mutation.

Persistent data is stored using ScriptableObjects, while ephemeral and runtime data exist only in memory.

## 2. Persistent Data Structure

`PersistentPlayerData_SO` is responsible for storing all long-term player progression, including:

- Gold stored in the persistent chest
- Permanent items
- Unlocked Fate Nodes
- Permanent attribute upgrades

This data is treated as immutable during gameplay and is only modified at controlled lifecycle boundaries.

## 3. Loop Start Flow

On scene load or loop initialization, the Loop Persistence Manager performs the following steps:

1. Load `PersistentPlayerData_SO`
2. Initialize `LPM_RuntimeState` using persistent data
3. Initialize world state and gameplay systems
4. Begin the active gameplay loop

This ensures a clean and deterministic starting state for every loop.

## 4. Loop End Flow

When the player dies or the day ends, the following sequence is executed:

1. Validate the runtime state
2. Apply approved changes back to persistent data
3. Discard all ephemeral data
4. Reload the scene to start the next loop

This process guarantees that only explicitly approved progress persists.

## 5. Minigame Integration

Minigames are designed as independent modules rather than extensions of the core world.

Key characteristics:

- Loaded independently from the main game flow
- Operate without direct access to persistent data
- Communicate outcomes through structured result objects

The Loop Persistence Manager evaluates these results and applies permanent effects only when appropriate, maintaining clear system boundaries.
