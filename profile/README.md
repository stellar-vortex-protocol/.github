# Vortex Protocol

**Intent-based cross-chain swaps with Stellar as the settlement layer.**

Users express a swap intent — *"I want to receive USDC on Stellar, and I'm willing to send 0.14 WETH from Base"* — and a competing solver network races to fill it. No bridges. No wrapped tokens. Settlement is guaranteed by on-chain solver bonds.

> **Project status: ~30% complete.** Core settlement contract, intent relay API, and swap/solver UI are functional against mock data and Stellar testnet primitives. The solver registry contract, on-chain proof verification, and live wallet/contract wiring are in progress. See the per-repo roadmaps and open issues for contribution opportunities.

---

## Repositories

| Repo | Stack | Description |
|---|---|---|
| [**vortex-contract**](https://github.com/vortex-protocol/vortex-contract) | Rust / Soroban | On-chain intent settlement: intent lifecycle, solver bonds, slashing |
| [**vortex-backend**](https://github.com/vortex-protocol/vortex-backend) | TypeScript / Express | Intent relay API + WebSocket intent feed |
| [**vortex-frontend**](https://github.com/vortex-protocol/vortex-frontend) | TypeScript / Next.js 14 | Swap UI + solver portal |
| [**.github**](https://github.com/vortex-protocol/.github) | — | Org-wide community health files (this repo) |

Each repository is independently buildable and deployable. Setup instructions live in each repo's README.

---

## The Problem

Getting tokens onto Stellar from Ethereum / Base / Polygon today requires:

1. Finding a bridge that supports your source token
2. Waiting for bridge finality (often 15–30 min)
3. Dealing with wrapped assets that carry bridge-specific trust assumptions
4. Paying multiple fees across multiple protocols

Vortex replaces this with a single UX primitive: **the swap intent**.

---

## How It Works

```
User                    Vortex                   Solver                   Stellar
 │                         │                        │                        │
 │─── submit_intent() ────►│                        │                        │
 │    (src: 0.14 WETH      │                        │                        │
 │     dst: min 480 USDC)  │◄── quote / accept ────►│                        │
 │                         │                        │                        │
 │                         │                        │── fill_intent() ──────►│
 │                         │                        │   (sends 485 USDC      │
 │◄── 485 USDC received ───│◄───────────────────────│    to user on Stellar) │
 │                         │                        │                        │
```

**Intent lifecycle:**

| State | Description |
|---|---|
| `open` | Awaiting a solver |
| `accepted` | Solver has 5 minutes to fill |
| `filled` | User received output on Stellar |
| `cancelled` | User cancelled before a solver accepted |
| `expired` | No solver filled before the deadline |
| `slashed` | Solver accepted but didn't fill — 10% of bond slashed |

---

## Security Model

Vortex's security relies on two primitives:

1. **Solver bonds** — solvers must lock USDC to participate. Failed fills slash 10% of their bond, making repeated failures unprofitable.
2. **Fill-window enforcement** — once a solver accepts, the intent is locked for 5 minutes. If they fail to fill, the intent reverts to `open` and is re-auctioned, and the bond is slashed permissionlessly via `slash_solver()`.

In production, on-chain proof verification (via cross-chain messaging or oracle attestation) will remove the remaining trust assumption on the solver's honest reporting.

To report a vulnerability, see [SECURITY.md](https://github.com/vortex-protocol/.github/blob/main/SECURITY.md).

---

## Contributing

Vortex is open source and contributions are welcome — this is part of why the project participates in the [Drips](https://www.drips.network/) ecosystem for sustainable open-source funding. Please read [CONTRIBUTING.md](https://github.com/vortex-protocol/.github/blob/main/CONTRIBUTING.md) and our [Code of Conduct](https://github.com/vortex-protocol/.github/blob/main/CODE_OF_CONDUCT.md) before opening a pull request.

---

## License

[MIT](https://github.com/vortex-protocol/.github/blob/main/LICENSE) © 2026 Vortex Protocol Contributors
