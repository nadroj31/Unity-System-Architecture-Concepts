# Loop Lifecycle

This document describes the responsibilities of the Loop Persistence Manager during loop start and loop end.

See Diagrams/LPM_Flowchart.png for a visual overview.

## Loop Start

The following sequence is executed when a loop begins:

1. Persistent player data is loaded
2. Runtime state is initialized from persistent data
3. World and gameplay systems are initialized
4. Gameplay begins

This ensures a deterministic and clean starting state for every loop.

## Loop End

Triggered by player death or narrative completion.

1. Runtime state is validated
2. Approved changes are committed to persistent data
3. All ephemeral data is discarded
4. The scene is reloaded

This guarantees that only explicitly approved progress persists across loops.
