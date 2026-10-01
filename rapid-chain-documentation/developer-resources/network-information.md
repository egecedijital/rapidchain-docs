---
icon: hexagon-nodes
---

# Network Information

#### To begin developing on Rapid Chain, you must configure your environment to interact with the execution layer and the Canton-compatible gateway. Rapid Chain provides a high-performance EVM environment for rapid prototyping and institutional deployment.

**9.1. Connectivity Parameters**

The following parameters are required to connect your local development tools (Hardhat, Foundry, or Metamask) to the Rapid Chain Beta Network:

| **Parameter**    | **Value**                           |
| ---------------- | ----------------------------------- |
| Network Name     | Rapid Chain Beta                    |
| RPC URL          | `https://rpc.rapidchain.io/v1/beta` |
| Chain ID         | `20261`                             |
| Currency Symbol  | `RAPID`                             |
| Block Explorer   | `https://explorer.rapidchain.io`    |
| Settlement Layer | Canton Network                      |

**9.2. Core Infrastructure Components**

* Rapid Sequencer: Handles transaction ordering and execution-level finality.
* Canton Adapter: The gateway for synchronizing execution results with the Canton settlement layer.
* Global Synchronizer: The trustless backbone facilitating cross-domain atomic commits.

