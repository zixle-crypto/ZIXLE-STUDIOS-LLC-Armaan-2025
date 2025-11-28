🎴 My Card Museum!!! 💸 — A Roblox Live-Economy Collecting Game
A bright, goofy, mobile-first Roblox experience where players buy cards, mount them on glowing pedestals inside a museum, watch live price swings, and sell for profit. Built with Roblox Lua and a server-authoritative economy.

🎮 About the Project
My Card Museum!!! turns collecting into a flex-worthy museum sim:


Rotate through featured shop offers on a timer.


Build your Inventory & Collection, then mount favorites on pedestals.


Price Ticker nudges values up/down with rare Mutation Events.


A Sell Counter buys your cards at current market price.


Style: punchy, 2D, meme-friendly, with ZIXLE STUDIOS branding.



🏗️ Architecture Overview
Client (StarterPlayerScripts)


GameClient.client.lua
Single entry for UI (Inventory/Collection/Shop/Sell), Money HUD (green↑/red↓), focus/blur, toasts, controller support.


ScreenGui layout
Top bar tabs, modal framework, shop list renderer with template cloning, collection grid.


Server (ServerScriptService & Workspace)


ServerCore.server.lua
Bootstraps DataStores, loads/creates player profiles, publishes MoneyChanged / InventoryChanged.


ShopNPC.server.lua (Workspace > shop)
ProximityPrompt → Open Shop. Validates buys, stock, and funds.


SellNPC.server.lua (Workspace > sell)
ProximityPrompt → Open Sell. Validates payload and pays out.


Pedestal.server.lua
Authoritative mount/unmount, prevents dupes, replicates museum state.


Shared (ReplicatedStorage)


SharedCore.lua
Canonical paths (Remotes, Modules), TitleCase, currency/format helpers, debounces, rate limits.


Modules
CardDefinitions.lua, Mutations.lua (event recipes), PriceRules.lua (drift ranges).


Networking Contract


OpenShopUI          : RemoteEvent


BuyFromShop         : RemoteFunction (cardId, qty) -> {ok, err}


SellCards           : RemoteFunction (payload)     -> {ok, cashDelta}


MountOnPedestal     : RemoteFunction (cardId, pedId) -> ok


UnmountFromPedestal : RemoteFunction (pedId) -> ok


MoneyChanged        : RemoteEvent (balance, delta)


InventoryChanged    : RemoteEvent (snapshot|patch)


PriceChanged        : RemoteEvent ([{cardId, newPrice, delta}])



🔐 Security & Anti-Exploit


Server-authoritative economy — cash, stock, inventory, and pedestal state mutate only on the server.


Validation on every transaction (card existence, stock, price snapshot, funds, qty caps).


Rate-limits & debounces (per-player cool-downs on buy/sell/mount).


Sanity caps (max qty per click, per offer; price clamps; cash floors).


Batched price updates (reduces replication spam & “queue exhausted” issues).


Owner-only Admin Panel (command gating by Player.UserId allowlist).



🗃️ Data Model
Profile (per player)
{
  cash = number,                            -- current balance
  inventory = { [cardId]=count, ... },      -- owned counts
  mounted = { [pedId]=cardId, ... },        -- museum placements
  seen = { lastShopRefresh = number }       -- UX helpers
}

CardDefinition
{
  id = "crystal_moth",
  displayName = "Crystal Moth",
  tier = "Common"|"Rare"|"Epic"|"Exotic"|"Mythic",
  basePrice = 120,
  rarityWeight = 30,                         -- shop weighting
  thumb = "rbxassetid://<image>"
}

ShopOffer
{
  cardId = "ember_bug",
  price = 55,
  stock = 6,
  expiresAt = os.time() + 240
}


🚀 Key Features
Game Mechanics


Featured Shop with countdown, stock, and per-item Buy (+/– qty).


Sell Counter that summarizes and pays at live price.


Museum Pedestals (mount/unmount with server checks).


Price Ticker + Mutation Events (e.g., “Nebula Surge” boosts Exotics).


Rarity tiers (Common → Rare → Epic → Exotic → Mythic).


Brainrot-friendly names (Gritty Gremlin, Void Phantom, Prismatic Oni).


UX / UI


Top-bar tabs (Inventory / Collection) always visible.


Money HUD with green flash on gain, red on spend.


Readable, mobile-first hit areas and labels.


Goofy, bright 2D vibe; thumbnails per card; title-case labels (no underscores).


Tiny line-chart detail & 💲 sparkles in the Shop banner for flavor.


Admin (owner-only)


Give cash, grant card, refresh offers, wipe inventory (dev/testing).



🛠️ Development Process (what we actually did)
Initial Setup


Created Remotes, Modules, and the six core scripts (see structure below).


Added ProximityPrompt to shop and sell NPCs.


Built UI shell (tabs + modal) & SafeBoot (consistent WaitForChild paths).


Feature Development


Shop rotation + offer rendering; fixed “no cards available” by populating CardDefinitions.


Buy flow: switched from OnServerInvoke misuse to a proper RemoteFunction.


Sell flow: server validation, debounced; HUD delta flashes.


Pedestals: authoritative mount/unmount + replication.


PriceTicker: drift with occasional Mutations; batched PriceChanged.


Admin Panel: gated actions for owner.


Quality & Stability


Killed infinite yield waits with centralized SharedCore.


De-duplicated remote names and hardened paths.


Event throttling to stop “invocation queue exhausted”.



📁 Project Structure
ReplicatedStorage/
├── Remotes/
│   ├── OpenShopUI                (RemoteEvent)
│   ├── BuyFromShop               (RemoteFunction)
│   ├── SellCards                 (RemoteFunction)
│   ├── MoneyChanged              (RemoteEvent)
│   ├── InventoryChanged          (RemoteEvent)
│   ├── PriceChanged              (RemoteEvent)
│   ├── MountOnPedestal           (RemoteFunction)
│   └── UnmountFromPedestal       (RemoteFunction)
└── Modules/
    ├── SharedCore.lua
    ├── CardDefinitions.lua
    ├── Mutations.lua
    └── PriceRules.lua

ServerScriptService/
├── ServerCore.server.lua
├── PriceTicker.server.lua        (*can be inlined into ServerCore if you want only 1 server script*)
└── ProfilesBootstrap.server.lua  (*optional; can be namespaced in ServerCore*)

Workspace/
├── shop/
│   ├── Head (with ProximityPrompt)
│   └── ShopNPC.server.lua
└── sell/
    ├── Head (with ProximityPrompt)
    └── SellNPC.server.lua
└── Museum/
    └── Pedestals... + Pedestal.server.lua

StarterPlayer/
└── StarterPlayerScripts/
    └── GameClient.client.lua     (UI hub + HUD + admin panel)


Six-script layout (as requested):


ServerCore.server.lua, 2) ShopNPC.server.lua, 3) SellNPC.server.lua, 4) Pedestal.server.lua, 5) SharedCore.lua, 6) GameClient.client.lua.
Any helpers (e.g., price ticker, profiles) can be embedded/namespaced inside these.




▶️ Run / Test


Open in Roblox Studio → Play (Current Client).


Confirm both NPCs show prompts (E to interact).


Use Inventory / Collection buttons at top; open Shop to see offers.


Buy → watch Money HUD turn red with spend; Inventory increments.


Sell → HUD flashes green; balance updates.


Walk to a Pedestal and press E to mount a card.


(Owner) Click the gear icon to open Admin Controls.



🧪 Testing Checklist


Buy with insufficient cash → error toast, no mutation.


Buy beyond stock → clamped/blocked, stock consistent for all clients.


Sell an unowned card → rejected.


Mount card already mounted elsewhere → rejected.


Multiple rapid clicks → rate-limited, no dupes.


Ticker pushes multiple updates → batched PriceChanged, no queue spam.



📊 Performance Considerations


Batched replication for price updates & inventory patches.


Minimal Remote traffic per interaction; server does heavy work.


UI renders via template cloning (no excessive Instance churn).


Clean teardown on modal close (unblur, disconnect connections).



💸 Monetization (not pay-to-win)


Cosmetic museum skins, trails, and pedestal auras.


Boosters (short-term buff for commons only, hard-capped).


No raw stat advantages in competitive selling.



🗓️ Dev Timeline (condensed)


Day 1–2: Prompts + UI shell; fixed dim overlay.


Day 3–4: Remotes/Modules backbone; Shop offers render.


Day 5–6: Buy/Sell pipelines hardened; Money HUD.


Day 7–8: Pedestals; anti-dupe; remote hygiene.


Day 9: PriceTicker + Mutation Events (throttled).


Day 10–11: Rarity polish, Exotic/Mythic pool, branding & thumbnail.



🎨 Content & Branding


Title: 🎴 My Card Museum!!! 💸


Tone: goofy, colorful, meme-friendly, highly readable.


Shirt/brand: ZIXLE STUDIOS


Card vibes: “Crystal Moth”, “Gritty Gremlin”, “Void Phantom (Exotic)”, “Aurora Seraph (Mythic)”.



🔮 Roadmap


Global leaderboards for net worth and museum prestige.


Trading & auctions with escrow and anti-scam flows.


Blueprint museum editor (skins, room unlocks).


Limited-time events & seasonal card sets.


Quests/Achievements with cosmetic rewards.


Cross-server museum visits and curated tours.



🤝 Credits


Game Owner/Direction: You — ZIXLE Studios.


Systems/Architecture: this README & implementation notes authored with ChatGPT.


Visual Direction: bright 2D, crisp icons, big hit targets, stream-friendly.



TL;DR
Buy → Mount → Watch Prices → Sell → Flex the Museum.
Server-auth, anti-exploit, and built to scale—with a silly, catchy vibe that invites players to tap “Play” and stick around.
