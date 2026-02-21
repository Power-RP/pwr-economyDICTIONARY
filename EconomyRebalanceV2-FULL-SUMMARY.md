# Power RP 5.0 — Economy Rebalance Plan V2

> **Date:** February 20, 2026  
> **Status:** DRAFT — Awaiting approval before any edits  
> **Scope:** All income-generating scripts across the server  
> **Goal:** Balance all jobs so no single activity dominates, ensure legal &lt; illegal &lt; risk-based progression, fix known exploits, integrate DevHub jobs into the economy tiers

---

## Table of Contents

- [PART 1 — Current State Audit (What's Actually Broken)](#part-1--current-state-audit)
- [PART 2 — Target Economy Framework](#part-2--target-economy-framework)
- [PART 3 — Survival Costs (Food/Drink Baseline)](#part-3--survival-costs)
- [PART 4 — Mining Fixes (RxMining + pwr-sellmaterials)](#part-4--mining-fixes)
- [PART 5 — Fishing Adjustments (0r-fishingv2)](#part-5--fishing-adjustments)
- [PART 6 — Diving Overhaul (s4-diving)](#part-6--diving-overhaul)
- [PART 7 — Job Center Tweaks (wais-jobpack)](#part-7--job-center-tweaks)
- [PART 8 — Illegal Tablet Corrections (0r-illegalpack)](#part-8--illegal-tablet-corrections)
- [PART 9 — Drug Selling Rebalance (op-drugselling)](#part-9--drug-selling-rebalance)
- [PART 10 — Private Drug Labs (0r-drugbusiness + plt_drugs)](#part-10--private-drug-labs)
- [PART 11 — DevHub Jobs Integration](#part-11--devhub-jobs-integration)
- [PART 12 — Final Master Pay Table](#part-12--final-master-pay-table)
- [PART 13 — Summary of All Changes](#part-13--summary-of-all-changes)

---

## PART 1 — Current State Audit

### Critical Problems Found

The previous economy guide had **major inaccuracies**. Here's what's actually broken:

#### 1. Mining is OP — Laser Drill Exploit
- **Laser Drill durability: 300 hits** — lasts 15-25 full rock nodes before breaking
- At Level 10 with Laser Drill (3.0× speed): Diamond ore takes only **10 seconds** per hit
- Each hit drops $125-250 cash (50% chance) PLUS 1 diamond item
- With 300 durability and fast hitting, a player can mine continuously for **~50 minutes** on one drill
- **Real $/hr at Level 10: $8,000-12,000+** when factoring in speed multipliers and gem drops
- **Coal/Carbon are underpaid**: $6 and $10 base sell price at foundry × 0.5 multiplier = **$3 and $5 per ore**. Nobody mines these because gems/gold pay 10-20x more per hit

#### 2. Diving Economy is Fantasy
The old economy doc claimed **$9,000-27,000/hr** for diving. This is completely wrong because:
- **Crate loot has NO cash drops** — the "money" reward type is not in the prize list, making the money branch unreachable in code
- Crates only give items (lockpicks, goldchains, rolexes, etc.)
- Actual item values at qb-pawnsystem: rolex=$100, diamond=$100, platinumbar=$200, 10kgoldchain=$75, goldbar=$120
- Many items (rubber, plastic, steel, aluminium etc.) have **no sell avenue at all**
- **Real $/hr for Mission 1**: $300 completion + ~7 items averaging ~$50 fenceable value = **~$650 per run → ~$2,600-3,900/hr**
- **Real $/hr for Mission 3**: $600 + $250 + goldbar($120) + rolex($100) + diamond_ring(no price in system!) + ~13 items = **~$1,700-2,500 per run → ~$5,100-8,300/hr**
- Still decent, but NOT the $21,000-27,000/hr claimed. Off by 3-4x.

#### 3. Drug Labs Have 0% Police Alert
The config files for weed, meth, and cocaine labs all have `police_alert_chance = 0.0`. The old economy doc listed 25%/35%/40% but these are NOT the actual values. Drug labs are currently **risk-free** production, which makes them overpowered relative to direct-payout jobs.

#### 4. Moonshine Material Costs Are Wrong
Old doc said: Still $60 + Pack $30 = $90 total. **Actual config**: Still $30 + Pack $15 = **$45 total**. This means moonshine net profit is $1,155 per run, not $1,110.

#### 5. Public Drug Labs Pay MORE Than Private Labs
| Source | Drug | Sell Price (optimal) | Cost per cycle | Net per cycle |
|--------|------|---------------------|----------------|---------------|
| **Public Cocaine** (0r-illegalpack) | packed_coke | $350 | $75 | **$625** for 2 bricks |
| **Public Meth** (0r-illegalpack) | packed_meth | $250 | $100 | **$400** for 2 bricks |
| **Public Weed** (0r-illegalpack) | rolled_weed | $50 | $0 (reusable) | **$250** for 5 joints |
| **Phantom Weed** (paid lab) | weed5/11/etc | $85 | ingredients+time+employees | much less per unit when factoring cost |
| **Phantom Meth** (paid lab) | bagmeth variants | $85 | ingredients+time+employees | much less |
| **Phantom Cocaine** (paid lab) | cocainepackage24/25 | $85 | ingredients+time+employees | much less |

Public lab drugs sell for $50-350 each. Phantom tier drugs sell for only **$85 optimal**. This is backwards — paid labs should produce superior product.

#### 6. DevHub Jobs Are Not Integrated
- **House Robbery**: Items sell for $5 each (pawn shop disabled), only real income is $500 from Crime Traders app = **~$525/run, ~$1,050/hr** — underpaid for the risk
- **Truck Robbery**: markedbills $200-1000 + chance at goldbar/diamond + $500 app reward = **~$1,700-4,000/run** — wildly variable but potentially OP
- **Drywood Cutter**: $250/job + quests ($600-800) = **~$800-1,200/hr** — reasonable
- **Herbal Alchemist**: $250/job + quests ($200-300) = **~$700-1,000/hr** — reasonable
- **Racing**: Entry fee gambling, weekly scheduled races $2,000-6,000 winner take all — not a reliable income source

#### 7. op-drugselling Actual Prices vs Economy Doc

| Drug | Old Doc Optimal | **Actual Config Optimal** | Diff |
|------|----------------|--------------------------|------|
| rolled_weed | $40 | **$50** | +25% |
| packed_meth | $250 | **$250** | same |
| packed_coke | $350 | **$350** | same |
| moonshine | $10 | **$45** | +350% |
| Phantom (all) | $25 | **$85** | +240% |
| Exotic (all) | $55 | **$185** | +236% |
| Mythical (all) | $150 | **$285** | +90% |

The old economy doc was using **completely wrong drug sell prices**. The actual values are significantly higher, especially for moonshine and phantom tier.

---

## PART 2 — Target Economy Framework

### Design Principles

1. **Legal jobs pay less but are safe** — zero risk, consistent income
2. **Illegal jobs pay more but carry escalating risk** — police, material loss, dirty money
3. **Paid private labs MUST out-earn public free labs** — real money investment = superior returns
4. **No single activity should dominate** — everything should be within 20-30% of its tier
5. **Progression within each system should feel rewarding** — each level/tier unlock is a noticeable bump
6. **Players must eat** — survival costs create a baseline income requirement
7. **Grinding should take time but not be boring** — 2-4 hours/day for 2-3 months to reach endgame

### Target $/hr Bands (After Rebalance)

| Tier | Activities | Target $/hr | Risk |
|------|-----------|-------------|------|
| **1 — Starter** | Fishing (Lvl 1-2), Hotdog, Gardener, Hunter | $500-1,000 | None |
| **2 — Beginner** | Fishing (Lvl 3-4), Road Helper, Drywood Cutter, Herbal Alchemist, Diving (Easy) | $1,000-1,800 | None-Low |
| **3 — Intermediate** | Fishing (Lvl 5), Bus Driver, Detectorist, Mining (Lvl 0-2), Illegal Tier 1-3, House Robbery | $1,500-2,500 | None-Medium |
| **4 — Skilled** | Fire Dept, Electrician, Mining (Lvl 3-4), Illegal Tier 4-6, Diving (Medium), Truck Robbery | $2,500-3,500 | None-Medium |
| **5 — Expert** | Project Car, Diver (JC), Mining (Lvl 5-6), Illegal Tier 7-8, Public Drug Labs | $3,000-4,500 | None-High |
| **6 — Master** | Trucker, Mining (Lvl 7-8), Illegal Tier 9-10, Phantom Drug Labs | $4,000-5,500 | None-High |
| **7 — Endgame** | Mining (Lvl 9-10), Fraud, Exotic/Mythical Drug Labs, Diving (Dangerous) | $5,000-7,000 | None-Extreme |

### Key Rule: Illegal Endgame > Legal Endgame (but with risk tax)
- Legal max (Laser Drill mining): ~$5,500-6,000/hr (zero risk, 350+ hour investment)
- Illegal max (Fraud): ~$6,000-7,000/hr (extreme risk, 50+ hour investment, can lose money)
- Paid Drug Labs max (Mythical): ~$6,500-7,500/hr (investment + time + employees + selling risk)

---

## PART 3 — Survival Costs

### Hunger/Thirst Drain Rates
- Hunger: 4.8 per tick (100% → 0% in ~20.8 minutes of game time)
- Thirst: 3.8 per tick (100% → 0% in ~26.3 minutes of game time)

### Food Restoration (mt-restaurants)
- Food: **+30% hunger** per item (50% with daily special)
- Drink: **+15% thirst** per item (30% with daily special)
- Food spoils in **3 hours** real time

### Daily Food Costs (assuming ~4 hour play session)
- Need ~4-6 food items ($40-60 each) = **$160-360** for hunger
- Need ~8-10 drink items ($40-60 each) = **$320-600** for thirst  
- **Total daily survival: ~$480-960/session**

### What This Means
- A starter player earning $500-1,000/hr needs to work ~30-60 min just for food
- This is intentional — early game should feel tight, motivating progression
- An endgame player at $5,000+/hr spends less than 10 min of earnings on food

---

## PART 4 — Mining Fixes (RxMining + pwr-sellmaterials)

### Problem Summary
Mining with Laser Drill is too strong. The 300 durability + 3.0× speed + high cash drops makes it the best $/hr in the game risk-free. Also, coal/carbon are worthless, creating a supply shortage.

### Changes

#### 4.1 — Reduce Laser Drill Durability
| Setting | Current | New |
|---------|---------|-----|
| Laser Drill durability | 300 | **100** |
| Mining Drill durability | 200 | **150** |

**Why:** 300 hits on a Laser Drill at 3.0× speed means ~50 min of continuous mining. At 100 hits, it lasts ~17 min before needing replacement ($25,000). This adds a real ongoing cost: ~$25,000 per 17 minutes = **~$1,470/min in tool overhead** which eats into profits.

#### 4.2 — Reduce Cash Drop Amounts (Per-Hit Random Cash)
| Ore | Current Cash | New Cash | Current Chance | New Chance |
|-----|-------------|----------|----------------|------------|
| Coal | $15-30 | **$10-20** | 50% | **40%** |
| Carbon | $18-35 | **$12-25** | 50% | **40%** |
| Copper | $25-50 | **$18-35** | 50% | 50% |
| Iron | $30-60 | **$22-45** | 50% | 50% |
| Aluminum | $40-80 | **$30-55** | 50% | 50% |
| Sulfur | $45-90 | **$32-60** | 50% | 50% |
| Gold | $50-100 | **$35-70** | 50% | 50% |
| Gems (all) | $75-150 | **$50-100** | 50% | 50% |
| Diamond | $125-250 | **$75-150** | 50% | 50% |
| Ruby | $100-200 | **$60-120** | 50% | 50% |
| Sapphire | $100-200 | **$60-120** | 50% | 50% |
| Tanzanite | $115-225 | **$70-140** | 50% | 50% |

**Why:** The per-hit cash combined with ore sales was stacking income too high. Reducing cash drops keeps ore sales as the primary income driver.

#### 4.3 — Boost Coal/Carbon Foundry Sell Prices
| Ore | Current Base | New Base | Current Min | New Min | Current Max | New Max |
|-----|-------------|----------|-------------|---------|-------------|---------|
| Coal | $6 | **$12** | $3 | **$7** | $9 | **$18** |
| Carbon | $10 | **$16** | $5 | **$9** | $14 | **$24** |

**Why:** Coal and carbon are needed by the server economy but nobody mines them because they pay terribly. Doubling their foundry value makes them worth mining at lower levels and fixes the supply shortage. At 0.5× foundry multiplier, effective coal price goes from $3 → $6 per unit, still the lowest ore but now viable.

#### 4.4 — Reduce Ore Item Drop Quantities at High Tiers  
| Ore | Current Drop | New Drop |
|-----|-------------|----------|
| Common (Coal/Carbon) | 1-4 | **1-4** (unchanged) |
| Uncommon (Copper/Iron) | 1-4 | **1-3** |
| Rare (Aluminum/Sulfur/Gold) | 1-4 | **1-3** |
| Gems T4 | 1 | **1** (unchanged) |
| Gems T5 | 1 | **1** (unchanged) |

**Why:** Fewer ore drops per hit at mid tiers means less foundry income per hit, compressing the gap between early and late mining.

#### 4.5 — Estimated New Mining $/hr

| Level | Tool | Current $/hr | New $/hr | Change |
|-------|------|-------------|----------|--------|
| 0 | Stone Pick | ~$600 | ~$500 | -17% |
| 1-2 | Iron Pick | ~$1,400 | ~$1,100 | -21% |
| 3-4 | Steel/Titanium | ~$2,750 | ~$2,200 | -20% |
| 5-6 | Diamond/Quantum | ~$3,300 | ~$2,800 | -15% |
| 7-8 | Mining Drill | ~$5,950 | ~$4,200 | -29% |
| 9-10 | Laser Drill | ~$8,000+ | ~$5,500 | -31% |

**Result:** Mining Lvl 10 drops from $8,000+ to ~$5,500/hr, making it competitive with Trucker and high-tier illegal jobs but no longer the undisputed king. The reduced drill durability adds a $25,000 replacement cost every ~17 min which factors into the real $/hr.

---

## PART 5 — Fishing Adjustments (0r-fishingv2)

### Problem Summary
Fishing is fine at its current position as a chill, low-risk activity. The old economy doc's rates ($275-1,470/hr) are roughly accurate. Minor tweaks needed for consistency with the new tiers.

### Changes

#### 5.1 — Small Fish Price Bumps
| Fish | Current Price | New Price | Why |
|------|-------------|-----------|-----|
| Fish (generic) | $8 | **$10** | Floor too low |
| Bluegill | $8 | **$10** | Floor too low |
| Bass | $10 | $10 | Fine |
| Drumfish | $12 | $12 | Fine |

#### 5.2 — Endgame Fish Price Bumps
| Fish | Current Price | New Price | Why |
|------|-------------|-----------|-----|
| Tuna | $65 | **$75** | Endgame fish should reward Rod 5 investment |
| Swordfish | $80 | **$90** | Same |
| Tiger Shark | $100 | **$115** | Same |
| Killer Whale | $130 | **$150** | Same |

#### 5.3 — Estimated New Fishing $/hr

| Rod Level | Current $/hr | New $/hr |
|-----------|-------------|----------|
| 1 | $275-385 | **$320-440** |
| 2 | $350-490 | **$380-520** |
| 3 | $450-630 | **$480-660** |
| 4 | $700-980 | **$750-1,050** |
| 5 | $1,050-1,470 | **$1,200-1,700** |

**Result:** Fishing stays in Tier 1-2 as intended. Rod 5 endgame fishing at ~$1,200-1,700/hr is comparable to drywood cutter and herbal alchemist.

---

## PART 6 — Diving Overhaul (s4-diving)

### Problem Summary
Diving's actual economy is vastly different from what was documented. There are NO cash drops from crates (code bug/oversight), and item fence values are low. The fixed completion rewards ($300-600) are the only reliable cash. Needs real rewards.

### Changes

#### 6.1 — Add Cash to Crate Loot Tables
Currently the prize list doesn't include "money" as a possible roll. We need to add it.

| Mission | Current Cash/Crate | New Cash/Crate |
|---------|-------------------|----------------|
| Mission 1 (Easy) | $0 (bugged) | **$50-150** |
| Mission 2 (Medium) | $0 (bugged) | **$75-200** |
| Mission 3 (Dangerous) | $0 (bugged) | **$100-250** |
| Mission 4 (Easy/Free) | $0 (bugged) | **$25-75** |

**Implementation:** Add `"money"` to the `prizes` table in the diving crate loot function. The money branch already exists in code but is unreachable because "money" is not in the prizes list.

#### 6.2 — Increase Completion Rewards
| Mission | Current Reward | New Reward |
|---------|---------------|------------|
| Mission 4 (Free, Easy) | $300 | **$400** |
| Mission 1 (Easy) | $300 | **$500** |
| Mission 2 (Medium) | $450 | **$750** |
| Mission 3 (Dangerous) | $600 | **$1,200** |

#### 6.3 — Add Mission Cooldowns
Currently there is NO cooldown between missions — a player can spam Mission 3 back-to-back.

| Mission | Current Cooldown | New Cooldown |
|---------|-----------------|--------------|
| All missions | 0 (none) | **15 minutes personal cooldown** |

#### 6.4 — Reduce Mission 3 Fixed Rewards
The diamond_ring + rolex + goldbar + $250 on top of crate loot is excessive for a single complete.

| Reward | Current | New |
|--------|---------|-----|
| diamond_ring | 1 | **1** (keep) |
| rolex | 1 | **0** (remove) |
| goldbar | 1 | **0** (remove) |
| cash bonus | $250 | **$0** (folded into completion reward) |

#### 6.5 — Estimated New Diving $/hr

| Mission | Current Real $/hr | New $/hr |
|---------|------------------|----------|
| Mission 4 (Free) | ~$800-1,200 | **$1,000-1,500** |
| Mission 1 (Easy) | ~$2,600-3,900 | **$2,500-3,500** |
| Mission 2 (Medium) | ~$3,500-5,000 | **$3,500-4,500** |
| Mission 3 (Dangerous) | ~$5,100-8,300 | **$5,000-6,500** |

**Result:** Diving now pays realistically. Mission 3 at ~$5,000-6,500/hr with 15-min cooldown slots it into Tier 7 (endgame) alongside Fraud and high-level mining. The $4,500 equipment buy-in and mission difficulty justify the pay.

---

## PART 7 — Job Center Tweaks (wais-jobpack)

### Problem Summary
Job Center is mostly well-balanced internally. The progression from Hotdog ($650-900/hr) to Trucker ($4,500-5,500/hr) is clean. Minor adjustments needed to align the overall curve.

### Changes

#### 7.1 — Slight Starter Job Bumps
| Job | Current Pay | New Pay | Why |
|-----|-----------|---------|-----|
| Mobile Hotdog | $65-85/sale | **$70-90/sale** | Starter needs to cover food costs |
| Hunter | $50-110/kill | Boar **$60**, Deer **$65**, Coyote **$80**, Mt Lion **$120** | Slightly underpaid |

#### 7.2 — Slight Mid-Tier Adjustment
| Job | Current Pay | New Pay | Why |
|-----|-----------|---------|-----|
| Fire Department | $280-400/fire | **$300-420/fire** | Slightly below electrician for same tier |

#### 7.3 — No Changes Needed
- Gardener ($800-1,200/hr): Fine for Tier 1
- Road Helper ($900-1,200/hr): Fine for Tier 2
- Bus Driver ($2,200-3,000/hr): Fine for Tier 3
- Detectorist (items only): Fine — utility job
- Electrician ($2,500-3,500/hr): Fine for Tier 4
- Project Car ($3,500-5,000/hr): Fine for Tier 5
- Diver JC ($3,500-4,500/hr): Fine for Tier 5
- Trucker ($4,500-5,500/hr): Fine for Tier 6

#### 7.4 — Estimated New Job Center $/hr

| Tier | Job | Current $/hr | New $/hr |
|------|-----|-------------|----------|
| 0 | Mobile Hotdog | $650-900 | **$700-950** |
| 0 | Gardener | $800-1,200 | $800-1,200 |
| 1 | Road Helper | $900-1,200 | $900-1,200 |
| 1 | Hunter | $500-800 | **$600-900** |
| 2 | Bus Driver | $2,200-3,000 | $2,200-3,000 |
| 3 | Fire Dept | $2,000-3,000 | **$2,200-3,200** |
| 3 | Electrician | $2,500-3,500 | $2,500-3,500 |
| 4 | Project Car | $3,500-5,000 | $3,500-5,000 |
| 4 | Diver (JC) | $3,500-4,500 | $3,500-4,500 |
| 5 | Trucker | $4,500-5,500 | $4,500-5,500 |

---

## PART 8 — Illegal Tablet Corrections (0r-illegalpack)

### Problem Summary
Drug lab police alerts are all 0% (should have risk). Moonshine material costs documented wrong. Otherwise the illegal tablet progression is reasonably sound.

### Changes

#### 8.1 — Fix Drug Lab Police Alert Chances
| Lab | Current | New |
|-----|---------|-----|
| Weed Lab | 0% | **20%** |
| Meth Lab | 0% | **30%** |
| Cocaine Lab | 0% | **40%** |

**Why:** Drug labs are supposed to be risky. The config values are 0 but the intent was clearly non-zero (comments reference higher values). These risk levels align with the tier progression: weed (beginner drug) has less risk than cocaine (advanced drug).

#### 8.2 — Reduce Fraud Payout
| Setting | Current | New |
|---------|---------|-----|
| Fraud completion pay | $4,000 | **$3,500** |

**Why:** At $4,000 with ~30 min cycles and $700 material cost, Fraud nets ~$3,300/run = ~$7,000-8,000/hr. This is too far above every other activity. At $3,500, net profit is $2,800/run = ~$5,600-6,000/hr, which properly sits at the top of Tier 7 without being uncatchable.

#### 8.3 — Slight Gun Smuggling Reduction
| Setting | Current | New |
|---------|---------|-----|
| Gun Smuggling completion pay | $2,200 | **$2,000** |

**Why:** At $2,200 with zero material cost, Gun Smuggling is $5,500-6,000/hr. At $2,000, it becomes ~$5,000-5,500/hr, properly fitting between Trucker (legal, $4,500-5,500) and Fraud (extreme risk, $5,600-6,000).

#### 8.4 — Slight Illegal Delivery Adjustment
| Setting | Current | New |
|---------|---------|-----|
| Illegal Delivery completion pay | $1,500 | **$1,400** |

**Why:** At $1,500 with zero material cost, this is pure $3,500-4,000/hr. At $1,400, it's ~$3,400/hr, sitting cleanly in Tier 5 alongside Meth Lab's two-phase earnings.

#### 8.5 — Estimated New Illegal Tablet $/hr

| Level | Job | Current $/hr | New $/hr | Risk |
|-------|-----|-------------|----------|------|
| 1 | Car Theft | $1,800-2,000 | $1,800-2,000 | Low |
| 2 | Bag Snatch | $1,500-2,000 | $1,500-2,000 | Low |
| 3 | NPC Boxing | $1,600-2,000 | $1,600-2,000 | Low |
| 4 | Chop Shop | $2,200-2,500 | $2,200-2,500 | Medium |
| 5 | Weed Lab | $2,000-3,000 | **$1,800-2,500** (police risk reduces efficiency) | Medium |
| 6 | Moonshine | $2,800-3,200 | $2,800-3,200 | Medium |
| 7 | Illegal Delivery | $3,500-4,000 | **$3,200-3,600** | High |
| 8 | Meth Lab | $3,500-5,000 | **$3,000-4,200** (police risk) | High |
| 9 | Cocaine Lab | $5,000-7,000 | **$4,000-5,500** (police risk) | Extreme |
| 10 | Gun Smuggling | $5,500-6,000 | **$5,000-5,500** | High |
| 12 | Fraud | $7,000-8,000 | **$5,600-6,000** | Extreme |

---

## PART 9 — Drug Selling Rebalance (op-drugselling)

### Problem Summary
The actual drug sell prices in op-drugselling are significantly different from the old economy doc. Public lab drugs (rolled_weed at $50, packed_coke at $350) out-earn phantom tier drugs ($85) per unit. This must be inverted.

### Changes

#### 9.1 — Reduce Public Lab Drug Sell Prices
These are drugs from the FREE public labs in 0r-illegalpack. They should be the lowest tier of sellable drugs.

| Drug | Current Optimal | New Optimal | Why |
|------|----------------|-------------|-----|
| moonshine | $45 | **$30** | Free byproduct, should be cheapest |
| rolled_weed | $50 | **$35** | Entry-level drug from free lab |
| packed_meth | $250 | **$175** | Free lab product, must be less than phantom |
| cutted_coke | (mid-product) | **$25** | Should barely be worth selling |
| packed_coke | $350 | **$225** | Free lab product, must be less than phantom |

Full price table adjustments:

| Drug | Current Min/Opt/Max | New Min/Opt/Max |
|------|---------------------|-----------------|
| moonshine | $40/$45/$50 | **$20/$30/$40** |
| rolled_weed | $40/$50/$70 | **$25/$35/$50** |
| packed_meth | $150/$250/$350 | **$100/$175/$250** |
| packed_coke | $200/$350/$500 | **$140/$225/$320** |

#### 9.2 — Ensure Phantom > Public, Exotic > Phantom, Mythical > Exotic
The current tier prices are actually decent for phantom/exotic/mythical. But with public drugs lowered, the gap is now clear:

| Tier | Current Optimal | New Optimal | Status |
|------|----------------|-------------|--------|
| Public (free labs) | $30-350 | **$30-225** | LOWERED |
| Phantom (paid, $25k) | $85 | **$110** | RAISED slightly |
| Exotic (paid, $100k) | $185 | **$200** | RAISED slightly |
| Mythical (paid, $200k) | $285 | **$300** | RAISED slightly |

Full phantom/exotic/mythical adjustments:

| Tier | Current Min/Opt/Max | New Min/Opt/Max |
|------|---------------------|-----------------|
| Phantom (all) | $75/$85/$100 | **$85/$110/$140** |
| Exotic (all) | $175/$185/$200 | **$165/$200/$240** |
| Mythical (all) | $275/$285/$300 | **$250/$300/$360** |

#### 9.3 — Result: New Drug Revenue Comparison

**Public Lab Drugs (free access, 0r-illegalpack labs):**
| Drug | Output/cycle | Revenue/cycle (optimal) | Material cost | Net/cycle |
|------|-------------|------------------------|---------------|-----------|
| Weed (5x rolled) | 5 joints | 5 × $35 = $175 | $0 (reusable) | **$175** |
| Meth (2x packed) | 2 bricks | 2 × $175 = $350 | $100 | **$250** |
| Cocaine (2x packed) | 2 bricks | 2 × $225 = $450 | $75 | **$375** |

**Phantom Drug Labs (paid, $25,000 + ongoing costs):**
| Drug | Revenue/unit | Qty per sale (max/ped=5) | Revenue/sale |
|------|-------------|------------------------|--------------|
| Phantom Weed | $110 | 5 | **$550** |
| Phantom Meth | $110 | 5 | **$550** |
| Phantom Cocaine | $110 | 4 | **$440** |

**Exotic Drug Labs (paid, $100,000 + ongoing costs):**
| Drug | Revenue/unit | Qty per sale (max/ped=5) | Revenue/sale |
|------|-------------|------------------------|--------------|
| Exotic Shrooms | $200 | 5 | **$1,000** |
| Exotic LSD | $200 | 5 | **$1,000** |
| Exotic Heroin | $200 | 5 | **$1,000** |

**Mythical Drug Labs (paid, $200,000 + ongoing costs):**
| Drug | Revenue/unit | Qty per sale (max/ped=5) | Revenue/sale |
|------|-------------|------------------------|--------------|
| Mythical Percocet | $300 | 5 | **$1,500** |
| Mythical Adderall | $300 | 5 | **$1,500** |

Now the hierarchy is clear: **Public < Phantom < Exotic < Mythical** as intended.

---

## PART 10 — Private Drug Labs (0r-drugbusiness + plt_drugs)

### Problem Summary
The 0r-drugbusiness warehouse production + plt_drugs processing pipeline is complex. Players who spent real money for these labs should earn more than public labs but less than endgame solo grinding (because labs are passive/semi-AFK income).

### No Code Changes Needed
The private lab system's economics are controlled by op-drugselling sell prices (adjusted in Part 9). The warehouse production rates, employee costs, and infrastructure are already well-designed money sinks. With the new drug sell prices:

- **Phantom labs**: $110/unit sell price makes the $25,000 buy-in + employee costs + ingredient sourcing worthwhile over time
- **Exotic labs**: $200/unit sell price justifies the $100,000 investment  
- **Mythical labs**: $300/unit sell price justifies the $200,000 investment

### Estimated Private Lab $/hr (selling phase only, not counting production time)
With 20-second sell timeout between peds, 80% sell chance in corner mode:

| Tier | Units sold/hr (realistic) | Revenue/hr | Overhead/hr | Net $/hr |
|------|--------------------------|------------|-------------|----------|
| Phantom | ~35-45 units | $3,850-4,950 | ~$500 (employees, utilities) | **$3,350-4,450** |
| Exotic | ~35-45 units | $7,000-9,000 | ~$800 | **$6,200-8,200** |
| Mythical | ~35-45 units | $10,500-13,500 | ~$1,200 | **$9,300-12,300** |

**Note:** These are SELLING phase rates only. Production requires waiting, sourcing ingredients, and the plt_drugs growing process (125-250 min per plant cycle). The actual hourly rate when including ALL time invested is much lower — probably 40-60% of the above numbers, landing at:

| Tier | Realistic all-inclusive $/hr |
|------|----------------------------|
| Phantom | **$1,500-2,500** |
| Exotic | **$2,800-4,500** |
| Mythical | **$4,200-6,500** |

This properly places Phantom around Tier 4-5, Exotic around Tier 6, and Mythical around Tier 7 — exactly where paid premium content should sit.

---

## PART 11 — DevHub Jobs Integration

### House Robbery — Target: Tier 3 ($1,500-2,500/hr)
House Robbery should match beginner-to-mid illegal tablet jobs (Car Theft through Chop Shop range).

| Setting | Current | New |
|---------|---------|-----|
| Pawn Shop enabled | false | **true** |
| Item sell prices | $5 each (all items) | **Tiered: $15-75 per item** (see below) |
| Crime Traders cash reward | $500 | **$500** (keep) |
| Min Police Required | 2 | **2** (keep) |
| Personal Cooldown | 30 min | **30 min** (keep) |

New item sell price tiers:
| Item Category | Examples | New Price |
|--------------|---------|-----------|
| Junk | Soap, mug, candle, towel | **$15** |
| Common | Phone, headphones, clock, book | **$25** |
| Valuable | Laptop, tablet, camera, jewelry | **$45** |
| Premium | TV, painting, drone, PC, gold items | **$75** |

With 5 required items and chance to grab more (20 min timer, ~10-15 items realistically):
- **Conservative (5 items)**: ~$175 pawn + $500 app = **$675/run → ~$1,350/hr** with 30-min cooldown
- **Aggressive (15 items)**: ~$525 pawn + $500 app = **$1,025/run → ~$2,050/hr**
- Lands in **Tier 3** ✓

### Truck Robbery — Target: Tier 4 ($2,500-3,500/hr)
Truck Robbery should match mid-tier illegal tablet jobs (Chop Shop through Moonshine range).

| Setting | Current | New |
|---------|---------|-----|
| markedbills per robbery | $200-1,000 | **$300-700** |
| goldbar chance | 40% | **25%** |
| goldbar quantity | 1-3 | **1-2** |
| diamond chance | 30% | **20%** |
| diamond quantity | 1-2 | **1** |
| Crime Traders cash | $500 | **$500** (keep) |
| Crime Traders goldbar reward | 2 | **1** |
| Personal Cooldown | 30 min | **30 min** (keep) |
| Required Items | 4 items | **4 items** (keep) |

Required item costs (bought from Crime Traders app):
- hr_pendrive: $200, hack_usb: $200, bomb_c4: $800, dh_antenna_disabler: $200 = **$1,400 total**

Estimated per run:
- markedbills: ~$500 avg + goldbar (25% × 1.5 avg × $120 fence = $45 expected) + diamond (20% × 1 × $100 = $20 expected) + $500 app cash + 1 goldbar from app ($120)
- **~$1,185/run gross - $1,400 materials = -$215 NET** on first run (materials are expensive!)
- But subsequent runs reuse app-purchased items that don't get consumed? Actually the required items ARE consumed per robbery.

This needs reconsideration. With $1,400 in material costs, the truck robbery currently barely breaks even. Let me adjust:

| Setting | Current | Revised New |
|---------|---------|------------|
| markedbills per robbery | $200-1,000 | **$500-1,200** |
| Required items cost | $1,400 | Reduce bomb_c4 price to **$400** → total **$1,000** |
| Crime Traders cash | $500 | **$750** |

Revised per run earnings:
- markedbills: ~$850 avg + goldbar expected: ~$45 + diamond expected: ~$20 + $750 app cash + 1 goldbar ($120) = **~$1,785/run**
- Net after $1,000 materials: **~$785/run → ~$1,570/hr** with 30-min cooldown

Hmm, that's Tier 2-3, not Tier 4. The 30-min cooldown really limits this. Let me adjust cooldown:

| Setting | Final Value |
|---------|------------|
| markedbills | $600-1,500 |
| Crime Traders cash | $750 |
| bomb_c4 price | $400 |
| Personal Cooldown | **20 minutes** |

Final per run: ~$1,050 avg markedbills + ~$65 expected items + $750 app + $120 goldbar = **~$1,985/run** 
Net after $1,000 materials: **~$985/run → ~$2,955/hr** with 20-min cooldown. ✓ Tier 4

### Drywood Cutter — Target: Tier 2 ($1,000-1,800/hr), on par with fishing
| Setting | Current | New |
|---------|---------|-----|
| Money per job | $250 | **$275** |
| Quest rewards | $600-800 | **$650-850** |

Estimated $/hr: ~$1,000-1,400/hr which matches fishing Rod 4-5 and road helper. ✓

### Herbal Alchemist — Target: Tier 2 ($1,000-1,800/hr), on par with fishing
| Setting | Current | New |
|---------|---------|-----|
| Money per job | $250 | **$275** |
| Quest rewards | $200-300 | **$250-350** |

Estimated $/hr: ~$900-1,300/hr which matches fishing and drywood cutter. ✓

### Racing — Standalone Entertainment
Racing is inherently a gambling/competitive system, not a grindable job. The weekly scheduled races with $2,000-6,000 prizes are fine as-is. No changes recommended — it's an entertainment system, not an economy system.

### DevHub Laptop (Crime Traders System)
The laptop itself is a gateway to house/truck robbery rewards. The Crime Traders level system (15 levels, 3,000-5,000 XP per level via robbery completions at 1,000 XP each) is reasonably gated. No changes needed to the laptop itself.

---

## PART 12 — Final Master Pay Table

Every income activity on the server, ranked by estimated $/hr after rebalance:

| Rank | Activity | Script | Est. $/hr (New) | Risk | Gate |
|------|----------|--------|----------------|------|------|
| **TIER 7 — ENDGAME** |
| 1 | Mythical Drug Labs (all-in) | plt_drugs+0r-drugbusiness | $4,200-6,500 | Selling risk | $200k+, employees, real $$ |
| 2 | Fraud | 0r-illegalpack | $5,600-6,000 | Extreme | Illegal Lvl 12 |
| 3 | Diving — DEEP SYNDICATE | s4-diving | $5,000-6,500 | High | $4,500 gear, 15min CD |
| 4 | Mining (Laser Drill, Lvl 9-10) | RxMining | $5,000-5,500 | None | ~350 hrs grind |
| **TIER 6 — MASTER** |
| 5 | Gun Smuggling | 0r-illegalpack | $5,000-5,500 | High | Illegal Lvl 10 |
| 6 | Exotic Drug Labs (all-in) | plt_drugs+0r-drugbusiness | $2,800-4,500 | Selling risk | $100k+, real $$ |
| 7 | Trucker | wais-jobpack | $4,500-5,500 | None | JC Lvl 10 |
| 8 | Cocaine Lab (public) | 0r-illegalpack | $4,000-5,500 | Extreme | Illegal Lvl 9 |
| **TIER 5 — EXPERT** |
| 9 | Mining Drill (Lvl 7-8) | RxMining | $3,800-4,200 | None | ~150 hrs |
| 10 | Project Car | wais-jobpack | $3,500-5,000 | None | JC Lvl 8 |
| 11 | Diver (Job Center) | wais-jobpack | $3,500-4,500 | None | JC Lvl 8 |
| 12 | Diving — Hightable Cargo | s4-diving | $3,500-4,500 | Medium | $1,500 gear, 15min CD |
| 13 | Illegal Delivery | 0r-illegalpack | $3,200-3,600 | High | Illegal Lvl 7 |
| 14 | Meth Lab (public) | 0r-illegalpack | $3,000-4,200 | High | Illegal Lvl 8 |
| **TIER 4 — SKILLED** |
| 15 | Moonshine | 0r-illegalpack | $2,800-3,200 | Medium | Illegal Lvl 6 |
| 16 | Truck Robbery | devhub_truckRobbery | $2,500-3,500 | High | Laptop, items, 20min CD |
| 17 | Mining (Lvl 5-6) | RxMining | $2,500-2,800 | None | ~50 hrs |
| 18 | Electrician | wais-jobpack | $2,500-3,500 | None | JC Lvl 6 |
| 19 | Diving — Saints Airlines | s4-diving | $2,500-3,500 | Low | $1,500 gear, 15min CD |
| **TIER 3 — INTERMEDIATE** |
| 20 | Bus Driver | wais-jobpack | $2,200-3,000 | None | JC Lvl 4 |
| 21 | Chop Shop | 0r-illegalpack | $2,200-2,500 | Medium | Illegal Lvl 4 |
| 22 | Mining (Lvl 3-4) | RxMining | $2,000-2,200 | None | ~20 hrs |
| 23 | Fire Department | wais-jobpack | $2,200-3,200 | None | JC Lvl 6 |
| 24 | Phantom Drug Labs (all-in) | plt_drugs+0r-drugbusiness | $1,500-2,500 | Selling risk | $25k+, real $$ |
| 25 | Weed Lab (public) | 0r-illegalpack | $1,800-2,500 | Medium | Illegal Lvl 5 |
| 26 | House Robbery | devhub_houseRobbery | $1,350-2,050 | Medium | Laptop, lockpick, 30min CD |
| 27 | Car Theft | 0r-illegalpack | $1,800-2,000 | Low | Illegal Lvl 1 |
| 28 | NPC Boxing | 0r-illegalpack | $1,600-2,000 | Low | Illegal Lvl 3 |
| 29 | Bag Snatch | 0r-illegalpack | $1,500-2,000 | Low | Illegal Lvl 2 |
| **TIER 2 — BEGINNER** |
| 30 | Fishing (Rod Lvl 5) | 0r-fishingv2 | $1,200-1,700 | None | Rod 5 (~$2,900) |
| 31 | Mining (Lvl 1-2) | RxMining | $1,000-1,100 | None | ~3 hrs |
| 32 | Diving — Medical Evac | s4-diving | $1,000-1,500 | Low | Free |
| 33 | Drywood Cutter | devhub_drywoodCutter | $1,000-1,400 | None | None |
| 34 | Herbal Alchemist | devhub_herbalAlchemist | $900-1,300 | None | None |
| 35 | Road Helper | wais-jobpack | $900-1,200 | None | JC Lvl 2 |
| **TIER 1 — STARTER** |
| 36 | Gardener | wais-jobpack | $800-1,200 | None | JC Lvl 0 |
| 37 | Fishing (Rod Lvl 3-4) | 0r-fishingv2 | $480-1,050 | None | Rod 3-4 |
| 38 | Mobile Hotdog | wais-jobpack | $700-950 | None | JC Lvl 0 |
| 39 | Hunter | wais-jobpack | $600-900 | None | JC Lvl 2 |
| 40 | Mining (Stone Pick, Lvl 0) | RxMining | $450-500 | None | License $300 |
| 41 | Fishing (Rod Lvl 1-2) | 0r-fishingv2 | $320-520 | None | Rod $500 |
| — | Racing | devhub_racing | Variable (gambling) | None | Entry fee |

---

## PART 13 — Summary of All Changes

### Scripts That Need Editing

#### RxMining (4 changes)
1. Laser Drill durability: 300 → **100**
2. Mining Drill durability: 200 → **150**
3. Cash drop amounts: Reduced across all ores (see Part 4.2)
4. Coal/Carbon drop chance: 50% → **40%**

#### pwr-sellmaterials (1 change)
1. Coal base price: $6 → **$12**, Carbon base price: $10 → **$16** (with proportional min/max adjustments)

#### 0r-fishingv2 (2 changes)
1. Starter fish prices: Fish/Bluegill $8 → **$10**
2. Endgame fish prices: Tuna $65→$75, Swordfish $80→$90, Tiger Shark $100→$115, Killer Whale $130→$150

#### s4-diving (4 changes)
1. Add "money" to crate prize list (fix the bug so cash drops actually work)
2. Increase completion rewards ($300-600 → $400-1,200)
3. Add 15-minute personal cooldown between missions
4. Remove rolex/goldbar from Mission 3 fixed rewards (keep diamond_ring)

#### wais-jobpack (3 changes)
1. Mobile Hotdog: $65-85 → **$70-90** per sale
2. Hunter animals: slight price bumps ($50-110 → $60-120)
3. Fire Department: $280-400 → **$300-420** per fire

#### 0r-illegalpack (4 changes)
1. Weed Lab police alert: 0% → **20%**
2. Meth Lab police alert: 0% → **30%**
3. Cocaine Lab police alert: 0% → **40%**
4. Fraud completion pay: $4,000 → **$3,500**
5. Gun Smuggling completion pay: $2,200 → **$2,000**
6. Illegal Delivery completion pay: $1,500 → **$1,400**

#### op-drugselling (2 changes)
1. Public lab drug prices: Lowered (moonshine $45→$30, rolled_weed $50→$35, packed_meth $250→$175, packed_coke $350→$225)
2. Phantom/Exotic/Mythical prices: Slightly raised (Phantom $85→$110, Exotic $185→$200, Mythical $285→$300)

#### devhub_houseRobbery (2 changes)
1. Enable pawn shop (false → **true**)
2. Item prices: $5 each → **$15-75 tiered** by item category

#### devhub_truckRobbery (5 changes)
1. markedbills range: $200-1,000 → **$600-1,500**
2. goldbar chance: 40% → **25%**, quantity: 1-3 → **1-2**
3. diamond chance: 30% → **20%**, quantity: 1-2 → **1**
4. Crime Traders cash: $500 → **$750**
5. Personal cooldown: 30 min → **20 min**

#### devhub_drywoodCutter (2 changes)
1. Money per job: $250 → **$275**
2. Quest rewards: +$50 each

#### devhub_herbalAlchemist (2 changes)
1. Money per job: $250 → **$275**
2. Quest rewards: +$50 each

### Scripts With NO Changes Needed
- **devhub_racing** — Entertainment/gambling system, not an economy grind
- **devhub_laptop** — Gateway system, economy controlled by connected scripts
- **0r-drugbusiness** — Production rates are fine; economy controlled by op-drugselling prices
- **plt_drugs** — Growth/processing system is fine; economy controlled by op-drugselling prices
- **mt-restaurants** — Reference only for food cost calculations

---

### Philosophy Preserved From Original Economy Guide

1. **No single job should dominate** — Every activity has a comparable option at its tier
2. **Risk = Reward** — Illegal jobs with police risk pay more than safe legal equivalents
3. **Time gates prevent get-rich-quick** — Mining takes 350+ hrs to max, JC takes 25+ hrs, Illegal takes 50+ hrs
4. **Variety is optimal** — Players should rotate activities for best overall progression
5. **Survival creates baseline spending** — ~$500-960/session on food keeps low-level income meaningful
6. **Paid content > Free content** — Mythical labs ($200k+ investment) properly out-earn free public labs
7. **Legal endgame ≈ Illegal mid-endgame** — Trucker/Mining Drill compete with mid-illegal, but Fraud/Mythical remain top earners with risk/investment tradeoffs

### What's New in This Plan
1. **DevHub jobs integrated** — House/Truck robbery, Drywood, Herbal all have clear tier placements
2. **Diving economy fixed** — Loot tables actually work, realistic pricing
3. **Drug hierarchy corrected** — Public < Phantom < Exotic < Mythical is now enforced
4. **Mining nerfed appropriately** — Still excellent at endgame, just not 30%+ better than everything
5. **Coal/Carbon shortage fixed** — Better prices incentivize mining these needed resources
