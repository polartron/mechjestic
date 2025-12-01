# Tutorial System

The Tutorial System provides guided gameplay experiences for new players, teaching game mechanics through interactive tutorials.

## Overview

The Tutorial System:
- Provides tutorial battles
- Shows first-time player tips
- Uses dialogue system for instructions
- Tracks tutorial completion
- Customizes gameplay for tutorials

## Tutorial Battles

### Tutorial Battle Settings
- **IsTutorial Flag**: Marks battle as tutorial
- **Special Mechanics**: Disabled overpower system
- **Custom Hand Drawing**: Tutorial-specific hand drawing
- **Tutorial Dialogues**: Tutorial-specific dialogues

### Tutorial Battle Features
- **No Overpower**: Overpower system disabled
- **Custom Opening Hand**: Custom hand size/contents
- **Guided Actions**: Guided player actions
- **Simplified Mechanics**: Simplified battle mechanics

## First-Time Tips

### Tip System
- **First-Time Flags**: Flags for first-time events
- **Tip Display**: Shows tips on first occurrence
- **Dialogue Integration**: Uses dialogue system
- **Completion Tracking**: Tracks tip completion

### Tip Examples
- **FirstTimeMultipleEnemies**: Tip when encountering multiple enemies
- **FirstTimeNoDamage**: Tip when taking no damage
- **FirstTimeCardPlay**: Tip when playing first card
- **FirstTimeAttack**: Tip when making first attack

## Dialogue System

### DialogueManager
- **Component**: Manages dialogue display
- **Show Dialogue**: Shows dialogue by ID
- **Dialogue Content**: Localized dialogue content
- **Visual Display**: Dialogue UI display

### Dialogue Integration
- **Tutorial Dialogues**: Tutorial-specific dialogues
- **First-Time Dialogues**: First-time event dialogues
- **Contextual**: Context-based dialogues
- **Localized**: Multi-language support

## Tutorial Progression

### Tutorial Flow
1. **Tutorial Start**: Tutorial battle begins
2. **Instructions**: Show instructions via dialogue
3. **Guided Actions**: Guide player through actions
4. **Completion**: Complete tutorial
5. **Flag Set**: Set completion flag
6. **Next Tutorial**: Proceed to next tutorial

### Tutorial Tracking
- **Completion Flags**: Track tutorial completion
- **Save System**: Save completion to SaveManager
- **Skip Option**: Skip completed tutorials
- **Replay Option**: Replay tutorials

## Tutorial Customization

### Battle Customization
- **Disabled Features**: Disable complex features
- **Simplified UI**: Simplified UI for tutorials
- **Guided Interactions**: Guide player interactions
- **Visual Hints**: Visual hints and highlights

### Card Customization
- **Tutorial Deck**: Special tutorial deck
- **Simplified Cards**: Simplified card effects
- **Guided Selection**: Guide card selection
- **Visual Feedback**: Enhanced visual feedback

## Save System Integration

### Tutorial Flags
- **SaveManager Integration**: Save tutorial flags
- **Completion Tracking**: Track completion
- **Skip Logic**: Skip based on completion
- **Replay Logic**: Allow replay

### Flag Examples
- **FIRST_MULTIPLE_ENEMIES_SHOWN**: Multiple enemies tip shown
- **NO_DAMAGE_TIP_SHOWN**: No damage tip shown
- **TUTORIAL_COMPLETE**: Tutorial completed

## Visual Feedback

### Tutorial UI
- **Highlight Elements**: Highlight tutorial elements
- **Arrow Indicators**: Arrow indicators for actions
- **Tooltips**: Tooltips for explanations
- **Progress Indicators**: Show tutorial progress

### Tutorial Animations
- **Guided Animations**: Animations guide actions
- **Highlight Animations**: Highlight important elements
- **Completion Animations**: Completion celebrations

## Technical Details

### TutorialManager
- **Component**: Manages tutorial system
- **Tutorial Detection**: Detects tutorial battles
- **Tip Management**: Manages first-time tips
- **Dialogue Integration**: Integrates with dialogue system

### Tutorial Utils
- **Utility Functions**: Tutorial utility functions
- **Target Types**: Tutorial target types
- **Helper Methods**: Helper methods for tutorials

### Tutorial Detection
- **Battle Settings**: Check battle settings for tutorial flag
- **Tutorial Mode**: Enable tutorial mode
- **Feature Toggles**: Toggle features for tutorial

---

*See also: [Battle System](Battle-System.md), [Save System](Save-System.md)*

