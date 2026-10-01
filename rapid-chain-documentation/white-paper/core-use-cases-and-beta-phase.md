---
icon: earth-americas
---

# Core Use Cases and Beta Phase

Rapid Chain’s initial beta phase is strategically focused on high-impact institutional workflows. By separating complex lifecycle management from final settlement, the network enables participants to execute sophisticated financial logic with unprecedented speed and efficiency.

#### 6.1. High-Speed Stablecoin Settlement

Rapid Chain serves as a high-performance routing and automation engine for stablecoin transfers. While the final ownership record is secured on the Canton Network, the execution layer handles the high-frequency operational load.

* Netting & Batching: Multiple cross-institutional transfers are netted in real-time, reducing the number of required settlement entries on the system of record.
* Conditional Payments: Smart contracts on Rapid Chain enable automated, event-driven payments (e.g., Delivery vs. Payment) that trigger only when pre-defined conditions are met.
* Latency Reduction: Cross-institutional settlement friction is minimized through rapid execution-level finality.

#### 6.2. Repo and Collateralized Lending

Repo transactions require intense lifecycle management, including valuation and margin calls, which are computationally expensive on a settlement layer. Rapid Chain offloads this complexity to maintain a lean settlement environment.

| **Workflow Component** | **Rapid Chain Execution**              | **Canton Settlement**             |
| ---------------------- | -------------------------------------- | --------------------------------- |
| Collateral Valuation   | Real-time pricing & risk calculation   | <p>Static asset record</p><p></p> |
| Margin Calls           | Automated triggering & logic execution | Final collateral movement         |
| Netting                | Multilateral exposure netting          | Clean state update                |

#### 6.3. OTC-Style Derivatives and RFQ Execution

Rapid Chain supports off-orderbook execution for derivative-like instruments, enabling bilateral or multilateral negotiation within a controlled environment.

* Exposure Calculation: Real-time monitoring of counterparty exposure occurs at the execution layer.
* RFQ Automation: Request-for-Quote (RFQ) workflows are managed through smart contracts, ensuring pricing integrity before settlement.
* Finalized Positioning: Only fully negotiated and finalized positions are prepared as instructions for the Canton Network.

#### 6.4. Technical Workflow: Automated Margin Call

The following logic illustrates how Rapid Chain automates a repo margin call before sending the final settlement instruction to Canton:

```
// Rapid Chain Repo Lifecycle Logic
contract RepoManagement {
    function processMarginCall(bytes32 repoId, uint256 currentCollateralValue) external {
        // 1. Calculate required margin based on execution-layer risk logic 
        if (currentCollateralValue < targetMaintenanceMargin(repoId)) {
            // 2. Trigger automated collateral request 
            emit MarginCallTriggered(repoId);
            
            // 3. Prepare minimal settlement instruction for Canton 
            prepareCantonSettlement(repoId, "COLLATERAL_ADJUSTMENT");
        }
    }
}
```
