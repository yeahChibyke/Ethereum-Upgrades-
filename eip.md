## EIP-0077: Sign-in with Ethereum 2.0 (SIWE-Plus)

- **Author:** Chukwubuike Victory Chime
- **Status:** Draft
- **Category:** Standards Track - ERC
- **Requirements:** EIP-4361, EIP-7702, EIP-7851, EIP-6327

### Abstract

This **EIP** extends [EIP-4361 (Sign-In with Ethereum)](https://developer.litprotocol.com/sdk/access-control/evm/siwe) by introducing reusable, cross-application session tokens, delegated ephemeral keys, optional privacy-preserving pseudonymous identifiers, and metadata fields to improve UX and security.
It is fully backward compatible with **EIP-4361** and can be adopted incrementally by wallets and dApps.

### Motivation

While **EIP-4361** successfully replaced centralized login flows with a self-custodial, Ethereum-based authentication standard, the ecosystem has evolved.
Today’s Web3 authentication faces three persistent challenges:

- **Key Exposure Risk:** Frequent signing with the main wallet key increases the risk of compromise.
- **Fragmented User Sessions:** Users must re-sign for every dApp, even within the same trust scope.
- **Permanent Identity Linkage:** Every login reveals the user’s permanent Ethereum address, reducing privacy.
  
This proposal builds on the solid foundation of EIP-4361 while addressing these challenges with modern security and UX improvements.

### Specifications

1) Session Tokens
   - Upon signing in, the wallet can optionally generate a s**ession token** — a structured, signed object that:
     - Contains the originating address (or pseudonymous ID)
     - Includes an expiry timestamp
     - Specifies allowed domains (scope)
     - Uses a delegated ephemeral key (if chosen)
   - Session tokens are reusable across multiple dApps within the allowed scope.
   - Session tokens must be signed using [EIP-191](https://eips.ethereum.org/EIPS/eip-191) or compatible signature schemes.
  
2) Delegated/Ephemeral
   - Uses [EIP-7702](https://eip7702.io/) / [EIP-7851](https://eips.ethereum.org/EIPS/eip-7851) delegation mechanics.
   - The ephemeral key:
     - Is valid only for the session duration.
     - Can be revoked at any time by the main key holder.
     - Is used for all subsequent sign-in verification during that session.

3) Pseudonymous Identifiers
   - Optional privacy mode using [EIP-6327](https://eips.ethereum.org/EIPS/eip-6327)-like ZKP proofs:
     - Instead of revealing the actual address, the wallet proves possession of a private key linked to an identity commitment.
     - Useful for forums, games, or other contexts where anonymity is preferred.

4) Hardware Signature Flag
   - Payload includes a `hardware` `boolean` field indicating whether the signature originated from:
     - A hardware wallet (Ledger, Trezor, etc.)
     - A secure enclave (e.g., iOS Secure Enclave, Android StrongBox)
   - dApps can choose to enforce stricter rules for non-hardware logins.

5) Backward Compatibility
   - If the wallet or dApp does not support SIWE-Plus fields, they are ignored.
   - Core SIWE fields from EIP-4361 remain intact.

### Rationale

This EIP is designed to:

   - Reduce main key exposure via delegated ephemeral keys.

   - Improve user experience by reducing repeated signing requests.

   - Support privacy-first logins without sacrificing security.

   - Allow dApps to enforce stronger authentication policies when needed.

   - Remain compatible with EIP-4361 to encourage gradual adoption.

### Security Considerations

- **Session Token Theft:** Tokens must be treated as bearer credentials; HTTPS and secure storage are mandatory.
- **Delegated Key Compromise:** Ephemeral keys have limited lifetimes and scopes to minimize damage.
- **Phishing Attacks:** dApps must clearly display token scope and expiry in the wallet prompt to reduce signing blind consent.

### Backwards Compatibility

- Fully compatible with EIP-4361 flows.
- dApps can adopt new fields and flows at their own pace.
- Wallets may continue to offer standard SIWE alongside SIWE-Plus.