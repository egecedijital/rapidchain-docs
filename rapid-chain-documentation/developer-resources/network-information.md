---
icon: hexagon-nodes
---

# Network Information

#### To begin developing on Rapid Chain, configure your environment to connect to the network. Rapid Chain is a fully EVM-compatible network, so your existing tools — Hardhat, Foundry, ethers, viem and standard wallets — work unchanged.

**9.1. Connectivity Parameters**

The following parameters are required to connect your local development tools to Rapid Chain:

| **Parameter**    | **Value**                                   |
| ---------------- | ------------------------------------------- |
| Network Name     | Rapid Chain                            |
| RPC URL          | `https://wallet.rapidchain.io/rpc-internal` |
| Chain ID         | `29250`                                |
| Currency Symbol  | `RAPID`                                |
| Block Explorer   | `https://scan.rapidchain.io`           |
| Wallet           | `https://wallet.rapidchain.io`         |
| Finality         | Single block (deterministic BFT)       |

{% hint style="success" %}
**One confirmation is final.** Rapid Chain never reorganises finalised blocks, so integrations can credit deposits and treat trades as settled after a single block.
{% endhint %}

**9.2. Core Infrastructure Components**

* Validators: Run the deterministic BFT consensus and co-sign every block. The validator set is governed by an on-chain contract.
* Execution & RPC Nodes: Serve JSON-RPC, WebSocket subscriptions and GraphQL for dApps, wallets and indexers.
* Rapid Scan: The native block explorer for transactions, contracts, approvals and CREATE2 verifications.
* SETBridge: Brings USDT from BNB Chain onto Rapid Chain as SETUSD, 1:1.
