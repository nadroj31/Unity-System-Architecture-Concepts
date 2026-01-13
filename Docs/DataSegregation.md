# Data Segregation Model

The Loop Persistence Manager enforces a strict separation between different categories of game data to ensure predictable behavior across loop resets.

## Data Categories Overview

| Data Type        | Examples                                   | Storage Method                                | Lifecycle Behavior          |
|------------------|--------------------------------------------|-----------------------------------------------|-----------------------------|
| Persistent Data  | Chest Gold, Fate Nodes, Permanent Upgrades | ScriptableObject (`PersistentPlayerData_SO`)  | Retained across all loops   |
| Ephemeral Data   | World State, Scene State, Temp Inventory   | Runtime classes / scene-bound objects         | Reset on every loop         |
| Runtime State    | Health Potions, Chest Gold Snapshot        | `LPM_RuntimeState` (runtime memory)           | Reinitialized on loop start |

## Persistent Data

- Represents long-term player progression
- Stored in ScriptableObjects
- Never mutated directly during gameplay
- Modified only at the loop end after validation

## Ephemeral Data

- Exists only during the current loop
- Fully discarded on loop reset
- Includes world and scene state created during gameplay

## Runtime State

- Runtime-only mirror of relevant persistent data
- Acts as the authoritative state during gameplay
- Buffers changes until loop end

All gameplay systems interact with runtime state rather than persistent data directly.
