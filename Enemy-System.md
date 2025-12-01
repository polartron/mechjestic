# Enemy System

The Enemy System manages enemy behavior, movement, roles, and combat interactions in the overworld and battles.

## Overview

Enemies are dynamic entities that:
- Move and chase the player in the overworld
- Have different roles determining behavior
- Initiate battles when conditions are met
- Provide adjacency buffs to other enemies
- Scale with difficulty and level

## Enemy Roles

### Aggressive
**Movement**: Chases player every turn

**Special Behavior**:
- When moving adjacent to player, pushes player away
- Push direction: Opposite from where enemy entered
- After 3 consecutive successful pushes, forces battle
- Has push cooldown to prevent infinite pushing
- If push fails, immediately forces battle

**On Entry**: 
- If player forced onto tile, pushes player away
- If push fails, forces battle

**Adjacency Buff**: +PWR to battle enemies (multiplied by group size and difficulty)

### Strategist
**Movement**: Chases player every turn

**Special Behavior**:
- When adjacent to player, evaluates pushing player towards other enemies
- Prioritizes pushing towards Aggressive enemies
- Uses A* pathfinding to determine push direction
- If no enemies within 1 tile radius, forces battle

**On Entry**:
- If player forced onto tile, moves player 1 tile towards closest enemy
- Prioritizes Aggressive enemies
- If no enemies nearby, forces battle

**Adjacency Buff**: +Attacks to battle enemies (multiplied by group size and difficulty)

### Resilient
**Movement**: Moves every **second** turn (not every turn)

**Special Behavior**:
- After moving, if player on same tile, forces battle
- Slower movement pattern

**On Entry**: Does not force battle, just moves every 2 turns

**Adjacency Buff**: +DEF to battle enemies (multiplied by group size and difficulty)

### Repairing (Support Role)
**Movement**: Chases player but stays behind other enemies

**Special Behavior**:
- Only moves if no other enemies between it and player
- If no other enemies nearby (within 2 tiles), forces battle
- Support role: Stays behind front-line enemies

**On Entry**:
- If no other enemies around, forces battle
- Otherwise stays behind

**Adjacency Buff**: +HP to battle enemies (multiplied by group size and difficulty)

### Utilitarian (Support Role)
**Movement**: Chases player but stays behind "strong" enemies

**Special Behavior**:
- Only moves if no strong enemies (Worthy, Insane, Boss difficulty) between it and player
- If no strong enemies nearby, forces battle
- Support role: Stays behind powerful enemies

**On Entry**:
- If no strong enemies around, forces battle
- Otherwise stays behind them

**Adjacency Buff**: +PWR and +DEF to battle enemies (multiplied by group size and difficulty)

### Disruptive
**Movement**: Chases player every turn

**Special Behavior**:
- Default behavior: Forces battle when adjacent or on player
- Standard chase pattern

**On Entry**: Forces battle

**Adjacency Buff**: -PWR or -DEF to player (multiplied by group size and difficulty)

## Enemy Difficulties

### Easy
- **Multiplier**: 1x
- **Stats**: Lower HP, Power, Defense
- **Rewards**: Standard rewards

### Regular
- **Multiplier**: 2x
- **Stats**: Standard stats
- **Rewards**: Standard rewards

### Worthy
- **Multiplier**: 3x
- **Stats**: Higher stats
- **Rewards**: Better rewards
- **Considered**: "Strong" enemy for Utilitarian positioning

### Insane
- **Multiplier**: 4x
- **Stats**: Very high stats
- **Rewards**: Excellent rewards
- **Considered**: "Strong" enemy for Utilitarian positioning

### Boss
- **Multiplier**: 5x
- **Stats**: Highest stats
- **Rewards**: Best rewards
- **Special**: Boss music, special mechanics
- **Considered**: "Strong" enemy for Utilitarian positioning

## Movement System

### Movement Priority
- Based on difficulty and size
- Higher number = moves first
- Boss enemies typically move first

### Movement Request System
- Enemies request moves through `OverworldManager`
- `OverworldManager` batches requests
- Resolves conflicts (e.g., two enemies wanting same tile)
- Prevents race conditions and movement conflicts

### Movement Conditions
Enemies will **not** move if:
- Battle is already loading or in progress
- Enemy tile is dead or already moving
- Player is being forced to move (prevents race conditions)
- Enemy is not awake (for procedural enemies with aggro system)

### Pathfinding
- Uses A* pathfinding (`TileManager.GetPath`)
- Only moves one tile per turn (first step in path)
- If no path exists or already adjacent, forces battle instead

## Procedural Enemy Features

### Aggro System
Enemies have states:
- **Sleeping**: Inactive, doesn't move
- **Awake**: Activated, can move
- **Chasing**: Actively chasing player
- **Fleeing**: Retreating (if applicable)

**Awakening**:
- Enemies wake up when player is within range
- Enemies go to sleep when player is 5+ tiles away
- Must wait 2 turns after awakening before moving or swapping

### Strategic Behaviors

#### Strategic Swapping
- Enemies can swap positions with other enemies
- Used for tactical advantage
- Evaluates benefit before swapping

#### Strategic Positioning
Enemies evaluate:
- **Treasure Protection**: Staying near treasure tiles
- **Group Cohesion**: Staying near other enemies
- **Role-Based Positioning**: Support roles stay behind

### Visual Feedback
VFX sequences for different behaviors:
- **Awakening**: Enemy wakes up
- **Sleeping**: Enemy goes to sleep
- **Chasing**: Enemy chases player
- **Fleeing**: Enemy flees
- **Strategic Swaps**: Position swaps
- **Strategic Positioning**: Tactical moves
- **Aggressive/Strategist Pushes**: Push behaviors

## Battle Initiation

### When Battles Start
1. **Player Activation**: Player activates enemy tile (normal activation)
2. **Enemy Moves Onto Player**: Enemy moves onto player's tile (forced battle)
3. **Enemy Becomes Adjacent** and:
   - Push fails (Aggressive/Strategist)
   - No valid push target (Strategist)
   - 3rd consecutive push (Aggressive)
   - Support roles with no other enemies nearby
   - Resilient after moving
   - Disruptive (default)

### Battle Prevention
Battles won't start if:
- Battle already loading or in progress
- Interactions are paused
- Enemy tile is dead

## Enemy Tile Lifecycle

### Creation
- Enemy tiles placed on base tiles
- Occupy tile and make it non-traversable
- Store reference to base tile for restoration after defeat

### Movement
When enemy moves:
1. Base tile restored at old position (becomes traversable)
2. Enemy tile moves to new position
3. Tilemap tile moved
4. Dictionary entries updated
5. Pathfinding cache cleared

### Defeat
After player wins battle:
1. Enemy tile destroyed
2. Base tile restored at that position
3. Other enemies can now walk over defeated enemy's space
4. Settings GameObject destroyed
5. Pathfinding cache cleared

## Adjacency Buffs

### How It Works
When battling enemies, adjacent overworld enemies provide buffs:
- Buff amounts multiplied by:
  - **Group Size**: Number of enemies in battle
  - **Difficulty Multiplier**: Enemy difficulty (Easy=1, Regular=2, Worthy=3, Insane=4, Boss=5)

### Buff Types by Role

#### Aggressive Adjacent Enemy
- **Effect**: +PWR to all battle enemies
- **Formula**: 1 * (group size * difficulty multiplier)

#### Resilient Adjacent Enemy
- **Effect**: +DEF to all battle enemies
- **Formula**: 1 * (group size * difficulty multiplier)

#### Disruptive Adjacent Enemy
- **Effect**: -PWR or -DEF to player (random)
- **Formula**: 1 * (group size * difficulty multiplier)

#### Utilitarian Adjacent Enemy
- **Effect**: +PWR and +DEF to all battle enemies
- **Formula**: 1 * (group size * difficulty multiplier) for each stat

#### Repairing Adjacent Enemy
- **Effect**: +HP to all battle enemies
- **Formula**: 2 * (group size * difficulty multiplier)

#### Strategist Adjacent Enemy
- **Effect**: +Attacks to all battle enemies
- **Formula**: 1 attack per enemy (not multiplied)

## Interaction with Other Systems

### Treasure Tiles
- Treasure tiles check for nearby enemies before opening
- If any active enemy tiles are touching (within 1 tile), treasure cannot be opened
- Prevents players from looting while enemies are nearby

### Tile Management
- Enemy tiles update `OverworldTiles` dictionary when moving
- Defeated enemies restore base tiles in the dictionary
- Pathfinding uses the dictionary to determine traversability

## Technical Details

### Movement Execution
- `RequestMoveTowardsPlayer()` → Registers move request with priority
- `ExecuteMove()` → Called by OverworldManager after conflict resolution
- `MoveEnemyToCell()` → Performs actual movement and updates all systems

### State Tracking
- `lastEnemyPosition`: Tracks where enemy came from (for Aggressive push direction)
- `movementCounter`: Tracks turns for Resilient enemies
- `aggressivePushCounter`: Tracks consecutive pushes for Aggressive enemies
- `aggressivePushCooldown`: Prevents infinite pushing

### Sequence Management
- Uses `SequenceManager` to coordinate animations
- Prevents race conditions
- Movement animations complete before push behaviors execute
- Battle activation uses sequences to prevent duplicate activations

### Enemy Data
- **EnemyData**: Battle stats and abilities
- **EnemyTileSettings**: Overworld behavior and difficulty
- **ProceduralEnemyTileSettings**: Procedural generation settings

---

*See also: [Battle System](Battle-System.md), [Overworld System](Overworld-System.md), [Progression & Endless Mode](Progression-Endless-Mode.md)*

