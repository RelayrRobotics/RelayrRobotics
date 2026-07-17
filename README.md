<div align="center">

# Relayr Robotics

**The payments & access layer for robotics**

Per-action billing, pay-gated live access, and **instant on-chain settlement** on Robinhood Chain.

[Website](https://relayr.tech) · [Docs](https://relayr.tech/docs) · [Dashboard](https://relayr.tech/dashboard) · [Pay](https://relayr.tech/pay) · [X](https://x.com/RelayrRobotics)

</div>

---

## What is Relayr?

Relayr turns robots into paid, on-chain products. Operators register robots, define billable actions, and get paid in **USDG** on **Robinhood Chain mainnet (`4663`)**. Developers integrate with a drop-in SDK and optional pay widget — no custom payment stack required.

Think **Stripe for robots**: connect hardware, charge per action, settle on-chain.

## What's live (mainnet)

- **Settlement Splitter** — USDG `pay()` instantly splits **88% / 5% / 4% / 3%** (operator / stakers / treasury / burn), then the robot fires
- **Per-action billing** — session → approve → splitter pay → `confirm` → SDK/webhook command
- **Pay-gated access** — short-lived access token unlocks the live stream after payment
- **Operator console** — robots, Activate/Pause, Configure, actions, earnings, webhooks, API keys
- **SDK & signed webhooks** — poll or push paid commands; HMAC-verified deliveries
- **Proof** — clip hash + optional on-chain proof anchor + explorer links
- **Withdraw / weekly auto-payout** — real USDG transfers for any off-chain accrued balance
- **Drop-in pay widget** — `@relayrrobotics/pay-widget` + hosted `/pay` checkout
- **Optional Virtuals ACP** — separate agent-commerce rail (feature-flagged)

## Robinhood Chain — deployed contracts

Network: **Robinhood Chain mainnet · chain id `4663`**  
Explorer: [robinhoodchain.blockscout.com](https://robinhoodchain.blockscout.com)

| Contract / role | Address |
| :-- | :-- |
| **SettlementSplitter** | [`0xc4bf94e197548938729ae38153b9200526edac48`](https://robinhoodchain.blockscout.com/address/0xc4bf94e197548938729ae38153b9200526edac48) |
| **USDG** (Paxos) | [`0x5fc5360D0400a0Fd4f2af552ADD042D716F1d168`](https://robinhoodchain.blockscout.com/address/0x5fc5360D0400a0Fd4f2af552ADD042D716F1d168) |
| Treasury (4%) | [`0x39335902F7CeB5785B49F4e55Db923AF09c5e249`](https://robinhoodchain.blockscout.com/address/0x39335902F7CeB5785B49F4e55Db923AF09c5e249) |
| Stakers (5%) | [`0xa7a1f2B02f98B2D9240A7bC1Fe68530586E8796e`](https://robinhoodchain.blockscout.com/address/0xa7a1f2B02f98B2D9240A7bC1Fe68530586E8796e) |
| Burn (3%) | [`0x000000000000000000000000000000000000dEaD`](https://robinhoodchain.blockscout.com/address/0x000000000000000000000000000000000000dEaD) |

**Deploy tx:** [`0xdbd554b80b47bb1590a0659ecc66250b641e3dfeaaaf46ee1cea26b5c13f578d`](https://robinhoodchain.blockscout.com/tx/0xdbd554b80b47bb1590a0659ecc66250b641e3dfeaaaf46ee1cea26b5c13f578d)

## Quick start

### Robot SDK

```bash
npm i @relayrrobotics/sdk
```

```ts
import { Relayr } from "@relayrrobotics/sdk";

const relayr = new Relayr({
  apiKey: process.env.RELAYR_API_KEY!,
});

await relayr.verify();

relayr.listen(async (command) => {
  await runRobotAction(command.action);
  return { outcome: "success" };
});
```

### Pay widget

```bash
npm i @relayrrobotics/pay-widget
# or: npm i github:RelayrRobotics/Relayr-widget
```

```ts
import { createRelayrPayClient, mountPayButton } from "@relayrrobotics/pay-widget";

mountPayButton(document.getElementById("pay")!, {
  apiOrigin: "https://relayr.tech",
  operatorId,
  actionId,
});
```

Hosted checkout: `https://relayr.tech/pay?operatorId=<uuid>&actionId=<uuid>`

Docs: [relayr.tech/docs](https://relayr.tech/docs) · [Widget](https://relayr.tech/docs/widget)

## Packages & repos

| | |
| :-- | :-- |
| **Website** | [relayr.tech](https://relayr.tech) |
| **Documentation** | [relayr.tech/docs](https://relayr.tech/docs) |
| **Operator Console** | [relayr.tech/dashboard](https://relayr.tech/dashboard) |
| **Pay** | [relayr.tech/pay](https://relayr.tech/pay) |
| **API** | [api.relayr.tech](https://api.relayr.tech) |
| **API Status** | [api.relayr.tech/health](https://api.relayr.tech/health) |
| **npm SDK** | [@relayrrobotics/sdk](https://www.npmjs.com/package/@relayrrobotics/sdk) |
| **npm Widget** | [@relayrrobotics/pay-widget](https://www.npmjs.com/package/@relayrrobotics/pay-widget) |
| **Chain Explorer** | [Robinhood Chain (Blockscout)](https://robinhoodchain.blockscout.com) |
| **X** | [@RelayrRobotics](https://x.com/RelayrRobotics) |

### Open source

| Repository | Description |
| :-- | :-- |
| [relayr-sdk](https://github.com/RelayrRobotics/relayr-sdk) | TypeScript SDK — connect robots, execute paid actions, report proof |
| [Relayr-widget](https://github.com/RelayrRobotics/Relayr-widget) | Drop-in pay widget — USDG Settlement Splitter checkout |

## Stack

Bun · TypeScript · tRPC · Drizzle · PostgreSQL · viem · Solidity · Robinhood Chain · USDG

---

<div align="center">

Built by **Relayr Robotics** on Robinhood Chain

</div>
