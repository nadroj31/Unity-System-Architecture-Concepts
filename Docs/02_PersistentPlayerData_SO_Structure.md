# PersistentPlayerData_SO Structure

This document describes the structure and responsibility of the PersistentPlayerData_SO asset.

## Conceptual Structure Diagram

```mermaid
classDiagram
direction TD

    class PersistentPlayerData_SO {
            +int GoldInChest
        +int HealthPotions
        +List~string~ FateNodesUnlockedSerialized
        -HashSet~string~ FateNodesUnlocked
        +void IntegrateMinigameResult(MinigameResult_SO result)
        +void ResetLoopEphemeral()
        +void OnAfterDeserialize() // rebuild HashSet
    }
```

## Stored Data Categories

| Field | Type | Description |
| --- | --- | --- |
| GoldInChest | int | Gold saved in persistent chest |
| HealthPotions | int | Health Potion count (persists across loops) |
| FateNodesUnlockedSerialized | List<string> | Serialized version of unlocked nodes |
| FateNodesUnlocked | HashSet<string> | Permanently unlocked fate nodes (e.g., “Chess Master”) |
| IntegrateMinigameResult() | Method | Merges minigame result into persistent state |
| ResetLoopEphemeral() | Method | Reset the non-persistent part |
| OnAfterDeserialize() | Method | Syncs HashSet after load |

## Design Notes

- This ScriptableObject represents authoritative persistent state
- It is treated as immutable during active gameplay
- Modifications occur only at the loop end after validation
