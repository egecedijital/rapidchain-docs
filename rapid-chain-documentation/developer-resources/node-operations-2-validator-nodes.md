---
icon: repeat
---

# Node Operations 2 - Validator Nodes

Validator Nodes are the finality engine of Rapid Chain. While Execution Nodes serve high-throughput application traffic, validators order transactions, co-sign blocks and make every block final the moment it is produced.

#### 13.1. Consensus and Finality

Validators run a deterministic BFT consensus protocol.

* Block Proposal: Validators take turns proposing blocks.
* Quorum Signing: Each block is co-signed by a quorum of validators before it is appended to the chain.
* Single-Block Finality: Once the quorum has signed, the block is final. There are no competing forks and no chain reorganisations.

#### 13.2. Admission and Governance

The validator set is managed transparently on-chain.

* Contract-Governed Set: The list of validators lives in an on-chain smart contract. Adding or removing a validator is itself a transaction, permanently auditable on Rapid Scan.
* Stake-Based Participation: Validators stake $RAPID, aligning their economic interests with the network's health.
* Institutional Identity: Validator roles can be linked to verified X.509 institutional identities, ensuring a high-trust environment.

#### 13.3. Security and Operations

* Key Management: Validator signing keys should be held in an HSM or equivalent secure key storage.
* Network Isolation: Validators should not expose public RPC; application traffic is served by separate Execution/RPC Nodes.
* Observability: Every node exports standard Prometheus and OpenTelemetry metrics for uptime monitoring and alerting.
* Permissioning: Node-level allowlists can restrict which peers may connect, where a deployment requires it.

#### 13.4. Hosting Models for Institutions

To meet varying security and infrastructure needs, Validator Nodes support multiple hosting paradigms:

* On-Premise Deployment: For maximum security, allowing institutions to maintain physical control over their hardware and signing keys.
* Managed Cloud Instances: Utilizing vetted cloud providers to ensure high availability while respecting jurisdictional data residency rules.
* Network Requirements: All hosting models require stable, low-latency connectivity to peer validators to maintain consensus performance.
