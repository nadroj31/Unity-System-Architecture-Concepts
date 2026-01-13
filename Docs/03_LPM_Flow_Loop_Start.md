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

1. Load PersistentPlayerData_SO
2. Initialize LPM_RuntimeState from persistent data
3. Initialize world and gameplay systems
4. Enable player input and begin gameplay

## Guarantees

- Persistent data is never modified during initialization
- Runtime state starts from a deterministic baseline
- All ephemeral state is freshly created
