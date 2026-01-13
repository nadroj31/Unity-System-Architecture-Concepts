# Overall UML Overview

This document provides a high-level conceptual overview of the system architecture.

## UML Overview Diagram

```mermaid
classDiagram
direction TD

        class LPM {
                +PersistentPlayerData_SO PersistentData
                +LPM_RuntimeState State
                +Queue~MinigameResult_SO~ MinigameResults
                +OnLoopStart()
                +OnPlayerDeath()
                +isLoopResetting : bool
        }

        class PersistentPlayerData_SO {
                +int HealthPotions
                +int GoldInChest
                +List~string~ FateNodesUnlockedSerialized
        }

        class LPM_RuntimeState {
                +int CurrentPotions
                +int CurrentGold
                +int DepositedGold
        }

        class MinigameResult_SO {
                +string FateNodeID
        }

        class MinigameLoader {
                +LoadMinigame()
                +UnloadMinigame()
        }

        LPM --> PersistentPlayerData_SO : singleton instance
        LPM --> LPM_RuntimeState : runtime buffer
        LPM --> MinigameResult_SO : integrates queued results
        MinigameLoader --> MinigameResult_SO : creates result
```

## Scalability Design

| Feature | Implement |
| --- | --- |
| Multiple minigames | Unified `MinigameResult` payload and event callback |
| Multiple player data | `PersistentPlayerData_SO` + `player ID` |

## Summary

The architecture centralizes loop control while maintaining strict data ownership boundaries.
This design minimizes coupling, improves testability, and supports future expansion.
