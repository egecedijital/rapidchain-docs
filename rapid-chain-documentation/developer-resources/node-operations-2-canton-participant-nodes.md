---
icon: repeat
---

# Node Operations 2 - Canton Participant Nodes

The Canton Participant Node serves as the institutional gateway to the settlement layer. While Rapid Chain manages high-speed execution, the Participant Node functions as the "Legal Memory" and the ultimate system of record for the network.

#### 13.1. System of Record and Legal Finality

The primary role of the Canton Participant Node is to provide an authoritative environment where asset ownership is recorded with legal rigor.

* Legal Sovereignty: This node ensures that ownership changes are finalized according to institutional identity frameworks and regulatory requirements.
* Asset Custody Recording: The Participant Node maintains the official record of asset custody, ensuring that no execution-level state change becomes final until it is committed to this layer.
* Regulatory Compliance Ledger: It acts as a dedicated ledger for compliance, where all state transitions are auditable and deterministic.

#### 13.2. Privacy and Data Sovereignty

In alignment with the "Need-to-Know" privacy model, the Participant Node ensures that institutional data remains protected.

* Localized Data Segregation: Unlike public validators, a Participant Node only stores data and transaction history relevant to the specific parties involved.
* Confidential State Updates: It ensures that while the Global Synchronizer coordinates the transaction, the actual sensitive business logic remains encrypted and isolated within the node.
*   Sovereign Control: Operators have full technical control over their own ledger, preventing third parties from unilaterally forking or altering their specific state.



#### 13.3. Technical Synchronization and Deployment

The Canton Participant Node connects to the Global Synchronizer to enable bridgeless, atomic interactions with Rapid Chain.

Deployment Configuration: Linking Execution to Settlement The following command structure is used to register an institution on the network and bind the Rapid Chain execution logic to the Canton settlement layer.

```
# Registering the Institution on the Canton Network
canton-participant register-party --moniker "Institutional-Entity-01"

# Binding the Rapid Chain Execution Result to Canton Settlement
# Ensures all 'Financial Intents' are translated into deterministic instructions
canton-participant bind-adapter \
  --rapid-rpc "https://rpc.rapidchain.io" \
  --sync-mode "atomic-commit" \
  --privacy-standard "institutional-grade"
```

#### 13.4. Hosting Models for Institutions

To meet varying security and infrastructure needs, the Canton Participant Node supports multiple hosting paradigms:

* On-Premise Deployment: For maximum security, allowing institutions to maintain physical control over their hardware and encryption keys.
* Managed Cloud Instances: Utilizing vetted cloud providers to ensure high availability while respecting jurisdictional data residency rules.
*   Global Synchronizer Alignment: All hosting models require a direct connection to the Canton Foundation’s Global Synchronizer for cross-domain composability.



