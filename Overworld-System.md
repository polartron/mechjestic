# Overworld System

The Overworld System manages the procedurally generated exploration areas where players navigate, encounter enemies, and discover treasures.

## Overview

The overworld is a tile-based map system where:
- Players move tile-by-tile
- Enemies move and chase the player
- Treasures and special tiles provide rewards
- Pathfinding determines valid movement
- Fog of war reveals areas as explored

## Tile Types

### Base Tiles
- **Type**: `TileType.Base`
- **Traversable**: Yes
- **Purpose**: Standard walkable terrain
- **Restoration**: Restored when enemy tiles are defeated

### Enemy Tiles
- **Type**: `TileType.Enemy`
- **Traversable**: No (blocks movement)
- **Purpose**: Hostile encounters
- **Behavior**: Moves and chases player
- **Defeat**: Converts back to base tile

### Boss Tiles
- **Type**: `TileType.Boss`
- **Traversable**: No
- **Purpose**: Boss encounters
- **Special**: Higher difficulty, better rewards

### Gate Tiles
- **Type**: `TileType.Gate`
- **Traversable**: Conditional
- **Purpose**: Level transitions
- **Activation**: Triggers next level generation

### Treasure Tiles
- **Type**: `TileType.Treasure`
- **Traversable**: Yes
- **Purpose**: Loot rewards
- **Activation**: Opens when no nearby enemies
- **Rewards**: Cards, loot items

### Boost Tiles
- **Type**: `TileType.Boost`
- **Traversable**: Yes
- **Purpose**: Temporary stat boosts
- **Effect**: Grants buffs when stepped on

### Start Tiles
- **Type**: `TileType.Start`
- **Traversable**: Yes
- **Purpose**: Level entry point
- **Spawn**: Player spawns here

### Prison Tiles
- **Type**: `TileType.Prison`
- **Traversable**: Conditional
- **Purpose**: Special mechanics
- **Effect**: May trap or restrict movement

### Crumbling Tiles
- **Type**: `TileType.Crumbling`
- **Traversable**: Yes
- **Purpose**: Hazard tiles
- **Effect**: May collapse or damage player

### End Tiles
- **Type**: `TileType.End`
- **Traversable**: Yes
- **Purpose**: Level exit
- **Activation**: Completes level

## Tile Management

### Tile Dictionary
- **OverworldTiles**: Dictionary mapping positions to tiles
- **Tile Updates**: Updated when tiles change
- **Pathfinding**: Uses dictionary for navigation

### Tile Restoration
When enemy tiles are defeated:
1. Enemy tile destroyed
2. Base tile restored at position
3. Dictionary updated
4. Pathfinding cache cleared
5. Area becomes traversable

## Movement System

### Player Movement
- **Tile-by-tile**: Move one tile per action
- **Pathfinding**: A* pathfinding to destination
- **Validation**: Check if destination is traversable
- **Animation**: Smooth movement animation

### Enemy Movement
- **Request System**: Enemies request moves through OverworldManager
- **Batching**: Moves batched and resolved together
- **Conflict Resolution**: Prevents multiple enemies on same tile
- **Priority**: Based on difficulty and size

### Movement Conditions
Enemies won't move if:
- Battle loading or in progress
- Enemy tile is dead
- Enemy already moving
- Player being forced to move
- Enemy not awake (procedural enemies)

## Pathfinding

### A* Algorithm
- **Implementation**: `TileManager.GetPath`
- **Heuristic**: Distance-based
- **Obstacles**: Non-traversable tiles block paths
- **Cache**: Pathfinding cache for performance

### Path Validation
- **Traversability**: Check if tiles are walkable
- **Enemy Blocks**: Enemy tiles block paths
- **Dynamic Updates**: Cache cleared on tile changes

## Fog of War

### Fog System
- **BatchedFogManager**: Manages fog rendering
- **Reveal**: Areas revealed as player explores
- **Visual**: Fog overlay on unexplored areas
- **Performance**: Batched rendering for efficiency

### Fog Updates
- **On Movement**: Fog updates when player moves
- **On Tile Change**: Fog updates when tiles change
- **Visibility**: Determines what player can see

## Tile Interactions

### Activation
- **Click/Tap**: Activate tile
- **Validation**: Check if tile can be activated
- **Sequence**: Activation sequences prevent conflicts

### Treasure Chests
- **Proximity Check**: Must have no nearby enemies
- **Loot Preview**: Preview loot before opening
- **Reward Selection**: Choose from loot options
- **Card Selection**: Use CardSelectionSequence UI

### Enemy Encounters
- **Activation**: Click enemy tile to battle
- **Forced Battle**: Enemy moves onto player
- **Adjacency**: Adjacent enemies affect battle

## Procedural Generation

### Level Generation
- **ProceduralTilemapController**: Generates levels
- **Seed-Based**: Deterministic generation from seed
- **Difficulty Scaling**: Enemies scale with level
- **Boss Floors**: Every 3rd level is boss floor

### Generation Parameters
- **Level Number**: Current floor level
- **Seed**: Random seed for generation
- **Boss Floor**: Whether to generate boss
- **Tile Types**: Distribution of tile types

### Tile Placement
- **Start Tile**: Player spawn point
- **End Tile**: Level exit
- **Enemy Tiles**: Distributed across map
- **Treasure Tiles**: Scattered throughout
- **Special Tiles**: Gate, boost, prison tiles

## Overworld Manager

### Responsibilities
- **Tile Management**: Track all tiles
- **Movement Coordination**: Coordinate player and enemy movement
- **Battle Initiation**: Start battles when triggered
- **Card Obtainment**: Handle card rewards
- **Overpower Tracking**: Track overpower between battles

### Initialization
1. Load level data
2. Generate or load level
3. Spawn player at start
4. Initialize enemies
5. Setup fog of war
6. Enable interactions

### State Management
- **Overpower**: Accumulated overpower value
- **Player Position**: Current player tile
- **Enemy Positions**: All enemy tile positions
- **Tile States**: State of all tiles

## Enemy Movement System

### Movement Request
- **RequestMoveTowardsPlayer()**: Enemy requests move
- **Priority System**: Higher priority moves first
- **Conflict Resolution**: OverworldManager resolves conflicts
- **Execution**: Move executed after resolution

### Movement Patterns
- **Chase**: Move towards player
- **Stay Behind**: Support roles stay behind
- **Strategic**: Tactical positioning
- **Sleeping**: Procedural enemies sleep until awakened

## Visual Systems

### Tile Rendering
- **Tilemap**: Unity Tilemap for rendering
- **Tile Sprites**: Visual representation
- **Animations**: Tile animations
- **VFX**: Visual effects on tiles

### Camera System
- **Follow Player**: Camera follows player
- **Smooth Movement**: Smooth camera transitions
- **Bounds**: Camera bounds to level

### UI Elements
- **Floor Counter**: Current floor display
- **Player Stats**: HP, stats display
- **Overpower Display**: Current overpower
- **Interaction Prompts**: UI prompts for interactions

## Sequence Management

### Activation Sequences
- **Prevent Conflicts**: Only one activation at a time
- **Sequence Registration**: Register activation sequences
- **Completion**: Wait for sequence completion
- **Error Handling**: Handle sequence failures

### Movement Sequences
- **Animation**: Movement animations
- **State Updates**: Update state during movement
- **Completion**: Movement completes when animation done

## Technical Details

### Tile Data Structure
- **Position**: Vector3Int tile position
- **Type**: TileType enum
- **Settings**: Tile-specific settings (enemy, treasure, etc.)
- **State**: Current tile state

### Performance Optimization
- **Pathfinding Cache**: Cache paths for performance
- **Batched Rendering**: Batch fog and tile rendering
- **LOD System**: Level of detail for distant tiles
- **Update Batching**: Batch tile updates

### Save System Integration
- **Save Position**: Save player position
- **Save Tiles**: Save tile states
- **Save Enemies**: Save enemy positions
- **Load State**: Restore state on load

---

*See also: [Enemy System](Enemy-System.md), [Progression & Endless Mode](Progression-Endless-Mode.md), [Battle System](Battle-System.md)*

