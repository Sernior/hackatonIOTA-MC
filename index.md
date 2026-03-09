---
layout: home
title: Home
nav_order: 1
---

# NPLEX - NPL Tokenization Platform

## Project Overview

NPLEX is a blockchain-based platform for tokenizing Non-Performing Loan (NPL) packages using the IOTA network. The platform enables retail investors to participate in NPL investments through fractional ownership via the LTC1 (Loan Token Contract) standard.

**Core Philosophy:** Align incentives between Investors (Capital) and Servicers (Labor) through "Skin in the Game".

## Core Concepts

### Business Flow

1. **NPL Acquisition**: A bank creates an NPL package
2. **Tokenization**: The package is tokenized via LTC1 contract
3. **Retail Funding**: Retail investors buy tokens to finance the bank
4. **Revenue Distribution**: As debts are recovered or package is resold, revenue flows back to token holders
5. **Contract Closure**: When package is fully liquidated or resold, contract closes.

### Revenue Sources

The LTC1 contract receives IOTA through **2 channels**:

1. **Debt Recovery**: Servicer recovers debts and deposits recovered amounts
2. **Package Resale**: If the package is sold to another party, sale proceeds are deposited

## Architecture: The 2-Asset Model + DID Gatekeeper

The architecture is built around **two distinct Move Objects** per NPL Package, with ownership tracked via **IOTA DID (Decentralized Identity)**:

1.  **LTC1Package (Shared Object)**: The "State". Holds the pools (funds/revenue), metadata, business logic, and `owner_identity: ID` pointing to the owner's DID document.
2.  **LTC1Token (Owned Object - Many)**: The "Investment". NFTs (`key` only) representing a share of the revenue. Held by investors.

**Ownership** is determined by the `owner_identity` field on LTC1Package, verified at runtime via `DelegationToken` from the IOTA Identity framework. There is no separate "OwnerBond" object.

### Layer 1: NPLEX Registry (Validation + Identity Layer)

- Managed by NPLEX
- Audits and approves NPL package notarizations via IOTA Notarization objects
- Prevents duplicate LTC1 contracts for the same notarization
- Can invalidate contracts (e.g., when all debts recovered)
- Only NPLEX admin can register notarizations after KYC of financial institutions and the creation of the NPL package
- Authorizes ownership transfers and sales toggles, backed by notarization references
- **Manages approved DID identities** with role-based access (Institution, Investor, Admin)

### Layer 2: LTC1 Contracts (Token Layer)

Each LTC1 contract operates using these assets:

#### 1. LTC1 Tokens (For Investors)

- **Role:** Capital contribution & Revenue rights.
- **Properties:** `key` only (no `store`), transferable via `transfer_token` (DID-gated).
- **Acquisition:** Investors mint these by paying into the funding pool.

#### 2. Owner Identity (For Owner — stored on LTC1Package)

- **Role:** Represents **legal ownership** of the NPL package & "Skin in the Game".
- **Mechanism:** The `owner_identity: ID` field on `LTC1Package` points to the owner's approved DID.
- **Verification:** All owner-gated functions verify the caller's `DelegationToken` matches the registered `owner_identity`.
- **Transfer:** Ownership can be transferred to a new DID with NPLEX approval via `transfer_ownership`.

#### Verifiable Credentials (VC) Integration

NPLEX uses a **hybrid architecture** that bridges off-chain W3C Verifiable Credentials with on-chain smart contract authorization:

- **Off-chain (Backend):** The NPLEX backend acts as an Issuer using the IOTA Identity SDK. After a user completes KYC/AML verification, the backend issues a signed W3C Verifiable Credential (JWT format) to the user's wallet.
- **On-chain (Smart Contract):** When the admin calls `approve_identity`, the raw bytes of the W3C VC (`vc_data: vector<u8>`) are **mandatory**. They are stored permanently inside the `ApprovedIdentity` record in the registry as an immutable on-chain audit trail.
- **Why not in events?** The `iota_identity::public_vc::PublicVc` struct (which wraps `vector<u8>`) has only the `store` ability — no `copy` or `drop`. This means VC data cannot be emitted in Move events. It is stored once in the registry table and can be queried directly.
- **User flow:** Once approved, the user interacts with the protocol using only their `DelegationToken` — no VC data is needed at transaction time. The on-chain VC serves as a compliance receipt for auditors.

### Layer 3: Fractionalization (Optional)

LTC1Tokens can be fractionalized into fungible DEX-tradeable coins:

- **Fractionalize**: Splits balance from an LTC1Token, mints fungible coins, creates a shared vault
- **Redeem**: Burns coins back into a new LTC1Token with proportional claimed_revenue
- **Merge Back**: Burns coins back into the SAME token (no new token created)
- **Destroy Empty Vault**: Cleanup when vault supply reaches 0

## API Reference

### NPLEX Registry Module

| Function                      | Description                                                                                                                                                      |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `register_notarization`       | Register an approved notarization by ID (Admin Only, for `create_contract` use)                                                                                  |
| `revoke_notarization`         | Revoke a notarization if fraud detected (Admin Only)                                                                                                             |
| `unrevoke_notarization`       | Un-revoke a previously revoked notarization (Admin Only)                                                                                                         |
| `update_authorized_creator`   | Update who can create a contract with a notarization (Admin Only)                                                                                                |
| `add_executor`                | Authorize a module (LTC1) to bind to notarizations (Admin Only)                                                                                                  |
| `remove_executor`             | De-authorize a module (Admin Only)                                                                                                                               |
| `authorize_transfer`          | Authorize ownership transfer to a new DID, backed by a notarization reference (Admin Only)                                                                       |
| `authorize_sales_toggle`      | Authorize a sales state change, backed by a notarization reference (Admin Only)                                                                                  |
| `approve_identity`            | Whitelist a DID with a role (Admin Only). Requires mandatory `vc_data` (raw W3C Verifiable Credential bytes) and backing notarization as an on-chain audit trail |
| `revoke_identity`             | Remove a DID from the whitelist (Admin Only, requires backing notarization)                                                                                      |
| `verify_identity`             | Verify a DelegationToken belongs to a whitelisted DID with a required role (Public)                                                                              |
| `claim_notarization`          | Start the contract creation process by claiming a notarization                                                                                                   |
| `bind_executor`               | Bind a claimed notarization to a new contract ID                                                                                                                 |
| `consume_transfer_ticket`     | Consume authorization to execute an ownership transfer                                                                                                           |
| `consume_sales_toggle_ticket` | Consume authorization to execute a sales toggle                                                                                                                  |
| `is_valid_notarization`       | Check if notarization is approved and not revoked                                                                                                                |
| `get_notarization_info`       | Get full status of a registered notarization                                                                                                                     |

### LTC1 Module

| Function              | Description                                                                                       |
| --------------------- | ------------------------------------------------------------------------------------------------- |
| `create_contract`     | Initialize new LTC1 with `Notarization<u256>` validation, accepts `owner_identity: ID`            |
| `buy_token`           | Investors purchase tokens (IOTA → funding pool, includes dividend-stripping protection)           |
| `withdraw_funding`    | Owner withdraws raised capital (DID-verified)                                                     |
| `deposit_revenue`     | Owner deposits recovered funds (DID-verified)                                                     |
| `claim_revenue`       | Token holders claim proportional revenue (DID-verified, **blocked when revoked**)                 |
| `claim_revenue_owner` | Owner claims revenue from unsold shares + legacy revenue (DID-verified, **blocked when revoked**) |
| `transfer_ownership`  | Transfer package ownership to a new DID (requires NPLEX approval)                                 |
| `transfer_token`      | DID-gated token transfer between investors                                                        |
| `toggle_sales`        | Toggle sales open/closed (requires NPLEX approval, consumes sales toggle ticket)                  |
| `verify_document`     | Verify document hash matches (Public)                                                             |
| `balance`             | View token balance (Public)                                                                       |
| `claimed_revenue`     | View total revenue claimed by a token (Public)                                                    |

### Fractional Module

| Function              | Description                                                                      |
| --------------------- | -------------------------------------------------------------------------------- |
| `fractionalize`       | Split LTC1Token balance into fungible DEX-tradeable coins                        |
| `redeem`              | Burn fraction coins back into a new LTC1Token with proportional revenue tracking |
| `merge_back`          | Burn fraction coins back into the same existing LTC1Token                        |
| `destroy_empty_vault` | Cleanup an empty FractionalVault (freezes TreasuryCap)                           |

## Events

All events are emitted via `public(package)` emitter functions in `events.move`.

### Registry Events

- `NotarizationRegistered` — notarization registered
- `NotarizationRevoked` / `NotarizationUnrevoked` — revocation state changes
- `AuthorizedCreatorUpdated` — authorized creator changed for a notarization
- `ExecutorAdded` / `ExecutorRemoved` — executor module authorization changes (idempotent, no event if no-op)
- `TransferAuthorized` / `TransferConsumed` / `TransferRevoked` — ownership transfer lifecycle
- `SalesToggleAuthorized` / `SalesToggleConsumed` / `SalesToggleRevoked` — sales toggle lifecycle
- `IdentityApproved` — new DID whitelisted (VC data stored in registry, not in event)
- `IdentityRoleUpdated` — existing DID role changed (VC data stored in registry, not in event)
- `IdentityRevoked` — DID removed from whitelist

### LTC1 Events

- `ContractCreated` — new LTC1 package created
- `TokenPurchased` — investor purchased tokens
- `RevenueDeposited` — owner deposited revenue
- `FundingWithdrawn` — owner withdrew funding
- `RevenueClaimedOwner` / `RevenueClaimedInvestor` — revenue claims
- `OwnershipTransferred` — package ownership transferred to new DID
- `OwnerDidUpdated` — owner DID set or changed on LTC1Package
- `SalesToggled` — sales state changed

### Fractional Events

- `VaultCreated` — new fractional vault created
- `FractionRedeemed` — fractions redeemed for new token
- `FractionMergedBack` — fractions merged back into existing token
- `VaultEmpty` — vault supply reached zero
- `VaultDestroyed` — empty vault destroyed

## Workflow

1. **NPLEX Audits**: NPLEX audits NPL package documents and approves notarization
2. **Notarization Registration**: NPLEX registers the approved `Notarization<u256>` object in the Registry
3. **LTC1 Creation**: Creator passes the `Notarization<u256>` object and their `owner_identity: ID` to `create_contract`
4. **Token Sale**: Investors buy tokens directly from LTC1 using `buy_token()`, IOTA goes to funding pool
5. **Funding Withdrawal**: Owner withdraws IOTA from funding pool to finance NPL acquisition (DID-verified)
6. **Recovery**: Owner recovers debt → deposits IOTA into revenue pool (DID-verified)
7. **Claim**: Token holders claim proportional share from revenue pool (DID-verified)
8. **Termination**: NPLEX revokes notarization in Registry (when all credits resolved) → blocks operations except claims

## Revenue Distribution Mechanism (Proportional / Pari-Passu)

Unlike complex **Waterfall Distribution** (or Tranche-based) models where Senior bonds get paid before Junior bonds, LTC1 uses a simple **Proportional Distribution** model. Every token holder is entitled to a share of the revenue exactly equal to their percentage of ownership in the total supply.

**Revenue formula:**

```
entitled = (token.balance × total_revenue_deposited) / total_supply
due = entitled - token.claimed_revenue
```

**Dividend-stripping protection:** When new tokens are bought, `claimed_revenue` is pre-set to prevent "buying into" past revenue. The equivalent amount goes to `owner_legacy_revenue`.

## Key Design Decisions

### 1. DID-Based Ownership

Ownership is tracked via the `owner_identity: ID` field on `LTC1Package`, pointing to the owner's **IOTA DID document**. All owner-gated operations verify the caller's `DelegationToken` against this identity.

**Why?** To enforce **Risk Retention** (or "Skin in the Game") without a separate transferable object.
In securitization markets, regulations often require the originator of a security to retain a certain percentage of the risk (e.g. 5%) to ensure their incentives are aligned with investors. If the asset performs poorly, the originator suffers losses alongside the investors.

The `owner_identity` enforces this by binding the unsold supply portion to the owner's DID. Ownership transfer requires NPLEX admin approval via `transfer_ownership`, ensuring the owner remains committed to the asset's performance.

**Token Purchase (Primary Sale):**

- Creator (Bank) creates the package — their DID is set as `owner_identity` on the shared `LTC1Package`.
- Investors call `buy_token()` to purchase shares. The contract **mints new LTC1 Tokens (NFTs)** directly to the investor.
- Creator may transfer ownership to a Servicer via `transfer_ownership` (requires NPLEX approval).
- The `owner_identity` represents the **legal ownership** of the NPL package and the **executive power** to manage it: all unsold shares, the right to claim their revenue, withdraw the funding pool, deposit revenue, and transfer ownership with NPLEX approval.

### 2. Cumulative Claims

Both Investors and Owner claim **all accumulated unclaimed revenue** when calling their claim functions.

### 3. Default Scenario

If the Owner never recovers any debts:

- Revenue pool remains empty
- Tokens remain valid but worthless
- Owner loses their time/effort (Skin in the Game penalty)
- NPLEX may initiate legal action

### 4. Metadata & Documentation

- **Name**: Name of the NPL package
- **Document Hash**: SHA-256 of NPL package ZIP (immutable, stored in Notarization object)
- **Metadata URI**: IPFS/HTTPS link to documents
- **On-chain**: Minimal metadata to save gas (Will change overtime due to compliance which is not yet defined)

## Contract Termination

**Trigger**: NPLEX sets `is_revoked = true` in Registry for the package notarization

**When revoked:**

- **buy_token()**: Blocked - No new token purchases
- **withdraw_funding()**: Blocked - Owner cannot withdraw
- **deposit_revenue()**: Blocked - Owner cannot deposit
- **claim_revenue()**: Blocked - Claims are not allowed when the contract is revoked (subject to change per future granular controls)
- **transfer_token()**: Allowed - Tokens remain tradeable

**Revocation reasons:**

- All debts fully recovered (package liquidated)
- Fraud detected (legal action initiated)

**Post-termination**: Tokens remain as proof of investment, and ownership is still reflected in the `owner_identity` on the package.

## Business Model (Future)

- **No fees** for notarization registration or LTC1 creation in MVP
- Revenue streams (planned):
  - Platform consultation services
  - LTC1 management services
  - Possible transaction fees (TBD when NPLEX must be involved, free otherwise)

## Compliance & Scope (MVP)

- **No jurisdiction/country fields** - compliance deferred to post-MVP
- Focus: Technical proof-of-concept for tokenization

## Future Implementations

### Granular Revocation Control

Currently, revocation is a binary state. Future versions will support granular permissions:

- **Block Deposits Only**: Stop new investments/deposits but allow withdrawals.
- **Block Trading**: Stop token transfers while allowing claims.
- **Full Freeze**: Stop all operations for investigation.
