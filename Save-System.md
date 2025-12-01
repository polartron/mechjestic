# Save System

The Save System manages persistent data storage, including run progress, perk inventory, customization settings, and game state.

## Overview

The Save System:
- Saves run progress (level, stats, loot)
- Saves perk inventory
- Saves character customization
- Saves daily run progress
- Loads saved data on game start
- Handles failed runs

## Save Data Structure

### GameData
Main game data structure:
```csharp
public class GameData
{
    // Run Progress
    public int currentLevel = 1;
    public int maxLevelReached = 1;
    public float totalRunTime = 0f;
    public int totalCardsObtained = 0;
    public int totalEnemiesDefeated = 0;
    public int totalTreasuresFound = 0;
    
    // Loot
    public int totalLootDrawn = 0;
    public int uniqueLootCards = 0;
    public int totalLootCards = 0;
    public int bossLootCardIndex = 0;
    
    // Overpower
    public int overpower = 5;
    
    // Character Customization
    public string selectedCharacter = "";
    public string selectedMech = "";
    public string selectedStarterDeck = "";
    public string selectedDifficulty = "";
    public string selectedGamemode = "";
    
    // Daily Run
    public bool hasDailyRunProgress = false;
    public int dailyRunLevel = 1;
    public int dailyRunSeed = 0;
}
```

## Save Methods

### Run Progress

#### SaveRunData()
Saves current run progress:
- Current level
- Max level reached
- Run time
- Cards obtained
- Enemies defeated
- Treasures found
- Loot stats
- Boss loot index
- Overpower value

#### LoadRunData()
Loads saved run data:
- Returns all run progress data
- Returns default values if no save exists

#### ClearRunData()
Clears run data:
- Resets all run progress
- Used for new runs

### Perk Inventory

#### SavePerkCardsTemporary()
Saves perk cards during run:
- Saves to temporary storage
- Used during active run

#### LoadPerkCardsTemporary()
Loads perk cards during run:
- Loads from temporary storage
- Returns perk card inventory

#### SavePerkCardsPermanent()
Saves perk cards permanently:
- Saves to permanent storage
- Persists across sessions

#### LoadPerkCardsPermanent()
Loads perk cards permanently:
- Loads from permanent storage
- Returns perk card inventory

### Character Customization

#### SaveCharacterSelection()
Saves character selection:
- Stores character card name
- Updates GameData

#### GetCharacterSelection()
Gets saved character selection:
- Returns character card name
- Returns empty if not set

#### SaveMechSelection()
Saves mech selection:
- Stores mech card name
- Updates GameData

#### GetMechSelection()
Gets saved mech selection:
- Returns mech card name
- Returns empty if not set

#### SaveStarterDeckSelection()
Saves starter deck selection:
- Stores starter deck card name
- Updates GameData

#### GetStarterDeckSelection()
Gets saved starter deck selection:
- Returns starter deck card name
- Returns empty if not set

#### SaveDifficultySelection()
Saves difficulty selection:
- Stores difficulty card name
- Updates GameData

#### GetDifficultySelection()
Gets saved difficulty selection:
- Returns difficulty card name
- Returns empty if not set

#### SaveGamemodeSelection()
Saves game mode selection:
- Stores game mode card name
- Updates GameData

#### GetGamemodeSelection()
Gets saved game mode selection:
- Returns game mode card name
- Returns empty if not set

#### HasAllCustomizationSelections()
Checks if all customization selections made:
- Returns true if all selected
- Returns false if any missing

#### ClearCharacterCustomization()
Clears all customization selections:
- Resets all selection fields
- Used for new runs

### Daily Run

#### SaveDailyRunProgress()
Saves daily run progress:
- Saves daily run level
- Saves daily run seed
- Sets hasDailyRunProgress flag

#### HasSavedDailyRunProgress()
Checks if daily run progress exists:
- Returns true if daily run in progress
- Returns false otherwise

#### GetDailyRunProgress()
Gets daily run progress:
- Returns daily run level and seed
- Returns default if not set

#### ClearDailyRunProgress()
Clears daily run progress:
- Resets daily run data
- Used for new runs

### Loot Inventory

#### SaveLootInventory()
Saves loot inventory:
- Saves loot card list
- Saves loot stats

#### LoadLootInventory()
Loads loot inventory:
- Loads loot card list
- Loads loot stats

#### ClearLootInventory()
Clears loot inventory:
- Resets loot data
- Used for new runs

## Save Triggers

### Automatic Saves
- **Level Transition**: Save before transitioning
- **Battle Completion**: Save after battle
- **Treasure Obtained**: Save after treasure
- **Loot Selection**: Save after loot selection
- **Periodic**: Periodic auto-save

### Manual Saves
- **Player Initiated**: Player can manually save
- **Menu Save**: Save from menu
- **Pause Save**: Save on pause

## Load Process

### On Game Start
1. **Load GameData**: Load main game data
2. **Check Failed Run**: Check if run failed
3. **Load Run Data**: Load run progress
4. **Load Perks**: Load perk inventory
5. **Load Customization**: Load customization settings
6. **Load Loot**: Load loot inventory
7. **Restore State**: Restore game state

### On Continue Run
1. **Load Run Data**: Load saved run data
2. **Restore Level**: Restore level and seed
3. **Restore Position**: Restore player position
4. **Restore Stats**: Restore stats
5. **Restore Loot**: Restore loot inventory
6. **Generate Level**: Generate level from seed

## Failed Run Handling

### Detection
- **Check on Load**: Check if run failed on load
- **Failure Conditions**: Mech dead, deckout, surrender
- **State Check**: Check run state

### Handling
- **Stats Reset**: Reset stats on failure
- **Loot Clear**: Clear loot inventory
- **State Cleanup**: Clean up failed run state
- **New Run Ready**: Prepare for new run

## Data Persistence

### Storage Locations
- **Temporary**: Temporary storage during run
- **Permanent**: Permanent storage across sessions
- **PlayerPrefs**: Unity PlayerPrefs for simple data
- **JSON Files**: JSON files for complex data

### Data Formats
- **JSON**: JSON format for complex data
- **Binary**: Binary format for performance
- **Text**: Text format for readability

## Save Validation

### Data Validation
- **Check Integrity**: Validate save data integrity
- **Check Version**: Check save data version
- **Handle Corruption**: Handle corrupted saves
- **Fallback**: Fallback to defaults if invalid

### Version Management
- **Version Number**: Save data version number
- **Migration**: Migrate old save data
- **Compatibility**: Handle version compatibility

## Technical Details

### SaveManager
- **Singleton**: Singleton pattern
- **Static Methods**: Static save/load methods
- **Data Access**: Centralized data access
- **Error Handling**: Error handling for saves

### Save Timing
- **Frame-Based**: Saves on specific frames
- **Event-Based**: Saves on events
- **Time-Based**: Periodic saves
- **On Destroy**: Saves on scene unload

### Performance
- **Async Saves**: Asynchronous save operations
- **Batch Saves**: Batch multiple saves
- **Compression**: Compress save data
- **Caching**: Cache frequently accessed data

---

*See also: [Progression & Endless Mode](Progression-Endless-Mode.md), [Perk System](Perk-System.md), [Character Customization](Character-Customization.md)*

