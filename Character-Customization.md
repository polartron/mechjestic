# Character Customization

The Character Customization system allows players to configure their character, mech, starter deck, difficulty, and game mode before starting a run.

## Overview

Before starting a run, players go through a setup sequence to customize:
1. **Character**: Select character
2. **Mech**: Select mech
3. **Starter Deck**: Select starter deck
4. **Difficulty**: Select difficulty
5. **Game Mode**: Select game mode

## Setup Sequence

### MechjesticSetupSequence
- **Component**: Orchestrates setup sequence
- **Sequential Steps**: Executes steps in order
- **Progress Indicator**: Shows progress (e.g., "Step 1 of 5")
- **Skip Option**: Skips if already configured
- **Auto-Complete**: Automatically initializes endless mode after setup

### Setup Steps
Each step:
1. **Load Options**: Load available options for card type
2. **Show Selection**: Show CardSelectionSequence with options
3. **Wait for Selection**: Wait for player selection
4. **Store Selection**: Store selection
5. **Apply Selection**: Apply selection immediately (consume card)
6. **Next Step**: Move to next step

### Setup Flow
1. **Check if Needed**: Check if setup is needed
2. **For Each Step**:
   - Load options
   - Show selection UI
   - Wait for selection
   - Store and apply
3. **After All Steps**:
   - Save selections to SaveManager
   - Call `EndlessModeManager.InitializeEndlessMode()`
   - Transition to game

## Card Types

### Character Cards
- **Type**: `CardType.Character`
- **Purpose**: Character selection
- **Effect**: Sets starting character properties
- **Storage**: Saved to SaveManager

### Mech Cards
- **Type**: `CardType.Mech`
- **Purpose**: Mech selection
- **Effect**: Sets starting mech configuration
- **Storage**: Saved to SaveManager

### Starter Deck Cards
- **Type**: `CardType.StarterDeck`
- **Purpose**: Starter deck selection
- **Effect**: Sets initial deck composition
- **Storage**: Saved to SaveManager

### Difficulty Cards
- **Type**: `CardType.Difficulty`
- **Purpose**: Difficulty selection
- **Effect**: Sets game difficulty settings
- **Storage**: Saved to SaveManager

### Game Mode Cards
- **Type**: `CardType.Gamemode`
- **Purpose**: Game mode selection
- **Effect**: Sets game mode (endless, daily run, etc.)
- **Storage**: Saved to SaveManager

## Card Selection UI

### CardSelectionSequence
- **Reusable Component**: Generic card selection UI
- **Single Selection**: Each step uses single selection
- **Animation**: Cards fall in with animation
- **Hover**: Hover to see card info
- **Selection**: Click to select
- **Auto-Complete**: Auto-completes on selection

### Selection Behavior
- **Single Selection**: Choose one card per step
- **Auto-Complete**: Immediately complete on selection
- **Visual Feedback**: Cards animate on selection
- **Non-Selected Fall**: Non-selected cards fall away

## Save System Integration

### GameData Structure
```csharp
public class GameData
{
    public string selectedCharacter = "";
    public string selectedMech = "";
    public string selectedStarterDeck = "";
    public string selectedDifficulty = "";
    public string selectedGamemode = "";
}
```

### Save Methods
- **SaveCharacterSelection()**: Save character selection
- **SaveMechSelection()**: Save mech selection
- **SaveStarterDeckSelection()**: Save starter deck selection
- **SaveDifficultySelection()**: Save difficulty selection
- **SaveGamemodeSelection()**: Save game mode selection

### Load Methods
- **GetCharacterSelection()**: Get saved character
- **GetMechSelection()**: Get saved mech
- **GetStarterDeckSelection()**: Get saved starter deck
- **GetDifficultySelection()**: Get saved difficulty
- **GetGamemodeSelection()**: Get saved game mode

### Utility Methods
- **HasAllCustomizationSelections()**: Check if all selected
- **ClearCharacterCustomization()**: Clear all selections

## Card Routing

### CardListSO Integration
When customization cards are added:
- **Detection**: Card type detected
- **Routing**: Routed to appropriate handler
- **Consumption**: Card consumed immediately
- **Application**: Effects applied immediately
- **No Inventory**: Not added to regular inventory

### Handler Methods
- **HandleCharacterCard()**: Handle character card
- **HandleMechCard()**: Handle mech card
- **HandleStarterDeckCard()**: Handle starter deck card
- **HandleDifficultyCard()**: Handle difficulty card
- **HandleGamemodeCard()**: Handle game mode card

## Effect Application

### Character Effects
- **ApplyCharacterEffects()**: Apply character effects
- **Starting Stats**: Modify starting stats
- **Special Abilities**: Grant special abilities
- **Visual**: Modify visual appearance

### Mech Effects
- **ApplyMechEffects()**: Apply mech effects
- **Mech Configuration**: Set mech configuration
- **Visual Prefab**: Set visual prefab
- **Stats**: Modify starting stats

### Starter Deck Effects
- **ApplyStarterDeckEffects()**: Apply starter deck effects
- **Deck Loading**: Load starter deck configuration
- **Card Addition**: Add cards to deck
- **Save Deck**: Save deck to SaveManager

### Difficulty Effects
- **ApplyDifficultyEffects()**: Apply difficulty effects
- **Enemy Scaling**: Modify enemy scaling
- **Loot Rates**: Modify loot rates
- **Settings**: Store difficulty settings

### Game Mode Effects
- **ApplyGamemodeEffects()**: Apply game mode effects
- **Mode Settings**: Set game mode settings
- **Daily Run Seed**: Set daily run seed (if applicable)
- **Features**: Enable/disable features

## EndlessModeManager Integration

### InitializeEndlessMode()
After setup completes:
1. **Load Settings**: Load customization settings from SaveManager
2. **Apply Effects**: Apply customization effects
3. **Level Generation**: Modify level generation parameters
4. **Initialization**: Initialize endless mode

### Customization Settings Applied
- **Difficulty**: Enemy scaling based on difficulty
- **Game Mode**: Level seed based on game mode
- **Character/Mech**: Starting conditions based on selections
- **Starter Deck**: Initial deck from starter deck selection

## Skip Logic

### Already Configured
- **Check**: Check if selections already made
- **Skip**: Skip setup if configured
- **Load**: Load existing selections
- **Initialize**: Initialize with existing selections

### New Run
- **Reset**: Reset selections on new run (optional)
- **Setup**: Run setup sequence
- **Save**: Save new selections

## UI Integration

### Setup UI
- **Setup Sequence UI**: Main setup UI
- **Progress Text**: Shows progress (e.g., "Step 1 of 5")
- **Card Selection**: CardSelectionSequence component
- **Canvas Groups**: Show/hide UI elements

### Editor Tools
- **Create Prefab**: Create setup sequence prefab
- **Validate**: Validate setup sequence prefab
- **Add to Scene**: Add setup sequence to scene

## Technical Details

### Setup Step Configuration
```csharp
public class SetupStep
{
    public CardType cardType;
    public string promptText;
    public string saveKey;
}
```

### Sequence Execution
- **Coroutine-Based**: Uses coroutines for sequence
- **Wait for Selection**: Waits for selection events
- **Error Handling**: Handles errors gracefully
- **Cleanup**: Cleans up on completion/cancel

### Card Consumption
- **Immediate**: Cards consumed immediately
- **No Inventory**: Not added to inventory
- **Effect Application**: Effects applied immediately
- **Save**: Selections saved to SaveManager

---

*See also: [Card System](Card-System.md), [Save System](Save-System.md), [Progression & Endless Mode](Progression-Endless-Mode.md)*

