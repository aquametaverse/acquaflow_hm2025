# ACQUAFlow – Phygital GameFi & DeFi Harbour

ACQUAFlow is a phygital GameFi and DeFi protocol for water‑sports communities, built for ETHGlobal HackMoney 2026. NFC/QR‑equipped paddleboard NFTs act as identities, payment devices, and DeFi access keys across Sui, Yellow, Uniswap v4, Arc, LI.FI, and ENS.

Players tap or scan their phygital boards to rent gear, enter races, and launch gamified DeFi “voyages” that automatically return funds to a safe USDC harbour on Arc. A built‑in impact fee funds real‑world plastic‑pollution research and cleanup.

---

## Core Ideas

- **Phygital paddleboard NFTs**
  - 3D‑printed or tag‑based boards with NFC chip + QR/barcode
  - Tied to Sui NFTs that store rider identity, stats, and equipment
  - ENS names (e.g. `rider123.ACQUA.eth`) link physical boards to on‑chain state

- **Scan / Tap to Pay with Yellow**
  - Yellow SDK + Nitrolite sessions for rentals, race fees, lessons, merch
  - All charges accrue off‑chain; a single on‑chain settlement per session
  - Gasless, instant user experience across EVM chains

- **ENS as Identity & Config**
  - Rider and Shack ENS names store:
    - Linked Sui object IDs
    - Yellow account IDs
    - Preferred chain/token and risk prefs
    - Impact and sponsorship metadata

- **Sui GameFi Layer**
  - Sui Move contracts define:
    - Rider identity objects (XP, rank, achievements)
    - Board/equipment NFTs
    - Event objects for races and sessions
  - Sui’s object model and PTBs power dynamic, composable gameplay

- **Sponsor Shacks Economy**
  - Brands, schools, and locations claim “Shacks” (virtual venues)
  - Shack = Sui object + ENS subname + Yellow account
  - Users visit Shacks to:
    - Trade NFTs
    - Buy real merch and services
    - Access gated digital content
  - Protocol fees from Shacks feed both ACQUA value capture and Impact Treasury

- **Impact & Sustainability Mission**
  - Impact Treasury receives:
    - % of all Yellow session settlements
    - % of protocol and Shack fees
  - Funds researchers and organizations fighting plastic pollution
  - Cleanup and awareness quests reward players with XP/FLOW and badges

- **DeFi Harbour Portal (NFT‑Gated)**
  - Access restricted to ACQUAFlow NFTs
  - Gamified DeFi “voyages”:
    - **Stable Harbour Run** – low‑risk USDC yield on Arc
    - **Cross‑Current LP** – Uniswap v4 LP with hooks‑based strategies
    - **Multi‑Chain Adventure** – cross‑chain strategies via LI.FI
  - LI.FI orchestrates swaps/bridges into/out of Arc and target chains
  - Arc is the USDC “home port” for chain‑abstracted liquidity and payouts
  - Yellow sessions wrap all DeFi actions into gasless, session‑based UX

- **Auto “Return to Harbour” Risk Management**
  - Strategies encode safety rules (drawdown, time, volatility)
  - When triggers fire:
    - Uniswap v4 hooks exit LP and convert to USDC
    - LI.FI routes assets back to Arc
  - User ends in stable USDC on Arc with clear status: “Docked at Harbour”

---

## Integrations by Track

### Yellow Network

- Yellow SDK + Nitrolite sessions for:
  - Rentals, race entries, in‑Shack purchases
  - DeFi Harbour voyages (bundling swaps, LP, bridging)
- Demonstrates:
  - Session‑based off‑chain balances
  - Single on‑chain settlement
  - Clear UX improvement vs. per‑tx gas

### Uniswap v4

- Uses Uniswap v4 pools + hooks to:
  - Manage concentrated liquidity ranges
  - Implement risk‑aware exit logic for DeFi voyages
- Hooks enforce “return to harbour” by exiting LP into USDC on triggers.

### Sui

- Sui contracts manage:
  - Rider identities and stats
  - Board/equipment NFTs
  - Event objects and GameFi logic
- Sui is the high‑performance game and identity layer.

### Arc (Circle)

- Arc is the USDC liquidity hub / harbour:
  - Safe storage and low‑risk yield for returned capital
  - Chain‑abstracted USDC payouts for users and Shacks
- Integrates Circle Wallets / Gateway (if time permits) for clean USDC flows.

### LI.FI

- LI.FI Composer/API orchestrates:
  - Cross‑chain swaps and bridges into/out of Arc
  - One‑click routes for DeFi voyages from any supported EVM chain
- Used to implement multi‑chain strategies without exposing complexity.

### ENS

- ENS names for:
  - Riders (`rider123.ACQUA.eth`)
  - Shacks (`brand.ACQUA.eth`)
  - Impact Treasury (`impact.ACQUA.eth`)
- ENS text records store:
  - Sui object IDs
  - Yellow accounts
  - Preferred chains/tokens
  - Impact and sponsorship metadata

---

## Repo Structure (planned)


├─ contracts/
│  ├─ sui/
│  │  ├─ Rider.move
│  │  ├─ Board.move
│  │  └─ Events.move
│  ├─ evm/
│  │  ├─ ImpactTreasury.sol
│  │  └─ (optional Uniswap v4 hook)
├─ apps/
│  ├─ web-portal/       # Next.js/React DeFi Harbour + Shacks
│  ├─ pos-terminal/     # Simple merchant UI for scan-to-pay
│  └─ mobile-poc/       # Optional mobile PoC for NFC/QR
├─ integrations/
│  ├─ yellow/
│  ├─ lifi/
│  ├─ arc/
│  └─ ens/
└─ README.md


=========================================================

Install dependencies

1 bash
pnpm install   # or yarn / npm

2 Configure environment
Create .env.local with:

RPC URLs
Yellow/Nitrolite keys
LI.FI API key (if required)
Arc testnet details
ENS resolver / chain config

3 Run web portal
bash
pnpm dev

4 Deploy / build Sui contracts
bash
cd contracts/sui
sui move build
# sui client publish --gas-budget <...>

5 Run demo scripts
Example:

scripts/demo_yellow_session.ts
scripts/demo_lifi_route.ts

