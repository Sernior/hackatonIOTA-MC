---
layout: default
title: events
parent: Nplex Smart Contracts
---


<a name="(nplex=0x0)_events"></a>

# Module `(nplex=0x0)::events`

NPLEX Events Module

Centralizes all event definitions to improve discoverability and indexing.


-  [Struct `NotarizationRegistered`](#(nplex=0x0)_events_NotarizationRegistered)
-  [Struct `NotarizationRevoked`](#(nplex=0x0)_events_NotarizationRevoked)
-  [Struct `NotarizationUnrevoked`](#(nplex=0x0)_events_NotarizationUnrevoked)
-  [Struct `AuthorizedCreatorUpdated`](#(nplex=0x0)_events_AuthorizedCreatorUpdated)
-  [Struct `ExecutorAdded`](#(nplex=0x0)_events_ExecutorAdded)
-  [Struct `ExecutorRemoved`](#(nplex=0x0)_events_ExecutorRemoved)
-  [Struct `TransferAuthorized`](#(nplex=0x0)_events_TransferAuthorized)
-  [Struct `TransferConsumed`](#(nplex=0x0)_events_TransferConsumed)
-  [Struct `TransferRevoked`](#(nplex=0x0)_events_TransferRevoked)
-  [Struct `SalesToggleAuthorized`](#(nplex=0x0)_events_SalesToggleAuthorized)
-  [Struct `SalesToggleConsumed`](#(nplex=0x0)_events_SalesToggleConsumed)
-  [Struct `SalesToggleRevoked`](#(nplex=0x0)_events_SalesToggleRevoked)
-  [Struct `IdentityApproved`](#(nplex=0x0)_events_IdentityApproved)
-  [Struct `IdentityRoleUpdated`](#(nplex=0x0)_events_IdentityRoleUpdated)
-  [Struct `TokenTransferred`](#(nplex=0x0)_events_TokenTransferred)
-  [Struct `ContractCreated`](#(nplex=0x0)_events_ContractCreated)
-  [Struct `IdentityRevoked`](#(nplex=0x0)_events_IdentityRevoked)
-  [Struct `TokenPurchased`](#(nplex=0x0)_events_TokenPurchased)
-  [Struct `RevenueDeposited`](#(nplex=0x0)_events_RevenueDeposited)
-  [Struct `FundingWithdrawn`](#(nplex=0x0)_events_FundingWithdrawn)
-  [Struct `RevenueClaimedOwner`](#(nplex=0x0)_events_RevenueClaimedOwner)
-  [Struct `RevenueClaimedInvestor`](#(nplex=0x0)_events_RevenueClaimedInvestor)
-  [Struct `OwnershipTransferred`](#(nplex=0x0)_events_OwnershipTransferred)
-  [Struct `SalesToggled`](#(nplex=0x0)_events_SalesToggled)
-  [Struct `VaultCreated`](#(nplex=0x0)_events_VaultCreated)
-  [Struct `FractionRedeemed`](#(nplex=0x0)_events_FractionRedeemed)
-  [Struct `FractionMergedBack`](#(nplex=0x0)_events_FractionMergedBack)
-  [Struct `VaultEmpty`](#(nplex=0x0)_events_VaultEmpty)
-  [Struct `VaultDestroyed`](#(nplex=0x0)_events_VaultDestroyed)
-  [Function `emit_notarization_registered`](#(nplex=0x0)_events_emit_notarization_registered)
-  [Function `emit_notarization_revoked`](#(nplex=0x0)_events_emit_notarization_revoked)
-  [Function `emit_notarization_unrevoked`](#(nplex=0x0)_events_emit_notarization_unrevoked)
-  [Function `emit_authorized_creator_updated`](#(nplex=0x0)_events_emit_authorized_creator_updated)
-  [Function `emit_executor_added`](#(nplex=0x0)_events_emit_executor_added)
-  [Function `emit_executor_removed`](#(nplex=0x0)_events_emit_executor_removed)
-  [Function `emit_transfer_authorized`](#(nplex=0x0)_events_emit_transfer_authorized)
-  [Function `emit_transfer_consumed`](#(nplex=0x0)_events_emit_transfer_consumed)
-  [Function `emit_transfer_revoked`](#(nplex=0x0)_events_emit_transfer_revoked)
-  [Function `emit_sales_toggle_authorized`](#(nplex=0x0)_events_emit_sales_toggle_authorized)
-  [Function `emit_sales_toggle_consumed`](#(nplex=0x0)_events_emit_sales_toggle_consumed)
-  [Function `emit_sales_toggle_revoked`](#(nplex=0x0)_events_emit_sales_toggle_revoked)
-  [Function `emit_transfer_token`](#(nplex=0x0)_events_emit_transfer_token)
-  [Function `emit_contract_created`](#(nplex=0x0)_events_emit_contract_created)
-  [Function `emit_token_purchased`](#(nplex=0x0)_events_emit_token_purchased)
-  [Function `emit_revenue_deposited`](#(nplex=0x0)_events_emit_revenue_deposited)
-  [Function `emit_funding_withdrawn`](#(nplex=0x0)_events_emit_funding_withdrawn)
-  [Function `emit_revenue_claimed_owner`](#(nplex=0x0)_events_emit_revenue_claimed_owner)
-  [Function `emit_revenue_claimed_investor`](#(nplex=0x0)_events_emit_revenue_claimed_investor)
-  [Function `emit_ownership_transferred`](#(nplex=0x0)_events_emit_ownership_transferred)
-  [Function `emit_identity_approved`](#(nplex=0x0)_events_emit_identity_approved)
-  [Function `emit_identity_role_updated`](#(nplex=0x0)_events_emit_identity_role_updated)
-  [Function `emit_identity_revoked`](#(nplex=0x0)_events_emit_identity_revoked)
-  [Function `emit_sales_toggled`](#(nplex=0x0)_events_emit_sales_toggled)
-  [Function `emit_vault_created`](#(nplex=0x0)_events_emit_vault_created)
-  [Function `emit_fraction_redeemed`](#(nplex=0x0)_events_emit_fraction_redeemed)
-  [Function `emit_fraction_merged_back`](#(nplex=0x0)_events_emit_fraction_merged_back)
-  [Function `emit_vault_empty`](#(nplex=0x0)_events_emit_vault_empty)
-  [Function `emit_vault_destroyed`](#(nplex=0x0)_events_emit_vault_destroyed)


<pre><code><b>use</b> <a href="../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="(nplex=0x0)_events_NotarizationRegistered"></a>

## Struct `NotarizationRegistered`

Emitted when a notarization is registered in the registry


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_NotarizationRegistered">NotarizationRegistered</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>document_hash: u256</code>
</dt>
<dd>
</dd>
<dt>
<code>authorized_creator: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>auditor: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>timestamp: u64</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_NotarizationRevoked"></a>

## Struct `NotarizationRevoked`

Emitted when a notarization is revoked


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_NotarizationRevoked">NotarizationRevoked</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_NotarizationUnrevoked"></a>

## Struct `NotarizationUnrevoked`

Emitted when a notarization revocation is undone


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_NotarizationUnrevoked">NotarizationUnrevoked</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_AuthorizedCreatorUpdated"></a>

## Struct `AuthorizedCreatorUpdated`

Emitted when the authorized creator for a notarization is updated


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_AuthorizedCreatorUpdated">AuthorizedCreatorUpdated</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>new_creator: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_ExecutorAdded"></a>

## Struct `ExecutorAdded`

Emitted when an executor module is added


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_ExecutorAdded">ExecutorAdded</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>executor_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_ExecutorRemoved"></a>

## Struct `ExecutorRemoved`

Emitted when an executor module is removed


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_ExecutorRemoved">ExecutorRemoved</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>executor_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_TransferAuthorized"></a>

## Struct `TransferAuthorized`

Emitted when a bond transfer is authorized by NPLEX


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_TransferAuthorized">TransferAuthorized</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>new_owner: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_TransferConsumed"></a>

## Struct `TransferConsumed`

Emitted when a transfer ticket is consumed


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_TransferConsumed">TransferConsumed</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>bond_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>new_owner: <b>address</b></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_TransferRevoked"></a>

## Struct `TransferRevoked`

Emitted when a previously authorized transfer is revoked/overwritten


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_TransferRevoked">TransferRevoked</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_SalesToggleAuthorized"></a>

## Struct `SalesToggleAuthorized`

Emitted when a sales toggle is authorized by NPLEX


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_SalesToggleAuthorized">SalesToggleAuthorized</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>target_state: bool</code>
</dt>
<dd>
</dd>
<dt>
<code>notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_SalesToggleConsumed"></a>

## Struct `SalesToggleConsumed`

Emitted when a sales toggle ticket is consumed


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_SalesToggleConsumed">SalesToggleConsumed</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>new_state: bool</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_SalesToggleRevoked"></a>

## Struct `SalesToggleRevoked`

Emitted when a previously authorized sales toggle is revoked/overwritten


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_SalesToggleRevoked">SalesToggleRevoked</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_IdentityApproved"></a>

## Struct `IdentityApproved`

Emitted when an Identity is approved/whitelisted for the first time


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_IdentityApproved">IdentityApproved</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>role: u8</code>
</dt>
<dd>
</dd>
<dt>
<code>backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_IdentityRoleUpdated"></a>

## Struct `IdentityRoleUpdated`

Emitted when an already-approved Identity's role is updated


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_IdentityRoleUpdated">IdentityRoleUpdated</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>old_role: u8</code>
</dt>
<dd>
</dd>
<dt>
<code>new_role: u8</code>
</dt>
<dd>
</dd>
<dt>
<code>backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_TokenTransferred"></a>

## Struct `TokenTransferred`

Emitted when a LTC1Token is transferred


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_TokenTransferred">TokenTransferred</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>token_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>new_owner: <b>address</b></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_ContractCreated"></a>

## Struct `ContractCreated`

Emitted when a new LTC1 Contract/Package is created


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_ContractCreated">ContractCreated</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>creator: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>nominal_value: u64</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_IdentityRevoked"></a>

## Struct `IdentityRevoked`

Emitted when an Identity is revoked from the whitelist


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_IdentityRevoked">IdentityRevoked</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_TokenPurchased"></a>

## Struct `TokenPurchased`

Emitted when an investor buys LTC1 tokens


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_TokenPurchased">TokenPurchased</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>investor: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>amount: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>cost: u64</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_RevenueDeposited"></a>

## Struct `RevenueDeposited`

Emitted when the owner deposits revenue into the pool


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_RevenueDeposited">RevenueDeposited</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>amount: u64</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_FundingWithdrawn"></a>

## Struct `FundingWithdrawn`

Emitted when the owner withdraws funding from the pool


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_FundingWithdrawn">FundingWithdrawn</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>amount: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>recipient: <b>address</b></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_RevenueClaimedOwner"></a>

## Struct `RevenueClaimedOwner`

Emitted when the owner claims their revenue share


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_RevenueClaimedOwner">RevenueClaimedOwner</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>amount: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>owner: <b>address</b></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_RevenueClaimedInvestor"></a>

## Struct `RevenueClaimedInvestor`

Emitted when an investor claims their revenue share


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_RevenueClaimedInvestor">RevenueClaimedInvestor</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>token_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>amount: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>investor: <b>address</b></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_OwnershipTransferred"></a>

## Struct `OwnershipTransferred`

Emitted when package ownership is transferred to a new DID


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_OwnershipTransferred">OwnershipTransferred</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>new_owner_identity: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_SalesToggled"></a>

## Struct `SalesToggled`

Emitted when sales state is toggled


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_SalesToggled">SalesToggled</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>new_state: bool</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_VaultCreated"></a>

## Struct `VaultCreated`

Event emitted when a new FractionalVault is created


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_VaultCreated">VaultCreated</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>fraction_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
<dt>
<code>amount: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>minter: <b>address</b></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_FractionRedeemed"></a>

## Struct `FractionRedeemed`

Event emitted when fractions are redeemed for a new LTC1Token


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_FractionRedeemed">FractionRedeemed</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>amount: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>redeemer: <b>address</b></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_FractionMergedBack"></a>

## Struct `FractionMergedBack`

Event emitted when fractions are merged back into an existing LTC1Token


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_FractionMergedBack">FractionMergedBack</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>token_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>amount: u64</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_VaultEmpty"></a>

## Struct `VaultEmpty`

Event emitted when a vault becomes empty (ready for manual destruction)


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_VaultEmpty">VaultEmpty</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>fraction_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_VaultDestroyed"></a>

## Struct `VaultDestroyed`

Event emitted when an empty vault is destroyed


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/events.md#(nplex=0x0)_events_VaultDestroyed">VaultDestroyed</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_events_emit_notarization_registered"></a>

## Function `emit_notarization_registered`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_notarization_registered">emit_notarization_registered</a>(notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, document_hash: u256, authorized_creator: <b>address</b>, auditor: <b>address</b>, timestamp: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_notarization_registered">emit_notarization_registered</a>(
    notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    document_hash: u256,
    authorized_creator: <b>address</b>,
    auditor: <b>address</b>,
    timestamp: u64,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_NotarizationRegistered">NotarizationRegistered</a> {
        notarization_id,
        document_hash,
        authorized_creator,
        auditor,
        timestamp,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_notarization_revoked"></a>

## Function `emit_notarization_revoked`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_notarization_revoked">emit_notarization_revoked</a>(notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_notarization_revoked">emit_notarization_revoked</a>(
    notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_NotarizationRevoked">NotarizationRevoked</a> { notarization_id, backing_notarization_id });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_notarization_unrevoked"></a>

## Function `emit_notarization_unrevoked`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_notarization_unrevoked">emit_notarization_unrevoked</a>(notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_notarization_unrevoked">emit_notarization_unrevoked</a>(
    notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_NotarizationUnrevoked">NotarizationUnrevoked</a> { notarization_id, backing_notarization_id });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_authorized_creator_updated"></a>

## Function `emit_authorized_creator_updated`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_authorized_creator_updated">emit_authorized_creator_updated</a>(notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, new_creator: <b>address</b>, backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_authorized_creator_updated">emit_authorized_creator_updated</a>(
    notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    new_creator: <b>address</b>,
    backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_AuthorizedCreatorUpdated">AuthorizedCreatorUpdated</a> {
        notarization_id,
        new_creator,
        backing_notarization_id,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_executor_added"></a>

## Function `emit_executor_added`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_executor_added">emit_executor_added</a>(executor_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_executor_added">emit_executor_added</a>(
    executor_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_ExecutorAdded">ExecutorAdded</a> { executor_type });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_executor_removed"></a>

## Function `emit_executor_removed`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_executor_removed">emit_executor_removed</a>(executor_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_executor_removed">emit_executor_removed</a>(
    executor_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_ExecutorRemoved">ExecutorRemoved</a> { executor_type });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_transfer_authorized"></a>

## Function `emit_transfer_authorized`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_authorized">emit_transfer_authorized</a>(contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, new_owner: <b>address</b>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_authorized">emit_transfer_authorized</a>(
    contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    new_owner: <b>address</b>,
    notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_TransferAuthorized">TransferAuthorized</a> {
        contract_id,
        new_owner,
        notarization_id,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_transfer_consumed"></a>

## Function `emit_transfer_consumed`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_consumed">emit_transfer_consumed</a>(bond_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, new_owner: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_consumed">emit_transfer_consumed</a>(
    bond_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    new_owner: <b>address</b>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_TransferConsumed">TransferConsumed</a> { bond_id, new_owner });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_transfer_revoked"></a>

## Function `emit_transfer_revoked`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_revoked">emit_transfer_revoked</a>(contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_revoked">emit_transfer_revoked</a>(
    contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_TransferRevoked">TransferRevoked</a> { contract_id, notarization_id });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_sales_toggle_authorized"></a>

## Function `emit_sales_toggle_authorized`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggle_authorized">emit_sales_toggle_authorized</a>(contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, target_state: bool, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggle_authorized">emit_sales_toggle_authorized</a>(
    contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    target_state: bool,
    notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_SalesToggleAuthorized">SalesToggleAuthorized</a> {
        contract_id,
        target_state,
        notarization_id,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_sales_toggle_consumed"></a>

## Function `emit_sales_toggle_consumed`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggle_consumed">emit_sales_toggle_consumed</a>(contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, new_state: bool)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggle_consumed">emit_sales_toggle_consumed</a>(
    contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    new_state: bool,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_SalesToggleConsumed">SalesToggleConsumed</a> { contract_id, new_state });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_sales_toggle_revoked"></a>

## Function `emit_sales_toggle_revoked`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggle_revoked">emit_sales_toggle_revoked</a>(contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggle_revoked">emit_sales_toggle_revoked</a>(
    contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_SalesToggleRevoked">SalesToggleRevoked</a> { contract_id, notarization_id });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_transfer_token"></a>

## Function `emit_transfer_token`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_token">emit_transfer_token</a>(token_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, new_owner: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_token">emit_transfer_token</a>(
    token_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    new_owner: <b>address</b>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_TokenTransferred">TokenTransferred</a> {
        token_id,
        new_owner,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_contract_created"></a>

## Function `emit_contract_created`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_contract_created">emit_contract_created</a>(package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, creator: <b>address</b>, nominal_value: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_contract_created">emit_contract_created</a>(
    package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    creator: <b>address</b>,
    nominal_value: u64
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_ContractCreated">ContractCreated</a> {
        package_id,
        creator,
        nominal_value
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_token_purchased"></a>

## Function `emit_token_purchased`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_token_purchased">emit_token_purchased</a>(package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, investor: <b>address</b>, amount: u64, cost: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_token_purchased">emit_token_purchased</a>(
    package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    investor: <b>address</b>,
    amount: u64,
    cost: u64
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_TokenPurchased">TokenPurchased</a> {
        package_id,
        investor,
        amount,
        cost
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_revenue_deposited"></a>

## Function `emit_revenue_deposited`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_revenue_deposited">emit_revenue_deposited</a>(package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, amount: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_revenue_deposited">emit_revenue_deposited</a>(
    package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    amount: u64
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_RevenueDeposited">RevenueDeposited</a> {
        package_id,
        amount
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_funding_withdrawn"></a>

## Function `emit_funding_withdrawn`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_funding_withdrawn">emit_funding_withdrawn</a>(package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, amount: u64, recipient: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_funding_withdrawn">emit_funding_withdrawn</a>(
    package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    amount: u64,
    recipient: <b>address</b>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_FundingWithdrawn">FundingWithdrawn</a> {
        package_id,
        amount,
        recipient,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_revenue_claimed_owner"></a>

## Function `emit_revenue_claimed_owner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_revenue_claimed_owner">emit_revenue_claimed_owner</a>(package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, amount: u64, owner: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_revenue_claimed_owner">emit_revenue_claimed_owner</a>(
    package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    amount: u64,
    owner: <b>address</b>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_RevenueClaimedOwner">RevenueClaimedOwner</a> {
        package_id,
        amount,
        owner,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_revenue_claimed_investor"></a>

## Function `emit_revenue_claimed_investor`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_revenue_claimed_investor">emit_revenue_claimed_investor</a>(package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, token_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, amount: u64, investor: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_revenue_claimed_investor">emit_revenue_claimed_investor</a>(
    package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    token_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    amount: u64,
    investor: <b>address</b>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_RevenueClaimedInvestor">RevenueClaimedInvestor</a> {
        package_id,
        token_id,
        amount,
        investor,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_ownership_transferred"></a>

## Function `emit_ownership_transferred`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_ownership_transferred">emit_ownership_transferred</a>(package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, new_owner_identity: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_ownership_transferred">emit_ownership_transferred</a>(
    package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    new_owner_identity: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_OwnershipTransferred">OwnershipTransferred</a> {
        package_id,
        new_owner_identity,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_identity_approved"></a>

## Function `emit_identity_approved`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_identity_approved">emit_identity_approved</a>(identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, role: u8, backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_identity_approved">emit_identity_approved</a>(
    identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    role: u8,
    backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_IdentityApproved">IdentityApproved</a> {
        identity_id,
        role,
        backing_notarization_id,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_identity_role_updated"></a>

## Function `emit_identity_role_updated`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_identity_role_updated">emit_identity_role_updated</a>(identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, old_role: u8, new_role: u8, backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_identity_role_updated">emit_identity_role_updated</a>(
    identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    old_role: u8,
    new_role: u8,
    backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_IdentityRoleUpdated">IdentityRoleUpdated</a> {
        identity_id,
        old_role,
        new_role,
        backing_notarization_id,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_identity_revoked"></a>

## Function `emit_identity_revoked`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_identity_revoked">emit_identity_revoked</a>(identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_identity_revoked">emit_identity_revoked</a>(
    identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    backing_notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_IdentityRevoked">IdentityRevoked</a> {
        identity_id,
        backing_notarization_id,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_sales_toggled"></a>

## Function `emit_sales_toggled`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggled">emit_sales_toggled</a>(package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, new_state: bool)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggled">emit_sales_toggled</a>(
    package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    new_state: bool,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_SalesToggled">SalesToggled</a> {
        package_id,
        new_state,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_vault_created"></a>

## Function `emit_vault_created`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_vault_created">emit_vault_created</a>(vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, fraction_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>, amount: u64, minter: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_vault_created">emit_vault_created</a>(
    vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    fraction_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>,
    amount: u64,
    minter: <b>address</b>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_VaultCreated">VaultCreated</a> {
        vault_id,
        package_id,
        fraction_type,
        amount,
        minter
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_fraction_redeemed"></a>

## Function `emit_fraction_redeemed`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_fraction_redeemed">emit_fraction_redeemed</a>(vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, amount: u64, redeemer: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_fraction_redeemed">emit_fraction_redeemed</a>(
    vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    amount: u64,
    redeemer: <b>address</b>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_FractionRedeemed">FractionRedeemed</a> {
        vault_id,
        amount,
        redeemer,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_fraction_merged_back"></a>

## Function `emit_fraction_merged_back`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_fraction_merged_back">emit_fraction_merged_back</a>(vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, token_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, amount: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_fraction_merged_back">emit_fraction_merged_back</a>(
    vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    token_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    amount: u64,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_FractionMergedBack">FractionMergedBack</a> {
        vault_id,
        token_id,
        amount,
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_vault_empty"></a>

## Function `emit_vault_empty`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_vault_empty">emit_vault_empty</a>(vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, fraction_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_vault_empty">emit_vault_empty</a>(
    vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
    fraction_type: <a href="../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_VaultEmpty">VaultEmpty</a> {
        vault_id,
        fraction_type
    });
}
</code></pre>



</details>

<a name="(nplex=0x0)_events_emit_vault_destroyed"></a>

## Function `emit_vault_destroyed`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_vault_destroyed">emit_vault_destroyed</a>(vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/events.md#(nplex=0x0)_events_emit_vault_destroyed">emit_vault_destroyed</a>(
    vault_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>,
) {
    <a href="../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../nplex/events.md#(nplex=0x0)_events_VaultDestroyed">VaultDestroyed</a> { vault_id });
}
</code></pre>



</details>
