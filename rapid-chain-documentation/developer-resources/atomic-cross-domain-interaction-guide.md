---
icon: atom
---

# Atomic Cross-Domain Interaction Guide

The defining feature of Rapid Chain is its inherent ability to interact with other Canton domains—such as a Bank Node or a Regulator Node—without the use of intermediary bridges. This technology ensures that ownership is synchronized across disparate ledgers simultaneously, rather than "locking and minting" wrapped assets on secondary chains.

#### 11.1. The Atomic Intent Workflow (In-Depth)

Unlike traditional "Bridge and Wrap" models, Rapid Chain utilizes "Financial Intents" for state synchronization. This process operates on an "Atomic Commit" principle (all-or-nothing); the transaction either occurs in both domains simultaneously or fails entirely, leaving no room for mismatched states.

**Step-by-Step Execution Process:**

1. Intent Creation: The user signs an intent on Rapid Chain, such as swapping $RAPID for a tokenized treasury bond.
2. Execution Validation: The Rapid Sequencer validates the trade logic, checks margin requirements, and calculates the net change.
3. Canton Synchronization: The execution result is forwarded to the Canton Network as a formal settlement instruction.
4. Global Commit: The Global Synchronizer ensures that both the execution layer (Rapid Chain) and the settlement layer (Canton) update their states in a single, indivisible step.

| **Feature** | **Traditional Bridging**    | **Rapid Chain Atomic Interaction** |
| ----------- | --------------------------- | ---------------------------------- |
| Asset Type  | Wrapped Assets              | Native Assets                      |
| Trust Model | Trust in Bridge Operator    | Protocol-Level Synchronization     |
| Speed       | Dependent on Confirmations  | Instant (Atomic)                   |
| Risk        | Smart Contract/Bridge Hacks | Mathematical Finality              |

#### 11.2. Cross-Domain Instruction Structure

To format execution results correctly for the Settlement Layer, developers must utilize the `CantonIntegrationAdapter` component.

**Advanced Solidity Interface (EVM Domain):**

The following interface demonstrates how a transaction initiated within the Rapid Chain environment triggers Legal Finality on the Canton Network.

```
// Advanced Atomic Cross-Domain Settlement Interface
interface ICantonAdapter {
    /**
     * @dev Submits the execution result to the Canton settlement layer.
     * @param targetCantonDomain The hash of the target institution's domain (e.g., DTCC).
     * @param assetIdentifier Unique identifier of the asset on Canton.
     * @param finalizedAmount The confirmed amount after netting/execution.
     * @param syncProof Cryptographic proof provided by the Global Synchronizer.
     */
    function submitSettlement(
        bytes32 targetCantonDomain, 
        address assetIdentifier, 
        uint256 finalizedAmount,
        bytes calldata syncProof
    ) external returns (bool success);

    /**
     * @dev Queries the legal finality status of a transaction.
     */
    function checkLegalFinality(bytes32 txHash) external view returns (bool isFinalized);
}
```

> Critical Note: Through this architecture, complex trade logic is processed in Rapid Chain's high-performance environment while Asset Custody and Legal Records remain securely anchored in the Canton Network’s regulated and secure system of record.
