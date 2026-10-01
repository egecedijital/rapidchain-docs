---
icon: atom
---

# SETBridge & Single-Block Finality Guide

Two properties shape how you integrate with Rapid Chain: **every block is final the moment it is produced**, and **SETBridge** brings stable liquidity from BNB Chain onto the network as SETUSD. This guide covers both.

#### 11.1. Designing for Single-Block Finality

Rapid Chain runs a deterministic BFT consensus. Validators co-sign each block before it is appended, so a block can never be replaced by a competing fork.

| **Integration Concern**        | **Probabilistic-Finality Chains** | **Rapid Chain**            |
| ------------------------------ | --------------------------------- | -------------------------- |
| Confirmations before crediting | Multiple                          | 1                          |
| Reorg handling logic           | Required                          | Not required               |
| Trade settlement               | Delayed until "confident"         | Immediate                  |
| Monitoring                     | Watch for rollbacks               | Watch for inclusion only   |

In practice this means you can remove reorg buffers and rollback handling from exchanges, payment processors and agents:

```javascript
// ethers v6 — on Rapid Chain one confirmation is final
const tx = await setusd.transfer(recipient, amount);
const receipt = await tx.wait(1); // final once included; no reorg buffer needed

console.log(`Settled in block ${receipt.blockNumber}: ${receipt.hash}`);
```

#### 11.2. The SETBridge Workflow

SETBridge connects BNB Chain to Rapid Chain. Every USDT locked on BNB Chain mints SETUSD 1:1 on Rapid Chain.

**Step-by-Step Process:**

1. Lock: The user locks USDT on BNB Chain through SETBridge.
2. Mint: SETUSD is minted 1:1 to the user's address on Rapid Chain — final in a single block.
3. Verify: The mint is publicly visible on Rapid Scan.
4. Use: SETUSD is immediately usable on Rapid Order (RAPID/SETUSD) and in RapidSwap liquidity pools.

#### 11.3. Working with SETUSD

SETUSD is a standard ERC-20 token, built to OpenZeppelin v5 standards with role-based access control and an emergency pause mechanism.

| **Property**   | **Value**                                                                                                                             |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Contract       | `0x6934a22c9734211e4Bf45551c48720CF37623Db2`                                                                                          |
| Standard       | ERC-20 (OpenZeppelin v5)                                                                                                              |
| Explorer       | [View on Rapid Scan](https://scan.rapidchain.io/address/0x6934a22c9734211e4Bf45551c48720CF37623Db2)                                   |

```javascript
// Reading a SETUSD balance with ethers v6
import { Contract, JsonRpcProvider, formatUnits } from "ethers";

const provider = new JsonRpcProvider(RAPID_CHAIN_RPC_URL);
const SETUSD = "0x6934a22c9734211e4Bf45551c48720CF37623Db2";
const erc20 = ["function balanceOf(address) view returns (uint256)", "function decimals() view returns (uint8)"];

const setusd = new Contract(SETUSD, erc20, provider);
const [raw, decimals] = await Promise.all([setusd.balanceOf(account), setusd.decimals()]);
console.log(`SETUSD balance: ${formatUnits(raw, decimals)}`);
```

> **Note:** Because trades on Rapid Order settle through smart-contract escrow on Rapid Chain, every fill inherits the same single-block finality — and can be verified on Rapid Scan.
