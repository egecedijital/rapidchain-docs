---
description: How to Create an ERC-20 Token with Custom Features Using Rapid Deployer
icon: location-arrow-up
---

# Node Operations 1 - Rapid Execution Nodes

Rapid Execution Nodes are the high-performance engines of the network, designed to handle high-frequency computational loads while ensuring data isolation. Unlike Validator Nodes, these units prioritize throughput and sophisticated smart contract logic to facilitate rapid market interactions.

#### 12.1. Execution Logic and State Management

Rapid Execution Nodes treat transactions as complex financial intents rather than simple value transfers. This approach allows for sophisticated pre-settlement logic to be processed efficiently before committing results on-chain.<br>

* Netting and Matching Engine: These nodes perform real-time multilateral netting, reducing the number of final transactions written on-chain by over 90%.
* Dual VM Support: Nodes concurrently run a high-performance EVM for standard dApp logic and the RAda VM for safety-critical, formally verified institutional operations.
* Local Data Isolation: To ensure institutional confidentiality, full execution details (such as intermediate state changes and netting logic) are maintained locally within the execution node and are not broadcast to the entire network.
* Intent-to-Transaction Pipeline: The node translates complex bilateral agreements and margin logic into clean, minimal on-chain transactions.

#### 12.2. Technical Deployment Specifications

To maintain the required latency and throughput for institutional DeFi and repo markets, operators must deploy nodes on hardware optimized for high-frequency state updates.

| **Component**    | **Minimum Specification**  | **Recommended (Institutional)** |
| ---------------- | -------------------------- | ------------------------------- |
| CPU              | 8 Cores (High clock speed) | 16+ Cores (Gold/Platinum Tier)  |
| RAM              | 32 GB ECC                  | 64 GB+ ECC                      |
| Storage          | 1 TB NVMe SSD              | 2 TB+ NVMe (RAID 1 Optimized)   |
| Network          | 1 Gbps Symmetric           | 10 Gbps Low-latency / Dedicated |
| Execution Engine | Rapid Execution Client     | Rapid Execution Client + RAda VM |

#### 12.3. Operational Parameters and Finality

The Execution Node operates under a deterministic trust model, ensuring that once a state change is netted, it is committed and final in a single block.

* BFT Sync Mode: Follows the Byzantine Fault Tolerant consensus run by the contract-governed validator set; every block is final as soon as it is produced.
* State Pruning: Automatic state pruning is enabled by default to ensure the database remains lean, focusing on the latest "financial intent" snapshots rather than an exhaustive monolithic history.
* RPC Gateway: Standard JSON-RPC (8545), WebSocket subscriptions and a built-in GraphQL endpoint are available for EVM interactions, while a dedicated FIX-compatible gateway is provided for institutional API access.
* Observability: Prometheus / OpenTelemetry metrics are exported for monitoring and alerting.



#### 12.4. Deployment Command Line (Beta)

Operators can initialize their execution environment using the following command structure.

```
# Initialize the Rapid Execution environment
rapid-node init --moniker "Execution-Node-Alpha" --chain-id 29250

# Launch the high-frequency netting service
rapid-node start --execution.mode "high-performance" --netting.enabled=true
```
