# Battle System

The Battle System is the core combat mechanic of SteamDeckBuilder, featuring turn-based card combat.

## Overview

Battles are initiated when:
- Player activates an enemy tile
- Enemy moves onto player's tile (forced battle)
- Enemy becomes adjacent and triggers battle conditions

## Battle Flow

### Initialization
1. Battle state is created from:
   - Player mech data
   - Engine data
   - Deck cards
   - Enemy data
   - Adjacent enemy buffs
   - Perk abilities

2. Opening hand is drawn (configurable size)
3. Turn counter initializes
4. Interactions are enabled

### Turn Structure

#### Player Turn
1. **Main Phase**: Player can:
   - Play cards from hand
   - Activate engine abilities (if fuel available)
   - Use hero abilities
   - Attack enemies
   - End turn

2. **Card Playing**:
   - Instant cards: Immediate effect, then discarded
   - Equip cards: Equipped to mech limbs, modify stats
   - Hero cards: Special equipment with unique abilities

3. **Attack System**:
   - First attack each turn is **free**
   - Subsequent attacks cost **Overpower**:
     - 2nd attack: 5 Overpower
     - 3rd attack: 10 Overpower
     - 4th attack: 15 Overpower
     - And so on (5 * attack number)

#### Enemy Turn
- Enemies attack based on their attack patterns
- Enemy abilities activate
- Turn counter increments

### Battle States

Battles track state per turn:
- **BattleState**: Complete snapshot of battle at a turn
- Tracks all entities, cards, abilities, and effects
- Supports "peeking" to preview consequences

### Victory Conditions

**Win**:
- All enemies defeated
- Player mech HP > 0
- Deck not exhausted

**Loss**:
- **Mech Dead**: Mech HP reaches 0
- **Deckout**: Deck runs out of cards
- **Give Up**: Player surrenders
- **Surrender**: Player surrenders

## Key Mechanics

### Overpower System

**Accumulation**:
- Gained when defeating enemies
- Amount based on enemy difficulty and type
- Displayed in UI during battle

**Usage**:
- Pay for multiple attacks per turn
- First attack is always free
- Costs increase: 5, 10, 15, 20...

**Visual Feedback**:
- Final blow effects on enemy defeat
- Camera shake
- Overpower popup display
- Text bounce animation

### Engine System

**Fuel Management**:
- Engines have fuel capacity
- Fuel consumed for active abilities
- Fuel can be refueled by cards/effects
- Fuel changes shown with fire/smoke VFX

**Engine Upgrades**:
- Engines upgrade based on conditions
- Visual engine swap when upgraded
- Passive and active abilities

### Rift System

**Enduring Rift**:
- Activated at level 10+ in endless mode
- Modifies battle mechanics
- Visual effect indicator
- Can be enabled/disabled

### Ability System

**Ability Types**:
- **Mech Abilities**: Base mech abilities
- **Engine Abilities**: Passive and active engine abilities
- **Card Abilities**: Abilities from equipped cards
- **Perk Abilities**: Abilities from perk cards
- **Enemy Abilities**: Enemy-specific abilities

**Ability Activation**:
- Automatic (passive) abilities trigger on conditions
- Active abilities require player activation
- Abilities show popups with effects
- Ability frequency tracking

### Card Management

**Hand**:
- Cards drawn from deck
- Maximum hand size (configurable)
- Cards can be played or discarded

**Deck**:
- Shuffled at battle start (except tutorial)
- Cards drawn from top
- Deckout occurs when deck is empty

**Scrap Pile**:
- Discarded cards go to scrap pile
- Some cards can recycle from scrap to deck
- Scrap pile visible in UI

**Card Effects**:
- Cards have multiple effects
- Effects modify stats, move cards, trigger abilities
- Effects can target mech, enemies, or battle state

### Stat System

**Mech Stats**:
- **HP**: Health points (durability)
- **Power**: Attack damage
- **Defense**: Damage reduction
- **Decay**: Damage over time
- **Attacks Left**: Remaining attacks this turn

**Enemy Stats**:
- Same stat types as mech
- Modified by difficulty and adjacency buffs

**Stat Changes**:
- Visual popups show stat changes
- Color-coded (green for increase, red for decrease)
- Animated stat bars

### Adjacency Buffs

When battling enemies adjacent to other overworld enemies:
- **Aggressive Adjacent**: +PWR to battle enemies
- **Resilient Adjacent**: +DEF to battle enemies
- **Disruptive Adjacent**: -PWR or -DEF to player
- **Utilitarian Adjacent**: +PWR and +DEF to battle enemies
- **Repairing Adjacent**: +HP to battle enemies
- **Strategist Adjacent**: +Attacks to battle enemies

Buff amounts multiplied by:
- Group size (number of enemies in battle)
- Difficulty multiplier (Easy=1, Regular=2, Worthy=3, Insane=4, Boss=5)

## Visual Systems

### Animations
- Card draw animations
- Card play animations
- Attack animations
- Death animations
- Stat change animations
- Ability popup animations

### VFX Sequences
- Card effects
- Attack effects
- Ability effects
- Final blow effects
- Overpower effects
- Engine effects

### Camera System
- Battle camera setup
- Camera shake on events
- Multiple camera angles
- Camera transitions

### UI Elements
- Player bars (HP, stats, abilities)
- Enemy bars
- Hand display
- Deck counter
- Scrap pile
- Overpower display
- Attack cost display
- Turn counter
- Fuel display

## Battle End

### Win Sequence
1. Victory music crossfade
2. Enemy death animations complete
3. End screen shows:
   - Victory state
   - Rewards preview
   - Card selection (if applicable)
4. Battle cleanup
5. Return to overworld

### Loss Sequence
1. Loss music crossfade
2. Mech death animation
3. End screen shows:
   - Loss state
   - Failure tracking
4. Battle cleanup
5. Return to overworld or main menu

## Technical Details

### Battle State Management
- Battle states stored per turn
- Supports state peeking/preview
- State copying for previews
- State history tracking

### Sequence Management
- Coordinated animation sequences
- Prevents race conditions
- Sequence registration and tracking
- Parallel sequence execution

### Property Change System
- Tracks all stat/property changes
- Clustered changes for visualization
- Change visualization system
- Change history

### Interaction System
- Interactable objects (cards, buttons)
- Hover states
- Click handling
- Interaction locking during animations

## Configuration

### Battle Settings
- Opening hand size
- Minimum ability popup time
- Card hover time
- Glow time
- Transition delays

### Tutorial Mode
- Special tutorial battles
- Disabled overpower system
- Custom hand drawing
- Tutorial-specific dialogues

---

*See also: [Card System](Card-System.md), [Enemy System](Enemy-System.md), [Perk System](Perk-System.md)*

