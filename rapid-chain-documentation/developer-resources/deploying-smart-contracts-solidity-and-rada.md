---
icon: file-signature
---

# Deploying Smart Contracts: Solidity & RAda

Rapid Chain supports a hybrid virtual machine architecture, allowing developers to choose the optimal environment based on the specific risk profile and complexity of their financial logic.

**10.1. Deploying Solidity Contracts (EVM)**

Standard Solidity contracts can be deployed using existing Ethereum tooling. This allows for rapid migration of existing DeFi protocols while benefiting from single-block finality.

```
// Hardhat Deployment Script Example
async function main() {
  const RapidStablecoin = await ethers.getContractFactory("RapidStablecoin");
  const token = await RapidStablecoin.deploy();
  
  await token.deployed();
  console.log("Rapid Stablecoin deployed to:", token.address);
}
```

\
**10.2. High-Assurance Logic with RAda**

For operations where correctness, determinism, and formal verifiability are paramount, Rapid Chain introduces RAda. RAda is a high-assurance smart contract language derived from safety-critical programming paradigms used in aerospace and defense systems.

\
Key Characteristics of RAda:

* Formal Verifiability: RAda is designed for mathematical proof of correctness, allowing developers to verify that a contract behaves exactly as specified before deployment.
* Safety-Critical Origins: Built upon paradigms used in environments where failure is not an option, RAda eliminates common smart contract vulnerabilities like integer overflows or reentrancy at the compiler level.
* Deterministic Execution: Every RAda instruction has a predictable and deterministic state transition, essential for high-value institutional settlement.
* Selective Usage: RAda is not a replacement for Solidity but a complementary tool; institutions can choose RAda for high-risk operations like collateral netting while using Solidity for general-purpose logic.

RAda Code Example (High-Assurance Settlement):

The following snippet demonstrates a secure asset netting operation using RAda’s high-assurance syntax (based on SPARK/Ada safety standards):

```
-- RAda High-Assurance Settlement Module
package Rapid_Settlement is
   type Asset_Amount is range 0 .. 10**18;
   
   -- Secure transfer procedure with pre-conditions and post-conditions
   procedure Secure_Netting (
      Sender    : in out Account;
      Receiver  : in out Account;
      Amount    : in     Asset_Amount
   ) with
      Pre  => Sender.Balance >= Amount, -- Formal verification of solvency
      Post => Sender.Balance = Sender.Balance'Old - Amount and
              Receiver.Balance = Receiver.Balance'Old + Amount;
end Rapid_Settlement;

package body Rapid_Settlement is
   procedure Secure_Netting (
      Sender    : in out Account;
      Receiver  : in out Account;
      Amount    : in     Asset_Amount
   ) is
   begin
      Sender.Balance   := Sender.Balance - Amount;
      Receiver.Balance := Receiver.Balance + Amount;
   end Secure_Netting;
end Rapid_Settlement;
```

This ensures that critical financial operations like Multilateral Netting or Repo Collateral Calls are executed with the same level of rigor as flight control systems.

**10.3. No-Code Option: Token Pilot**

For standard ERC-20 tokens, [Token Pilot](https://tokenpilot.online) generates and deploys the contract straight from your own wallet — no Solidity required. Choose only the features you need (mint, burn, max-wallet limit, transfer cooldown); deployments are verifiable on Rapid Scan via CREATE2.
