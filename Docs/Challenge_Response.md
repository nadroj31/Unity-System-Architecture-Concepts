# Technical Challenge Response

This document provides a structured response to a technical design challenge focused on building a Loop Persistence Manager (LPM) for a time-loop–based game concept.

The challenge required designing a system that supports full scene reloads while selectively preserving player progression across loops.  
The following sections explicitly address the five requested areas.

## 1. Data Segregation

Game data is divided into three clearly defined categories to ensure predictable behavior across loop resets.

- Persistent data that survives across loops
- Ephemeral data that exists only within a single loop
- Runtime state that buffers gameplay changes safely

Persistent data is never mutated directly during gameplay.

## 2. Persistent Data Structure

Persistent player progression is stored in a ScriptableObject named `PersistentPlayerData_SO`.

This includes:
- Gold stored in the persistent chest
- Permanent items
- Unlocked Fate Nodes
- Permanent attribute upgrades

All persistent data changes occur only at controlled lifecycle boundaries.

## 3. Loop Start Flow

At the beginning of a loop:

1. Load persistent player data
2. Initialize runtime state from persistent data
3. Initialize world and gameplay systems
4. Begin the active gameplay loop

## 4. Loop End Flow

When the player dies or the day ends:

1. Validate runtime state
2. Apply approved changes to persistent data
3. Discard all ephemeral data
4. Reload the scene to begin the next loop

## 5. Minigame Integration

Minigames are treated as independent modules.

They are loaded separately from the core world and communicate results through explicit result objects.  
The Loop Persistence Manager evaluates these results and applies permanent effects only when appropriate.
