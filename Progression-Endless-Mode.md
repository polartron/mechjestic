# Progression & Endless Mode

The Progression System manages player advancement through endless mode, tracking stats, levels, and run progression.

## Overview

Endless Mode is the main game mode where:
- Players progress through procedurally generated floors
- Each floor is a new level with enemies and treasures
- Stats are tracked across the run
- Victory conditions determine run completion
- Daily runs provide seeded challenges

## Level Progression

### Floor System
- **Current Level**: Current floor number (starts at 1)
- **Max Level Reached**: Highest floor reached in run
- **Level Increment**: Increases when transitioning to next level
- **Display**: Floor counter shows current level

### Level Transitions
1. **Gate Activation**: Player activates gate tile
2. **Transition Sequence**: 
   - Save current progress
   - Generate next level
   - Update loot manager with new level
   - Transition to new level
3. **Level Generation**: Procedural generation with seed
4. **Player Spawn**: Player spawns at start tile

### Level Generation

#### Seed System
- **Random Seed**: Generated for each level
- **Daily Seed**: Fixed seed for daily runs
- **Deterministic**: Same seed = same level layout
- **Seed Storage**: Saved for daily runs

#### Generation Parameters
- **Level Number**: Current floor level
- **Seed**: Random or daily seed
- **Boss Floor**: Every 3rd level is boss floor
- **Difficulty Scaling**: Enemies scale with level

#### Level Types
- **Regular Floor**: Standard enemies and treasures
- **Boss Floor**: Boss enemy, better rewards (every 3rd level)

## Stats Tracking

### Run Stats
- **Current Level**: Current floor number
- **Max Level Reached**: Highest floor reached
- **Total Cards Obtained**: Cards collected this run
- **Total Enemies Defeated**: Enemies defeated this run
- **Total Treasures Found**: Treasures opened this run
- **Total Run Time**: Time spent in run
- **Total Loot Drawn**: Loot items drawn
- **Unique Loot Cards**: Unique cards in loot inventory
- **Total Loot Cards**: Total cards in loot inventory

### Stats Updates
- **On Level Change**: Level stats update
- **On Card Obtained**: Card count increments
- **On Enemy Defeated**: Enemy count increments
- **On Treasure Obtained**: Treasure count increments
- **On Loot Drawn**: Loot stats update
- **Runtime**: Run time continuously updates

### Stats Events
- **OnLevelChanged**: Fired when level changes
- **OnStatsUpdated**: Fired when stats update
- **OnNewRunStarted**: Fired when new run starts

## Run Management

### New Run
- **Stats Reset**: All stats reset to initial values
- **Loot Clear**: Loot inventory cleared
- **Boss Loot Reset**: Boss loot index reset
- **Level Reset**: Start at level 1
- **Seed Generation**: New random seed
- **Level Generation**: Generate initial level

### Restart Run
- **Stats Reset**: Reset stats but preserve max level
- **Loot Clear**: Clear loot inventory
- **Boss Loot Reset**: Reset boss loot index
- **Daily Run Preserve**: Preserve daily seed if applicable
- **Level Reset**: Start at level 1
- **Player Reset**: Reset player to start position

### Continue Run
- **Load Progress**: Load saved run data
- **Restore State**: Restore level, stats, loot
- **Resume Position**: Resume at saved position
- **Skip Setup**: Skip customization if configured

### Failed Run Handling
- **Detection**: Check if run failed (e.g., player died)
- **Stats Reset**: Reset stats on failure
- **Loot Clear**: Clear loot inventory
- **State Cleanup**: Clean up failed run state

## Victory Conditions

### Win Condition
- **Level Threshold**: Reach specific level (configurable)
- **Victory Scene**: Loads victory scene
- **Run Complete**: Marks run as complete
- **Stats Finalize**: Final stats recorded

### Loss Conditions
- **Mech Dead**: Mech HP reaches 0 in battle
- **Deckout**: Deck runs out of cards
- **Give Up**: Player surrenders
- **Surrender**: Player surrenders

## Daily Runs

### Daily Run System
- **Fixed Seed**: Same seed for all players each day
- **Progress Saving**: Save daily run progress
- **Resume**: Can resume daily run
- **Seed Preservation**: Daily seed preserved on restart

### Daily Run Features
- **Shared Challenge**: Same level layout for all players
- **Leaderboards**: Compare progress (if implemented)
- **Reset**: Resets daily at specified time

## Loot System Integration

### Level-Based Loot
- **Loot Manager**: Manages loot per level
- **Level Seed**: Loot uses level seed for generation
- **Boss Loot**: Special loot on boss floors
- **Treasure Loot**: Loot from treasure chests
- **Battle Loot**: Loot from battle victories

### Loot Inventory
- **Persistent**: Loot persists across levels
- **Unique Tracking**: Tracks unique vs total cards
- **Save/Load**: Saves and loads loot inventory
- **Storage**: Separate from deck inventory

## Save System Integration

### Run Data Saved
- **Current Level**: Current floor number
- **Max Level**: Highest floor reached
- **Run Time**: Total run time
- **Stats**: Cards, enemies, treasures counts
- **Loot**: Loot inventory data
- **Boss Loot Index**: Current boss loot index
- **Overpower**: Current overpower value
- **Daily Seed**: Daily run seed (if applicable)

### Save Triggers
- **Level Transition**: Save before transitioning
- **Battle Completion**: Save after battle
- **Treasure Obtained**: Save after treasure
- **Manual Save**: Player-initiated save
- **Auto Save**: Periodic auto-save

### Load Process
1. **Load Run Data**: Load saved run data
2. **Restore Stats**: Restore stats from save
3. **Restore Loot**: Restore loot inventory
4. **Restore Level**: Restore level and seed
5. **Restore Position**: Restore player position
6. **Generate Level**: Generate level from seed

## Seasonal Features

### Seasonal Cards
- **At Start**: Can give seasonal card at run start
- **Configuration**: Seasonal card name configurable
- **Obtainment**: Card obtained via OverworldManager
- **Sequence**: Card obtainment sequence plays

### Perk Cards at Start
- **Configuration**: Can give perk cards at start
- **Perk Names**: List of perk card names
- **Obtainment**: Perks added to perk inventory
- **Persistence**: Perks persist across runs

## Component Managers

### EndlessModeStatsTracker
- **Responsibility**: Track and update stats
- **Stats Storage**: Stores all run stats
- **Event Firing**: Fires stats update events
- **Save Data**: Provides save data

### EndlessModeLevelManager
- **Responsibility**: Manage level progression
- **Level Generation**: Triggers level generation
- **Transition**: Handles level transitions
- **Seed Management**: Manages level seeds
- **Floor Display**: Updates floor counter UI

### EndlessModeLootManager
- **Responsibility**: Manage loot system
- **Loot Inventory**: Manages loot inventory
- **Loot Generation**: Generates loot for contexts
- **Save/Load**: Saves and loads loot inventory
- **Boss Loot**: Manages boss loot index

### EndlessModeRunManager
- **Responsibility**: Manage run state
- **Run Data**: Saves and loads run data
- **Failed Run**: Handles failed runs
- **New Run**: Manages new run initialization
- **Restart**: Handles run restart

## Technical Details

### Initialization
1. **Component Setup**: Initialize component managers
2. **Load Data**: Load saved run data or start new
3. **Handle Failed Run**: Check and handle failed runs
4. **Setup Seed**: Setup level seed (random or daily)
5. **Generate Level**: Generate initial level
6. **Initialize Overworld**: Initialize overworld manager
7. **Subscribe Events**: Subscribe to battle events

### Update Loop
- **Run Time**: Continuously update run time
- **Stats**: Update stats as events occur
- **Level Transition**: Handle level transitions
- **Save**: Periodic auto-save

### Event Subscriptions
- **Battle Finished**: Track enemy defeats
- **Card Obtained**: Track card collection
- **Treasure Obtained**: Track treasure collection
- **Loot Drawn**: Track loot drawing

---

*See also: [Battle System](Battle-System.md), [Loot System](Loot-System.md), [Save System](Save-System.md)*

