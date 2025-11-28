# Perception Shift - A Secure React Game with Supabase Backend

A modern web-based puzzle game built with React, TypeScript, and Supabase, featuring advanced security implementations and real-time multiplayer capabilities.

## 🎮 About the Project

Perception Shift is an interactive puzzle game where players navigate through rooms, collect shards, and compete on global leaderboards. The project demonstrates modern web development practices with a focus on security, scalability, and user experience.

## 🏗️ Architecture Overview

### Frontend Stack
- **React 18** with TypeScript for type-safe development
- **Vite** for fast development and optimized builds
- **Tailwind CSS** with custom design system and semantic tokens
- **Zustand** for efficient state management
- **React Router** for client-side routing
- **Lucide React** for consistent iconography

### Backend Infrastructure
- **Supabase** as the primary backend service
- **PostgreSQL** database with Row Level Security (RLS)
- **Supabase Edge Functions** for serverless API endpoints
- **Resend** for secure email delivery
- **Real-time subscriptions** for live updates

## 🔐 Security Implementation

This project implements enterprise-grade security measures:

### Database Security
- **Row Level Security (RLS)** on all tables
- **User-specific data isolation** - users can only access their own data
- **Sanitized leaderboard** - no PII exposure (usernames instead of emails)
- **Rate limiting** for verification codes (3 attempts per 5 minutes)
- **Hashed verification codes** stored in database
- **Search path hardening** for all database functions

### API Security
- **CORS restrictions** to project domain only
- **JWT authentication** for protected endpoints
- **Input validation** and sanitization
- **Anti-abuse measures** for game mechanics
- **Secure headers** implementation

### Authentication Flow
- **Email verification** with time-limited codes
- **Passwordless authentication** system
- **Session management** with auto-refresh
- **User enumeration protection**

## 🗃️ Database Schema

### Core Tables
- `profiles` - User profile information
- `user_game_data` - Game statistics and power-ups
- `user_inventory` - Player's collected items
- `leaderboard` - Global rankings (sanitized)
- `verification_codes` - Email verification system
- `verification_attempts` - Rate limiting data

### Security Features
- All tables have RLS policies
- Foreign key constraints for data integrity
- Automated triggers for data consistency
- Indexed columns for performance

## 🚀 Key Features

### Game Mechanics
- **Multi-room progression** with increasing difficulty
- **Shard collection system** with anti-inflation measures
- **Time-based bonuses** for efficient completion
- **Power-up system** with temporary effects
- **Global leaderboards** with ranking system

### User Experience
- **Responsive design** for all screen sizes
- **Dark/light theme support** with system preference detection
- **Real-time updates** for leaderboards and game state
- **Smooth animations** and transitions
- **Accessible UI** with proper ARIA labels

### Administrative Features
- **Comprehensive logging** for debugging
- **Performance monitoring** through analytics
- **Security scanning** with automated reports
- **Database health checks** and optimization

## 🛠️ Development Process

### Initial Setup
1. **Project scaffolding** with Vite + React + TypeScript
2. **Tailwind CSS integration** with custom design system
3. **Supabase project creation** and configuration
4. **Database schema design** with security-first approach

### Security Implementation
1. **Comprehensive security audit** identifying vulnerabilities
2. **RLS policy implementation** for all data access
3. **Edge function hardening** with rate limiting
4. **CORS and authentication** security measures
5. **Anti-abuse systems** for game mechanics

### Feature Development
1. **Core game mechanics** implementation
2. **Authentication system** with email verification
3. **Leaderboard system** with real-time updates
4. **User interface** with responsive design
5. **State management** with Zustand

### Quality Assurance
1. **TypeScript integration** for type safety
2. **ESLint configuration** for code quality
3. **Security linting** with automated checks
4. **Performance optimization** and monitoring
5. **Cross-browser testing** and compatibility

## 📁 Project Structure

```
src/
├── components/           # React components
│   ├── ui/              # Reusable UI components (shadcn/ui)
│   ├── game/            # Game-specific components
│   └── auth/            # Authentication components
├── pages/               # Route components
├── stores/              # Zustand stores
├── lib/                 # Utility functions
├── hooks/               # Custom React hooks
└── integrations/        # Third-party integrations
    └── supabase/        # Supabase client and types

supabase/
├── functions/           # Edge functions
│   ├── send-verification-code/
│   ├── verify-code/
│   └── complete-room/
└── migrations/          # Database migrations
```

## 🚀 Deployment

### Environment Setup
The application uses Supabase for backend services with the following configuration:
- **Project ID**: `ihvnriqsrdhayysfcywm`
- **Environment**: Production-ready with security hardening
- **CDN**: Global edge network for optimal performance

### Edge Functions
Three serverless functions handle backend operations:
1. **send-verification-code**: Email delivery with rate limiting
2. **verify-code**: User verification with security measures
3. **complete-room**: Game completion with anti-abuse protection

## 🔧 Local Development

```bash
# Clone the repository
git clone [repository-url]
cd perception-shift

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

## 🧪 Testing

The project includes comprehensive testing strategies:
- **Type checking** with TypeScript
- **Linting** with ESLint
- **Security scanning** with Supabase linter
- **Manual testing** across browsers and devices

## 📊 Performance Considerations

- **Code splitting** for optimal bundle sizes
- **Lazy loading** for non-critical components
- **Database indexing** for query optimization
- **CDN delivery** for static assets
- **Real-time optimizations** for live features

## 🔮 Future Enhancements

- **Mobile app** development with React Native
- **Advanced analytics** and user behavior tracking
- **Social features** like friend systems and chat
- **Tournament system** with scheduled competitions
- **Achievement system** with unlockable rewards

## 🤝 Contributing

This project demonstrates modern web development practices and can serve as a reference for:
- Secure authentication implementations
- Real-time game mechanics
- Supabase integration patterns
- TypeScript best practices
- Security-first development

---

## Original Lovable Project Info

**Lovable Project URL**: https://lovable.dev/projects/8409cf31-86a0-4af3-9f6a-f9e97eeb6792

### Technologies Used
- Vite
- TypeScript
- React
- shadcn-ui
- Tailwind CSS
- Supabase

### How to Edit
- **Use Lovable**: Visit the project URL and start prompting
- **Use your IDE**: Clone repo and push changes (auto-syncs to Lovable)
- **GitHub Codespaces**: Available for cloud development

### Deployment
Open Lovable and click Share → Publish for instant deployment.

**Built with ❤️ using Lovable, React, and Supabase**

🎴 My Card Museum!!! 💸 — Official README

A development journal + technical overview for classmates, recruiters, and future me.

0) One-liner

Buy goofy-to-exotic cards, mount your flex on glowing pedestals, ride live price swings, and sell smart to build the ultimate Card Museum.

1) What this repo/project is

A Roblox experience built around a live-economy collecting loop:

Shop rotates featured cards on a timer.

Inventory / Collection shows what you own and what you’ve mounted.

Sell Counter buys your cards at current market price.

Pedestals in the museum let you showcase any owned card globally.

Price Ticker nudges prices up/down with occasional rare mutations (events) that spike or dip subsets of cards.

The experience is intentionally bright, meme-y, and readable—think mobile-first clarity with punchy UI and playful names (Gritty Gremlin, Void Phantom).

2) Quick start (developer)

Open the place in Roblox Studio (Play → Current Client).

Verify these service folders exist and are populated:

ReplicatedStorage/Remotes

ReplicatedStorage/Modules (CardDefinitions, Mutations, Shared bootstrap)

StarterPlayerScripts (UI clients, Money HUD, Admin panel)

ServerScriptService (ShopGateway, PriceTicker, ProfilesBootstrap, PedestalRemotes, Commerce gateway)

Make sure each NPC (Shop, Sell) has a ProximityPrompt under a visible part (e.g., Head or an InteractPart).

Press Play; you should see Inventory and Collection buttons at the top. Approach the Card Merchant to open the shop; approach the Card Buyer to sell.

(Owner-only) Open the Admin gear button (top-right) to grant cash/cards for testing.

3) High-level architecture
Core scripts (the “six” pillars you asked for)

ServerScriptService/ServerCore.server.lua
Boot order, profile init, MoneyChanged/InventoryChanged relays, data saves.

Workspace/ShopNPC.server.lua
Binds ProximityPrompt → opens Shop UI, validates requests, calls buy server endpoints.

Workspace/SellNPC.server.lua
Binds ProximityPrompt → opens Sell UI, validates sell requests & payouts.

ServerScriptService/Pedestal.server.lua
Mount/Unmount server authority; replicates museum displays; anti-dupe checks.

ReplicatedStorage/SharedCore.lua
Canonical WaitForChild bootstrap (paths to Remotes/Modules), string utils (TitleCase), currency and rate-limit helpers.

StarterPlayerScripts/GameClient.client.lua
UI hub (Inventory/Collection/Shop/Sell), Money HUD flash (green↑/red↓), admin panel (owner-only), toasts, focus/blur rules.

Under the hood there are gateway helpers (ShopGateway, CommerceGateway, PriceTicker, ProfilesBootstrap). If you need to collapse them into the six, you can embed them (namespaced) inside the above pillars without changing the public API.

Remotes contract

Remotes/OpenShopUI : RemoteEvent

Remotes/BuyFromShop : RemoteFunction (cardId, qty) → {ok, err}

Remotes/SellCards : RemoteFunction (payload) → {ok, cashDelta}

Remotes/MoneyChanged : RemoteEvent (balance, delta)

Remotes/InventoryChanged : RemoteEvent (snapshot or patch)

Remotes/PriceChanged : RemoteEvent (array of {cardId, newPrice, delta})

Remotes/MountOnPedestal : RemoteFunction (cardId, pedId) → ok

Remotes/UnmountFromPedestal : RemoteFunction (pedId) → ok

Data model (simplified)
Profile = {
  cash = number,
  inventory = { [cardId]=count, ... },
  mounted = { [pedId]=cardId, ... },
  seen = { lastShopRefresh = t, ... },
}

CardDefinition = {
  id = "crystal_moth",
  displayName = "Crystal Moth",
  tier = "Common" | "Rare" | "Epic" | "Exotic" | "Mythic",
  basePrice = number,
  rarityWeight = number,   -- for shop weighting
  thumb = "rbxassetid://...",
}

4) Game loop

Browse Shop (3-5 featured cards, refreshes on a timer).

Buy with cash (server checks stock/funds).

Mount prized cards on pedestals (flex your museum).

Wait / watch prices (ticker & mutations).

Sell at a profit (or take the L 😅).

Re-invest into rarer Exotics/Mythics.

5) Feature list (implemented)

Top-bar Inventory / Collection UX (grid with rarity chips & art).

Card Merchant (Shop) and Card Buyer (Sell) NPCs with prompts.

Rotating Shop Offers (stock, price, countdown).

Buy/Sell with full server validation and Money HUD feedback.

Pedestal mount/unmount, replicated museum displays.

Price Ticker + Mutation Events (rare spikes/dips).

Admin Panel (owner-only): give cash, grant card, refresh shop, wipe inv.

Name cleanup (no underscores; Title Case everywhere).

Branding: game = “🎴 My Card Museum!!! 💸”, thumbnail in bright 2D style; shirt text ZIXLE STUDIOS.

6) Day-to-day dev log (reality, not fluff)
Day 1 — Skeleton & prompts

Placed Shop and Sell NPCs; added ProximityPrompt.

First pass ShopNPC.server.lua / SellNPC.server.lua to fire OpenShopUI.

✅ Win: prompts appear; UI hub loads.

❌ Pain: “No ProximityPrompt found” → fixed search path & part parenting.

Day 2 — UI boot & cleanup

Enabled Inventory/Collection top bar.

Hid demo bubbles; moved Trade/Gamepass aside.

Fixed screen dimming not restoring on modal close.

Day 3 — Remotes & modules backbone

Created ReplicatedStorage/Remotes + Modules (CardDefinitions, Mutations, Shared).

Killed infinite yield waits by standard SharedCore boot.

Day 4 — Shop offers & rendering

Implemented ShopGateway; “No cards available” → populated CardDefinitions with starter set.

Title-case display names; thumbnails slotted.

Day 5 — Buy pipeline (server auth)

Swapped brittle OnServerInvoke misuse with proper RemoteFunction/RemoteEvent split.

Money debits → inventory increments → stock decrements → HUD flash.

Day 6 — Sell pipeline

Sell UI summary + server cash credit.

Fixed double-fire & dupe edge cases with per-player cooldown.

Day 7 — Money, HUD, admin

Introduced starting cash for new profiles.

HUD green/red flash on deltas.

Small owner panel (cash + grant card + refresh shop).

Day 8 — Pedestals v1

Mount/unmount with E; replicated museum state.

Resolved GetPedestalHoverInfo infinite yield by publishing ped remotes at boot.

Day 9 — Price ticker & mutations

Background price drift; occasional Mutation Event (e.g., “Nebula Surge”).

Addressed event spam by coalescing updates and throttling signals.

Day 10 — Catalog & tiers polish

Added Exotic/Mythic pool and fun names (brainrot-friendly 😜).

Weighted shop selection by rarity.

Day 11 — Branding + art + blueprint

Finalized name 🎴 My Card Museum!!! 💸.

Produced bright 2D thumbnail; added tiny $ line chart detail.

Drafted blueprint & interior/exterior notes for the museum vibe.

7) Notable bugs & how they were fixed

“No ProximityPrompt found under X” → ensure InteractPart/Head contains a Prompt; search with FindFirstChildWhichIsA("ProximityPrompt", true).

Infinite yield on WaitForChild("SellCards"/"GetPedState") → create remotes at boot; centralize paths in SharedCore.

OnServerInvoke misuse → move to RemoteFunction for requests, RemoteEvent for broadcasts.

“Queue exhausted” spam → throttle price events; batch to arrays per tick.

Underscore names → TitleCase util in the display layer.

8) Design system (UI/UX)

Mobile-first tappable hit areas; consistent padding & rounded corners.

16px/20px/28px type scale; strong contrast; status colors only for deltas.

Modal open/close restores camera & blur every time.

Inventory grid supports thumbnails + rarity chip + price tag.

9) Performance & safety

Server-authoritative buys/sells/mounts.

Per-player rate limit on transactions.

No client-trust for cash/inventory mutations.

Batching price updates to reduce replication churn.

10) Monetization (non-pay-to-win)

Optional Gamepasses (extra pedestal slot, cosmetic trails, museum skin).

Booster: temporary +% sell price for commons only (caps applied).

Avoid selling raw power. Cosmetics + convenience only.

11) Credits

Design/Direction: you (ZIXLE Studios energy 💥).

Engineering assistance: ChatGPT (architecture, debugging, copy).

In-game art direction: bright 2D, goofy, readable; Slap Battles-style clarity as a north star.

12) Appendix — Card tiers & sample names

Common: Ember Bug, Crystal Moth, Gritty Gremlin, Leaf Sprite

Rare: Neon Koi, Byte Bat, Chrome Toad

Epic: Starbound Lynx, Plasma Warden

Exotic: Void Phantom, Glitch Wisp, Prismatic Oni

Mythic: Cosmic Raptor, Aurora Seraph, Null Hydra

Final note

This README documents how the project actually came together—from wiring prompts and stomping infinite-yield errors to a functioning live-economy loop with pedestals, shop rotation, mutations, and owner tools. If you’re reviewing this for coursework or hiring: the emphasis is server authority, predictable UI states, and clean contracts between client and server.
