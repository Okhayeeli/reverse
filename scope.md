# PR46 Audit Scope

> **Deployment target:** Base (Aerodrome Slipstream)  
> **Solidity:** `0.8.24` — Foundry (`via_ir=true`, `optimizer_runs=25`)  
> **Branch:** `codex/aerodrome-slipstream-reimpl`

---

## 🔴 Priority 1 — Core Custody & Accounting
*Highest risk. Review first. Any bug here is critical.*

| File | Local Link | Focus |
|------|-----------|-------|
| `V3Vault.sol` | [open](./src/V3Vault.sol) | Borrow/repay/liquidate/transform lifecycle, debt cap, socialization |
| `V3Oracle.sol` | [open](./src/V3Oracle.sol) | Slot0 signed-tick decode, ticks() ABI compat, TWAP valuation overflow |
| `InterestRateModel.sol` | [open](./src/InterestRateModel.sol) | Rate math precision, no underflow |

---

## 🟠 Priority 2 — Staking / Gauge Integration
*New to this PR. Adversarial gauge reverting, one-time `setGaugeManager` risk.*

| File | Local Link | Focus |
|------|-----------|-------|
| `GaugeManager.sol` | [open](./src/GaugeManager.sol) | `getReward` revert paths, fee accounting, withdrawer role |
| `IGaugeManager.sol` | [open](./src/interfaces/IGaugeManager.sol) | Interface completeness |
| `IAerodromeSlipstreamPool.sol` | [open](./src/interfaces/aerodrome/IAerodromeSlipstreamPool.sol) | ABI compatibility with Slipstream |
| `IAerodromeSlipstreamFactory.sol" | [open](./src/interfaces/aerodrome/IAerodromeSlipstreamFactory.sol) | Factory interface |
| `IAerodromeNonfungiblePositionManager.sol` | [open](./src/interfaces/aerodrome/IAerodromeNonfungiblePositionManager.sol) | NFT position manager interface |
| `IGauge.sol` | [open](./src/interfaces/aerodrome/IGauge.sol) | Gauge interface |

---

## 🟡 Priority 3 — Flash + Swap Boundary
*Authentication of flash callbacks; pool authenticity across layouts.*

| File | Local Link | Focus |
|------|-----------|-------|
| `FlashloanLiquidator.sol` | [open](./src/utils/FlashloanLiquidator.sol) | Callback auth, context binding, stateless dust |
| `Swapper.sol` | [open](./src/utils/Swapper.sol) | Slippage enforcement, swap path validation |

---

## 🟢 Priority 4 — Automation / Transforms
*Important but lower novelty; review after P1–P3.*

| File | Local Link | Focus |
|------|-----------|-------|
| `Automator.sol` | [open](./src/automators/Automator.sol) | Operator controls, slot0 usage |
| `AutoExit.sol` | [open](./src/automators/AutoExit.sol) | Exit conditions, price checks |
| `AutoRangeAndCompound.sol` | [open](./src/transformers/AutoRangeAndCompound.sol) | Range migration, compound logic |
| `Transformer.sol` | [open](./src/transformers/Transformer.sol) | Base transform safety |
| `V3Utils.sol` | [open](./src/transformers/V3Utils.sol) | Utility transform paths |

---

## 🔵 Supporting / Reference Only
*Read for context, not primary audit targets.*

| File | Local Link |
|------|-----------|
| `IInterestRateModel.sol` | [open](./src/interfaces/IInterestRateModel.sol) |
| `IProtocolFeeController.sol` | [open](./src/interfaces/IProtocolFeeController.sol) |
| `IV3Oracle.sol` | [open](./src/interfaces/IV3Oracle.sol) |
| `IVault.sol" | [open](./src/interfaces/IVault.sol) |
| `ChainlinkFeedCombinator.sol` | [open](./src/utils/ChainlinkFeedCombinator.sol) |
| `Constants.sol` | [open](./src/utils/Constants.sol) |

---

## Key Test Files (Orientation)

| Test | Local Link |
|------|-----------|
| `BaseAerodromeIntegration.t.sol` | [open](./test/integration/base/BaseAerodromeIntegration.t.sol) |
| `V3VaultAerodrome.t.sol` | [open](./test/integration/aerodrome/V3VaultAerodrome.t.sol) |
| `GaugeManagerVulnerability.t.sol` | [open](./test/integration/aerodrome/GaugeManagerVulnerability.t.sol) |
| `FlashloanLiquidator.t.sol" | [open](./test/integration/aerodrome/FlashloanLiquidator.t.sol) |
| `FlashloanLiquidatorCallback.t.sol` | [open](./test/unit/FlashloanLiquidatorCallback.t.sol) |
| `AutomatorSlot0.t.sol` | [open](./test/unit/AutomatorSlot0.t.sol) |
| `V3OracleSlot0.t.sol" | [open](./test/unit/V3OracleSlot0.t.sol) |
| `AtlasTransitions.t.sol" | [open](./test/atlas/AtlasTransitions.t.sol) |
| `AtlasInvariants.t.sol" | [open](./test/invariants/AtlasInvariants.t.sol) |
