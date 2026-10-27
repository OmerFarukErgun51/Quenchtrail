# ⚒️ Demirici Oyunu — Game Design Prompt for Claude

---

## PROMPT (Kopyala & Claude'a yapıştır)

---

I am developing a 2D pixel art mobile game for Android (Google Play Store). I need your help with game development using Unity 2D. Here is the complete game design document:

---

## 🎮 GAME OVERVIEW

**Game Name:** Demir Usta (Iron Master)
**Platform:** Android (Google Play Store)
**Genre:** Casual RPG + Crafting Simulation + Monster Hunting
**Art Style:** Cute pixel art (Stardew Valley / Forager style)
**Perspective:** Top-down / Side-scrolling 2D
**Target Audience:** Global — all ages, families, casual players
**Session Length:** 5-15 minutes per session
**Tone:** Wholesome, cute, cozy — NOT dark or violent
**Monetization:** Google AdMob (rewarded ads) + In-App Purchases (IAP)
**Development Tool:** Unity 2D (free Personal license)
**Budget:** $0 (free assets only) + $25 Play Store registration

---

## 🎯 CORE CONCEPT

The player is a cute chubby dwarf blacksmith who runs their own forge. During the day, they craft weapons and sell them to villagers. In their free time, they go on monster hunting adventures using the weapons they crafted themselves. Monster loot is used to craft even better weapons. The game loop is satisfying, relaxing, and endlessly engaging.

**Key design philosophy:**
- Cute and wholesome — grandma and kids can both play
- Every system feeds into another (craft → hunt → loot → craft better)
- Short satisfying sessions (5-15 min)
- No pay-to-win — all content reachable for free (ads optional)

---

## 🕹️ CORE GAME LOOP

```
Mine materials (tap to collect)
        ↓
Craft weapons in the forge (mini-game)
        ↓
Go monster hunting with crafted weapon
        ↓
Collect monster loot & gold
        ↓
Sell extra weapons to villager NPCs
        ↓
Upgrade the forge / unlock new recipes
        ↓
Hunt stronger monsters → repeat
```

---

## 🏘️ MAIN HUB — THE VILLAGE

The central screen is a cute pixel art village with:
- **Blacksmith Shop** (player's main base) — with chimney smoke, anvil sign
- **Mine Entrance** — tap to gather ore and gems
- **Monster Portal** — enter to start hunting sessions
- **Marketplace** — sell weapons, buy materials, trade with NPCs
- **Upgrade Board** — spend gold to upgrade buildings

NPC villagers walk around and post weapon orders:
- "I need a sword! 🗡️" → Craft it → Deliver → Earn gold + bonus

---

## ⚒️ CRAFTING SYSTEM (Blacksmith Mini-Game)

When player enters the forge:

### Step 1: Select Recipe
- Choose weapon from recipe book
- See required materials (iron ore, gems, coal, monster loot)
- See result quality preview

### Step 2: Forging Mini-Game (3 steps)
```
HEAT: Hold button to heat metal
  → Keep temperature bar in GREEN zone
  → Too cold = weak weapon
  → Too hot = metal ruined

HAMMER: Tap rhythmically to shape
  → Hit at the right moment (timing mechanic)
  → Miss = lower quality

COOL: Swipe quickly through water
  → Speed matters
  → Too slow = warped blade
```

### Step 3: Quality Result
- ⭐⭐⭐ Perfect craft → Bonus stats, higher sell price
- ⭐⭐ Good craft → Normal stats
- ⭐ Poor craft → Reduced stats, sells for less

### Weapon Types (unlock progressively):
| Weapon | Materials | Effect in Combat |
|---|---|---|
| Wooden Sword | Wood x3 | Basic slash |
| Iron Sword | Iron x3, Coal x2 | Normal damage |
| Fire Sword | Iron x3, Ruby x1, Coal x2 | Burns enemies |
| Ice Axe | Iron x2, Crystal x2 | Slows enemies |
| Thunder Hammer | Iron x4, Lightning Stone x1 | Area damage |
| Dragon Blade | Dragon Scale x2, Gold x3 | Legendary — max damage |

---

## ⛏️ MINING SYSTEM

Simple tap mechanic:
- Tap on ore veins to collect materials
- Different mines unlock as player levels up:
  - Iron Mine (start)
  - Gold Mine (level 5)
  - Gem Cave (level 10)
  - Dragon Cavern (level 20 — rare materials)
- Each mine has limited daily resources (refills over time or watch ad)

---

## ⚔️ MONSTER HUNTING SYSTEM

Player enters the Monster Portal and selects a zone.

### Combat Mechanics (simple swipe-based):
```
Swipe RIGHT → Attack
Swipe LEFT → Block / Dodge
TAP monster → Special attack (weapon-specific)
Draw CIRCLE → Super attack (uses stamina)
```

### Monster types (all cute, not scary):
| Monster | Behavior | Loot |
|---|---|---|
| 🟢 Fat Slime | Slow, bounces | Gel (crafting material) |
| 👺 Sleepy Goblin | Falls asleep sometimes | Gold coins |
| 🐲 Baby Dragon | Breathes tiny fire puffs | Dragon scale (rare) |
| 🍄 Mushroom Man | Multiplies if ignored | Magic powder |
| 🐻 Bear King | WEEKLY BOSS — very tough | Special rare loot |
| 🌙 Night Bat | Only appears at night | Moon crystal |
| 💎 Crystal Golem | Strong armor, slow | Gems |

### Hunting Zones (unlock by level):
1. Green Forest (start) — easy monsters
2. Dark Cave (level 5) — medium difficulty
3. Volcano Mountain (level 10) — hard monsters
4. Haunted Castle (level 15) — elite monsters
5. Dragon's Lair (level 20) — boss-level zone

### Combat Rewards:
- Monster loot (for crafting)
- Gold coins
- XP points (for leveling up)
- Rare drops (special crafting materials)

---

## 📦 INVENTORY & EQUIPMENT

- Player equips ONE weapon at a time
- Weapon durability: degrades with use, must repair at forge
- Weapon storage: hold up to 10 weapons
- Material storage: upgradeable (costs gold)
- Gold wallet: unlimited

---

## 🏪 MARKETPLACE SYSTEM

### NPC Orders (daily quests):
- Villagers post weapon requests
- Example: "Knight needs Iron Sword x2 by tomorrow!"
- Complete order → Gold reward + relationship bonus
- Relationship with NPC grows → better prices, special orders

### Player Selling:
- Sell crafted weapons directly at market stall
- Price depends on quality (⭐⭐⭐ = much higher price)
- Supply/demand: if too many of same weapon, price drops

### Player Trading (multiplayer feature — add later):
- Trade weapons with other players
- Auction system for rare/legendary weapons
- Game takes 5% commission

---

## 📈 PROGRESSION SYSTEM

### Player Level (1-50):
- Gain XP from crafting and hunting
- Each level unlocks: new recipes, new zones, forge upgrades

### Forge Upgrades:
| Level | Name | Unlock |
|---|---|---|
| 1 | Basic Forge | Iron weapons |
| 2 | Stone Forge | Steel weapons, 2nd crafting slot |
| 3 | Steel Forge | Enchanted weapons |
| 4 | Magic Forge | Elemental weapons |
| 5 | Legendary Forge | Dragon weapons, fastest crafting |

### Skill Tree (3 paths):
```
⚒️ BLACKSMITH PATH → Better crafting quality, faster forging
⚔️ HUNTER PATH → More damage, better loot drops
💰 MERCHANT PATH → Better sell prices, more NPC orders
```
Player can invest in all three but must choose focus.

---

## ⏰ TIME & DAILY SYSTEM

- **Day/Night cycle** in game (1 game day = 10 real minutes)
- Night: special monsters appear (Night Bat, Moon Wolf)
- **Daily login reward**: grows each consecutive day
- **Daily missions** (3 per day):
  - "Craft 2 weapons" → 100 gold
  - "Defeat 5 monsters" → special gem
  - "Complete 1 NPC order" → rare material
- **Weekly boss**: Bear King appears every Monday, special loot

---

## 🏆 ACHIEVEMENT SYSTEM

- "First Sword" — craft your first weapon
- "Monster Slayer" — defeat 100 monsters
- "Perfect Smith" — craft 10 ⭐⭐⭐ weapons in a row
- "Dragon Hunter" — defeat first Baby Dragon
- "Market King" — earn 10,000 gold from sales
- "Legend" — reach max forge level

Each achievement: gold reward + profile badge

---

## 🎵 SOUND DESIGN

**Background music:** Cozy, cheerful pixel art style music
- Village: upbeat, friendly tune
- Forge: rhythmic, satisfying metal sounds
- Hunting: slightly more adventurous, fun tune
- Boss fight: exciting but not scary

**Sound effects:**
- Hammer hitting anvil: satisfying "clang"
- Fire crackling in forge
- Slime squishing when hit
- Coin pickup chime
- Level up fanfare
- Weapon crafted successfully: sparkle sound

---

## 📢 MONETIZATION STRATEGY

### Rewarded Ads (AdMob) — OPTIONAL, never forced:
- Watch ad → Refill mine resources instantly
- Watch ad → Double crafting XP for 30 minutes
- Watch ad → Extra daily mission slot
- Watch ad → Revive in combat (1 time per hunt)
- Watch ad → Extra NPC order slot

### In-App Purchases:
- Starter Pack: 5,000 gold + special hammer skin — $0.99
- Material Pack: rare gems bundle — $1.99
- VIP Pass (monthly): daily gold bonus + extra order slots — $2.99/month
- No Ads Pack: remove banner ads forever — $1.99
- Cosmetic skins: forge skin, character outfit — $0.99 each

### Local Pricing:
- Turkey: Turkish Lira (TL) — lower price point
- International: USD/EUR — standard pricing
- Google Play handles currency automatically

---

## 💻 TECHNICAL REQUIREMENTS

**Engine:** Unity 2D (free Personal license)

**Free Assets:**
- Character sprites: itch.io free pixel art packs, Kenney.nl
- Monster sprites: itch.io "free pixel monsters" packs
- Tiles/environment: Kenney.nl free tile packs
- UI: Kenney.nl free UI pack
- Music: OpenGameArt.org (free, CC licensed)
- Sound effects: Freesound.org (free)

**Required Integrations:**
- Google AdMob (free SDK) — rewarded ads + banner ads
- Unity IAP (free) — in-app purchases
- Google Firebase (free tier) — save data, leaderboards
- Unity Analytics (free) — player behavior tracking

**Technical specs:**
- Android 8.0+
- Portrait orientation (9:16)
- Target: mid-range phones (optimize for performance)
- Offline play: YES (marketplace/trading requires internet)
- Save system: cloud save via Firebase

---

## 🚀 MVP (First Version) SCOPE

Keep first release small and focused:

**Include:**
1. Village hub screen
2. Blacksmith forge (crafting mini-game)
3. Iron Mine (basic materials)
4. Green Forest hunting zone (3 monster types)
5. 5 weapon recipes
6. Basic NPC orders (3 per day)
7. AdMob rewarded ads
8. Basic IAP (starter pack + no ads)
9. Player level 1-20
10. Achievements (5 basic ones)

**Save for updates:**
- Multiplayer trading marketplace
- More hunting zones (cave, volcano, castle)
- Skill tree system
- Weekly boss events
- More weapon types (legendary tier)
- Player-to-player trading

---

## ❓ WHAT I NEED FROM YOU

Please help me:
1. Set up Unity 2D project structure for this game
2. Write the core crafting mini-game system (C#)
3. Create the combat/swipe mechanic system (C#)
4. Set up ScriptableObjects for weapons and monsters
5. Build the village hub scene with navigation
6. Integrate Google AdMob rewarded ads
7. Set up basic save/load system
8. Guide me step by step — I am a beginner / I have some experience

(Edit the last line to match your experience level before sending)

---

*Game: Demirici Oyunu (Demir Usta)*
*Platform: Android — Google Play Store*
*Engine: Unity 2D*
*Target Release: [Your Target Date]*
