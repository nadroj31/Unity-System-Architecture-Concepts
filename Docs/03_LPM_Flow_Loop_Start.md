# LPM Flow – Loop Start (Scene Load)

This document describes the responsibilities of the Loop Persistence Manager when a new loop begins.

## Flow Diagram

```mermaid
flowchart TD
        A["Scene Load Event Triggered"] --> B["LPM.Awake()"]
        B --> C{"PersistentPlayerData_SO exists?"}
        C -->|No| D["Create new SO instance & Set DontDestroyOnLoad"]
        C -->|Yes| E["Load existing SO instance"]
        E --> F["Initialize RuntimeState"]
        D --> F["Initialize RuntimeState"]
        F --> G["Copy data from SO to RuntimeState"]
        G --> H["Reset all Ephemeral objects"]
        H --> I["OnLoopStart event"]
        I --> J["Gameplay Begins"]
```

## Sequence

1. `LPM.Awake()` checks for existing `PersistentPlayerData_SO` . If another `LPM` or `PersistentPlayerData_SO` instance exists, destroy duplicates to ensure a single persistent source.
2. If no→ Create new SO instance + `DontDestroyOnLoad`
3. Load persistent data from SO → write to `LPM_RuntimeState`
4. Reset all Ephemeral objects
5. Trigger `GameEvents.OnLoopStart?.Invoke()`

## Guarantees

- Persistent data is never modified during initialization
- Runtime state starts from a deterministic baseline
- All ephemeral state is freshly created
