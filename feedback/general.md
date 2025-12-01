## Game Design Review: Mechjestic (SteamDeckBuilder)

### What's Working Well ✓

**Tactical Enemy System** — The six enemy roles (Aggressive, Strategist, Resilient, Repairing, Utilitarian, Disruptive) create genuine tactical puzzles. The push mechanics and support role positioning give the overworld real strategic depth. This is your strongest system.

**Adjacency Buff System** — Fights becoming harder based on adjacent enemies in the overworld is clever. It creates a natural "clearing the perimeter" gameplay loop and rewards spatial awareness.

**Overpower Economy** — First attack free, escalating costs for additional attacks is elegant. It creates interesting decisions between efficient one-hit kills vs. burning resources for burst damage.

**Pre-run Customization** — Character → Mech → Starter Deck → Difficulty → Game Mode is a solid onboarding flow that lets players express preference without overwhelming them.

---

### Critical Improvements Needed

#### 1. **The Overworld Needs More "Verbs"**

Currently the overworld loop is: Move → Fight → Loot Treasure → Repeat.

**Missing elements:**
- **Shops/Merchants** — No way to spend a currency or trade cards
- **Card Removal/Upgrade Stations** — Deck thinning is fundamental to deck-builders (Slay the Spire, Monster Train)
- **Random Events** — Risk/reward narrative moments ("A damaged mech offers you a deal...")
- **Repair/Rest Tiles** — Recovery options between fights
- **Environmental Hazards** — Tiles that damage you, modify battles, or change rules

**Recommendation:** Add 3-4 new tile types that create meaningful choices, not just fights and treasure.

---

#### 2. **The Engine/Fuel System is Underutilized**

You have this fascinating engine upgrade system with fuel management, but it feels bolted on rather than central to the identity. 

**The Problem:** Cards have costs, engines have fuel, but where's the tension? Where's the "I have to manage my resources carefully" moment?

**Recommendations:**
- Make engine choice as impactful as mech choice (different playstyles, not just stat sticks)
- Add cards that interact with fuel (sacrifice fuel for power, cards that generate fuel)
- Engine overheating risk? Push-your-luck mechanics with the engine
- Fuel scarcity in harder difficulties

---

#### 3. **Deckout as a Loss Condition Needs Counterplay**

**(DECKOUT REMOVED)**

#### 4. **Meta-Progression Feels Shallow**

The perk system persists across runs — great! But it needs more:

**Missing:**
- **Unlockable Characters/Mechs/Cards** — Long-term goals beyond "reach floor X"
- **Achievement System** — "Win without taking damage" → Unlock Stealth Mech
- **Mastery Tracks** — Play a character enough → unlock their legendary variant
- **Starter Deck Unlocks** — Earn new starter deck options through play

**Roguelikes live and die on meta-progression.** Players need a reason to play run #50 as much as run #5.

---

#### 5. **Card Synergy/Build Identity is Unclear**

Reading through your card types, I don't see clear "archetypes" or synergistic build paths.

**Good deck-builders have identifiable builds:**
- Slay the Spire: Poison build, Shiv build, Strength scaling, Block fortress
- Monster Train: Burnout, Incant, Frostbite, etc.

**Recommendations:**
- Define 3-5 distinct "archetypes" per mech
- Design cards that specifically synergize within archetypes
- Make loot tables weighted toward current build direction
- Add "signature cards" that define builds (like Dead Cells weapons)

---

#### 6. **The Rift System Needs Explanation and Expansion**

"Enduring Rift" activates at level 10+ — but what does it *do*? This sounds like it could be a fantastic difficulty escalation system (like Ascension in Slay the Spire or Heat in Hades).

**Recommendations:**
- Make Rift a visible, escalating challenge system
- Let players opt into higher Rift levels for better rewards
- Each Rift level adds a modifier ("Enemies have +10% HP", "Draw 1 less card", etc.)
- Leaderboards for Rift levels reached

---

#### 7. **Boss Design Needs Mechanical Variety**

Every 3rd floor is a boss — but are bosses mechanically distinct? Or just stat sticks with higher numbers?

**Great bosses should:**
- Have unique mechanics (multi-phase, summons, environmental effects)
- Require different strategies to defeat
- Be memorable encounters, not just "bigger enemy"

**Recommendation:** Design 5-7 distinct boss archetypes with unique mechanics, then scale them for different floor depths.

---

#### 8. **The Treasure System Could Create More Tension**

Currently: Clear nearby enemies → Open treasure safely.

**What if:**
- Some treasures are "trapped" (fight after opening)
- Some treasures have rarity visible before opening (risk assessment)
- Cursed treasures offer powerful cards with downsides
- Treasure contents vary based on how *quickly* you reached them (speed bonus)

---

### Quick Wins (Low Effort, High Impact)

| Suggestion | Why |
|------------|-----|
| Add a "card remove" tile type | Deck thinning is expected in deck-builders |
| Show enemy intent in overworld | Let players plan approaches by seeing enemy types |
| Add "elite" enemies between bosses | Harder fights with better rewards (floor 2, 5, 8...) |
| Equipment comparison view | When equipping, show stat diff vs. current |
| Run summary screen | After death, show stats, choices made, "what killed you" |
| Daily run leaderboards | Competitive element for the daily seed system |

---

### The One Big Question

**What makes Mechjestic *Mechjestic*?**

Reading the documentation, I don't yet feel the *fantasy* of piloting a mech. The limb equipment system is there (Torso, Arms, Legs), but where's:
- Component damage (losing an arm changes your options)?
- Overheating/heat management?
- Weapon loadout choices that change combat fundamentally?
- The weight and power of being in a war machine?

The best deck-builders have a *feeling*. Slay the Spire feels like a dungeon crawl. Monster Train feels like a desperate defense. **What does Mechjestic feel like?**

---

### Priority Recommendations

1. **Add overworld variety** (shop, upgrade, events) — This is the biggest gap
2. **Define card archetypes** — Players need build identity
3. **Expand meta-progression** — Unlockables keep players invested
4. **Make the engine matter** — It's your unique system; lean into it
5. **Enhance boss design** — Make them memorable, not just harder

Would you like me to dive deeper into any of these areas, or sketch out specific implementations?
