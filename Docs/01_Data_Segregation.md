# Data Segregation

The Loop Persistence Manager enforces a strict separation of data responsibilities to ensure predictable behavior across loop resets.

## Data Categories Overview

| Data Type        | Purpose                                 | Storage Method                               | Reset Behavior              |
|------------------|------------------------------------------|----------------------------------------------|-----------------------------|
| Persistent Data  | Long-term player progression             | ScriptableObject (`PersistentPlayerData_SO`) | Never reset                 |
| Ephemeral Data   | Loop-specific world and gameplay state   | Scene objects / runtime classes              | Reset every loop            |
| Runtime State    | Safe mutable gameplay state              | `LPM_RuntimeState` (runtime memory)          | Reinitialized on loop start |

## Key Principles

- Persistent data is never modified directly during gameplay
- All gameplay systems operate on runtime state
- Ephemeral data is fully discarded on scene reload

This separation prevents unintended persistence and simplifies reasoning about loop behavior.
