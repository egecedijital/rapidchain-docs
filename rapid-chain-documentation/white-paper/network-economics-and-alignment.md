---
icon: diagram-project
---

# Network Economics & Alignment

The economic framework of Rapid Chain is engineered to ensure long-term sustainability and institutional alignment. By decoupling execution costs from settlement finality, the network provides a predictable and scalable environment for complex financial operations.

#### 4.1. The Dual-Layer Settlement & Fee Model

Rapid Chain introduces a symbiotic economic relationship with its settlement partner, utilizing a dual-layer approach to manage network costs and incentives.

* Execution Metering ($RAPID): Computational resources within the EVM and RAda environments are metered using $RAPID. This allows for granular control over gas prices and resource allocation.
* Synchronization Settlement ($CC): Global interoperability and legal finality costs are settled in the background via the Canton Network’s native utility component.
*   Predictable Cost Structures: To meet institutional budgeting requirements, all fees are algorithmically stabilized to maintain a consistent USD-denominated value.



#### 4.2. Comparative Economic Parameters

![Network Economics](https://rapidchain.io/images/12.png)

The following table outlines the distinction between the execution-level utility and the settlement-level security:

| **Economic Function** | **Rapid Chain (Execution)**    | **Canton Network (Settlement)** |
| --------------------- | ------------------------------ | ------------------------------- |
| Primary Unit          | $RAPID                         | $CC                             |
| Fee Denomination      | USD-Stabilized                 | USD-Stabilized                  |
| Utility Role          | Computational Gas & Netting    | Finality & Synchronization      |
| Governance            | Validator Set & Protocol Logic | Network-wide Interoperability   |

#### 4.3. Logic Implementation: Fee Handling

This pseudocode demonstrates how the Sequencer handles the dual-layer fee logic to ensure the Canton synchronization cost is covered:

```
// Rapid Chain Economic Controller
contract EconomicAlignment {
    uint256 public constant USD_GAS_PRICE = 100; // Stabilized USD base

    function calculateTotalFee(uint256 gasUsed) public view returns (uint256) {
        // 1. Calculate the $RAPID execution fee based on current USD rates
        uint256 rapidExecutionFee = gasUsed * getRapidPriceOracle();
        
        // 2. Account for the $CC synchronization cost required by the Global Synchronizer
        uint256 synchronizationCost = getCantonSyncCost();
        
        return rapidExecutionFee + synchronizationCost;
    }
}
```

#### 4.4. Validator Incentives

The network’s security is maintained by a set of vetted, known entities. These validators are incentivized to maintain high uptime and deterministic performance through a structured reward system.

* Stake-Based Participation: Validators must stake $RAPID to participate in the BFT-style consensus, aligning their economic interests with the network's health.
*   Operational Rewards: Incentives are distributed based on the accuracy and speed of state transitions, rather than speculative drivers.

