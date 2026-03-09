---
layout: default
title: registry
parent: Nplex Smart Contracts
---


<a name="(nplex=0x0)_registry"></a>

# Module `(nplex=0x0)::registry`

NPLEX Registry - Manages approval and validation of NPL package hashes

This contract provides the validation layer for the NPLEX platform.
Only NPLEX admin can register and revoke package hashes.
LTC1 contracts must validate against this registry before creation.


-  [Struct `REGISTRY`](#(nplex=0x0)_registry_REGISTRY)
-  [Struct `NotarizationClaim`](#(nplex=0x0)_registry_NotarizationClaim)
-  [Struct `NPLEXAdminCap`](#(nplex=0x0)_registry_NPLEXAdminCap)
-  [Struct `ExecutorKey`](#(nplex=0x0)_registry_ExecutorKey)
-  [Struct `NPLEXRegistry`](#(nplex=0x0)_registry_NPLEXRegistry)
-  [Struct `NotarizationInfo`](#(nplex=0x0)_registry_NotarizationInfo)
-  [Struct `NotarizedTransfer`](#(nplex=0x0)_registry_NotarizedTransfer)
-  [Struct `NotarizedSaleToggle`](#(nplex=0x0)_registry_NotarizedSaleToggle)
-  [Struct `ApprovedIdentity`](#(nplex=0x0)_registry_ApprovedIdentity)
-  [Constants](#@Constants_0)
-  [Function `init`](#(nplex=0x0)_registry_init)
-  [Function `register_notarization`](#(nplex=0x0)_registry_register_notarization)
    -  [Arguments](#@Arguments_1)
    -  [Aborts](#@Aborts_2)
-  [Function `update_authorized_creator`](#(nplex=0x0)_registry_update_authorized_creator)
-  [Function `revoke_notarization`](#(nplex=0x0)_registry_revoke_notarization)
-  [Function `unrevoke_notarization`](#(nplex=0x0)_registry_unrevoke_notarization)
-  [Function `add_executor`](#(nplex=0x0)_registry_add_executor)
-  [Function `remove_executor`](#(nplex=0x0)_registry_remove_executor)
-  [Function `bind_executor`](#(nplex=0x0)_registry_bind_executor)
-  [Function `authorize_transfer`](#(nplex=0x0)_registry_authorize_transfer)
-  [Function `authorize_sales_toggle`](#(nplex=0x0)_registry_authorize_sales_toggle)
-  [Function `approve_identity`](#(nplex=0x0)_registry_approve_identity)
-  [Function `revoke_identity`](#(nplex=0x0)_registry_revoke_identity)
-  [Function `claim_notarization`](#(nplex=0x0)_registry_claim_notarization)
    -  [Arguments](#@Arguments_3)
    -  [Returns](#@Returns_4)
    -  [Aborts](#@Aborts_5)
-  [Function `consume_transfer_ticket`](#(nplex=0x0)_registry_consume_transfer_ticket)
-  [Function `consume_sales_toggle_ticket`](#(nplex=0x0)_registry_consume_sales_toggle_ticket)
-  [Function `verify_identity`](#(nplex=0x0)_registry_verify_identity)
-  [Function `get_identity_role`](#(nplex=0x0)_registry_get_identity_role)
-  [Function `role_institution`](#(nplex=0x0)_registry_role_institution)
-  [Function `role_investor`](#(nplex=0x0)_registry_role_investor)
-  [Function `role_admin`](#(nplex=0x0)_registry_role_admin)
-  [Function `is_valid_notarization`](#(nplex=0x0)_registry_is_valid_notarization)
-  [Function `is_notarization_used`](#(nplex=0x0)_registry_is_notarization_used)
-  [Function `is_notarization_revoked`](#(nplex=0x0)_registry_is_notarization_revoked)
-  [Function `get_notarization_info`](#(nplex=0x0)_registry_get_notarization_info)
-  [Function `notarization_document_hash`](#(nplex=0x0)_registry_notarization_document_hash)
-  [Function `notarization_contract_id`](#(nplex=0x0)_registry_notarization_contract_id)
-  [Function `notarization_is_revoked`](#(nplex=0x0)_registry_notarization_is_revoked)
-  [Function `notarization_auditor`](#(nplex=0x0)_registry_notarization_auditor)
-  [Function `notarization_approved_timestamp`](#(nplex=0x0)_registry_notarization_approved_timestamp)
-  [Function `notarization_authorized_creator`](#(nplex=0x0)_registry_notarization_authorized_creator)


<pre><code><b>use</b> (iota_identity=0x0)::controller;
<b>use</b> (iota_identity=0x0)::permissions;
<b>use</b> (iota_notarization=0x0)::method;
<b>use</b> (iota_notarization=0x0)::notarization;
<b>use</b> (iota_notarization=0x0)::timelock;
<b>use</b> (nplex=0x0)::<a href="../nplex/events.md#(nplex=0x0)_events">events</a>;
<b>use</b> <a href="../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../dependencies/iota/borrow.md#iota_borrow">iota::borrow</a>;
<b>use</b> <a href="../dependencies/iota/clock.md#iota_clock">iota::clock</a>;
<b>use</b> <a href="../dependencies/iota/display.md#iota_display">iota::display</a>;
<b>use</b> <a href="../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../dependencies/iota/package.md#iota_package">iota::package</a>;
<b>use</b> <a href="../dependencies/iota/table.md#iota_table">iota::table</a>;
<b>use</b> <a href="../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="(nplex=0x0)_registry_REGISTRY"></a>

## Struct `REGISTRY`

One-Time Witness for the module. Has <code>drop</code> ability.


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_REGISTRY">REGISTRY</a> <b>has</b> drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="(nplex=0x0)_registry_NotarizationClaim"></a>

## Struct `NotarizationClaim`

Hot potato struct to ensure hash usage flow


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationClaim">NotarizationClaim</a>
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
</dl>


</details>

<a name="(nplex=0x0)_registry_NPLEXAdminCap"></a>

## Struct `NPLEXAdminCap`

Admin capability - only NPLEX holds this
This is a "hot potato" pattern - whoever owns this can admin the registry


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a> <b>has</b> key, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(nplex=0x0)_registry_ExecutorKey"></a>

## Struct `ExecutorKey`

Key for Authorized Executors (Dynamic Field)


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_ExecutorKey">ExecutorKey</a>&lt;<b>phantom</b> T&gt; <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="(nplex=0x0)_registry_NPLEXRegistry"></a>

## Struct `NPLEXRegistry`

Central registry of approved NPL package notarizations
Shared object - anyone can read, only admin can mutate


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a> <b>has</b> key
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>approved_notarizations: <a href="../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">registry::NotarizationInfo</a>&gt;</code>
</dt>
<dd>
 Maps Notarization ID -> package information
</dd>
<dt>
<code>authorized_transfers: <a href="../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizedTransfer">registry::NotarizedTransfer</a>&gt;</code>
</dt>
<dd>
 Maps Bond ID -> Notarized transfer authorization
</dd>
<dt>
<code>authorized_sales_toggles: <a href="../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizedSaleToggle">registry::NotarizedSaleToggle</a>&gt;</code>
</dt>
<dd>
 Maps LTC1Package ID -> Notarized sales toggle authorization
</dd>
<dt>
<code>approved_identities: <a href="../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_ApprovedIdentity">registry::ApprovedIdentity</a>&gt;</code>
</dt>
<dd>
 Maps Identity object ID -> ApprovedIdentity (DID whitelist)
</dd>
</dl>


</details>

<a name="(nplex=0x0)_registry_NotarizationInfo"></a>

## Struct `NotarizationInfo`

Information about an approved notarization (has store, copy, drop properties)


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">NotarizationInfo</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>document_hash: u256</code>
</dt>
<dd>
 The document hash associated with this notarization (u256)
</dd>
<dt>
<code>approved_timestamp: u64</code>
</dt>
<dd>
 When this hash was approved (u64)
</dd>
<dt>
<code>auditor: <b>address</b></code>
</dt>
<dd>
 Address that approved this hash (NPLEX auditor)
</dd>
<dt>
<code>is_revoked: bool</code>
</dt>
<dd>
 Whether this hash has been revoked (bool)
</dd>
<dt>
<code>contract_id: <a href="../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;</code>
</dt>
<dd>
 ID of LTC1 contract created with this notarization (None if not yet used)
</dd>
<dt>
<code>authorized_creator: <b>address</b></code>
</dt>
<dd>
 Only this address is authorized to create a contract with this notarization
 This is potentially useless if the notarization we use is not transferable
 Ideally the user creates it and it cannot be transfered, I am leaving this like this for now
</dd>
</dl>


</details>

<a name="(nplex=0x0)_registry_NotarizedTransfer"></a>

## Struct `NotarizedTransfer`

Notarized transfer authorization — ties a bond transfer to a specific notarization (has store, copy, drop properties)


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizedTransfer">NotarizedTransfer</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 The notarization backing this transfer authorization: ID
</dd>
<dt>
<code>new_owner: <b>address</b></code>
</dt>
<dd>
 The authorized recipient of the bond: address
</dd>
<dt>
<code>new_owner_identity: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 The DID Identity of the new owner explicitly approved by NPLEX Admin: ID
</dd>
</dl>


</details>

<a name="(nplex=0x0)_registry_NotarizedSaleToggle"></a>

## Struct `NotarizedSaleToggle`

Notarized sales toggle authorization — ties a sales state change to a specific notarization (has store, copy, drop properties)


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizedSaleToggle">NotarizedSaleToggle</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 The notarization backing this sales toggle authorization: ID
</dd>
<dt>
<code>target_state: bool</code>
</dt>
<dd>
 The target sales state (true = open, false = closed): bool
</dd>
</dl>


</details>

<a name="(nplex=0x0)_registry_ApprovedIdentity"></a>

## Struct `ApprovedIdentity`

Information about an approved DID identity
The link between a user's address and their DID Identity is proven
at runtime via DelegationToken, never stored statically.
The vc_data field holds the raw bytes of the W3C Verifiable Credential
(typically JWT) that justified this approval — an immutable audit trail.


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_ApprovedIdentity">ApprovedIdentity</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>role: u8</code>
</dt>
<dd>
 Bitmask role: 1 = Institution, 2 = Investor, 4 = Admin (combinable)
</dd>
<dt>
<code>vc_data: vector&lt;u8&gt;</code>
</dt>
<dd>
 Pseudonymize has to happen by saving Identity information offchain
 reason being that people have the right to be deleted and forgotten
 which cannot happen on an immutable blockchain.
 in this data we should write something like
 {
  "Did_ID": "0x1234...abcd",
  "Issuer": "NPLEX",
  "Role": "Institution",
  "ApprovedAt": 1708900000
 }
 Moreover when we have a NPLEX DID we should setup a RevocationBitmap2022
 and use this in conjunction with the IOTA SDK to create credentials.
 This is optional put 0x0 if not used and use it only in the future if needed.
 (non-empty, VC audit trail)
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(nplex=0x0)_registry_E_NOTARIZATION_NOT_APPROVED"></a>

Notarization is not registered in the registry or has been revoked


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_NOT_APPROVED">E_NOTARIZATION_NOT_APPROVED</a>: u64 = 1;
</code></pre>



<a name="(nplex=0x0)_registry_E_NOTARIZATION_ALREADY_USED"></a>

Notarization has already been used to create an LTC1 contract


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_ALREADY_USED">E_NOTARIZATION_ALREADY_USED</a>: u64 = 2;
</code></pre>



<a name="(nplex=0x0)_registry_E_NOTARIZATION_REVOKED"></a>

Notarization has been revoked by NPLEX


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_REVOKED">E_NOTARIZATION_REVOKED</a>: u64 = 3;
</code></pre>



<a name="(nplex=0x0)_registry_E_UNAUTHORIZED_EXECUTOR"></a>

Executor module is not authorized to bind hashes


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_UNAUTHORIZED_EXECUTOR">E_UNAUTHORIZED_EXECUTOR</a>: u64 = 4;
</code></pre>



<a name="(nplex=0x0)_registry_E_TRANSFER_NOT_AUTHORIZED"></a>

Bond transfer not authorized by NPLEX


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_TRANSFER_NOT_AUTHORIZED">E_TRANSFER_NOT_AUTHORIZED</a>: u64 = 5;
</code></pre>



<a name="(nplex=0x0)_registry_E_UNAUTHORIZED_CREATOR"></a>

Creator is not authorized for this hash


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_UNAUTHORIZED_CREATOR">E_UNAUTHORIZED_CREATOR</a>: u64 = 6;
</code></pre>



<a name="(nplex=0x0)_registry_E_SALES_TOGGLE_NOT_AUTHORIZED"></a>

Sales toggle not authorized by NPLEX


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_SALES_TOGGLE_NOT_AUTHORIZED">E_SALES_TOGGLE_NOT_AUTHORIZED</a>: u64 = 7;
</code></pre>



<a name="(nplex=0x0)_registry_E_NOTARIZATION_NOT_REVOKED"></a>

Notarization not revoked


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_NOT_REVOKED">E_NOTARIZATION_NOT_REVOKED</a>: u64 = 8;
</code></pre>



<a name="(nplex=0x0)_registry_E_NOTARIZATION_ALREADY_REVOKED"></a>

Notarization already revoked


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_ALREADY_REVOKED">E_NOTARIZATION_ALREADY_REVOKED</a>: u64 = 9;
</code></pre>



<a name="(nplex=0x0)_registry_E_IDENTITY_NOT_APPROVED"></a>

Identity not approved in whitelist


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_IDENTITY_NOT_APPROVED">E_IDENTITY_NOT_APPROVED</a>: u64 = 10;
</code></pre>



<a name="(nplex=0x0)_registry_E_IDENTITY_WRONG_ROLE"></a>

Identity does not have required role


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_IDENTITY_WRONG_ROLE">E_IDENTITY_WRONG_ROLE</a>: u64 = 11;
</code></pre>



<a name="(nplex=0x0)_registry_E_INVALID_ROLE"></a>

Invalid role value


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_INVALID_ROLE">E_INVALID_ROLE</a>: u64 = 12;
</code></pre>



<a name="(nplex=0x0)_registry_E_AUTHORIZED_CREATOR_ALREADY_SET"></a>

Authorized creator already set to this value


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_E_AUTHORIZED_CREATOR_ALREADY_SET">E_AUTHORIZED_CREATOR_ALREADY_SET</a>: u64 = 13;
</code></pre>



<a name="(nplex=0x0)_registry_ROLE_INSTITUTION"></a>

Institution role (originators, servicers)


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_ROLE_INSTITUTION">ROLE_INSTITUTION</a>: u8 = 1;
</code></pre>



<a name="(nplex=0x0)_registry_ROLE_INVESTOR"></a>

Investor role


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_ROLE_INVESTOR">ROLE_INVESTOR</a>: u8 = 2;
</code></pre>



<a name="(nplex=0x0)_registry_ROLE_ADMIN"></a>

Admin role (NPLEX platform admin)


<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_ROLE_ADMIN">ROLE_ADMIN</a>: u8 = 4;
</code></pre>



<a name="(nplex=0x0)_registry_DISPLAY_KEY_NAME"></a>



<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_DISPLAY_KEY_NAME">DISPLAY_KEY_NAME</a>: vector&lt;u8&gt; = vector[110, 97, 109, 101];
</code></pre>



<a name="(nplex=0x0)_registry_DISPLAY_KEY_DESCRIPTION"></a>



<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_DISPLAY_KEY_DESCRIPTION">DISPLAY_KEY_DESCRIPTION</a>: vector&lt;u8&gt; = vector[100, 101, 115, 99, 114, 105, 112, 116, 105, 111, 110];
</code></pre>



<a name="(nplex=0x0)_registry_DISPLAY_KEY_IMAGE_URL"></a>



<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_DISPLAY_KEY_IMAGE_URL">DISPLAY_KEY_IMAGE_URL</a>: vector&lt;u8&gt; = vector[105, 109, 97, 103, 101, 95, 117, 114, 108];
</code></pre>



<a name="(nplex=0x0)_registry_DISPLAY_KEY_PROJECT_URL"></a>



<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_DISPLAY_KEY_PROJECT_URL">DISPLAY_KEY_PROJECT_URL</a>: vector&lt;u8&gt; = vector[112, 114, 111, 106, 101, 99, 116, 95, 117, 114, 108];
</code></pre>



<a name="(nplex=0x0)_registry_ADMIN_DISPLAY_NAME"></a>



<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_ADMIN_DISPLAY_NAME">ADMIN_DISPLAY_NAME</a>: vector&lt;u8&gt; = vector[78, 80, 76, 69, 88, 32, 65, 100, 109, 105, 110, 105, 115, 116, 114, 97, 116, 111, 114, 32, 67, 97, 112, 97, 98, 105, 108, 105, 116, 121];
</code></pre>



<a name="(nplex=0x0)_registry_ADMIN_DISPLAY_DESCRIPTION"></a>



<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_ADMIN_DISPLAY_DESCRIPTION">ADMIN_DISPLAY_DESCRIPTION</a>: vector&lt;u8&gt; = vector[71, 114, 97, 110, 116, 115, 32, 97, 100, 109, 105, 110, 105, 115, 116, 114, 97, 116, 105, 118, 101, 32, 99, 111, 110, 116, 114, 111, 108, 32, 111, 118, 101, 114, 32, 116, 104, 101, 32, 78, 80, 76, 69, 88, 32, 82, 101, 103, 105, 115, 116, 114, 121, 46];
</code></pre>



<a name="(nplex=0x0)_registry_ADMIN_DISPLAY_IMAGE_URL"></a>



<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_ADMIN_DISPLAY_IMAGE_URL">ADMIN_DISPLAY_IMAGE_URL</a>: vector&lt;u8&gt; = vector[104, 116, 116, 112, 115, 58, 47, 47, 97, 112, 105, 46, 110, 112, 108, 101, 120, 46, 101, 117, 47, 105, 99, 111, 110, 115, 47, 97, 100, 109, 105, 110, 95, 99, 114, 111, 119, 110, 46, 112, 110, 103];
</code></pre>



<a name="(nplex=0x0)_registry_ADMIN_DISPLAY_PROJECT_URL"></a>



<pre><code><b>const</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_ADMIN_DISPLAY_PROJECT_URL">ADMIN_DISPLAY_PROJECT_URL</a>: vector&lt;u8&gt; = vector[104, 116, 116, 112, 115, 58, 47, 47, 110, 112, 108, 101, 120, 46, 101, 117];
</code></pre>



<a name="(nplex=0x0)_registry_init"></a>

## Function `init`

Module initializer - called once when contract is published
Creates the registry and gives admin capability to publisher


<pre><code><b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_init">init</a>(otw: (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_REGISTRY">registry::REGISTRY</a>, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_init">init</a>(otw: <a href="../nplex/registry.md#(nplex=0x0)_registry_REGISTRY">REGISTRY</a>, ctx: &<b>mut</b> TxContext) {
    // 1. Claim Publisher
    <b>let</b> publisher = package::claim(otw, ctx);
    // Create Display <b>for</b> Admin Cap
    <a href="../nplex/display_utils.md#(nplex=0x0)_display_utils_setup_display">display_utils::setup_display</a>! &lt;<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a>&gt; (
        &publisher,
        vector[
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry_DISPLAY_KEY_NAME">DISPLAY_KEY_NAME</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry_DISPLAY_KEY_DESCRIPTION">DISPLAY_KEY_DESCRIPTION</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry_DISPLAY_KEY_IMAGE_URL">DISPLAY_KEY_IMAGE_URL</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry_DISPLAY_KEY_PROJECT_URL">DISPLAY_KEY_PROJECT_URL</a>),
        ],
        vector[
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry_ADMIN_DISPLAY_NAME">ADMIN_DISPLAY_NAME</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry_ADMIN_DISPLAY_DESCRIPTION">ADMIN_DISPLAY_DESCRIPTION</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry_ADMIN_DISPLAY_IMAGE_URL">ADMIN_DISPLAY_IMAGE_URL</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry_ADMIN_DISPLAY_PROJECT_URL">ADMIN_DISPLAY_PROJECT_URL</a>),
        ],
        ctx
    );
    // 3. Create admin capability and send to deployer
    <b>let</b> admin_cap = <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a> {
        id: object::new(ctx),
    };
    transfer::transfer(admin_cap, tx_context::sender(ctx));
    // 4. Create shared <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>
    <b>let</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a> = <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a> {
        id: object::new(ctx),
        approved_notarizations: table::new(ctx),
        authorized_transfers: table::new(ctx),
        authorized_sales_toggles: table::new(ctx),
        approved_identities: table::new(ctx),
    };
    transfer::share_object(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>);
    // 5. Cleanup
    transfer::public_transfer(publisher, tx_context::sender(ctx));
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_register_notarization"></a>

## Function `register_notarization`

Register a new approved notarization in the registry

These are the documents which are used only for <code>create_contract</code>.
Notarizations for other approvals are managed in other tables, not in <code>approved_notarizations</code>.

**Note:** We pass <code>notarization_id</code> and <code>document_hash</code> instead of the <code>Notarization</code> object
because the locked Notarization object cannot be traded. The user must create it via SDK,
have it audited off-chain, and then pass it to the <code>create_contract</code> function.


<a name="@Arguments_1"></a>

### Arguments

* <code><a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a></code> - The NPLEX Registry shared object.
* <code>_admin_cap</code> - The NPLEX Administrator Capability (authorization).
* <code>notarization_id</code> - The <code>ID</code> of the Notarization object created via SDK.
* <code>document_hash</code> - The <code>u256</code> SHA256/Keccak hash of the off-chain PDF asset document.
* <code>authorized_creator</code> - The address allowed to consume this hash to create an LTC1.
* <code>clock</code> - The system clock for auditing timestamp.
* <code>ctx</code> - Transaction context.


<a name="@Aborts_2"></a>

### Aborts

* <code><a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_ALREADY_USED">E_NOTARIZATION_ALREADY_USED</a></code> - If the <code>notarization_id</code> is already registered.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_register_notarization">register_notarization</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, _admin_cap: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">registry::NPLEXAdminCap</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, document_hash: u256, authorized_creator: <b>address</b>, clock: &<a href="../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_register_notarization">register_notarization</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    _admin_cap: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a>,
    notarization_id: ID,
    document_hash: u256,
    authorized_creator: <b>address</b>,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext
) {
    <b>assert</b>!(!table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_ALREADY_USED">E_NOTARIZATION_ALREADY_USED</a>);
    <b>let</b> notarization_info = <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">NotarizationInfo</a> {
        document_hash,
        approved_timestamp: clock::timestamp_ms(clock),
        auditor: tx_context::sender(ctx),
        is_revoked: <b>false</b>,
        contract_id: option::none(),
        authorized_creator,
    };
    table::add(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id, notarization_info);
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_notarization_registered">events::emit_notarization_registered</a>(
        notarization_id,
        document_hash,
        authorized_creator,
        tx_context::sender(ctx),
        clock::timestamp_ms(clock),
    );
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_update_authorized_creator"></a>

## Function `update_authorized_creator`

Update the authorized creator for a registered notarization


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_update_authorized_creator">update_authorized_creator</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, _admin_cap: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">registry::NPLEXAdminCap</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, new_creator: <b>address</b>, backing_notarization: &(iota_notarization=0x0)::notarization::Notarization&lt;u256&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_update_authorized_creator">update_authorized_creator</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    _admin_cap: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a>,
    notarization_id: ID,
    new_creator: <b>address</b>,
    backing_notarization: &Notarization&lt;u256&gt;,
) {
    <b>let</b> backing_notarization_id = object::id(backing_notarization);
    <b>assert</b>!(table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_NOT_APPROVED">E_NOTARIZATION_NOT_APPROVED</a>);
    <b>let</b> hash_info = table::borrow_mut(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id);
    <b>assert</b>!(option::is_none(&hash_info.contract_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_ALREADY_USED">E_NOTARIZATION_ALREADY_USED</a>);
    <b>assert</b>!(hash_info.authorized_creator != new_creator, <a href="../nplex/registry.md#(nplex=0x0)_registry_E_AUTHORIZED_CREATOR_ALREADY_SET">E_AUTHORIZED_CREATOR_ALREADY_SET</a>);
    hash_info.authorized_creator = new_creator;
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_authorized_creator_updated">events::emit_authorized_creator_updated</a>(notarization_id, new_creator, backing_notarization_id);
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_revoke_notarization"></a>

## Function `revoke_notarization`

Revoke a previously approved notarization


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_revoke_notarization">revoke_notarization</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, _admin_cap: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">registry::NPLEXAdminCap</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, backing_notarization: &(iota_notarization=0x0)::notarization::Notarization&lt;u256&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_revoke_notarization">revoke_notarization</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    _admin_cap: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a>,
    notarization_id: ID,
    backing_notarization: &Notarization&lt;u256&gt;,
) {
    <b>let</b> backing_notarization_id = object::id(backing_notarization);
    <b>assert</b>!(table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_NOT_APPROVED">E_NOTARIZATION_NOT_APPROVED</a>);
    <b>let</b> hash_info = table::borrow_mut(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id);
    <b>assert</b>!(!hash_info.is_revoked, <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_ALREADY_REVOKED">E_NOTARIZATION_ALREADY_REVOKED</a>);
    hash_info.is_revoked = <b>true</b>;
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_notarization_revoked">events::emit_notarization_revoked</a>(notarization_id, backing_notarization_id);
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_unrevoke_notarization"></a>

## Function `unrevoke_notarization`

Un-revoke a notarization


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_unrevoke_notarization">unrevoke_notarization</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, _admin_cap: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">registry::NPLEXAdminCap</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, backing_notarization: &(iota_notarization=0x0)::notarization::Notarization&lt;u256&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_unrevoke_notarization">unrevoke_notarization</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    _admin_cap: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a>,
    notarization_id: ID,
    backing_notarization: &Notarization&lt;u256&gt;,
) {
    <b>let</b> backing_notarization_id = object::id(backing_notarization);
    <b>assert</b>!(table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_NOT_APPROVED">E_NOTARIZATION_NOT_APPROVED</a>);
    <b>let</b> hash_info = table::borrow_mut(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id);
    <b>assert</b>!(hash_info.is_revoked, <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_NOT_REVOKED">E_NOTARIZATION_NOT_REVOKED</a>);
    hash_info.is_revoked = <b>false</b>;
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_notarization_unrevoked">events::emit_notarization_unrevoked</a>(notarization_id, backing_notarization_id);
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_add_executor"></a>

## Function `add_executor`

Add an allowed executor module
Invariant: only callable by NPLEX admin


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_add_executor">add_executor</a>&lt;T&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, _admin_cap: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">registry::NPLEXAdminCap</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_add_executor">add_executor</a>&lt;T&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    _admin_cap: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a>,
) {
    <b>if</b> (!df::exists_(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.id, <a href="../nplex/registry.md#(nplex=0x0)_registry_ExecutorKey">ExecutorKey</a>&lt;T&gt; {})) {
        df::add(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.id, <a href="../nplex/registry.md#(nplex=0x0)_registry_ExecutorKey">ExecutorKey</a>&lt;T&gt; {}, <b>true</b>);
        <a href="../nplex/events.md#(nplex=0x0)_events_emit_executor_added">events::emit_executor_added</a>(<a href="../dependencies/std/type_name.md#std_type_name_get">std::type_name::get</a>&lt;T&gt;().into_string());
    };
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_remove_executor"></a>

## Function `remove_executor`

Remove an allowed executor module
Invariant: only callable by NPLEX admin


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_remove_executor">remove_executor</a>&lt;T&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, _admin_cap: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">registry::NPLEXAdminCap</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_remove_executor">remove_executor</a>&lt;T&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    _admin_cap: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a>,
) {
    <b>if</b> (df::exists_(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.id, <a href="../nplex/registry.md#(nplex=0x0)_registry_ExecutorKey">ExecutorKey</a>&lt;T&gt; {})) {
        <b>let</b> _: bool = df::remove(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.id, <a href="../nplex/registry.md#(nplex=0x0)_registry_ExecutorKey">ExecutorKey</a>&lt;T&gt; {});
        <a href="../nplex/events.md#(nplex=0x0)_events_emit_executor_removed">events::emit_executor_removed</a>(<a href="../dependencies/std/type_name.md#std_type_name_get">std::type_name::get</a>&lt;T&gt;().into_string());
    };
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_bind_executor"></a>

## Function `bind_executor`

Finalize hash usage by binding it to an LTC1 contract ID


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_bind_executor">bind_executor</a>&lt;T: drop&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, claim: (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationClaim">registry::NotarizationClaim</a>, new_contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, _witness: T)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_bind_executor">bind_executor</a>&lt;T: drop&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    claim: <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationClaim">NotarizationClaim</a>,
    new_contract_id: ID,
    _witness: T
) {
    // Verify witness type is allowed
    <b>assert</b>!(df::exists_(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.id, <a href="../nplex/registry.md#(nplex=0x0)_registry_ExecutorKey">ExecutorKey</a>&lt;T&gt; {}), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_UNAUTHORIZED_EXECUTOR">E_UNAUTHORIZED_EXECUTOR</a>);
    <b>let</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationClaim">NotarizationClaim</a> { notarization_id, document_hash: _ } = claim;
    <b>let</b> notarization_info = table::borrow_mut(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id);
    // Double check
    <b>assert</b>!(<a href="../dependencies/std/option.md#std_option_is_none">std::option::is_none</a>(&notarization_info.contract_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_ALREADY_USED">E_NOTARIZATION_ALREADY_USED</a>);
    // Mark <b>as</b> used
    <a href="../dependencies/std/option.md#std_option_fill">std::option::fill</a>(&<b>mut</b> notarization_info.contract_id, new_contract_id);
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_authorize_transfer"></a>

## Function `authorize_transfer`

Authorize an Ownership Transfer for a specific contract
If there is already an authorized transfer, it will be revoked.
Invariant: only callable by NPLEX admin


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_authorize_transfer">authorize_transfer</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, _admin_cap: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">registry::NPLEXAdminCap</a>, contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, new_owner: <b>address</b>, identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_authorize_transfer">authorize_transfer</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    _admin_cap: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a>,
    contract_id: ID,
    new_owner: <b>address</b>,
    identity_id: ID, // The Identity that `new_owner` represents
    notarization_id: ID
) {
    // 1. Verify Identity exists
    <b>assert</b>!(table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_identities, identity_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_IDENTITY_NOT_APPROVED">E_IDENTITY_NOT_APPROVED</a>);
    <b>let</b> identity = table::borrow(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_identities, identity_id);
    // 2. Verify Role (Must be Institution to own a package)
    <b>assert</b>!(identity.role & <a href="../nplex/registry.md#(nplex=0x0)_registry_ROLE_INSTITUTION">ROLE_INSTITUTION</a> != 0, <a href="../nplex/registry.md#(nplex=0x0)_registry_E_IDENTITY_WRONG_ROLE">E_IDENTITY_WRONG_ROLE</a>);
    <b>if</b> (table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.authorized_transfers, contract_id)) {
        table::remove(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.authorized_transfers, contract_id);
        <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_revoked">events::emit_transfer_revoked</a>(contract_id, notarization_id);
    };
    table::add(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.authorized_transfers, contract_id, <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizedTransfer">NotarizedTransfer</a> {
        notarization_id,
        new_owner,
        new_owner_identity: identity_id,
    });
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_authorized">events::emit_transfer_authorized</a>(contract_id, new_owner, notarization_id);
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_authorize_sales_toggle"></a>

## Function `authorize_sales_toggle`

Authorize a Sales Toggle for a specific contract
If there is already an authorized sales toggle, it will be revoked.
Invariant: only callable by NPLEX admin
new_state: true = open sales, false = close sales


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_authorize_sales_toggle">authorize_sales_toggle</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, _admin_cap: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">registry::NPLEXAdminCap</a>, contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, new_state: bool, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_authorize_sales_toggle">authorize_sales_toggle</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    _admin_cap: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a>,
    contract_id: ID,
    new_state: bool,
    notarization_id: ID
) {
    <b>if</b> (table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.authorized_sales_toggles, contract_id)) {
        table::remove(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.authorized_sales_toggles, contract_id);
        <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggle_revoked">events::emit_sales_toggle_revoked</a>(contract_id, notarization_id);
    };
    table::add(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.authorized_sales_toggles, contract_id, <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizedSaleToggle">NotarizedSaleToggle</a> {
        notarization_id,
        target_state: new_state,
    });
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggle_authorized">events::emit_sales_toggle_authorized</a>(contract_id, new_state, notarization_id);
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_approve_identity"></a>

## Function `approve_identity`

Whitelist a DID Identity for a specific role (Admin Only)
role: 1 = Institution, 2 = Investor, 4 = Admin (bitmask, combinable up to 7)
vc_data: Mandatory raw bytes of the W3C Verifiable Credential (JWT/hash) that
justified this approval. Stored permanently as an on-chain audit trail.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_approve_identity">approve_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, _admin_cap: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">registry::NPLEXAdminCap</a>, identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, role: u8, vc_data: vector&lt;u8&gt;, backing_notarization: &(iota_notarization=0x0)::notarization::Notarization&lt;u256&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_approve_identity">approve_identity</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    _admin_cap: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a>,
    identity_id: ID,
    role: u8,
    vc_data: vector&lt;u8&gt;,
    backing_notarization: &Notarization&lt;u256&gt;,
) {
    <b>let</b> backing_notarization_id = object::id(backing_notarization);
    <b>assert</b>!(role &gt;= 1 && role &lt;= 7, <a href="../nplex/registry.md#(nplex=0x0)_registry_E_INVALID_ROLE">E_INVALID_ROLE</a>);
    <b>assert</b>!(!<a href="../dependencies/std/vector.md#std_vector_is_empty">std::vector::is_empty</a>(&vc_data), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_INVALID_ROLE">E_INVALID_ROLE</a>); // VC data must not be empty
    <b>if</b> (table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_identities, identity_id)) {
        // Update existing identity — replace role and VC data
        <b>let</b> info = table::borrow_mut(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_identities, identity_id);
        <b>let</b> old_role = info.role;
        info.role = role;
        info.vc_data = vc_data;
        <a href="../nplex/events.md#(nplex=0x0)_events_emit_identity_role_updated">events::emit_identity_role_updated</a>(identity_id, old_role, role, backing_notarization_id);
    } <b>else</b> {
        table::add(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_identities, identity_id, <a href="../nplex/registry.md#(nplex=0x0)_registry_ApprovedIdentity">ApprovedIdentity</a> { role, vc_data });
        <a href="../nplex/events.md#(nplex=0x0)_events_emit_identity_approved">events::emit_identity_approved</a>(identity_id, role, backing_notarization_id);
    };
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_revoke_identity"></a>

## Function `revoke_identity`

Remove a DID Identity from the whitelist (Admin Only)


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_revoke_identity">revoke_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, _admin_cap: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">registry::NPLEXAdminCap</a>, identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, backing_notarization: &(iota_notarization=0x0)::notarization::Notarization&lt;u256&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_revoke_identity">revoke_identity</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    _admin_cap: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXAdminCap">NPLEXAdminCap</a>,
    identity_id: ID,
    backing_notarization: &Notarization&lt;u256&gt;,
) {
    <b>let</b> backing_notarization_id = object::id(backing_notarization);
    <b>assert</b>!(table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_identities, identity_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_IDENTITY_NOT_APPROVED">E_IDENTITY_NOT_APPROVED</a>);
    table::remove(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_identities, identity_id);
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_identity_revoked">events::emit_identity_revoked</a>(identity_id, backing_notarization_id);
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_claim_notarization"></a>

## Function `claim_notarization`

Claim a notarization to start the package creation flow

Consumes an approved notarization and returns a "Hot Potato" <code><a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationClaim">NotarizationClaim</a></code>
that must be immediately bound to a new contract via <code><a href="../nplex/registry.md#(nplex=0x0)_registry_bind_executor">bind_executor</a></code>.


<a name="@Arguments_3"></a>

### Arguments

* <code><a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a></code> - The NPLEX Registry shared object.
* <code>notarization_id</code> - The ID of the notarization being claimed.
* <code>document_hash</code> - The hash of the document, must match the registered one.
* <code>ctx</code> - Transaction context.


<a name="@Returns_4"></a>

### Returns

* <code><a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationClaim">NotarizationClaim</a></code> - A Hot Potato struct containing the hash and ID.


<a name="@Aborts_5"></a>

### Aborts

* <code><a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_NOT_APPROVED">E_NOTARIZATION_NOT_APPROVED</a></code> - If not found or <code>document_hash</code> mismatches.
* <code><a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_REVOKED">E_NOTARIZATION_REVOKED</a></code> - If it was revoked by NPLEX Admin.
* <code><a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_ALREADY_USED">E_NOTARIZATION_ALREADY_USED</a></code> - If it was already bound to a contract.
* <code><a href="../nplex/registry.md#(nplex=0x0)_registry_E_UNAUTHORIZED_CREATOR">E_UNAUTHORIZED_CREATOR</a></code> - If the caller is not the <code>authorized_creator</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_claim_notarization">claim_notarization</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, document_hash: u256, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationClaim">registry::NotarizationClaim</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_claim_notarization">claim_notarization</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    notarization_id: ID,
    document_hash: u256,
    ctx: &<b>mut</b> TxContext
): <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationClaim">NotarizationClaim</a> {
    // Verify notarization is approved
    <b>assert</b>!(table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_NOT_APPROVED">E_NOTARIZATION_NOT_APPROVED</a>);
    <b>let</b> notarization_info = table::borrow(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id);
    // Verify document hash matches the approved one mathematically
    <b>assert</b>!(notarization_info.document_hash == document_hash, <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_NOT_APPROVED">E_NOTARIZATION_NOT_APPROVED</a>);
    // Verify not revoked
    <b>assert</b>!(!notarization_info.is_revoked, <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_REVOKED">E_NOTARIZATION_REVOKED</a>);
    // Verify not already used
    <b>assert</b>!(option::is_none(&notarization_info.contract_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_NOTARIZATION_ALREADY_USED">E_NOTARIZATION_ALREADY_USED</a>);
    // Verify authorized creator
    <b>assert</b>!(tx_context::sender(ctx) == notarization_info.authorized_creator, <a href="../nplex/registry.md#(nplex=0x0)_registry_E_UNAUTHORIZED_CREATOR">E_UNAUTHORIZED_CREATOR</a>);
    <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationClaim">NotarizationClaim</a> { notarization_id, document_hash: notarization_info.document_hash }
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_consume_transfer_ticket"></a>

## Function `consume_transfer_ticket`

Consume a transfer ticket to allow Bond transfer
Validates that the Caller (via Witness) is authorized, the Transfer is approved by NPLEX,


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_consume_transfer_ticket">consume_transfer_ticket</a>&lt;T: drop&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, bond_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, new_owner: <b>address</b>, new_owner_identity: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, _witness: T)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_consume_transfer_ticket">consume_transfer_ticket</a>&lt;T: drop&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    bond_id: ID,
    new_owner: <b>address</b>,
    new_owner_identity: ID,
    _witness: T
) {
    // 1. Verify Witness (Caller) is an allowed executor
    <b>assert</b>!(df::exists_(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.id, <a href="../nplex/registry.md#(nplex=0x0)_registry_ExecutorKey">ExecutorKey</a>&lt;T&gt; {}), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_UNAUTHORIZED_EXECUTOR">E_UNAUTHORIZED_EXECUTOR</a>);
    // 2. Verify Transfer is Authorized
    <b>assert</b>!(table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.authorized_transfers, bond_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_TRANSFER_NOT_AUTHORIZED">E_TRANSFER_NOT_AUTHORIZED</a>);
    // 3. Verify Recipient and Identity matches
    <b>let</b> authorization = *table::borrow(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.authorized_transfers, bond_id);
    <b>assert</b>!(authorization.new_owner == new_owner, <a href="../nplex/registry.md#(nplex=0x0)_registry_E_TRANSFER_NOT_AUTHORIZED">E_TRANSFER_NOT_AUTHORIZED</a>);
    <b>assert</b>!(authorization.new_owner_identity == new_owner_identity, <a href="../nplex/registry.md#(nplex=0x0)_registry_E_TRANSFER_NOT_AUTHORIZED">E_TRANSFER_NOT_AUTHORIZED</a>);
    // 4. Consume Ticket
    table::remove(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.authorized_transfers, bond_id);
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_consumed">events::emit_transfer_consumed</a>(bond_id, new_owner);
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_consume_sales_toggle_ticket"></a>

## Function `consume_sales_toggle_ticket`

Consume a sales toggle ticket
Validates that the Caller (via Witness) is authorized, the toggle is approved by NPLEX,
Returns the target sales state (true = open, false = closed)


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_consume_sales_toggle_ticket">consume_sales_toggle_ticket</a>&lt;T: drop&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, contract_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, _witness: T): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_consume_sales_toggle_ticket">consume_sales_toggle_ticket</a>&lt;T: drop&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    contract_id: ID,
    _witness: T
): bool {
    // 1. Verify Witness (Caller) is an allowed executor
    <b>assert</b>!(df::exists_(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.id, <a href="../nplex/registry.md#(nplex=0x0)_registry_ExecutorKey">ExecutorKey</a>&lt;T&gt; {}), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_UNAUTHORIZED_EXECUTOR">E_UNAUTHORIZED_EXECUTOR</a>);
    // 2. Verify Toggle is Authorized
    <b>assert</b>!(table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.authorized_sales_toggles, contract_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_SALES_TOGGLE_NOT_AUTHORIZED">E_SALES_TOGGLE_NOT_AUTHORIZED</a>);
    // 3. Consume Ticket and <b>return</b> target state
    <b>let</b> target_state = table::remove(&<b>mut</b> <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.authorized_sales_toggles, contract_id).target_state;
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggle_consumed">events::emit_sales_toggle_consumed</a>(contract_id, target_state);
    target_state
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_verify_identity"></a>

## Function `verify_identity`

Verify that a DelegationToken's Identity is whitelisted with the required role
required_role: ROLE_INSTITUTION (1), ROLE_INVESTOR (2), or ROLE_ADMIN (4)


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_verify_identity">verify_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, token: &(iota_identity=0x0)::controller::DelegationToken, required_role: u8)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_verify_identity">verify_identity</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    token: &DelegationToken,
    required_role: u8,
) {
    <b>let</b> identity_id = <a href="../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_delegation_token_controller_of">iota_identity::controller::delegation_token_controller_of</a>(token);
    <b>assert</b>!(table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_identities, identity_id), <a href="../nplex/registry.md#(nplex=0x0)_registry_E_IDENTITY_NOT_APPROVED">E_IDENTITY_NOT_APPROVED</a>);
    <b>let</b> info = table::borrow(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_identities, identity_id);
    // Bitmask check: role must contain required_role bits
    <b>assert</b>!(info.role & required_role != 0, <a href="../nplex/registry.md#(nplex=0x0)_registry_E_IDENTITY_WRONG_ROLE">E_IDENTITY_WRONG_ROLE</a>);
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_get_identity_role"></a>

## Function `get_identity_role`

Get the role of a given DID Identity (returns 0 if not approved/not found)
Signature: <code><a href="../nplex/registry.md#(nplex=0x0)_registry_get_identity_role">get_identity_role</a>(&<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>, ID) -&gt; u8</code>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_get_identity_role">get_identity_role</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, identity_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): u8
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_get_identity_role">get_identity_role</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    identity_id: ID
): u8 {
    <b>if</b> (table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_identities, identity_id)) {
        table::borrow(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_identities, identity_id).role
    } <b>else</b> {
        0
    }
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_role_institution"></a>

## Function `role_institution`

Accessor for ROLE_INSTITUTION constant


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_role_institution">role_institution</a>(): u8
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_role_institution">role_institution</a>(): u8 { <a href="../nplex/registry.md#(nplex=0x0)_registry_ROLE_INSTITUTION">ROLE_INSTITUTION</a> }
</code></pre>



</details>

<a name="(nplex=0x0)_registry_role_investor"></a>

## Function `role_investor`

Accessor for ROLE_INVESTOR constant


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_role_investor">role_investor</a>(): u8
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_role_investor">role_investor</a>(): u8 { <a href="../nplex/registry.md#(nplex=0x0)_registry_ROLE_INVESTOR">ROLE_INVESTOR</a> }
</code></pre>



</details>

<a name="(nplex=0x0)_registry_role_admin"></a>

## Function `role_admin`

Accessor for ROLE_ADMIN constant


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_role_admin">role_admin</a>(): u8
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_role_admin">role_admin</a>(): u8 { <a href="../nplex/registry.md#(nplex=0x0)_registry_ROLE_ADMIN">ROLE_ADMIN</a> }
</code></pre>



</details>

<a name="(nplex=0x0)_registry_is_valid_notarization"></a>

## Function `is_valid_notarization`

Check if a notarization is approved and not revoked


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_is_valid_notarization">is_valid_notarization</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_is_valid_notarization">is_valid_notarization</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    notarization_id: ID
): bool {
    <b>if</b> (!table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id)) {
        <b>return</b> <b>false</b>
    };
    <b>let</b> hash_info = table::borrow(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id);
    !hash_info.is_revoked
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_is_notarization_used"></a>

## Function `is_notarization_used`

Check if a notarization has already been used


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_is_notarization_used">is_notarization_used</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_is_notarization_used">is_notarization_used</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    notarization_id: ID
): bool {
    <b>if</b> (!table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id)) {
        <b>return</b> <b>false</b>
    };
    <b>let</b> notarization_info = table::borrow(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id);
    option::is_some(&notarization_info.contract_id)
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_is_notarization_revoked"></a>

## Function `is_notarization_revoked`

Check if a notarization is revoked


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_is_notarization_revoked">is_notarization_revoked</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_is_notarization_revoked">is_notarization_revoked</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    notarization_id: ID
): bool {
    <b>if</b> (!table::contains(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id)) {
        <b>return</b> <b>false</b>
    };
    <b>let</b> notarization_info = table::borrow(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id);
    notarization_info.is_revoked
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_get_notarization_info"></a>

## Function `get_notarization_info`

Get notarization info (for UI/debugging)


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_get_notarization_info">get_notarization_info</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, notarization_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">registry::NotarizationInfo</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_get_notarization_info">get_notarization_info</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">NPLEXRegistry</a>,
    notarization_id: ID
): <a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">NotarizationInfo</a> {
    *table::borrow(&<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>.approved_notarizations, notarization_id)
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_notarization_document_hash"></a>

## Function `notarization_document_hash`

Accessor for NotarizationInfo.document_hash


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_document_hash">notarization_document_hash</a>(info: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">registry::NotarizationInfo</a>): u256
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_document_hash">notarization_document_hash</a>(info: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">NotarizationInfo</a>): u256 {
    info.document_hash
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_notarization_contract_id"></a>

## Function `notarization_contract_id`

Accessor for NotarizationInfo.contract_id


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_contract_id">notarization_contract_id</a>(info: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">registry::NotarizationInfo</a>): <a href="../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_contract_id">notarization_contract_id</a>(info: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">NotarizationInfo</a>): Option&lt;ID&gt; {
    info.contract_id
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_notarization_is_revoked"></a>

## Function `notarization_is_revoked`

Accessor for NotarizationInfo.is_revoked


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_is_revoked">notarization_is_revoked</a>(info: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">registry::NotarizationInfo</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_is_revoked">notarization_is_revoked</a>(info: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">NotarizationInfo</a>): bool {
    info.is_revoked
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_notarization_auditor"></a>

## Function `notarization_auditor`

Accessor for NotarizationInfo.auditor


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_auditor">notarization_auditor</a>(info: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">registry::NotarizationInfo</a>): <b>address</b>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_auditor">notarization_auditor</a>(info: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">NotarizationInfo</a>): <b>address</b> {
    info.auditor
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_notarization_approved_timestamp"></a>

## Function `notarization_approved_timestamp`

Accessor for NotarizationInfo.approved_timestamp


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_approved_timestamp">notarization_approved_timestamp</a>(info: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">registry::NotarizationInfo</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_approved_timestamp">notarization_approved_timestamp</a>(info: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">NotarizationInfo</a>): u64 {
    info.approved_timestamp
}
</code></pre>



</details>

<a name="(nplex=0x0)_registry_notarization_authorized_creator"></a>

## Function `notarization_authorized_creator`

Accessor for NotarizationInfo.authorized_creator


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_authorized_creator">notarization_authorized_creator</a>(info: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">registry::NotarizationInfo</a>): <b>address</b>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/registry.md#(nplex=0x0)_registry_notarization_authorized_creator">notarization_authorized_creator</a>(info: &<a href="../nplex/registry.md#(nplex=0x0)_registry_NotarizationInfo">NotarizationInfo</a>): <b>address</b> {
    info.authorized_creator
}
</code></pre>



</details>
