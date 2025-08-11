## Shanghai (April 12, 2023)

The **Shanghai** upgrade (also known as **Shapella** when paired with the **Capella** consensus-layer change) finally enabled withdrawals of staked **ETH**, a critical milestone post-Merge.

**Noteworthy EIPs:**

- **EIP-4895 – Beacon Chain Push Withdrawals**

Introduces a "push" mechanism where validator withdrawals from the Beacon Chain are processed as operations in the execution layer. It cleanly integrates consensus-side events with EVM execution without requiring gas, simplifying logic and enabling testing.

- **EIP-3651 – Warm COINBASE**

Optimizes gas by pre-warming the COINBASE address at transaction start, drastically reducing gas cost for access—saving ~2,500 gas per access.

- **EIP-3855 – PUSH0 Instruction**

Adds a dedicated `PUSH0` opcode to push the constant zero onto the stack, reducing reliance on workaround instructions and contract size.  

- **EIP-3860 – Limit and Meter Initcode**

Caps initialization code (`initcode`) at 49,152 bytes and imposes per-chunk gas costs, ensuring fair billing and simplifying EVM engine behavior.

- **EIP-6049 – Deprecate SELFDESTRUCT**

Introduces warnings when using `SELFDESTRUCT`, signaling its imminent removal while avoiding immediate breaking changes.

## Dencun (March 13, 2024)

This combined **Deneb + Cancun** upgrade focuses on modular scalability, primarily through proto-danksharding.

**Noteworthy EIPs:**

- **EIP-4844 – Proto-Danksharding (Blob-Carrying Transactions)** 

Introduces a new transaction type that carries a blob (~125 KB opaque data), stored off-chain but referenced via KZG commitments. Blobs are temporary, pruned after ~2 weeks, massively reducing Layer 2 calldata costs and boosting roll-up scalability by 10–100×.

Sets cryptographic groundwork and constructs the scaffolding for future full Danksharding, enabling data availability sampling and erasure-coded shards .

- **EIP-1153** – Transient storage opcodes cleared post-transaction.

- **EIP-7045** – Extends attestation inclusion window to two epochs.

- **EIP-7514** – Adjusts staking rewards curve to anticipate a high stake ratio.

- **EIP-7516** – Introduces BLOBBASEFEE opcode for cost estimation and future blob fee 

## Pectra (May 7, 2025)

A pivotal upgrade promoting usability, flexibility, and validator efficiency.

**Noteworthy EIPs:**

- **EIP-7702 – Set EOA Account Code (Account Abstraction Seed)**

Enables **Externally Owned Accounts (EOAs)** to temporarily point to and execute smart contract logic—for instance, delegation to a validation contract. It unlocks features like batching, gas sponsorship, session keys, and enhanced UX without full migration to Smart Contract Accounts (SCAs). The EOA's private key remains in control.

Security guidance emphasizes reentrancy awareness, safe delegation patterns, and initialization safeguards.

- **EIP-7251 – Increase MAX_EFFECTIVE_BALANCE**

Raises validator effective balance limit from 32 ETH to 2,048 ETH. Reduces validator count, lowering network overhead and making node operation more sustainable.

- **EIP-7002 – Execution-Layer Triggerable Exits**

Allows validators to initiate exits via the execution layer, enabling programmable staking workflows—paving the way for smart staking contracts and automated validator management.

Post-Merge, Ethereum’s evolution reflects a methodical, layered approach—successive upgrades each target different architectural challenges:

1) **Shanghai** prioritized core functionality (staking withdrawals) and EVM-level gas optimizations.

2) **Dencun** tackled scalability via modular design, introducing proto-danksharding—blobs decouple Layer 1 storage from Layer 2 throughput.

3) **Pectra** advances usability and validator efficiency—EOAs gain smart-contract-like flexibility; staking becomes more scalable and autonomous.

