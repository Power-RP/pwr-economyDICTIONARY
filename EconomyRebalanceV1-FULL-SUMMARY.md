# Power RP 5.0 — Master Economy Guide

> **Last Updated:** February 14, 2026  
> **Scripts Covered:** `0r-illegalpack` (Illegal Tablet), `op-drugselling` (Street Selling), `0r-fishingv2` (Fishing), `s4-diving` (Diving Missions), Illegal Market

---

## Table of Contents

- [PART 1 — ILLEGAL ECONOMY (0r-illegalpack + op-drugselling)](#part-1--illegal-economy-0r-illegalpack--op-drugselling)
  - [1. Illegal Tablet — Overview](#1-illegal-tablet--overview)
    - [1.1 Leveling System](#11-leveling-system)
    - [1.2 Time-to-Level Breakdown](#12-time-to-level-breakdown)
  - [2. Job Breakdown — Direct-Payout Jobs](#2-job-breakdown--direct-payout-jobs)
    - [2.1 Car Theft (Level 1)](#21-car-theft-level-1)
    - [2.2 Bag Snatch (Level 2)](#22-bag-snatch-level-2)
    - [2.3 NPC Boxing (Level 3)](#23-npc-boxing-level-3)
    - [2.4 Chop Shop (Level 4)](#24-chop-shop-level-4)
    - [2.5 Moonshine (Level 6)](#25-moonshine-level-6)
    - [2.6 Illegal Delivery (Level 7)](#26-illegal-delivery-level-7)
    - [2.7 Gun Smuggling (Level 10)](#27-gun-smuggling-level-10)
    - [2.8 Fraud (Level 12)](#28-fraud-level-12)
  - [3. Job Breakdown — Drug Lab Jobs (Two-Phase)](#3-job-breakdown--drug-lab-jobs-two-phase)
    - [3.1 Weed Lab (Level 5)](#31-weed-lab-level-5)
    - [3.2 Meth Lab (Level 8)](#32-meth-lab-level-8)
    - [3.3 Cocaine Lab (Level 9)](#33-cocaine-lab-level-9)
  - [4. Street Drug Selling (op-drugselling)](#4-street-drug-selling-op-drugselling)
    - [4.1 Selling Leveling System](#41-selling-leveling-system)
    - [4.2 Drug Price Table](#42-drug-price-table)
    - [4.3 Selling Mechanics & Risk](#43-selling-mechanics--risk)
  - [5. Illegal Market — Material Costs](#5-illegal-market--material-costs)
  - [6. Illegal Progression Overview](#6-illegal-progression-overview)
  - [7. Balance Philosophy — Why No Illegal Job Is Worth Min-Maxing](#7-balance-philosophy--why-no-illegal-job-is-worth-min-maxing)
- [PART 2 — FISHING ECONOMY (0r-fishingv2)](#part-2--fishing-economy-0r-fishingv2)
  - [8. Fishing — Overview](#8-fishing--overview)
    - [8.1 Rod Leveling System](#81-rod-leveling-system)
    - [8.2 XP Rewards by Quality Tier](#82-xp-rewards-by-quality-tier)
    - [8.3 Fishing Mechanics](#83-fishing-mechanics)
  - [9. Fish Price Table — Full Breakdown](#9-fish-price-table--full-breakdown)
    - [9.1 Lake Fish](#91-lake-fish)
    - [9.2 River Fish](#92-river-fish)
    - [9.3 Saltwater Fish](#93-saltwater-fish)
    - [9.4 Lucky Items](#94-lucky-items)
  - [10. Shop — Equipment Costs](#10-shop--equipment-costs)
  - [11. Fishing $/hr Estimates by Rod Level](#11-fishing-hr-estimates-by-rod-level)
- [PART 3 — DIVING ECONOMY (s4-diving)](#part-3--diving-economy-s4-diving)
  - [12. Diving — Overview](#12-diving--overview)
  - [13. Diving Missions — Full Breakdown](#13-diving-missions--full-breakdown)
    - [13.1 Mission 1 — Saints Airlines Flight 370 (EASY)](#131-mission-1--saints-airlines-flight-370-easy)
    - [13.2 Mission 2 — Hightable Cargo Drop (MEDIUM)](#132-mission-2--hightable-cargo-drop-medium)
    - [13.3 Mission 3 — DEEP SYNDICATE (DANGEROUS)](#133-mission-3--deep-syndicate-dangerous)
    - [13.4 Mission 4 — Medical Evac Flight 09 (EASY)](#134-mission-4--medical-evac-flight-09-easy)
  - [14. Diving Shop — Equipment Costs](#14-diving-shop--equipment-costs)
  - [15. Diving $/hr Estimates](#15-diving-hr-estimates)
- [PART 4 — JOB CENTER ECONOMY (wais-jobpack)](#part-4--job-center-economy-wais-jobpack)
  - [16. Job Center — Overview](#16-job-center--overview)
    - [16.1 Job Center Leveling System](#161-job-center-leveling-system)
    - [16.2 Job Tier Unlock Progression](#162-job-tier-unlock-progression)
    - [16.3 XP Formula](#163-xp-formula)
  - [17. Job Center — Full Job Breakdown](#17-job-center--full-job-breakdown)
  - [18. Job Center $/hr Estimates](#18-job-center-hr-estimates)
- [PART 5 — MINING ECONOMY (RxMining + pwr-sellmaterials)](#part-5--mining-economy-rxmining--pwr-sellmaterials)
  - [19. Mining — Overview](#19-mining--overview)
    - [19.1 Mining Leveling System](#191-mining-leveling-system)
    - [19.2 Pickaxe & Tool Progression](#192-pickaxe--tool-progression)
  - [20. Ore Table — Full Breakdown](#20-ore-table--full-breakdown)
  - [21. Ore Selling — Foundries (pwr-sellmaterials)](#21-ore-selling--foundries-pwr-sellmaterials)
  - [22. Mining Shop — Equipment Costs](#22-mining-shop--equipment-costs)
  - [23. Mining $/hr Estimates by Level](#23-mining-hr-estimates-by-level)
- [PART 6 — CROSS-SCRIPT ECONOMY SUMMARY](#part-6--cross-script-economy-summary)
  - [24. Master Pay Comparison (All Scripts)](#24-master-pay-comparison-all-scripts)
  - [25. Server Economy Design Philosophy](#25-server-economy-design-philosophy)

---

# PART 1 — ILLEGAL ECONOMY (0r-illegalpack + op-drugselling)

---

## 1. Illegal Tablet — Overview

The **Illegal Tablet** (`illegal_tablet` item) is the central hub for all illegal jobs. Players open it to browse available missions, buy materials from the Illegal Market, and start jobs. Jobs are gated behind a **linear level progression** — you must reach the required level before a job appears on the tablet.

### 1.1 Leveling System

The tablet uses a **14-level XP system**. Each level requires a specific cumulative XP threshold:

| Level | XP to Reach | XP for This Level | Cumulative XP |
|:-----:|:-----------:|:------------------:|:-------------:|
| 1 | 0 | 0 | 0 |
| 2 | 1,000 | 1,000 | 1,000 |
| 3 | 2,000 | 1,000 | 2,000 |
| 4 | 4,000 | 2,000 | 4,000 |
| 5 | 8,000 | 4,000 | 8,000 |
| 6 | 10,000 | 2,000 | 10,000 |
| 7 | 15,000 | 5,000 | 15,000 |
| 8 | 30,000 | 15,000 | 30,000 |
| 9 | 45,000 | 15,000 | 45,000 |
| 10 | 60,000 | 15,000 | 60,000 |
| 11 | 75,000 | 15,000 | 75,000 |
| 12 | 90,000 | 15,000 | 90,000 |
| 13 | 105,000 | 15,000 | 105,000 |
| 14 | 120,000 | 15,000 | 120,000 |

**Key Observations:**
- Levels 1–3 are fast (1,000 XP each) — new players unlock starter jobs quickly
- Level 4 doubles the requirement (2,000 XP) — first soft gate
- Level 5 doubles again (4,000 XP) — drug labs start opening up here
- Level 6 drops back to 2,000 XP — brief relief
- Level 7 jumps to 5,000 XP — mid-game gate
- Levels 8–14 are all 15,000 XP each — the long grind for endgame content

### 1.2 Time-to-Level Breakdown

Assuming a player runs the highest-available job repeatedly at average cycle times:

| Target Level | Unlock | Best XP Source | XP/Run | Runs Needed | Est. Time |
|:-----------:|:------:|:--------------:|:------:|:-----------:|:---------:|
| 2 (1,000 XP) | Bag Snatch | Car Theft (100 XP) | 100 | 10 runs | ~3 hrs |
| 3 (2,000 XP) | Boxing | Bag Snatch (90 XP) + Car Theft (100 XP) | ~95 avg | 11 more | ~3.5 hrs |
| 4 (4,000 XP) | Chop Shop | Boxing (60 XP) + Car/Bag (~95) | ~78 avg | 26 more | ~6 hrs |
| 5 (8,000 XP) | Weed Lab | Chop Shop (120 XP) | 120 | 33 more | ~11 hrs |
| 6 (10,000 XP) | Moonshine | Weed (75 XP) + Chop (120 XP) | ~98 avg | 20 more | ~7 hrs |
| 7 (15,000 XP) | Illegal Delivery | Moonshine (300 XP) | 300 | 17 more | ~7 hrs |
| 8 (30,000 XP) | Meth Lab | Moonshine (300 XP) | 300 | 50 more | ~21 hrs |
| 9 (45,000 XP) | Cocaine Lab | Moonshine (300 XP) + Delivery (150 XP) | ~225 avg | 67 more | ~26 hrs |
| 10 (60,000 XP) | Gun Smuggling | Moonshine (300 XP) | 300 | 50 more | ~21 hrs |
| 12 (90,000 XP) | Fraud | Gun Smuggling (170 XP) + Moonshine (300 XP) | ~235 avg | 128 more | ~50 hrs |

> **Note:** These are rough estimates. Players will mix jobs for variety, and drug lab jobs also give XP. Real progression will vary based on player behavior, cooldowns, and risk.

---

## 2. Job Breakdown — Direct-Payout Jobs

These jobs pay a **flat amount on completion**. No second phase required — you do the mission, get paid.

---

### 2.1 Car Theft (Level 1)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay (Task-Oriented) |
| **Level Required** | 1 (Starter) |
| **Completion Pay** | $600 |
| **XP per Completion** | 100 XP |
| **Material Cost** | Lockpick ($200) |
| **Net Profit per Run** | ~$400 |
| **Estimated Time** | ~18 minutes |
| **Estimated $/hr** | $1,800–2,000 |
| **Risk Level** | Low |
| **Police Alert** | None (escrowed) |
| **Cooldown** | 2,600 seconds (~43 min) |
| **Team Size** | Solo |

**How it Works:** Player receives a mission to steal specific vehicles. You need a lockpick to break in. Multi-step: locate car, steal 5 vehicles, deliver them, complete. Timed steps (900s each).

---

### 2.2 Bag Snatch (Level 2)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay (Task-Oriented) |
| **Level Required** | 2 |
| **Completion Pay** | Random (escrowed, estimated $500–700) |
| **XP per Completion** | 90 XP |
| **Material Cost** | Crowbar ($200) |
| **Net Profit per Run** | ~$300–500 |
| **Estimated Time** | ~20 minutes |
| **Estimated $/hr** | $1,500–2,000 |
| **Risk Level** | Low |
| **Police Alert** | None (escrowed) |
| **Team Size** | Solo |

**How it Works:** Snatch bags from NPCs using a crowbar. Multi-step: go to location, snatch 10 bags, deliver them. The reward is randomized (escrowed, exact formula hidden).

---

### 2.3 NPC Boxing (Level 3)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay (Combat) |
| **Level Required** | 3 |
| **Completion Pay** | $400 |
| **XP per Completion** | 60 XP |
| **Material Cost** | None |
| **Net Profit per Run** | $400 (pure profit) |
| **Estimated Time** | ~12 minutes |
| **Estimated $/hr** | $1,600–2,000 |
| **Risk Level** | Low |
| **Police Alert** | 15% chance (underground fight ring) |
| **Team Size** | Solo only (max 1) |

**How it Works:** Underground boxing ring. Fight 5 progressively harder NPCs fist-to-fist. Opponents scale from 220 HP (round 1) to 300 HP + 20 armor (round 5). No items needed — pure combat skill. Quick rounds make this the fastest job by cycle time. Nerfed pay ($400) balances the zero material cost and fast cycles.

**Fighter Progression:**

| Round | HP | Armor | Difficulty |
|:-----:|:--:|:-----:|:----------:|
| 1 | 220 | 0 | Easy |
| 2 | 240 | 0 | Easy |
| 3 | 260 | 10 | Medium |
| 4 | 280 | 15 | Medium |
| 5 | 300 | 20 | Hard |

---

### 2.4 Chop Shop (Level 4)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay (Task-Oriented) |
| **Level Required** | 4 |
| **Completion Pay** | $800 |
| **XP per Completion** | 120 XP |
| **Material Cost** | Digiscanner ($150) |
| **Net Profit per Run** | ~$650 |
| **Estimated Time** | ~20 minutes |
| **Estimated $/hr** | $2,200–2,500 |
| **Risk Level** | Medium |
| **Police Alert** | Escrowed (estimated moderate) |
| **Team Size** | Solo |

**How it Works:** Locate a target vehicle using the digiscanner, steal it, drive to the chop shop, and disassemble it. 4-step timed mission. First real step up in both pay and risk from the starter jobs.

---

### 2.5 Moonshine (Level 6)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay (Multi-Step Production) |
| **Level Required** | 6 |
| **Completion Pay** | $1,200 |
| **XP per Completion** | 300 XP |
| **Material Cost** | Moonshine Still ($60) + Moonshine Pack ($30) = $90 |
| **Net Profit per Run** | ~$1,110 |
| **Estimated Time** | ~25 minutes |
| **Estimated $/hr** | $2,800–3,200 |
| **Risk Level** | Medium |
| **Police Alert** | 35% per step |
| **Team Size** | Solo |
| **Byproduct** | Produces 9x moonshine items (sellable via op-drugselling for additional income) |

**How it Works:** Meet contact NPC, collect ingredients (old corn, fruit, water), crush ingredients at crates, blend at barrel, cook with still (180s timer), pack 5 moonshine, deliver via vehicle. Longest non-drug production chain. The 300 XP reward makes this the **best XP source in the game** — critical for leveling from 7 onwards. The 9x moonshine byproduct can also be street-sold for extra dirty money.

---

### 2.6 Illegal Delivery (Level 7)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay (Delivery) |
| **Level Required** | 7 |
| **Completion Pay** | $1,500 |
| **XP per Completion** | 150 XP |
| **Material Cost** | None |
| **Net Profit per Run** | $1,500 (pure profit) |
| **Estimated Time** | ~25 minutes |
| **Estimated $/hr** | $3,500–4,000 |
| **Risk Level** | High |
| **Police Alert** | 40% per delivery |
| **Team Size** | Solo |

**How it Works:** Pick up boxes from a warehouse, load 10 into a vehicle, deliver to 10 drop-off points across the map, complete under a 10-minute time limit on the last step. High police alert chance (40%) at every delivery means you'll likely get heat. No material cost, but driving across the map under time pressure with cops is the challenge.

---

### 2.7 Gun Smuggling (Level 10)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay (Multi-Step Heist) |
| **Level Required** | 10 |
| **Completion Pay** | $2,200 |
| **XP per Completion** | 170 XP |
| **Material Cost** | None |
| **Net Profit per Run** | $2,200 (pure profit) |
| **Estimated Time** | ~22 minutes |
| **Estimated $/hr** | $5,500–6,000 |
| **Risk Level** | High |
| **Police Alert** | 55% when opening container |
| **Team Size** | Up to 2 players |

**How it Works:** Meet contact, steal a truck, drive to container yard, open containers (55% police alert!), load crates onto trailer with forklift, deliver to buyer. 6-step mission with a timed final delivery (800s). The 55% police chance on container opening is the highest single-alert in the game. Can bring a partner (max 2 team).

---

### 2.8 Fraud (Level 12)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay (Multi-Step Heist) |
| **Level Required** | 12 |
| **Completion Pay** | $4,000 |
| **XP per Completion** | 110 XP |
| **Material Cost** | ATM Hack Device ($300) + Blank Card ($400) = $700 |
| **Net Profit per Run** | ~$3,300 |
| **Estimated Time** | ~30 minutes |
| **Estimated $/hr** | $7,000–8,000 |
| **Risk Level** | Extreme |
| **Police Alert** | 100% (guaranteed dispatch) |
| **Team Size** | Solo only (max 1) |

**How it Works:** Hack 3 ATMs to capture card data, go to an office to program a fake credit card, sell the fake card to a banker. **Police are ALWAYS called** (100% alert chance), making this the most dangerous job in the game. The $700 material cost is the highest upfront investment, but the $4,000 payout makes it the best single-run earner. Locked behind level 12 for good reason — this is endgame content.

---

## 3. Job Breakdown — Drug Lab Jobs (Two-Phase)

Drug lab jobs are fundamentally different from direct-payout jobs. They require **two phases**:

1. **Phase 1 — Lab Production** (0r-illegalpack): Buy materials, enter the MLO lab, process drugs through 2-4 workstations, receive finished product
2. **Phase 2 — Street Selling** (op-drugselling): Take finished product to a corner, sell to NPCs one at a time, receive dirty money (markedbills)

This two-phase structure means **more time invested, more risk, but higher total payouts**. The lab phase pays XP + a small random cash bonus. The real money comes from selling.

---

### 3.1 Weed Lab (Level 5)

| Property | Value |
|----------|-------|
| **Type** | Two-Phase (Lab + Selling) |
| **Level Required** | 5 |
| **XP per Lab Run** | 75 XP |
| **Lab Phase Cash** | Random (small, escrowed) |
| **Police Alert (Lab)** | 25% per step |
| **Time Limit (Lab)** | 30 minutes |
| **Interior** | MLO (custom placed coordinates) |

#### Phase 1 — Lab Production Pipeline

| Step | Station | Input | Output | Workstations |
|:----:|:-------:|:-----:|:------:|:------------:|
| 1 | Gathering | 1x plant_spray (reusable) | 1x unpacked_weed | 6 stations |
| 2 | Packing | 1x unpacked_weed | 1x packed_weed | 2 stations |
| 3 | Rolling | 1x packed_weed | **5x rolled_weed** | 2 stations |

**Material Cost:** $100 (plant_spray — reusable, one-time purchase)

#### Phase 2 — Street Selling (rolled_weed)

| Sell Price | Min | Optimal | Max | Max per Transaction |
|:----------:|:---:|:-------:|:---:|:-------------------:|
| rolled_weed | $25 | $40 | $55 | 5 |

#### Full Cycle Economics

| Metric | Value |
|--------|-------|
| **Lab output per cycle** | 5x rolled_weed |
| **Selling revenue (optimal)** | 5 x $40 = $200 per batch |
| **Material cost** | $100 (one-time, plant_spray is reusable) |
| **Net profit (first run)** | ~$100 from lab + selling |
| **Net profit (subsequent)** | ~$200 per lab cycle (no material cost) |
| **Lab time** | ~15 minutes |
| **Selling time** | ~5–8 minutes (5 peds at 20s intervals + walk time) |
| **Total cycle** | ~20–25 minutes |
| **Estimated $/hr** | $2,000–3,000 |
| **Risk Level** | Medium |

**Why it's balanced:** Weed is the entry-level drug. Low police alert (25%), reusable materials, but modest per-unit prices. The 5x yield on rolling compensates for cheap individual joints. It's slightly better than Chop Shop (Level 4) but requires the selling phase.

---

### 3.2 Meth Lab (Level 8)

| Property | Value |
|----------|-------|
| **Type** | Two-Phase (Lab + Selling) |
| **Level Required** | 8 |
| **XP per Lab Run** | 100 XP |
| **Lab Phase Cash** | Random (small, escrowed) |
| **Police Alert (Lab)** | 35% per step |
| **Time Limit (Lab)** | 30 minutes |
| **Interior** | MLO (custom placed coordinates) |

#### Phase 1 — Lab Production Pipeline

| Step | Station | Input | Output | Workstations |
|:----:|:-------:|:-----:|:------:|:------------:|
| 1 | Cooking | 1x ammonia + 1x sacid | 1x cooked_meth | 2 stations |
| 2 | Hammering | 1x cooked_meth | 1x breaked_meth | 2 stations |
| 3 | Packing | 1x breaked_meth | **2x packed_meth** | 1 station |

**Material Cost:** $50 (ammonia) + $50 (sacid) = **$100 per cycle**

#### Phase 2 — Street Selling (packed_meth)

| Sell Price | Min | Optimal | Max | Max per Transaction |
|:----------:|:---:|:-------:|:---:|:-------------------:|
| packed_meth | $150 | $250 | $350 | 2 |

#### Full Cycle Economics

| Metric | Value |
|--------|-------|
| **Lab output per cycle** | 2x packed_meth |
| **Selling revenue (optimal, 1 txn)** | 2 x $250 = $500 |
| **Material cost per cycle** | $100 |
| **Net profit per cycle** | ~$400 |
| **Lab time** | ~15 minutes |
| **Selling time** | ~3–5 minutes (1–2 peds) |
| **Total cycle** | ~18–22 minutes |
| **Estimated $/hr** | $3,500–5,000 |
| **Risk Level** | High |

**Why it's balanced:** Meth requires consumable materials every cycle ($100), 35% police chance, and is locked behind the steep Level 8 wall (30,000 cumulative XP). The 2x packed_meth yield makes each brick valuable ($250 optimal), but you only get 2 per cycle. Faster selling phase than weed (fewer items to move), but higher police risk and ongoing costs.

---

### 3.3 Cocaine Lab (Level 9)

| Property | Value |
|----------|-------|
| **Type** | Two-Phase (Lab + Selling) |
| **Level Required** | 9 |
| **XP per Lab Run** | 150 XP |
| **Lab Phase Cash** | Random (small, escrowed) |
| **Police Alert (Lab)** | 40% per step |
| **Time Limit (Lab)** | 30 minutes |
| **Interior** | MLO (custom placed coordinates) |

#### Phase 1 — Lab Production Pipeline

| Step | Station | Input | Output | Workstations |
|:----:|:-------:|:-----:|:------:|:------------:|
| 1 | Unpacking | 1x powdered_milk | 1x unpacked_coke | 3 stations |
| 2 | Cutting | 1x unpacked_coke | 1x cutted_coke | 6 stations |
| 3 | Packing | 1x cutted_coke | **2x packed_coke** | 3 stations |

**Material Cost:** $75 (powdered_milk) per cycle

#### Sellable Products (Two Options)

Cocaine is unique — you can sell the **mid-product** (cutted_coke) OR the **final product** (packed_coke):

| Product | Min | Optimal | Max | Max/Txn |
|:-------:|:---:|:-------:|:---:|:-------:|
| cutted_coke | $20 | $35 | $50 | 3 |
| packed_coke | $200 | $350 | $500 | 2 |

> **Strategy:** Always pack to final product. 2x packed_coke at $350 = $700, vs 1x cutted_coke at $35. Packing multiplies value by 20x.

#### Full Cycle Economics

| Metric | Value |
|--------|-------|
| **Lab output per cycle** | 2x packed_coke |
| **Selling revenue (optimal)** | 2 x $350 = $700 |
| **Material cost per cycle** | $75 |
| **Net profit per cycle** | ~$625 |
| **Lab time** | ~15–20 minutes (4 steps, most workstations) |
| **Selling time** | ~3–5 minutes (1–2 peds) |
| **Total cycle** | ~20–25 minutes |
| **Estimated $/hr** | $5,000–7,000 |
| **Risk Level** | Extreme |

**Why it's balanced:** Cocaine is the king of drug jobs — highest per-unit value ($350 optimal per brick), but comes with the highest police alert (40% per step across 4 stations), the highest level gate (Level 9 = 45,000 cumulative XP), and consumable materials every cycle. The 4-step lab process is the longest of any drug. High reward, high risk, high investment.

---

## 4. Street Drug Selling (op-drugselling)

### 4.1 Selling Leveling System

The street selling system has its **own separate leveling system** from the illegal tablet. It uses op-drugselling's built-in progression:

| Level | XP Required | Cumulative XP | Price Boost |
|:-----:|:-----------:|:-------------:|:-----------:|
| 1 | 1,000 | 1,000 | +1% |
| 2 | 1,000 | 2,000 | +2% |
| 3 | 1,000 | 3,000 | +3% |
| 4 | 1,000 | 4,000 | +4% |
| 5 | 1,000 | 5,000 | +5% |
| 6 | 1,000 | 6,000 | +6% |
| 7 | 1,000 | 7,000 | +7% |
| 8 | 1,000 | 8,000 | +8% |
| 9 | 1,000 | 9,000 | +9% |
| 10 | 1,000 | 10,000 | +10% |

- **XP per sale** depends on ped type (1–10 XP per transaction)
- Each level gives a **percentage boost** to sell prices
- At Level 10, all drug prices are **10% higher** than base
- Leveling is flat (1,000 per level) unlike the tablet's exponential curve

**XP Sources by Ped Type:**

| Ped Type | XP/Sale | Buy Chance | Steal Chance | Dispatch? |
|:--------:|:-------:|:----------:|:------------:|:---------:|
| Addicted | 1 | 90% | 40% | No |
| Normal | 3 | 75% | 20% | Yes |
| Party | 5 | 80% | 25% | Yes |
| Snitch | 5 | 50% | 0% | Yes |
| Dealer | 7 | 50% | 50% | No |
| Rich Guy | 7 | 80% | 0% | Yes |
| Junkie | 1 | 90% | 40% | No |
| Undercover | 10 | 20% | 40% | Yes |

### 4.2 Drug Price Table

All drugs sellable via op-drugselling corner dealing:

#### Lab-Refined Products (from 0r-illegalpack)

| Drug | Item | Min $ | Optimal $ | Max $ | Max/Txn | Source |
|:----:|:----:|:-----:|:---------:|:-----:|:-------:|:------:|
| Rolled Joint | rolled_weed | $25 | $40 | $55 | 5 | Weed Lab |
| Packed Meth | packed_meth | $150 | $250 | $350 | 2 | Meth Lab |
| Cut Cocaine | cutted_coke | $20 | $35 | $50 | 3 | Coke Lab (mid) |
| Packed Cocaine | packed_coke | $200 | $350 | $500 | 2 | Coke Lab (final) |

#### Basic / BASIC-Tier Drugs

| Drug | Item | Min $ | Optimal $ | Max $ | Max/Txn | Source |
|:----:|:----:|:-----:|:---------:|:-----:|:-------:|:------:|
| Weed (basic) | packed_weed | $5 | $10 | $15 | 5 | Weed Lab (mid-product) |
| Moonshine | moonshine | $5 | $10 | $15 | 5 | Moonshine Job byproduct |

#### Phantom Tier (from op-gangs)

| Drug | Min $ | Optimal $ | Max $ | Max/Txn |
|:----:|:-----:|:---------:|:-----:|:-------:|
| Weed (phantom strains) | $15 | $25 | $35 | 5 |
| Meth (phantom bags) | $15 | $25 | $35 | 5 |
| Cocaine (phantom packs) | $15 | $25 | $35 | 4 |

#### Exotic Tier (from op-gangs)

| Drug | Min $ | Optimal $ | Max $ | Max/Txn |
|:----:|:-----:|:---------:|:-----:|:-------:|
| Shrooms | $40 | $55 | $75 | 5 |
| LSD | $40 | $55 | $75 | 5 |
| Heroin | $40 | $55 | $75 | 5 |

#### Mythical Tier (from op-gangs)

| Drug | Min $ | Optimal $ | Max $ | Max/Txn |
|:----:|:-----:|:---------:|:-----:|:-------:|
| Percocet | $100 | $150 | $200 | 5 |
| Adderall | $100 | $150 | $200 | 5 |

### 4.3 Selling Mechanics & Risk

| Setting | Value |
|---------|-------|
| **Sell Timeout** | 20 seconds between peds |
| **Dispatch Chance** | 15% per transaction (on top of ped-specific dispatch) |
| **Currency** | Dirty money (markedbills item) |
| **Corner Command** | `/startselling` |
| **Level Command** | `/startselling:mylevel` |

**Risk Factors During Selling:**
- **Steal chance:** Some peds (Addicted 40%, Dealer 50%, Junkie 40%, Undercover 40%) will try to steal your drugs
- **Refuse chance:** 10% base refusal rate on most ped types
- **Dispatch:** 15% global dispatch chance PLUS ped-type specific dispatch calls
- **Undercover cops:** Only 20% buy chance, 40% steal, always call dispatch — worst-case scenario ped

---

## 5. Illegal Market — Material Costs

All materials are purchased from the Illegal Market tab on the tablet:

| Item | Price | Used By | Consumable? |
|:----:|:-----:|:-------:|:-----------:|
| Lockpick | $200 | Car Theft | Yes (consumed on use) |
| Crowbar | $200 | Bag Snatch | Yes |
| Digiscanner | $150 | Chop Shop | Yes |
| ATM Hack Device | $300 | Fraud | Yes |
| Blank Credit Card | $400 | Fraud | Yes |
| Moonshine Still | $60 | Moonshine | Yes |
| Moonshine Pack | $30 | Moonshine | Yes |
| Plant Spray | $100 | Weed Lab | **Reusable** (not consumed) |
| Powdered Milk | $75 | Cocaine Lab | Yes |
| Ammonia | $50 | Meth Lab | Yes |
| Sacid | $50 | Meth Lab | Yes |
| Anchor | $500 | Diving | Yes |

**Key Material Economy Notes:**
- **Fraud** has the highest material cost ($700 per run) but also the highest payout ($4,000)
- **Drug lab materials** are intentionally cheap ($50–100) so the real money comes from selling, not from material arbitrage
- **Plant spray** is the only reusable material — weed lab runs become material-free after the first purchase
- **Moonshine** materials are cheap ($90 total) relative to its $1,200 completion payout

---

## 6. Illegal Progression Overview

The complete linear progression ordered by level unlock:

| Level | Job | Type | Pay/Run | Material Cost | Net Profit | XP/Run | Est. $/hr | Risk |
|:-----:|:---:|:----:|:-------:|:-------------:|:----------:|:------:|:---------:|:----:|
| 1 | Car Theft | Completion | $600 | $200 | ~$400 | 100 | $1,800–2,000 | Low |
| 2 | Bag Snatch | Completion | ~$500–700 | $200 | ~$300–500 | 90 | $1,500–2,000 | Low |
| 3 | NPC Boxing | Completion | $400 | $0 | $400 | 60 | $1,600–2,000 | Low |
| 4 | Chop Shop | Completion | $800 | $150 | ~$650 | 120 | $2,200–2,500 | Medium |
| 5 | Weed Lab | Two-Phase | ~$200/cycle | $100 (once) | ~$200 | 75 | $2,000–3,000 | Medium |
| 6 | Moonshine | Completion | $1,200 | $90 | ~$1,110 | 300 | $2,800–3,200 | Medium |
| 7 | Illegal Delivery | Completion | $1,500 | $0 | $1,500 | 150 | $3,500–4,000 | High |
| 8 | Meth Lab | Two-Phase | ~$500/cycle | $100 | ~$400 | 100 | $3,500–5,000 | High |
| 9 | Cocaine Lab | Two-Phase | ~$700/cycle | $75 | ~$625 | 150 | $5,000–7,000 | Extreme |
| 10 | Gun Smuggling | Completion | $2,200 | $0 | $2,200 | 170 | $5,500–6,000 | High |
| 12 | Fraud | Completion | $4,000 | $700 | ~$3,300 | 110 | $7,000–8,000 | Extreme |

---

## 7. Balance Philosophy — Why No Illegal Job Is Worth Min-Maxing

The economy is designed around a core principle: **every job should be viable at its level tier, and no single job should dominate all others.**

### How Jobs Are Balanced Against Each Other

**Tier 1 — Starters (Levels 1–3): $1,500–2,000/hr**
- **Car Theft**, **Bag Snatch**, and **NPC Boxing** all hover around $1,500–2,000/hr
- Boxing is the fastest (12 min cycles) but pays the least ($400) and gives the least XP (60)
- Car Theft pays more ($600) and gives 100 XP, but costs $200 in materials and takes longer
- Bag Snatch has randomized pay — sometimes better, sometimes worse than Car Theft
- **Result:** All three are roughly equal. Players pick based on preference, not optimization

**Tier 2 — Mid-Game (Levels 4–6): $2,000–3,200/hr**
- **Chop Shop** is a reliable $650 net per run with good XP (120)
- **Weed Lab** introduces the two-phase system — slightly higher ceiling but takes longer and requires selling
- **Moonshine** is the star — $1,110 net profit AND 300 XP makes it the leveling king
- **Why moonshine doesn't dominate:** It takes 25 minutes, requires vehicle delivery, and 35% police alert. The pay per hour is good but not massively better than Chop Shop when accounting for risk

**Tier 3 — High-Risk (Levels 7–9): $3,500–7,000/hr**
- **Illegal Delivery** is straightforward — no materials, $1,500 cash, but 40% police on every drop
- **Meth Lab** matches Delivery in $/hr but requires the two-phase workflow and ongoing material costs
- **Cocaine Lab** is the highest-paying drug — $625 net per cycle, but 40% police per step across 4 stations, and locked behind 45,000 cumulative XP
- **Why drugs don't make delivery obsolete:** Drug jobs need 2 phases (lab + selling), ongoing material purchases, and carry selling risks (steal/dispatch). Delivery is one-and-done with clean cash

**Tier 4 — Endgame (Levels 10–12): $5,500–8,000/hr**
- **Gun Smuggling** pays $2,200 with zero material cost and only 55% alert on one step
- **Fraud** pays $4,000 but costs $700 in materials and has GUARANTEED police dispatch
- **Why fraud doesn't dominate:** $700 investment + 100% police contact means you can fail and lose money. Gun Smuggling is "safer" endgame grinding

### The Anti-Min-Max Design

Several intentional design choices prevent any single job from being "the meta":

1. **Cooldowns** — Jobs have cooldowns preventing spam. You MUST rotate between jobs
2. **Two-phase tax** — Drug jobs pay more per unit but require double the time (lab + selling). Direct-payout jobs are simpler but pay less per hour
3. **Material costs scale with payout** — Higher-paying jobs need more expensive materials, keeping profit margins comparable
4. **XP vs Money tradeoff** — Moonshine gives 300 XP (best for leveling) but only $1,200. Fraud gives $4,000 but only 110 XP (terrible for leveling). Players must choose: level fast or earn fast
5. **Risk taxes the reward** — Higher-paying jobs have higher police detection. A busted run = lost time, potential death, lost materials
6. **Dirty money ceiling** — Drug money arrives as markedbills (dirty), requiring money laundering. Direct-payout jobs pay clean cash. This creates a practical cap on drug income
7. **Selling RNG** — Drug selling peds can steal your product, refuse to buy, or call police. You never get 100% of theoretical value
8. **Two separate leveling systems** — Tablet level gates job access. Selling level boosts drug prices. Neither helps the other, forcing investment in both if you want to do drugs

### The Optimal Strategy (By Design) Is Variety

- **Leveling?** Run Moonshine (300 XP/run, best in game)
- **Quick cash?** NPC Boxing or Car Theft (fast cycles, no selling phase)
- **Big payouts?** Fraud or Gun Smuggling (endgame, high risk)
- **Passive income?** Drug labs produce items you sell on your schedule
- **Low risk?** Starter jobs (Car Theft, Bag Snatch, Boxing) — minimal police
- **High roller?** Cocaine — highest per-unit value, most steps, most risk

**No matter what a player optimizes for, they sacrifice something else.** That's the balance.

---

# PART 2 — FISHING ECONOMY (0r-fishingv2)

---

## 8. Fishing — Overview

The fishing system (`0r-fishingv2`) is a **legal, progression-based economy** that provides a slow-and-steady income alternative to illegal work. Players buy equipment, fish at various locations, and sell their catches at fish markets. Progression is gated by **rod level** (1–5) and **player level**, with higher-tier fish requiring better equipment.

Fishing is designed to be a **relaxing, low-risk activity** that pays less per hour than illegal jobs but carries zero risk of police or product loss. It serves as a "chill money" alternative — a player who doesn't want the stress of crime can earn a living here.

### 8.1 Rod Leveling System

Players start with a Level 1 Fishing Rod and can upgrade up to Level 5. Each rod level unlocks access to higher-tier fish.

| Rod Level | Upgrade Cost | Success Chance | Fish Unlocked |
|:---------:|:----------:|:--------------:|:-------------:|
| 1 | $500 (initial purchase) | — | Common lake/river/salt fish |
| 2 | $300 | 50% | Perch, Northern Pike, Bluefish, Trout |
| 3 | $300 | 50% | Rock Bass, Sweet Fish, Redfin Pickerel, Eel, Codfish |
| 4 | $300 | 50% | Smallmouth Bass, Rainbow Trout, Sockeye Salmon, Redfish |
| 5 | $300 | 50% | Whitefish, Tuna, Swordfish, Tiger Shark, Killer Whale |

**Upgrade Economics:**
- Each upgrade costs $300 with a **50% success chance**
- On average, reaching Rod Level 5 costs: $500 (rod) + ~$2,400 (8 attempts at $300 to land 4 successes) = **~$2,900 total investment**
- Failed upgrades consume the $300 fee but do not break the rod
- This upgrade RNG adds a money sink that delays but doesn't block progression

### 8.2 XP Rewards by Quality Tier

Every fish caught gives XP based on its quality tier. XP contributes to the player's fishing level, which gates access to certain fish.

| Quality | Default XP | Random Range | Typical XP |
|:-------:|:----------:|:------------:|:----------:|
| **Common** | 50 | 40–70 | ~55 |
| **Eco** | 60 | 50–80 | ~65 |
| **Rare** | 100 | 80–130 | ~105 |
| **Epic** | 175 | 140–220 | ~180 |

**XP Design Notes:**
- Common and Eco fish give modest XP — they're plentiful but not efficient for leveling
- Rare fish give a solid 80–130 XP, making them the sweet spot for balanced fishing
- Epic fish are the best XP source (140–220) but require Rod Level 4–5 and higher player level to access
- The **Lucky Hat** (bought for $5,000) provides a **1.5x XP multiplier** on all catches

### 8.3 Fishing Mechanics

| Setting | Value |
|---------|-------|
| **Rod Cast Wait** | 5–12 seconds |
| **Net Cast Wait** | 10–15 seconds |
| **Trash Catch Chance** | 20% (catch garbage instead of fish) |
| **Long Distance Bonus** | 9% chance for rare item on long cast |
| **Boat Rental** | $200 (required for ocean/deep fishing) |
| **Net Cost** | $2,500 (alternative to rod) |
| **Minigame** | Distance throw + fish catch box game |
| **AFK Mode** | Disabled (minigame required) |

---

## 9. Fish Price Table — Full Breakdown

All fish are sold at **Fish Market** locations scattered across the map. Prices are fixed per species.

### 9.1 Lake Fish

| Fish | Price | Player Level | Rod Level | Quality | $/hr Tier |
|:----:|:-----:|:-----------:|:---------:|:-------:|:---------:|
| Fish | $8 | 1 | 1 | Eco | Starter |
| Bluegill | $8 | 1 | 1 | Common | Starter |
| Bass | $10 | 1 | 1 | Common | Starter |
| Perch | $12 | 3 | 2 | Eco | Low |
| Common Carp | $15 | 2 | 1 | Eco | Low |
| Northern Pike | $18 | 2 | 2 | Eco | Low-Mid |
| Rock Bass | $18 | 4 | 3 | Rare | Mid |
| Smallmouth Bass | $25 | 5 | 4 | Epic | Mid-High |
| Whitefish | $40 | 7 | 5 | Epic | High |

### 9.2 River Fish

| Fish | Price | Player Level | Rod Level | Quality | $/hr Tier |
|:----:|:-----:|:-----------:|:---------:|:-------:|:---------:|
| Small Trout | $10 | 1 | 1 | Common | Starter |
| Trout | $14 | 3 | 2 | Eco | Low |
| Catfish | $15 | 1 | 1 | Common | Low |
| Sweet Fish | $15 | 3 | 3 | Rare | Low-Mid |
| Redfin Pickerel | $20 | 4 | 3 | Rare | Mid |
| Rainbow Trout | $35 | 6 | 4 | Epic | Mid-High |
| Sockeye Salmon | $45 | 6 | 4 | Epic | High |

### 9.3 Saltwater Fish

| Fish | Price | Player Level | Rod Level | Quality | $/hr Tier |
|:----:|:-----:|:-----------:|:---------:|:-------:|:---------:|
| Drumfish | $12 | 1 | 1 | Common | Starter |
| Bluefish | $14 | 2 | 2 | Eco | Low |
| Eel | $16 | 4 | 3 | Common | Low-Mid |
| Codfish | $40 | 3 | 2 | Rare | Mid |
| Redfish | $50 | 5 | 3 | Epic | Mid-High |
| Tuna | $65 | 7 | 5 | Epic | High |
| Swordfish | $80 | 7 | 5 | Epic | High |
| Tiger Shark | $100 | 8 | 5 | Epic | Elite |
| Killer Whale | $130 | 9 | 5 | Epic | Elite |

### 9.4 Lucky Items

Lucky Items are rare drops that can appear while fishing. They are not quality-gated and can drop at any rod level.

| Item | Price | Player Level | Quality |
|:----:|:-----:|:-----------:|:-------:|
| Red Pearl | $150 | 1 | Epic |
| Blue Pearl | $150 | 1 | Epic |
| Yellow Pearl | $150 | 1 | Epic |
| Green Pearl | $150 | 1 | Epic |
| Green Crab | $120 | 1 | Rare |
| Red Crab | $120 | 1 | Rare |
| Blue Crab | $120 | 1 | Rare |
| King Crab | $175 | 1 | Epic |
| Goldfish | $100 | 3 | Rare |

---

## 10. Shop — Equipment Costs

| Item | Price | Level Req | Quality | Purpose |
|:----:|:-----:|:---------:|:-------:|:-------:|
| Fishing Rod (Lvl 1) | $500 | 1 | Common | Required to fish |
| Fishing Net | $2,500 | 1 | Common | Alternative fishing tool |
| Worm Fish Bait | $2 | 1 | Common | Consumable bait |
| Simple Fish Bait | $3 | 1 | Common | Consumable bait |
| Illegal Fish Bait | $15 | 1 | Common | Premium bait |
| Diving Cloth | $1,000 | 1 | Eco | Underwater fishing |
| Diving Gear | $1,000 | 1 | Rare | Underwater fishing |
| Diving Tube | $1,000 | 1 | Rare | Underwater fishing |
| Lucky Hat | $5,000 | 1 | Rare | 1.5x XP multiplier |
| Anchor | $1,000 | 1 | Common | Boat anchoring |

**Total Startup Cost (Rod fishing):** $500 (rod) + $2–15 (bait) = **~$502–515**  
**Total Startup Cost (Full kit):** $500 + $2,500 (net) + $5,000 (hat) + $1,000 (anchor) = **~$9,000**

---

## 11. Fishing $/hr Estimates by Rod Level

The catch rate is approximately **4–7 fish per 10 minutes** with a rod (5–12s wait + minigame time + selling travel). Accounting for 20% trash catches, effective catches drop to ~3–6 sellable fish per 10 minutes.

| Rod Level | Accessible Fish | Avg Sell Price | Catches/hr | Gross $/hr | Notes |
|:---------:|:--------------:|:--------------:|:----------:|:----------:|:-----:|
| 1 | Common tier ($8–15) | ~$11 | ~25–35 | **$275–385** | Starter, very low income |
| 2 | + Perch, Pike, Bluefish ($12–18) | ~$14 | ~25–35 | **$350–490** | Slight improvement |
| 3 | + Rock Bass, Sweet Fish, Codfish ($15–40) | ~$18 | ~25–35 | **$450–630** | Codfish ($40) starts appearing |
| 4 | + Smallmouth Bass, Rainbow Trout, Salmon, Redfish ($25–50) | ~$28 | ~25–35 | **$700–980** | Major jump with epic fish |
| 5 | + Whitefish, Tuna, Swordfish, Tiger Shark, Killer Whale ($40–130) | ~$42 | ~25–35 | **$1,050–1,470** | Endgame fishing |

**Key Observations:**
- Rod Level 1–2 fishing is extremely low income ($275–490/hr) — it's a starter activity, not a moneymaker
- Rod Level 3 gets a boost from Codfish ($40) but is still below $700/hr
- Rod Level 4 is the inflection point where epic fish make fishing respectable ($700–980/hr)
- Rod Level 5 caps around $1,000–1,500/hr — competitive with starter illegal jobs but FAR below mid-tier illegal work
- **Lucky Items** can spike income unpredictably (a Pearl at $150 or King Crab at $175 is like catching 10 common fish at once)
- The **Lucky Hat** (1.5x XP) doesn't increase income directly but accelerates leveling to access higher fish faster

> **Design Intent:** Fishing is meant to be a **legal, zero-risk** activity. It pays roughly 25–50% of what illegal jobs pay at comparable progression levels. The tradeoff: no police, no material costs (just bait), no product loss, no time pressure. It's income for players who want peace.

---

# PART 3 — DIVING ECONOMY (s4-diving)

---

## 12. Diving — Overview

The diving system (`s4-diving`) offers **4 underwater missions** of varying difficulty. Players purchase diving equipment from a shop, accept missions from a ped, and dive to collect items and cash from underwater crash sites, wrecks, and bunkers. Each mission has a time limit, depth requirement, and specific equipment needs.

Diving is a **solo, mission-based activity** with no leveling system — all 4 missions are available from the start. Progression is gated by **equipment cost** (you need gear to attempt harder missions) and **skill** (deeper dives with time pressure).

Dispatch alerts can be sent to police (configurable, currently enabled).

---

## 13. Diving Missions — Full Breakdown

### 13.1 Mission 1 — Saints Airlines Flight 370 (EASY)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay + Item Loot |
| **Difficulty** | EASY |
| **Completion Reward** | $300 |
| **Time Limit** | 15 minutes |
| **Depth** | 15m |
| **Equipment Required** | Oxygen Tank |
| **Equipment Cost** | $1,500 (O2 Tank) |
| **Loot Type** | Random items (5–10 crates) + random cash per crate |
| **Random Cash per Crate** | $150–400 |
| **Random Item per Crate** | 1–2x random (lockpick, goldchain, rolex, rubber, etc.) |
| **Risk Level** | Low |
| **Police Dispatch** | Possible (global dispatch enabled) |

**Earnings Estimate:**
- Completion: $300
- Crates: ~7 avg x ~$275 avg cash = ~$1,925
- Items: ~7 x 1.5 avg = ~10 random items (variable value)
- **Total estimated: $2,225 + items per run**
- **Time: ~10–15 minutes**
- **Estimated $/hr: $9,000–13,000 (with items)**

**How it Works:** Dive to a sunken airplane off Paleto Beach, collect crates from the wreck. Each crate gives random cash ($150–400) and 1–2 random items. Uses the `lostTreasure` mission script internally.

---

### 13.2 Mission 2 — Hightable Cargo Drop (MEDIUM)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay + Item Loot |
| **Difficulty** | MEDIUM |
| **Completion Reward** | $450 |
| **Time Limit** | 15 minutes |
| **Depth** | 25m |
| **Equipment Required** | Oxygen Tank |
| **Equipment Cost** | $1,500 (O2 Tank) |
| **Loot Type** | Random items (10–15 crates) + random cash per crate |
| **Random Cash per Crate** | $150–400 |
| **Random Item per Crate** | 1–2x random |
| **Risk Level** | Medium |
| **Police Dispatch** | Possible |

**Earnings Estimate:**
- Completion: $450
- Crates: ~12 avg x ~$275 avg cash = ~$3,300
- Items: ~12 x 1.5 avg = ~18 random items
- **Total estimated: $3,750 + items per run**
- **Time: ~12–15 minutes**
- **Estimated $/hr: $15,000–18,000 (with items)**

**How it Works:** Dive deeper (25m) to a sabotaged cargo ship and collect scattered crates. More crates than Mission 1 (10–15 vs 5–10), deeper dive, more oxygen consumption. Uses `marineResearch` script — more prop spawns.

---

### 13.3 Mission 3 — DEEP SYNDICATE (DANGEROUS)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay + Fixed Item Loot + Random Loot |
| **Difficulty** | DANGEROUS |
| **Completion Reward** | $600 |
| **Time Limit** | 20 minutes |
| **Depth** | 40m (deepest) |
| **Equipment Required** | Oxygen Tank + Diving Suit |
| **Equipment Cost** | $1,500 + $3,000 = $4,500 |
| **Risk Level** | High |
| **Police Dispatch** | Possible |

**Fixed Earnings (on completion):**

| Item | Count | Est. Value |
|:----:|:-----:|:----------:|
| diamond_ring | 1 | ~$500–1,000 (fenceable) |
| rolex | 1 | ~$300–600 (fenceable) |
| goldbar | 1 | ~$1,000–2,000 (fenceable) |
| cash | 250 | $250 |
| Completion reward | — | $600 |

**Random Loot (crates):**
- Crates: 12–15 spawn, each gives $200–500 cash + 1–2 items
- ~13 avg x ~$350 avg = ~$4,550 in random cash
- Items: ~20 random items

**Total Estimated Earnings:**
- Fixed: $600 + $250 + fenceable items (~$1,800–3,600)
- Random: ~$4,550 + items
- **Grand total: ~$7,200–9,000+ per run**
- **Time: ~15–20 minutes**
- **Estimated $/hr: $21,000–27,000 (with items)**

**How it Works:** The hardest mission — 40m depth, requires both O2 tank and diving suit, 20-minute limit. Collect crates from a breached Syndicate bunker. On completion, receive fixed high-value items (diamond ring, rolex, goldbar, cash) IN ADDITION to random crate loot. Uses `deepExploration` script with generous random money ($200–500 range) and the largest prop spawn (12–15).

> **Note:** Mission 3's earnings are the highest in the diving system by a significant margin. The depth requirement, equipment cost ($4,500), and time pressure provide the gates.

---

### 13.4 Mission 4 — Medical Evac Flight 09 (EASY)

| Property | Value |
|----------|-------|
| **Type** | Completion Pay + Item Loot |
| **Difficulty** | EASY |
| **Completion Reward** | $300 |
| **Time Limit** | 15 minutes |
| **Depth** | 15m |
| **Equipment Required** | None (no O2 tank or suit needed) |
| **Equipment Cost** | $0 |
| **Loot Type** | Random items (1 crate) + random cash per crate |
| **Random Cash per Crate** | $150–400 |
| **Random Item per Crate** | 1–2x random |
| **Risk Level** | Low |
| **Police Dispatch** | Possible |

**Earnings Estimate:**
- Completion: $300
- Crates: 1 x ~$275 avg cash = ~$275
- Items: 1–2 random items
- **Total estimated: $575 + items per run**
- **Time: ~8–12 minutes**
- **Estimated $/hr: $2,900–4,300**

**How it Works:** The most accessible mission — no equipment required at all. Dive to a crashed EMS plane in the Alamo Sea (shallow, 15m). Only 1 crate spawns, making the loot minimal. This is a "tryout" mission for new divers who haven't bought gear yet. Uses `emsPlaneCrash` script.

---

## 14. Diving Shop — Equipment Costs

All equipment is purchased from the Diving Mission Ped shop:

| Item | Price | Required For | Description |
|:----:|:-----:|:------------:|:-----------:|
| Oxygen Tank | $1,500 | Missions 1, 2, 3 | +5 min dive time, essential for most missions |
| Diving Suit | $3,000 | Mission 3 | Cold water protection, required for deep dives |
| Underwater Headlight | $800 | Optional | Illuminates dark areas, quality of life |
| Anchor | $500 | Optional | Secures boat position during dive |
| Sonar Device | $4,000 | Optional | Detects underwater objects, navigation aid |

**Equipment Investment Tiers:**

| Tier | Equipment | Total Cost | Missions Accessible |
|:----:|:---------:|:----------:|:-------------------:|
| Free | None | $0 | Mission 4 only |
| Basic | O2 Tank | $1,500 | Missions 1, 2, 4 |
| Full | O2 Tank + Diving Suit | $4,500 | All missions (1–4) |
| Loaded | All gear | $9,800 | All missions + comfort items |

---

## 15. Diving $/hr Estimates

| Mission | Difficulty | Equip Cost | Est. Earnings/Run | Time | Est. $/hr | Entry Barrier |
|:-------:|:----------:|:----------:|:------------------:|:----:|:---------:|:-------------:|
| 4 — Medical Evac | EASY | $0 | ~$575 | ~10 min | $2,900–4,300 | None |
| 1 — Saints Airlines | EASY | $1,500 | ~$2,225 | ~12 min | $9,000–13,000 | O2 Tank |
| 2 — Hightable Cargo | MEDIUM | $1,500 | ~$3,750 | ~14 min | $15,000–18,000 | O2 Tank |
| 3 — DEEP SYNDICATE | DANGEROUS | $4,500 | ~$7,200–9,000 | ~18 min | $21,000–27,000 | O2 + Suit |

> **Important:** Diving mission earnings are heavily item-dependent. The "$/hr" figures include the estimated value of random items (lockpicks, gold chains, rolexes, etc.) which must be **fenced or used** to realize their value. Raw cash income is much lower — the completion rewards ($300–600) are modest. The real money is in the random loot from crates.

> **Break-Even Analysis:** A player spending $4,500 on full gear breaks even after ~1 successful Mission 3 run. After that, every run is pure profit. Even at the basic tier ($1,500 for O2), Mission 1 pays back the investment in a single run.

---

# PART 4 — JOB CENTER ECONOMY (wais-jobpack)

---

## 16. Job Center — Overview

The **Job Center** (`wais-jobpack`) provides a roster of **legal side jobs** accessible from a single ped at the job center location. Unlike illegal jobs, these have zero police risk, pay clean cash, and are available to everyone. The system uses `Config.SideJob = true`, meaning jobs run as side activities — players keep their main job while doing these.

There are **11 enabled jobs** (4 are disabled in config). Jobs are gated by a **10-level XP system** stored in QBCore player metadata, with tiers unlocking progressively harder/better-paying jobs.

### 16.1 Job Center Leveling System

XP is stored via `player.metadata.jobcenter` and mirrors the RxMining progression curve:

| Level | Cumulative XP | XP for This Level | Est. Active Grind Time |
|:-----:|:------------:|:------------------:|:----------------------:|
| 0 | 0 | — | Starter |
| 1 | 300 | 300 | ~0.3 hr |
| 2 | 750 | 450 | ~0.5 hr |
| 3 | 1,500 | 750 | ~0.9 hr |
| 4 | 3,000 | 1,500 | ~1.8 hrs |
| 5 | 6,000 | 3,000 | ~3.5 hrs |
| 6 | 10,000 | 4,000 | ~5.5 hrs |
| 7 | 16,000 | 6,000 | ~9 hrs |
| 8 | 25,000 | 9,000 | ~14 hrs |
| 9 | 40,000 | 15,000 | ~20 hrs |
| 10 | 60,000 | 20,000 | ~25 hrs |

### 16.2 Job Tier Unlock Progression

| Tier | Level Required | Jobs Unlocked |
|:----:|:-------------:|:-------------:|
| 0 — Starter | 0 | Mobile Hotdog, Gardener |
| 1 — Beginner | 2 | Road Helper, Hunter |
| 2 — Intermediate | 4 | Bus Driver, Detectorist |
| 3 — Skilled | 6 | Fire Department, Electrician |
| 4 — Expert | 8 | Project Car, Diver (Job Center) |
| 5 — Master | 10 | Trucker |

### 16.3 XP Formula

Every job payout awards XP using:

```
XP = BaseXP + (rewardAmount × Multiplier)
XP = 5 + (reward × 0.12)
```

**Examples:**
- Hotdog sale ($75 avg): 5 + (75 × 0.12) = **14 XP**
- Bus route ($500 avg): 5 + (500 × 0.12) = **65 XP**
- Trucker delivery ($1,000 avg): 5 + (1000 × 0.12) = **125 XP**

---

## 17. Job Center — Full Job Breakdown

### Tier 0 — Starter Jobs (Level 0)

#### Mobile Hotdog

| Property | Value |
|----------|-------|
| **Reward per Sale** | $65–85 |
| **Customer Interval** | 5–7 seconds |
| **Estimated $/hr** | $650–900 |
| **XP per Sale** | ~14 XP |
| **Risk** | None |
| **Team Size** | Solo |

**How it Works:** Pick up a hotdog cart, push it to a location, press G to set up. NPCs approach every 5–7 seconds and order hotdogs/soda. You serve them and get paid per customer.

#### Gardener

| Property | Value |
|----------|-------|
| **Reward per Garden** | $150 (flat) |
| **Gardens Available** | 8 zones |
| **Full Run Revenue** | $1,200 (8 × $150) |
| **Estimated $/hr** | $800–1,200 |
| **XP per Garden** | ~23 XP |
| **Risk** | None |
| **Team Size** | Solo |

**How it Works:** Travel to garden zones around the map, mow lawns and trim hedges at each location. Flat $150 per zone completed.

### Tier 1 — Beginner Jobs (Level 2)

#### Road Helper

| Property | Value |
|----------|-------|
| **Reward per Event** | $200–225 |
| **Events per Shift** | Random (3–7 calls between events) |
| **Event Types** | Refuelling ($200), Wheel Change ($225), Towing ($200) |
| **Time per Event** | 9–14 minutes |
| **Timer Deduction** | $50/min over time |
| **Estimated $/hr** | $900–1,200 |
| **XP per Event** | ~30 XP |
| **Risk** | None |
| **Team Size** | Solo |

#### Hunter

| Property | Value |
|----------|-------|
| **Reward per Animal** | Boar $50, Deer $50, Coyote $70, Mountain Lion $110 |
| **Hunting Zones** | 4 zones |
| **Animal Attack Chance** | 20% |
| **Estimated $/hr** | $500–800 |
| **XP per Kill** | ~11–18 XP |
| **Risk** | Low (animal attacks) |
| **Team Size** | Multiplayer supported |

### Tier 2 — Intermediate Jobs (Level 4)

#### Bus Driver

| Property | Value |
|----------|-------|
| **Reward per Route** | $475–550 |
| **Routes Available** | 5 lines |
| **Time per Route** | 9–13 minutes |
| **Timer Deduction** | $50/min over time |
| **Estimated $/hr** | $2,200–3,000 |
| **XP per Route** | ~65 XP |
| **Risk** | None |
| **Team Size** | Solo |

**Route Breakdown:**

| Line | Reward | Mission Time |
|:----:|:------:|:----------:|
| #33 | $475 | 9 min |
| #19S | $525 | 12 min |
| #6C | $500 | 10 min |
| #522 | $500 | 13 min |
| #11 | $550 | 13 min |

#### Detectorist (Metal Detecting)

| Property | Value |
|----------|-------|
| **Reward** | Items only (no cash) |
| **Items Found** | Iron, steel, copper, metal scrap, laptop, etc. |
| **Estimated $/hr** | Variable (depends on item selling) |
| **XP per Find** | ~5 XP (base only, no reward multiplier) |
| **Risk** | None |
| **Team Size** | Solo |

**How it Works:** Walk around with a metal detector finding buried items. No direct cash — you keep the items and sell them elsewhere. Good for materials stockpiling.

### Tier 3 — Skilled Jobs (Level 6)

#### Fire Department

| Property | Value |
|----------|-------|
| **Reward per Fire** | $280–400 |
| **Fires Available** | 11 events |
| **Time per Fire** | 6–10 minutes |
| **Timer Deduction** | $100/min over time |
| **Estimated $/hr** | $2,000–3,000 |
| **XP per Fire** | ~43 XP |
| **Risk** | None |
| **Team Size** | Multiplayer supported |

#### Electrician

| Property | Value |
|----------|-------|
| **Reward per Mission** | $550–625 |
| **Missions Available** | 6 maintenance jobs |
| **Time per Mission** | 8–12 minutes |
| **Timer Deduction** | $50/min over time |
| **Estimated $/hr** | $2,500–3,500 |
| **XP per Mission** | ~76 XP |
| **Risk** | None |
| **Team Size** | Multiplayer supported |

### Tier 4 — Expert Jobs (Level 8)

#### Project Car

| Property | Value |
|----------|-------|
| **Reward per Project** | $600–700 |
| **Projects Available** | 3 cars (Jugular $700, Asbo $600, Moonbeam $700) |
| **Time per Project** | 7–8 minutes |
| **Timer Deduction** | Varies |
| **Estimated $/hr** | $3,500–5,000 |
| **XP per Project** | ~84 XP |
| **Risk** | None |
| **Team Size** | Multiplayer (reward split) |

#### Diver (Job Center)

| Property | Value |
|----------|-------|
| **Reward per Dive** | $600–650 |
| **Missions Available** | 7 dive missions |
| **Time per Mission** | 8 minutes |
| **Timer Deduction** | $50/min over time |
| **Estimated $/hr** | $3,500–4,500 |
| **XP per Dive** | ~80 XP |
| **Risk** | None |
| **Team Size** | Multiplayer (reward split) |

> **Note:** This is the Job Center's LEGAL diver job — collecting sea urchins, coral, and moss. It is SEPARATE from the s4-diving treasure hunting missions. Similar pay range but zero loot items.

### Tier 5 — Master Jobs (Level 10)

#### Trucker

| Property | Value |
|----------|-------|
| **Reward per Delivery** | $900–1,050 |
| **Routes Available** | 5 delivery routes |
| **Time per Route** | 10–12 minutes |
| **Timer Deduction** | $50/min over time |
| **Estimated $/hr** | $4,500–5,500 |
| **XP per Delivery** | ~125 XP |
| **Risk** | None |
| **Team Size** | Solo |

**Route Breakdown:**

| Route | Cargo | Reward | Mission Time |
|:-----:|:-----:|:------:|:----------:|
| 1 | Lumber | $900 | 10 min |
| 2 | Ship Transport | $1,000 | 12 min |
| 3 | Aircraft Fuel | $1,050 | 12 min |
| 4 | New Cars | $1,050 | 12 min |
| 5 | Teddy Bears | $950 | 10 min |

---

## 18. Job Center $/hr Estimates

| Tier | Job | Level Req | Pay/Run | Time | $/hr Estimate | XP/Run |
|:----:|:---:|:---------:|:-------:|:----:|:------------:|:------:|
| 0 | Mobile Hotdog | 0 | $65–85/sale | ongoing | $650–900 | ~14 |
| 0 | Gardener | 0 | $150/zone | ~5 min/zone | $800–1,200 | ~23 |
| 1 | Road Helper | 2 | $200–225 | ~12 min | $900–1,200 | ~30 |
| 1 | Hunter | 2 | $50–110/kill | ongoing | $500–800 | ~11–18 |
| 2 | Bus Driver | 4 | $475–550 | ~11 min | $2,200–3,000 | ~65 |
| 2 | Detectorist | 4 | Items only | ongoing | Variable | ~5 |
| 3 | Fire Department | 6 | $280–400 | ~8 min | $2,000–3,000 | ~43 |
| 3 | Electrician | 6 | $550–625 | ~10 min | $2,500–3,500 | ~76 |
| 4 | Project Car | 8 | $600–700 | ~8 min | $3,500–5,000 | ~84 |
| 4 | Diver (Job Center) | 8 | $600–650 | ~8 min | $3,500–4,500 | ~80 |
| 5 | Trucker | 10 | $900–1,050 | ~11 min | $4,500–5,500 | ~125 |

---

# PART 5 — MINING ECONOMY (RxMining + pwr-sellmaterials)

---

## 19. Mining — Overview

The mining system (`RxMining`) is a **legal, progression-heavy economy** centered around an open-world mining zone. Players buy a mining license, purchase pickaxes, and mine ores from rock nodes that spawn in the mining area. Ores are then sold to player-owned **foundries** via the `pwr-sellmaterials` system.

Mining features the deepest tool progression in the server — 6 pickaxe tiers plus 2 drill tiers, each with unique multipliers for loot amount, mining speed, and XP gain. Combined with a 10-level XP system and 5 ore rarity tiers, mining offers **months** of progression content.

### 19.1 Mining Leveling System

| Level | Cumulative XP | XP for This Level | Tier | Est. Active Hours |
|:-----:|:------------:|:------------------:|:----:|:-----------------:|
| 0 | 0 | — | Starter | — |
| 1 | 300 | 300 | Beginner | 2–3 hrs |
| 2 | 750 | 450 | Beginner | 5–6 hrs |
| 3 | 1,500 | 750 | Skilled | 10–12 hrs |
| 4 | 3,000 | 1,500 | Skilled | 20–24 hrs |
| 5 | 6,000 | 3,000 | Expert | 40–50 hrs |
| 6 | 10,000 | 4,000 | Expert | 65–80 hrs |
| 7 | 16,000 | 6,000 | Master | 100–120 hrs |
| 8 | 25,000 | 9,000 | Master | 150–180 hrs |
| 9 | 40,000 | 15,000 | Legendary | 240–280 hrs |
| 10 | 60,000 | 20,000 | Legendary | 350–400 hrs |

> **Note:** Mining has the longest grind in the server by far. Level 10 takes an estimated 350–400 active mining hours (~3 months at 2–3 hrs/day). This is intentional — mining is the "forever progression" system.

### 19.2 Pickaxe & Tool Progression

| Tool | Level Req | Shop Price | Durability | Loot × | Speed × | XP × |
|:----:|:---------:|:----------:|:----------:|:------:|:-------:|:----:|
| Stone Pickaxe | 0 | $50 | 100 hits | 1.0× | 1.0× | 1.0× |
| Iron Pickaxe | 1 | $300 | 120 hits | 1.1× | 1.2× | 1.2× |
| Steel Pickaxe | 3 | $600 | 150 hits | 1.2× | 1.5× | 1.15× |
| Titanium Pickaxe | 4 | $800 | 200 hits | 1.3× | 1.8× | 1.25× |
| Diamond Pickaxe | 5 | $900 | 250 hits | 1.4× | 2.0× | 1.35× |
| Quantum Pickaxe | 6 | $1,000 | 300 hits | 1.5× | 2.2× | 1.45× |
| Mining Drill | 8 | $10,000 | 200 hits | 1.6× | 2.5× | 1.5× |
| Laser Drill | 10 | $25,000 | 300 hits | 1.8× | 3.0× | 1.6× |

**Key Observations:**
- Pickaxes scale smoothly: each tier is a modest improvement, not a quantum leap
- The **Mining Drill** ($10,000 at Level 8) is the first big jump — 1.6× loot and 2.5× speed
- The **Laser Drill** ($25,000 at Level 10) is endgame — 1.8× loot, 3× speed, 1.6× XP
- Durability means tools break and must be repurchased — an ongoing money sink
- Speed multiplier reduces mining time: a 30s ore at 1.0× becomes 10s at 3.0×

---

## 20. Ore Table — Full Breakdown

### Tier 1 — Common Ores (Level 0+, Any Tool)

| Ore | Spawn % | Mine Time | Hits | Cash Drop | Ore Drop | XP/Mine |
|:---:|:-------:|:---------:|:----:|:---------:|:--------:|:-------:|
| Coal | 60% | 5s | 3–5 | $15–30 (50%) | 1–4 coal_ore | 4 XP |
| Carbon | 55% | 6s | 3–6 | $18–35 (50%) | 1–4 carbon | 5 XP |

### Tier 2 — Uncommon Ores (Level 1+, Iron Pickaxe+)

| Ore | Spawn % | Mine Time | Hits | Cash Drop | Ore Drop | XP/Mine |
|:---:|:-------:|:---------:|:----:|:---------:|:--------:|:-------:|
| Copper | 45% | 8s | 4–7 | $25–50 (50%) | 1–4 copperore | 7 XP |
| Iron | 40% | 10s | 5–8 | $30–60 (50%) | 1–4 ironore | 8 XP |

### Tier 3 — Rare Ores (Level 3+, Steel Pickaxe+)

| Ore | Spawn % | Mine Time | Hits | Cash Drop | Ore Drop | XP/Mine |
|:---:|:-------:|:---------:|:----:|:---------:|:--------:|:-------:|
| Aluminum | 30% | 14s | 6–10 | $40–80 (50%) | 1–4 aluminumore | 10 XP |
| Sulfur | 25% | 14s | 6–10 | $45–90 (50%) | 1–4 sulfurore | 11 XP |
| Gold | 20% | 16s | 7–12 | $50–100 (50%) | 1–4 goldingot | 12 XP |

### Tier 4 — Very Rare Gems (Level 5+, Titanium Pickaxe+)

| Gem | Spawn % | Mine Time | Hits | Cash Drop | Gem Drop | XP/Mine |
|:---:|:-------:|:---------:|:----:|:---------:|:--------:|:-------:|
| Onyx | 15% | 20s | 8–14 | $75–150 (50%) | 1 onyx-stone | 15 XP |
| Aquamarine | 15% | 20s | 8–14 | $75–150 (50%) | 1 aquamarine-stone | 16 XP |
| Citrine | 15% | 20s | 8–14 | $75–150 (50%) | 1 citrine-stone | 17 XP |
| Jade | 15% | 20s | 8–14 | $75–150 (50%) | 1 jade-stone | 18 XP |

### Tier 5 — Ultra Rare Gems (Level 7+, Diamond Pickaxe+)

| Gem | Spawn % | Mine Time | Hits | Cash Drop | Gem Drop | XP/Mine |
|:---:|:-------:|:---------:|:----:|:---------:|:--------:|:-------:|
| Diamond | 8% | 30s | 12–20 | $125–250 (50%) | 1 diamond | 30 XP |
| Ruby | 10% | 25s | 10–18 | $100–200 (50%) | 1 ruby-stone | 22 XP |
| Sapphire | 10% | 25s | 10–18 | $100–200 (50%) | 1 sapphire-stone | 24 XP |
| Tanzanite | 8% | 28s | 11–19 | $115–225 (50%) | 1 tanzanite-stone | 26 XP |

> **Note:** Cash drops have a 50% chance. Ore/gem drops are guaranteed (100% chance). The cash is a small bonus on top of the ore which is the main value.

---

## 21. Ore Selling — Foundries (pwr-sellmaterials)

Ores are sold to **player-owned foundries** via the `pwr-sellmaterials` system. There are **5 foundry locations** across the map, each with a 0.5× base multiplier. Prices rotate every 6 hours, and "wanted" materials get a 1.5× bonus.

### Base Sell Prices (at Foundries)

| Material | Base Price | Min Price | Max Price | Effective Range (×0.5 multiplier) |
|:--------:|:---------:|:---------:|:---------:|:----------------------------------:|
| Coal Ore | $6 | $3 | $9 | $1.50–$4.50 |
| Carbon | $10 | $5 | $14 | $2.50–$7.00 |
| Copper Ore | $15 | $10 | $22 | $5.00–$11.00 |
| Iron Ore | $22 | $14 | $32 | $7.00–$16.00 |
| Aluminum Ore | $28 | $16 | $40 | $8.00–$20.00 |
| Sulfur Ore | $25 | $14 | $36 | $7.00–$18.00 |
| Gold Ingot | $55 | $32 | $80 | $16.00–$40.00 |

### Selling Mechanics

| Setting | Value |
|---------|-------|
| **Price Rotation** | Every 6 hours |
| **Wanted Materials** | 2 per foundry per rotation |
| **Wanted Bonus** | 1.5× price (City Hall pays the bonus) |
| **Demand Saturation** | After 500 units sold, price drops (min 0.5× floor) |
| **Sell Cooldown** | 3 seconds between sells |
| **Foundry Multiplier** | 0.5× (all 5 foundries) |

### Gem Selling

**Gems (Tier 4–5) CANNOT be sold to foundries.** They are explicitly excluded:
- Onyx, Aquamarine, Citrine, Jade, Diamond, Ruby, Sapphire, Tanzanite

Gems must be sold through other means (player trading, fencing, etc.), making them a **premium currency** that requires social interaction to monetize.

---

## 22. Mining Shop — Equipment Costs

| Item | Price | Level Req | Purpose |
|:----:|:-----:|:---------:|:-------:|
| Mining License | $300 | 0 | Required to mine, use shop, sell, rent vehicles |
| Stone Pickaxe | $50 | 0 | Starter tool |
| Iron Pickaxe | $300 | 1 | Tier 2 tool |
| Steel Pickaxe | $600 | 3 | Tier 3 tool |
| Titanium Pickaxe | $800 | 4 | Tier 4 tool |
| Diamond Pickaxe | $900 | 5 | Tier 5 tool (mystery unlock) |
| Quantum Pickaxe | $1,000 | 6 | Tier 6 tool (mystery unlock) |
| Mining Drill | $10,000 | 8 | Tier 7 power tool |
| Laser Drill | $25,000 | 10 | Endgame tool |

**Total Investment Path:**
- **Starter:** License ($300) + Stone Pick ($50) = **$350**
- **Through Level 6:** + Iron ($300) + Steel ($600) + Titanium ($800) + Diamond ($900) + Quantum ($1,000) = **$3,950 cumulative**
- **Through Level 10:** + Mining Drill ($10,000) + Laser Drill ($25,000) = **$38,950 cumulative**

> Tools break via durability. A Stone Pickaxe (100 durability) lasts ~100 hits, meaning you'll need replacements. Higher-tier tools have better durability but are proportionally more expensive to replace.

---

## 23. Mining $/hr Estimates by Level

Assuming focused mining with appropriate tool, selling ores at foundries at base multiplier (0.5×):

| Level | Best Tool | Ore Access | Avg Cash/Ore | Avg Sell/Ore | Ores/hr | Gross $/hr | Notes |
|:-----:|:---------:|:----------:|:------------:|:------------:|:-------:|:----------:|:-----:|
| 0 | Stone Pick | Coal, Carbon | ~$12 cash | ~$3 sell | ~40 | **$600** | Starter, very slow |
| 1–2 | Iron Pick | + Copper, Iron | ~$20 cash | ~$8 sell | ~50 | **$1,400** | 1.2× speed helps |
| 3–4 | Steel/Titanium | + Aluminum, Sulfur, Gold | ~$35 cash | ~$15 sell | ~55 | **$2,750** | Gold ore is the prize |
| 5–6 | Diamond/Quantum | + Gems (Onyx, etc.) | ~$55 cash | varies | ~60 | **$3,300+** | Gems can't sell at foundry |
| 7–8 | Mining Drill | + Diamond, Ruby, etc. | ~$85 cash | varies | ~70 | **$5,950+** | Ultra rares spawn rarely |
| 9–10 | Laser Drill | All ores, max efficiency | ~$100 cash | varies | ~80 | **$8,000+** | 3× speed, 1.8× loot |

**Key Observations:**
- Mining cash drops alone are decent (50% chance per ore, $15–250 range)
- The real sustained income comes from selling ores to foundries, but the 0.5× multiplier means foundry prices are LOW
- Gems (Tier 4–5) are the wildcard — they're worth the most but can't be sold at foundries. Their value depends on player-to-player economy
- At endgame (Laser Drill), mining competes with mid-tier illegal jobs in raw $/hr
- The **wanted material bonus** (1.5×) can significantly boost income for specific ores during their rotation window
- Mining also generates **XP** — at high levels with XP multiplier tools, you earn XP faster, but the overall grind to Level 10 is still ~350+ hours

> **Design Intent:** Mining is the **long-game legal economy**. It rewards patience and consistency over quick returns. Players who invest months building their mining level and buying better tools eventually reach competitive income levels — but the journey IS the content. It's not about rushing to Laser Drill; it's about enjoying each tier's progression.

---

# PART 6 — CROSS-SCRIPT ECONOMY SUMMARY

---

## 24. Master Pay Comparison (All Scripts)

Every income activity on the server, ranked by estimated $/hr:

| Rank | Activity | Script | Type | Pay/Run | $/hr Estimate | Risk | Progression Gate |
|:----:|:--------:|:------:|:----:|:-------:|:-------------:|:----:|:----------------:|
| 1 | Diving — DEEP SYNDICATE | s4-diving | Mission + Loot | ~$7,200–9,000 | $21,000–27,000 | High | $4,500 gear |
| 2 | Diving — Hightable Cargo | s4-diving | Mission + Loot | ~$3,750 | $15,000–18,000 | Medium | $1,500 gear |
| 3 | Diving — Saints Airlines | s4-diving | Mission + Loot | ~$2,225 | $9,000–13,000 | Low | $1,500 gear |
| 4 | Mining (Laser Drill, Lvl 10) | RxMining | Mine + Sell | ~$100/ore | $8,000+ | None | Lvl 10 (~350 hrs) |
| 5 | Fraud | 0r-illegalpack | Completion | $3,300 net | $7,000–8,000 | Extreme | Illegal Lvl 12 |
| 6 | Mining (Drill, Lvl 7–8) | RxMining | Mine + Sell | ~$85/ore | $5,950+ | None | Lvl 8 (~150 hrs) |
| 7 | Gun Smuggling | 0r-illegalpack | Completion | $2,200 | $5,500–6,000 | High | Illegal Lvl 10 |
| 8 | Cocaine Lab | 0r-illegalpack | Two-Phase | ~$625/cycle | $5,000–7,000 | Extreme | Illegal Lvl 9 |
| 9 | Trucker | wais-jobpack | Delivery | $900–1,050 | $4,500–5,500 | None | JC Lvl 10 |
| 10 | Project Car | wais-jobpack | Task | $600–700 | $3,500–5,000 | None | JC Lvl 8 |
| 11 | Diver (Job Center) | wais-jobpack | Task | $600–650 | $3,500–4,500 | None | JC Lvl 8 |
| 12 | Illegal Delivery | 0r-illegalpack | Completion | $1,500 | $3,500–4,000 | High | Illegal Lvl 7 |
| 13 | Meth Lab | 0r-illegalpack | Two-Phase | ~$400/cycle | $3,500–5,000 | High | Illegal Lvl 8 |
| 14 | Mining (Steel/Titanium, Lvl 3–4) | RxMining | Mine + Sell | ~$35/ore | $2,750 | None | Lvl 4 (~20 hrs) |
| 15 | Diving — Medical Evac | s4-diving | Mission + Loot | ~$575 | $2,900–4,300 | Low | None |
| 16 | Moonshine | 0r-illegalpack | Completion | $1,110 net | $2,800–3,200 | Medium | Illegal Lvl 6 |
| 17 | Electrician | wais-jobpack | Task | $550–625 | $2,500–3,500 | None | JC Lvl 6 |
| 18 | Bus Driver | wais-jobpack | Delivery | $475–550 | $2,200–3,000 | None | JC Lvl 4 |
| 19 | Chop Shop | 0r-illegalpack | Completion | $650 net | $2,200–2,500 | Medium | Illegal Lvl 4 |
| 20 | Weed Lab | 0r-illegalpack | Two-Phase | ~$200/cycle | $2,000–3,000 | Medium | Illegal Lvl 5 |
| 21 | Fire Department | wais-jobpack | Task | $280–400 | $2,000–3,000 | None | JC Lvl 6 |
| 22 | Car Theft | 0r-illegalpack | Completion | $400 net | $1,800–2,000 | Low | Illegal Lvl 1 |
| 23 | NPC Boxing | 0r-illegalpack | Completion | $400 | $1,600–2,000 | Low | Illegal Lvl 3 |
| 24 | Bag Snatch | 0r-illegalpack | Completion | ~$400 net | $1,500–2,000 | Low | Illegal Lvl 2 |
| 25 | Mining (Iron Pick, Lvl 1–2) | RxMining | Mine + Sell | ~$20/ore | $1,400 | None | Lvl 1 (~3 hrs) |
| 26 | Fishing (Rod Lvl 5) | 0r-fishingv2 | Sell at Market | ~$42/fish | $1,050–1,470 | None | Rod 5 (~$2,900) |
| 27 | Road Helper | wais-jobpack | Task | $200–225 | $900–1,200 | None | JC Lvl 2 |
| 28 | Gardener | wais-jobpack | Task | $150/zone | $800–1,200 | None | JC Lvl 0 |
| 29 | Fishing (Rod Lvl 4) | 0r-fishingv2 | Sell at Market | ~$28/fish | $700–980 | None | Rod 4 (~$1,700) |
| 30 | Mobile Hotdog | wais-jobpack | Vending | $65–85/sale | $650–900 | None | JC Lvl 0 |
| 31 | Mining (Stone Pick, Lvl 0) | RxMining | Mine + Sell | ~$12/ore | $600 | None | License ($300) |
| 32 | Hunter | wais-jobpack | Task | $50–110/kill | $500–800 | Low | JC Lvl 2 |
| 33 | Fishing (Rod Lvl 1–3) | 0r-fishingv2 | Sell at Market | ~$11–18/fish | $275–630 | None | Rod ($500) |

---

## 25. Server Economy Design Philosophy

### The Five-Layer Economy

The Power RP 5.0 economy is designed in **five layers**, each serving a different player archetype:

#### Layer 1 — Casual Legal Work (Fishing + Starter Jobs): Safe, Low Pay
- **$/hr range:** $275–1,200
- **Risk:** Zero
- **Progression:** Rod upgrades (fishing) / Job Center Level 0–2
- **Scripts:** 0r-fishingv2, wais-jobpack (hotdog, gardener, hunter, road helper)
- **Target player:** Brand-new players, casual players, players who want zero stress
- **Key mechanic:** Always available, no prerequisites beyond basic equipment. Fishing has rod upgrades; job center has simple task completion
- **Tradeoff:** The lowest income on the server. You'll never get rich here — but you'll never go broke either

#### Layer 2 — Structured Legal Work (Mid-Tier Jobs + Mining): Moderate Pay, Time Investment
- **$/hr range:** $1,400–5,500
- **Risk:** Zero
- **Progression:** Job Center Level 4–10 / Mining Level 1–6
- **Scripts:** wais-jobpack (bus driver through trucker), RxMining
- **Target player:** Players who enjoy structured progression, "career" players who want to build something
- **Key mechanic:** Both systems have deep leveling. Job Center takes ~25 hrs to max. Mining takes months. The long grind keeps players engaged through incremental tool/job unlocks
- **Tradeoff:** Competitive pay at high levels requires significant time investment. Mining Level 10 takes ~350 hours. Trucker (JC Level 10) takes ~25 hours

#### Layer 3 — Illegal Work (Tablet Jobs + Drug Selling): Medium-High Pay, Escalating Risk
- **$/hr range:** $1,500–8,000
- **Risk:** Low to Extreme (scales with pay)
- **Progression:** 14-level Illegal Tablet XP + 10-level Selling XP (two independent tracks)
- **Scripts:** 0r-illegalpack, op-drugselling
- **Target player:** Active players who want excitement, RPers who enjoy the criminal lifestyle
- **Key mechanic:** Police detection, material costs, dirty money, cooldowns. Two-phase drug jobs require lab production + street selling. Level gates ensure gradual exposure
- **Tradeoff:** Highest risk on the server. Busted runs mean lost time, materials, and potentially your life

#### Layer 4 — Diving (Mission Loot): High Pay, Equipment-Gated
- **$/hr range:** $2,900–27,000
- **Risk:** Low to High (depth-dependent)
- **Progression:** Equipment purchases only (no XP system)
- **Scripts:** s4-diving
- **Target player:** Players who have capital and want quick cash injections
- **Key mechanic:** Random loot-based income. Real value depends on fencing/selling items
- **Tradeoff:** No progression hook = low retention. Repetitive missions. Item values are uncertain

#### Layer 5 — Endgame Mining (Drill Tier): Legal High Pay, Extreme Time Gate
- **$/hr range:** $5,950–8,000+
- **Risk:** Zero
- **Progression:** Mining Level 7–10 (150–400 active hours)
- **Scripts:** RxMining, pwr-sellmaterials
- **Target player:** Dedicated long-term players. The "I've been here for months" crowd
- **Key mechanic:** Laser Drill at Level 10 makes mining competitive with mid-to-high illegal jobs — but it takes 3 months to reach. This is the ultimate "patience pays" reward
- **Tradeoff:** The time investment is massive. Most players will never reach Level 10

### Cross-System Synergies

Several systems feed into each other:

1. **Mining → Foundries:** Ores from RxMining sell at player-owned foundries (pwr-sellmaterials). Foundry owners profit from other players' mining labor
2. **Fishing → Market:** Fish sell at fixed-price markets. No player interaction needed
3. **Drug Labs → Street Selling:** 0r-illegalpack produces drugs, op-drugselling sells them. Two scripts, one pipeline
4. **Diving → Fencing:** s4-diving produces random items that must be fenced or traded to other players
5. **Job Center + Mining shared XP curve:** Both use nearly identical level thresholds (300, 750, 1500, 3000...), creating a consistent "feel" for progression across legal activities

### Why the Numbers Still Work

| Concern | Resolution |
|---------|-----------|
| Diving pays $27k/hr?! | That's item-inclusive. Real cash is ~$600. You need to fence everything. |
| Mining $8k/hr at endgame? | It takes 350 HOURS to get there. That's 3 months at 4hr/day. |
| Trucker at $5.5k/hr? Legal? | Requires JC Level 10 (25 hrs grinding). Same pay as Gun Smuggling but zero risk. |
| Why do illegal jobs at all? | Speed. You can earn $7k/hr at Fraud within ~50 hrs of illegal grinding. Mining takes 6× longer for the same income. |
| Fishing seems useless? | It's the economic floor. No risk, no prerequisites, always available. It's for new/casual players. |
| Hotdog vendor pays $700/hr? | Yes. It's boring, repetitive, and available at Level 0. It exists so brand-new players have SOMETHING to do. |

### The Optimal Strategy Is Still Variety

A veteran player on Power RP 5.0 will naturally use ALL income streams:

- **Morning session (chill):** Fish for 30 minutes or do a gardener/hotdog shift — earn $500–1,000
- **Progress grind:** Run Job Center jobs or mining sessions to push levels
- **Main session (excitement):** Run illegal tablet jobs for the criminal RP experience
- **Big money play:** Dive Mission 3 for a quick $7,000–9,000 cash injection
- **Passive income:** Cook drugs in the lab, sell on the corner when convenient
- **Long-term investment:** Mine when you want zero-risk progression. Each session gets you closer to Laser Drill
- **Endgame rotation:** Mix Fraud, Trucker, and Mining Drill for $5,000–8,000/hr sustained legal+illegal income

**No single activity is meant to be done exclusively.** The economy rewards breadth of engagement across all six scripts, not depth of exploitation in any one.

---

*End of Master Economy Guide — Power RP 5.0*
