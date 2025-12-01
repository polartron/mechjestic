# Card System

The Card System is the foundation of SteamDeckBuilder, managing all card types, effects, and interactions.

## Card Types

### Instant Cards
- **Type**: `CardType.Instant`
- **Usage**: One-time use cards
- **Effect**: Immediate effect when played, then discarded
- **Examples**: Damage cards, healing cards, utility cards

### Equip Cards
- **Type**: `CardType.Equip`
- **Usage**: Equipment cards
- **Effect**: Equipped to mech limbs, modify stats permanently
- **Slots**: Torso, Left Arm, Right Arm, Left Leg, Right Leg
- **Effects**: Modify HP, Power, Defense, Decay, or grant abilities

### Hero Cards
- **Type**: `CardType.Hero`
- **Usage**: Special hero equipment
- **Effect**: Equipped to torso slot, provides:
  - Hero ability (unique powerful ability)
  - Bonus ability (additional effect)
- **Limitation**: Hero abilities have usage limits

### Perk Cards
- **Type**: `CardType.Perk`
- **Usage**: Permanent upgrades
- **Effect**: Consumed immediately, grants perk ability
- **Persistence**: Perks persist across runs
- **Storage**: Perk inventory (separate from deck)

### Customization Cards

#### Character Cards
- **Type**: `CardType.Character`
- **Usage**: Character selection before run
- **Effect**: Sets starting character properties

#### Mech Cards
- **Type**: `CardType.Mech`
- **Usage**: Mech selection before run
- **Effect**: Sets starting mech configuration

#### Starter Deck Cards
- **Type**: `CardType.StarterDeck`
- **Usage**: Starter deck selection before run
- **Effect**: Sets initial deck composition

#### Difficulty Cards
- **Type**: `CardType.Difficulty`
- **Usage**: Difficulty selection before run
- **Effect**: Sets game difficulty settings

#### Game Mode Cards
- **Type**: `CardType.Gamemode`
- **Usage**: Game mode selection before run
- **Effect**: Sets game mode (endless, daily run, etc.)

## Card Data Structure

### Base Properties
- **BaseID**: Unique identifier
- **PrefabName**: Visual prefab reference
- **Cost**: Fuel cost to play
- **DisplayNames**: Localized names (multi-language)
- **Descriptions**: Localized descriptions (multi-language)
- **BaseEffectIDs**: List of effect IDs
- **CardEffectRuntimeIDs**: Runtime effect IDs (generated)

### Loot Configuration
- **LootRarity**: Common, Uncommon, Rare, Epic, Legendary
- **IncludedInGame**: Whether card appears in game
- **CustomWeight**: Custom loot weight override
- **Tags**: Categorization tags

### Card Effects

Cards contain multiple effects that execute when played:

#### Effect Types
- **MoveCard**: Move cards between locations (draw, discard, recycle, etc.)
- **NoDraw**: Prevent card drawing
- **Fuel**: Modify engine fuel
- **HP**: Modify health points
- **Power**: Modify attack power
- **Defense**: Modify defense
- **ActiveEffects**: Trigger active effects
- **Decay**: Modify decay (damage over time)
- **Rift**: Modify rift effects

#### Effect Calculation Types
- **Absolute**: Direct value
- **Reference**: Reference to another value
- **MultiplierWithReference**: Multiply by reference
- **TriggeringChangeAmount**: Use triggering change amount

#### Effect Targets
- **MechOrEnemy**: Can target mech or enemy
- **Mech**: Only mech
- **Enemy**: Only enemy
- **Engine**: Engine only
- **BattleState**: Battle state
- **CardLocation**: Card location (deck, hand, scrap)

## Card Locations

### Hand
- Cards available to play
- Maximum hand size (configurable)
- Cards drawn from deck

### Deck
- Draw pile
- Shuffled at battle start
- Cards drawn from top
- Deckout occurs when empty

### Scrap Pile
- Discarded cards
- Can be recycled back to deck (via effects)
- Visible in UI

### Equipped
- Cards equipped to mech limbs
- Modify stats permanently
- Can be replaced by new equips

## Card Interactions

### Playing Cards
1. Card selected from hand
2. Cost checked (fuel/overpower)
3. Card effects execute
4. Card moved to appropriate location:
   - Instant → Scrap pile
   - Equip → Equipped slot
   - Hero → Equipped to torso

### Card Effects Execution
1. Effects activate in order
2. Each effect checks activation conditions
3. Effects modify battle state
4. Visual feedback shown
5. Stat changes visualized

### Card Drawing
- **Draw**: From deck to hand
- **Discard**: From hand to scrap
- **Recycle**: From scrap to deck
- **Salvage**: From scrap to hand
- **Mill**: Remove from deck
- **Spin**: Shuffle and draw

## Card Selection UI

### CardSelectionSequence
Generic reusable card selection component:
- **Features**:
  - Single or multiple selection
  - Animated card reveal
  - Hover interactions
  - Selection confirmation
  - Auto-complete option

- **Usage**:
  - Battle end rewards
  - Treasure chests
  - Character customization
  - Perk selection

### Selection Behavior
- **Single Selection**: Choose one card
- **Multiple Selection**: Choose multiple cards (up to max)
- **Auto-complete**: Immediately complete on selection
- **Manual Complete**: Require confirmation

## Card Visuals

### Card Display
- **Card Object**: Visual representation
- **Graphics**: Card art and icons
- **Info Box**: Hover information display
- **VFX**: Visual effects on cards
- **Animations**: Card animations (hover, select, play)

### Card Sorting
- **Alphabetical**: By name
- **CardType**: By card type
- **FuelCost**: By cost
- **Limb**: By equip slot

## Card Data Management

### DataManager
- Loads card data from assets
- Provides card data by type
- Manages card text assets
- Card type detection

### CardListSO
- ScriptableObject for card lists
- Manages card inventory
- Handles card addition/removal
- Routes cards to appropriate systems:
  - Perk cards → Perk inventory
  - Customization cards → Applied immediately
  - Regular cards → Deck/inventory

## Loot System Integration

### Loot Rarity
Cards have loot rarity that affects:
- Drop rates
- Loot table weighting
- Visual display

### Loot Tags
Cards can have tags for:
- Loot table filtering
- Context-based drops
- Special loot conditions

## Card Customization

### Character Customization
Cards used for pre-run setup:
1. Character selection
2. Mech selection
3. Starter deck selection
4. Difficulty selection
5. Game mode selection

### Setup Sequence
- Sequential card selection steps
- Progress indicator
- Skip if already configured
- Saves selections to SaveManager

## Technical Details

### Card Creation
- Cards created from TextAsset data
- Runtime IDs generated
- Effects instantiated
- Visual prefab spawned

### Card Copying
- Cards copied for battle state
- Prevents state mutation
- Deep copy of effects
- Runtime ID preservation

### Card Peeking
- Preview card consequences
- Creates temporary battle state
- Shows stat changes
- Non-destructive preview

---

*See also: [Battle System](Battle-System.md), [Loot System](Loot-System.md), [Character Customization](Character-Customization.md)*

