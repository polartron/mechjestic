# Perk System

The Perk System provides permanent upgrades that persist across runs, allowing players to build power over multiple playthroughs.

## Overview

Perks are permanent upgrades that:
- Are collected during runs
- Persist across runs
- Modify gameplay mechanics
- Provide abilities and stat modifications
- Are stored in a separate perk inventory

## Perk Cards

### Perk Card Type
- **CardType**: `CardType.Perk`
- **Consumption**: Consumed immediately when obtained
- **Storage**: Stored in perk inventory (separate from deck)
- **Persistence**: Persists across runs

### Perk Card Data
- **BaseID**: Unique perk identifier
- **PerkAbilityBaseID**: Ability granted by perk
- **Display Names**: Localized names
- **Descriptions**: Localized descriptions
- **Effects**: Card effects (if any)

## Perk Collection

### Obtaining Perks
Perks can be obtained from:
- **Battle Rewards**: Selected after battle victories
- **Treasure Chests**: Found in treasure chests
- **Boss Rewards**: Rewarded after boss defeats
- **Start of Run**: Can be given at run start (configurable)

### Selection Process
- **Card Selection UI**: Uses CardSelectionSequence
- **Single Selection**: Choose one perk from options
- **Immediate Effect**: Perk applied immediately
- **Inventory Addition**: Added to perk inventory

## Perk Inventory

### Storage
- **Separate Inventory**: Perks stored separately from deck
- **Persistent**: Saved across game sessions
- **Temporary Storage**: Uses temporary save slot during run
- **Permanent Storage**: Saved to permanent storage

### Inventory Management
- **Add Perk**: Add perk to inventory
- **Remove Perk**: Remove perk (if needed)
- **List Perks**: List all collected perks
- **Save/Load**: Save and load perk inventory

## Perk Abilities

### Ability System
- **Perk Ability Base ID**: Each perk grants an ability
- **Ability Addition**: Abilities added to battle state
- **Battle Integration**: Abilities active during battles
- **Effect Application**: Abilities modify gameplay

### Ability Types
Perk abilities can:
- **Modify Stats**: Change HP, Power, Defense, Decay
- **Grant Effects**: Provide special effects
- **Modify Mechanics**: Change game mechanics
- **Trigger Conditions**: Activate on specific conditions

## Perk Application

### At Battle Start
1. **Load Perks**: Load perk cards from inventory
2. **Collect Abilities**: Collect perk ability IDs
3. **Add to Battle**: Add perk abilities to battle state
4. **Apply Effects**: Perk effects modify battle

### Perk Effects on Mech
- **Pre-Battle Application**: Perks applied before battle starts
- **Mech Modification**: Perks modify mech stats/abilities
- **Temporary Battle State**: Uses temporary state for application
- **Effect Activation**: Perk card effects activate
- **Stat Copying**: Modified stats copied back to mech

### Perk Abilities in Battle
- **Ability Integration**: Perk abilities integrated into battle
- **Automatic Activation**: Abilities activate automatically
- **Condition-Based**: Abilities trigger on conditions
- **Visual Feedback**: Ability popups show perk effects

## Perk Persistence

### Save System
- **Temporary Save**: Perks saved during run
- **Permanent Save**: Perks saved to permanent storage
- **Load on Start**: Perks loaded when game starts
- **Cross-Run**: Perks persist across runs

### SaveManager Integration
- **SavePerkCardsTemporary()**: Save perks during run
- **LoadPerkCardsTemporary()**: Load perks during run
- **Permanent Storage**: Perks saved permanently
- **Data Structure**: Perk cards stored as CardListSO

## Perk Configuration

### At Run Start
- **Configuration**: Can give perk cards at start
- **Perk Names**: List of perk card names to give
- **Obtainment Sequence**: Perks obtained via sequence
- **Inventory Addition**: Added to perk inventory

### Seasonal Perks
- **Seasonal Cards**: Can include seasonal perks
- **Limited Time**: Seasonal perks available for limited time
- **Special Effects**: Seasonal perks may have special effects

## Perk Effects

### Stat Modifications
- **HP**: Modify maximum HP
- **Power**: Modify attack power
- **Defense**: Modify defense
- **Decay**: Modify decay (damage over time)
- **Attacks**: Modify attacks per turn

### Ability Modifications
- **Grant Abilities**: Add new abilities
- **Modify Abilities**: Change existing abilities
- **Ability Frequency**: Modify ability trigger frequency

### Mechanic Modifications
- **Card Drawing**: Modify card draw mechanics
- **Fuel**: Modify engine fuel mechanics
- **Deck**: Modify deck mechanics
- **Battle**: Modify battle mechanics

## Visual Feedback

### Perk Obtainment
- **Card Selection**: Perk shown in card selection UI
- **Obtainment VFX**: Visual effects on obtainment
- **Inventory Update**: Perk inventory updated
- **Notification**: Notification of perk obtained

### Perk Effects in Battle
- **Ability Popups**: Perk abilities show popups
- **Stat Changes**: Stat changes visualized
- **Effect Indicators**: Visual indicators for perk effects

## Technical Details

### Perk Card Detection
- **Card Type Check**: Check if card is Perk type
- **Data Loading**: Load PerkCardData
- **Ability Extraction**: Extract perk ability ID
- **Inventory Routing**: Route to perk inventory

### Perk Ability Collection
1. **Load Perk Inventory**: Load perk cards from save
2. **Iterate Perks**: Iterate through perk cards
3. **Extract Abilities**: Extract ability IDs from perks
4. **Return List**: Return list of ability IDs

### Perk Application Process
1. **Load Perks**: Load perk cards from inventory
2. **Create Temporary State**: Create temporary battle state
3. **Apply Perk Effects**: Apply each perk's effects
4. **Copy Stats**: Copy modified stats to mech
5. **Add Abilities**: Add perk abilities to battle state

### Data Structures
- **PerkCardData**: Perk card data structure
- **CardListSO**: Perk inventory storage
- **AbilityData**: Perk ability data
- **BattleState**: Battle state with perk abilities

---

*See also: [Card System](Card-System.md), [Battle System](Battle-System.md), [Save System](Save-System.md)*

