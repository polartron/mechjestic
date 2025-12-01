# Loot System

The Loot System manages reward generation, loot tables, and loot inventory across the game.

## Overview

The Loot System:
- Generates rewards for battles, treasures, and bosses
- Manages loot tables with rarity and weighting
- Provides loot preview before selection
- Tracks loot inventory across runs
- Integrates with card selection UI

## Loot Generation

### Loot Contexts

#### Treasure Chest Loot
- **Trigger**: Opening treasure chests
- **Context Tags**: Position-based tags
- **Preview**: Preview loot before opening
- **Selection**: Choose from loot options

#### Battle Victory Loot
- **Trigger**: Winning battles
- **Difficulty**: Based on enemy difficulty
- **Context Tags**: Battle context tags
- **Preview**: Preview loot before selection
- **Selection**: Choose from loot options

#### Boss Victory Loot
- **Trigger**: Defeating bosses
- **Difficulty**: Boss difficulty
- **Context Tags**: Boss context tags
- **Preview**: Preview loot before selection
- **Selection**: Choose from loot options
- **Special**: Better rewards than regular battles

### Loot Tables

#### LootTableDatabase
- **Database**: Contains all loot tables
- **Context-Based**: Different tables for different contexts
- **Rarity System**: Common, Uncommon, Rare, Epic, Legendary
- **Weighting**: Cards have weights for selection

#### Loot Entry
- **Card Name**: Card to be rewarded
- **Rarity**: Loot rarity
- **Weight**: Selection weight
- **Tags**: Context tags
- **Context**: Loot context

### Loot Generation Process
1. **Context Determination**: Determine loot context
2. **Table Selection**: Select appropriate loot table
3. **Filtering**: Filter by context tags
4. **Weighted Selection**: Select cards based on weights
5. **Rarity Distribution**: Ensure rarity distribution
6. **Preview Generation**: Generate loot preview
7. **Selection UI**: Show selection UI

## Loot Rarity

### Rarity Levels
- **Common**: Most common loot
- **Uncommon**: Less common loot
- **Rare**: Rare loot
- **Epic**: Very rare loot
- **Legendary**: Extremely rare loot

### Rarity Distribution
- **Weighted**: Rarity affects selection weight
- **Guaranteed**: Some contexts guarantee rarity
- **Visual**: Rarity shown in UI

## Loot Inventory

### Inventory Management
- **Persistent**: Loot persists across levels
- **Separate**: Separate from deck inventory
- **Tracking**: Tracks unique vs total cards
- **Save/Load**: Saves and loads inventory

### Inventory Stats
- **Unique Loot Cards**: Number of unique cards
- **Total Loot Cards**: Total number of cards
- **Card List**: List of cards in inventory

### Inventory Operations
- **Add Card**: Add card to inventory
- **Remove Card**: Remove card (if needed)
- **Check Exists**: Check if card exists
- **Get Cards**: Get list of cards

## Loot Selection

### CardSelectionSequence Integration
- **UI Component**: Uses CardSelectionSequence
- **Loot Display**: Shows loot options
- **Selection**: Choose from loot options
- **Confirmation**: Confirm selection

### Selection Process
1. **Preview Generated**: Loot preview generated
2. **UI Shown**: Card selection UI shown
3. **Player Selects**: Player selects loot
4. **Added to Inventory**: Selected loot added to inventory
5. **Stats Updated**: Loot stats updated

## Loot Preview

### Preview Generation
- **Context-Based**: Preview based on context
- **Loot Table**: Uses appropriate loot table
- **Filtering**: Filters by context tags
- **Selection**: Selects loot entries
- **Return**: Returns preview list

### Preview Methods
- **PreviewTreasureChestLoot()**: Preview treasure loot
- **PreviewBattleVictoryLoot()**: Preview battle loot
- **PreviewBossVictoryLoot()**: Preview boss loot

### Preview Display
- **Card Display**: Shows cards in preview
- **Rarity Display**: Shows rarity
- **Info**: Shows card information
- **Selection**: Allows selection

## Boss Loot System

### Boss Loot Index
- **Tracking**: Tracks current boss loot index
- **Increment**: Increments on boss defeat
- **Reset**: Resets on new run
- **Special Loot**: Boss-specific loot tables

### Boss Loot Generation
- **Index-Based**: Uses boss loot index
- **Special Tables**: Boss-specific loot tables
- **Better Rewards**: Better rewards than regular battles
- **Unique Loot**: May include unique boss loot

## Level-Based Loot

### Level Integration
- **Level Number**: Loot uses level number
- **Level Seed**: Loot uses level seed
- **Scaling**: Loot scales with level
- **Difficulty**: Loot difficulty based on level

### Level Loot Settings
- **Set Level**: Set current level for loot
- **Set Seed**: Set level seed for loot
- **Generation**: Generate loot for level

## Loot Tags

### Tag System
- **Card Tags**: Cards have tags
- **Context Tags**: Contexts have tags
- **Filtering**: Filter loot by tags
- **Matching**: Match cards to contexts

### Tag Usage
- **Context Matching**: Match tags to contexts
- **Filtering**: Filter loot by tags
- **Special Loot**: Tags enable special loot

## Save System Integration

### Loot Inventory Saving
- **Save to Storage**: Save loot inventory
- **Load from Storage**: Load loot inventory
- **Persistence**: Loot persists across sessions
- **Data Structure**: Loot stored as CardListSO

### Save Triggers
- **On Selection**: Save after loot selection
- **On Level Transition**: Save before level transition
- **On Run End**: Save on run end
- **Auto Save**: Periodic auto-save

## Visual Feedback

### Loot Display
- **Card Visuals**: Show card visuals
- **Rarity Colors**: Color-code by rarity
- **Info Box**: Show card information on hover
- **Selection Highlight**: Highlight selected card

### Loot Obtainment
- **Obtainment VFX**: Visual effects on obtainment
- **Inventory Update**: Inventory updated visually
- **Stats Update**: Stats updated in UI

## Technical Details

### Loot Manager
- **EndlessModeLootManager**: Manages loot system
- **Initialization**: Initializes with loot database
- **Level Integration**: Integrates with level system
- **Inventory Management**: Manages loot inventory

### Loot Database
- **LootTableDatabase**: Contains loot tables
- **Table Lookup**: Lookup tables by context
- **Card Data**: Card data for loot entries

### Loot Generation Algorithm
1. **Determine Context**: Determine loot context
2. **Select Table**: Select appropriate table
3. **Filter Tags**: Filter by context tags
4. **Weighted Selection**: Select based on weights
5. **Rarity Check**: Ensure rarity distribution
6. **Generate Preview**: Generate preview list

### Data Structures
- **LootEntry**: Loot entry data
- **LootTable**: Loot table data
- **LootInventory**: Loot inventory data
- **CardListSO**: Card list storage

---

*See also: [Card System](Card-System.md), [Progression & Endless Mode](Progression-Endless-Mode.md), [Save System](Save-System.md)*

