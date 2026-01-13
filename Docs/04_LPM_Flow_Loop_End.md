# LPM Flow – Loop End (Reset)

This document describes how the system handles loop termination caused by player death or day completion.

## Flow Diagram

```mermaid
flowchart TD
        A["Player Death Event Triggered"] --> B["Collect Loop Changes"]
        B --> C["Merge into PersistentPlayerData_SO"]
        C --> D["HealthPotions = RuntimeState.CurrentPotions"]
        C --> E["GoldInChest += RuntimeState.DepositedGold"]
        D --> F["Integrate Minigame Result (if exists)"]
        E --> F["Integrate Minigame Result (if exists)"]
        F --> G["Mark isLoopResetting = true"]
        G --> H["Clear RuntimeState"]
        H --> I["Scene Reload (SceneManager.LoadScene(currentScene))"]
        I --> J["Back to Loop Start"]
```

## Sequence

1. Sync changes from `RuntimeState` → back to SO
2. Intergrate `MinigameResult_SO`
3. The `isLoopResetting` flag ensures that other systems stop modifying runtime data during scene reload.
4. Clear `RuntimeState` (prepare for next loop)
5. `SceneManager.LoadScene()` → Loop Start

## Guarantees

- Only explicitly approved progress persists
- No ephemeral state leaks into the next loop
- Scene reload restores a clean baseline
