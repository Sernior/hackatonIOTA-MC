---
layout: default
title: ltc1
parent: Nplex Smart Contracts
---


<a name="(nplex=0x0)_ltc1"></a>

# Module `(nplex=0x0)::ltc1`

NPLEX LTC1 - Manages the creation of LTC1 contracts

This contract provides the logic for the LTC1 contract.


-  [Struct `LTC1`](#(nplex=0x0)_ltc1_LTC1)
-  [Struct `LTC1Witness`](#(nplex=0x0)_ltc1_LTC1Witness)
-  [Struct `LTC1Token`](#(nplex=0x0)_ltc1_LTC1Token)
-  [Struct `LTC1Package`](#(nplex=0x0)_ltc1_LTC1Package)
-  [Constants](#@Constants_0)
-  [Function `init`](#(nplex=0x0)_ltc1_init)
-  [Function `create_contract`](#(nplex=0x0)_ltc1_create_contract)
    -  [Arguments](#@Arguments_1)
    -  [Aborts](#@Aborts_2)
-  [Function `buy_token`](#(nplex=0x0)_ltc1_buy_token)
    -  [Arguments](#@Arguments_3)
    -  [Logic](#@Logic_4)
    -  [Aborts](#@Aborts_5)
-  [Function `withdraw_funding`](#(nplex=0x0)_ltc1_withdraw_funding)
-  [Function `deposit_revenue`](#(nplex=0x0)_ltc1_deposit_revenue)
-  [Function `claim_revenue_owner`](#(nplex=0x0)_ltc1_claim_revenue_owner)
-  [Function `transfer_ownership`](#(nplex=0x0)_ltc1_transfer_ownership)
-  [Function `transfer_token`](#(nplex=0x0)_ltc1_transfer_token)
-  [Function `send_token_to`](#(nplex=0x0)_ltc1_send_token_to)
-  [Function `toggle_sales`](#(nplex=0x0)_ltc1_toggle_sales)
-  [Function `claim_revenue`](#(nplex=0x0)_ltc1_claim_revenue)
-  [Function `balance`](#(nplex=0x0)_ltc1_balance)
-  [Function `claimed_revenue`](#(nplex=0x0)_ltc1_claimed_revenue)
-  [Function `package_id`](#(nplex=0x0)_ltc1_package_id)
-  [Function `verify_document`](#(nplex=0x0)_ltc1_verify_document)
-  [Function `owner_identity`](#(nplex=0x0)_ltc1_owner_identity)
-  [Function `subtract_balance`](#(nplex=0x0)_ltc1_subtract_balance)
-  [Function `create_token_from_fraction`](#(nplex=0x0)_ltc1_create_token_from_fraction)
-  [Function `add_fraction_balance`](#(nplex=0x0)_ltc1_add_fraction_balance)


<pre><code><b>use</b> (iota_identity=0x0)::controller;
<b>use</b> (iota_identity=0x0)::permissions;
<b>use</b> (iota_notarization=0x0)::method;
<b>use</b> (iota_notarization=0x0)::notarization;
<b>use</b> (iota_notarization=0x0)::timelock;
<b>use</b> (nplex=0x0)::<a href="../nplex/events.md#(nplex=0x0)_events">events</a>;
<b>use</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>;
<b>use</b> <a href="../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../dependencies/iota/borrow.md#iota_borrow">iota::borrow</a>;
<b>use</b> <a href="../dependencies/iota/clock.md#iota_clock">iota::clock</a>;
<b>use</b> <a href="../dependencies/iota/coin.md#iota_coin">iota::coin</a>;
<b>use</b> <a href="../dependencies/iota/config.md#iota_config">iota::config</a>;
<b>use</b> <a href="../dependencies/iota/deny_list.md#iota_deny_list">iota::deny_list</a>;
<b>use</b> <a href="../dependencies/iota/display.md#iota_display">iota::display</a>;
<b>use</b> <a href="../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../dependencies/iota/package.md#iota_package">iota::package</a>;
<b>use</b> <a href="../dependencies/iota/table.md#iota_table">iota::table</a>;
<b>use</b> <a href="../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="(nplex=0x0)_ltc1_LTC1"></a>

## Struct `LTC1`

The OTW for package initialization
The <code>drop</code> ability ensures it's a valid One-Time Witness.


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1">LTC1</a> <b>has</b> drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="(nplex=0x0)_ltc1_LTC1Witness"></a>

## Struct `LTC1Witness`

The LTC1 Witness for Registry Binding


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Witness">LTC1Witness</a> <b>has</b> drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="(nplex=0x0)_ltc1_LTC1Token"></a>

## Struct `LTC1Token`

The Investor Token
Represents a share of the NPL package and revenue rights.
No <code>store</code> ability — transfers are DID-gated via <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_transfer_token">transfer_token</a></code>.


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a> <b>has</b> key
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
 Unique identifier: UID
</dd>
<dt>
<code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>: u64</code>
</dt>
<dd>
 Number of "shares" this token represents: u64
</dd>
<dt>
<code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a>: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 Reference to parent LTC1Package: ID
</dd>
<dt>
<code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>: u64</code>
</dt>
<dd>
 Total Coin<T> this token has already claimed: u64
</dd>
</dl>


</details>

<a name="(nplex=0x0)_ltc1_LTC1Package"></a>

## Struct `LTC1Package`

The LTC1 Package (Shared Object)
Contains the state, pools, and metadata visible to everyone.
TODO Immutable fields like name hash and total supply should be made immutable by embedding them in a different obj and using transfer::freeze_object


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>&lt;<b>phantom</b> T&gt; <b>has</b> key
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
<code>name: <a href="../dependencies/std/string.md#std_string_String">std::string::String</a></code>
</dt>
<dd>
</dd>
<dt>
<code>document_hash: u256</code>
</dt>
<dd>
</dd>
<dt>
<code>notary_object_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 ID of the external Notarization Object (created via IOTA SDK)
</dd>
<dt>
<code>total_supply: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>max_sellable_supply: u64</code>
</dt>
<dd>
 Maximum supply that can be sold to investors
</dd>
<dt>
<code>tokens_sold: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>token_price: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>nominal_value: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>funding_pool: <a href="../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>revenue_pool: <a href="../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>total_revenue_deposited: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>owner_legacy_revenue: u64</code>
</dt>
<dd>
 Revenue earned by unsold tokens (belongs to owner)
</dd>
<dt>
<code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a>: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 DID Identity ID of the current owner (Originator/Servicer)
</dd>
<dt>
<code>owner_claimed_revenue: u64</code>
</dt>
<dd>
 Total revenue claimed by the owner so far (moved from deleted OwnerBond)
</dd>
<dt>
<code>creation_timestamp: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>metadata_uri: <a href="../dependencies/std/string.md#std_string_String">std::string::String</a></code>
</dt>
<dd>
</dd>
<dt>
<code>sales_open: bool</code>
</dt>
<dd>
 Whether primary sales are open (controlled by NPLEX admin)
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(nplex=0x0)_ltc1_E_INSUFFICIENT_SUPPLY"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INSUFFICIENT_SUPPLY">E_INSUFFICIENT_SUPPLY</a>: u64 = 1001;
</code></pre>



<a name="(nplex=0x0)_ltc1_E_INSUFFICIENT_PAYMENT"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INSUFFICIENT_PAYMENT">E_INSUFFICIENT_PAYMENT</a>: u64 = 1002;
</code></pre>



<a name="(nplex=0x0)_ltc1_E_CONTRACT_REVOKED"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_CONTRACT_REVOKED">E_CONTRACT_REVOKED</a>: u64 = 1003;
</code></pre>



<a name="(nplex=0x0)_ltc1_E_WRONG_BOND"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_WRONG_BOND">E_WRONG_BOND</a>: u64 = 1004;
</code></pre>



<a name="(nplex=0x0)_ltc1_E_INVALID_SPLIT"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INVALID_SPLIT">E_INVALID_SPLIT</a>: u64 = 1005;
</code></pre>



<a name="(nplex=0x0)_ltc1_E_INVALID_TOKEN"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INVALID_TOKEN">E_INVALID_TOKEN</a>: u64 = 1006;
</code></pre>



<a name="(nplex=0x0)_ltc1_E_SUPPLY_TOO_LOW"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_SUPPLY_TOO_LOW">E_SUPPLY_TOO_LOW</a>: u64 = 1007;
</code></pre>



<a name="(nplex=0x0)_ltc1_E_SALES_CLOSED"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_SALES_CLOSED">E_SALES_CLOSED</a>: u64 = 1008;
</code></pre>



<a name="(nplex=0x0)_ltc1_E_ZERO_AMOUNT"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_ZERO_AMOUNT">E_ZERO_AMOUNT</a>: u64 = 1009;
</code></pre>



<a name="(nplex=0x0)_ltc1_E_INSUFFICIENT_BALANCE"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INSUFFICIENT_BALANCE">E_INSUFFICIENT_BALANCE</a>: u64 = 1010;
</code></pre>



<a name="(nplex=0x0)_ltc1_E_INVALID_AMOUNT"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INVALID_AMOUNT">E_INVALID_AMOUNT</a>: u64 = 1011;
</code></pre>



<a name="(nplex=0x0)_ltc1_MAX_INVESTOR_BPS"></a>

Max investor share in BPS (95.0000%) - 6 decimals


<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_MAX_INVESTOR_BPS">MAX_INVESTOR_BPS</a>: u64 = 950000;
</code></pre>



<a name="(nplex=0x0)_ltc1_SPLIT_DENOMINATOR"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_SPLIT_DENOMINATOR">SPLIT_DENOMINATOR</a>: u64 = 1000000;
</code></pre>



<a name="(nplex=0x0)_ltc1_MIN_SUPPLY"></a>

Min total supply (decrease the dust due to divisions rounding)


<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_MIN_SUPPLY">MIN_SUPPLY</a>: u64 = 1000000000;
</code></pre>



<a name="(nplex=0x0)_ltc1_TOKEN_DISPLAY_NAME"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_TOKEN_DISPLAY_NAME">TOKEN_DISPLAY_NAME</a>: vector&lt;u8&gt; = vector[78, 80, 76, 69, 88, 32, 73, 110, 118, 101, 115, 116, 111, 114, 32, 84, 111, 107, 101, 110];
</code></pre>



<a name="(nplex=0x0)_ltc1_TOKEN_DISPLAY_DESCRIPTION"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_TOKEN_DISPLAY_DESCRIPTION">TOKEN_DISPLAY_DESCRIPTION</a>: vector&lt;u8&gt; = vector[73, 110, 118, 101, 115, 116, 111, 114, 32, 115, 104, 97, 114, 101, 32, 102, 111, 114, 32, 76, 84, 67, 49, 32, 80, 97, 99, 107, 97, 103, 101, 32, 123, 112, 97, 99, 107, 97, 103, 101, 95, 105, 100, 125];
</code></pre>



<a name="(nplex=0x0)_ltc1_TOKEN_DISPLAY_IMAGE_URL"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_TOKEN_DISPLAY_IMAGE_URL">TOKEN_DISPLAY_IMAGE_URL</a>: vector&lt;u8&gt; = vector[104, 116, 116, 112, 115, 58, 47, 47, 97, 112, 105, 46, 110, 112, 108, 101, 120, 46, 101, 117, 47, 105, 99, 111, 110, 115, 47, 116, 111, 107, 101, 110, 95, 98, 108, 117, 101, 46, 112, 110, 103];
</code></pre>



<a name="(nplex=0x0)_ltc1_TOKEN_DISPLAY_PROJECT_URL"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_TOKEN_DISPLAY_PROJECT_URL">TOKEN_DISPLAY_PROJECT_URL</a>: vector&lt;u8&gt; = vector[104, 116, 116, 112, 115, 58, 47, 47, 110, 112, 108, 101, 120, 46, 101, 117];
</code></pre>



<a name="(nplex=0x0)_ltc1_DISPLAY_KEY_NAME"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_DISPLAY_KEY_NAME">DISPLAY_KEY_NAME</a>: vector&lt;u8&gt; = vector[110, 97, 109, 101];
</code></pre>



<a name="(nplex=0x0)_ltc1_DISPLAY_KEY_DESCRIPTION"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_DISPLAY_KEY_DESCRIPTION">DISPLAY_KEY_DESCRIPTION</a>: vector&lt;u8&gt; = vector[100, 101, 115, 99, 114, 105, 112, 116, 105, 111, 110];
</code></pre>



<a name="(nplex=0x0)_ltc1_DISPLAY_KEY_IMAGE_URL"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_DISPLAY_KEY_IMAGE_URL">DISPLAY_KEY_IMAGE_URL</a>: vector&lt;u8&gt; = vector[105, 109, 97, 103, 101, 95, 117, 114, 108];
</code></pre>



<a name="(nplex=0x0)_ltc1_DISPLAY_KEY_PROJECT_URL"></a>



<pre><code><b>const</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_DISPLAY_KEY_PROJECT_URL">DISPLAY_KEY_PROJECT_URL</a>: vector&lt;u8&gt; = vector[112, 114, 111, 106, 101, 99, 116, 95, 117, 114, 108];
</code></pre>



<a name="(nplex=0x0)_ltc1_init"></a>

## Function `init`

Module initializer.
Automatically called when the package is published. Sets up the
IOTA Display standard for <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a></code> objects.


<pre><code><b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_init">init</a>(otw: (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1">ltc1::LTC1</a>, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_init">init</a>(otw: <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1">LTC1</a>, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>) {
    // 1. Claim Publisher
    <b>let</b> publisher = package::claim(otw, ctx);
    // 2. Setup Display <b>for</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>
    <a href="../nplex/display_utils.md#(nplex=0x0)_display_utils_setup_display">display_utils::setup_display</a>! &lt;<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>&gt; (
        &publisher,
        vector[
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_DISPLAY_KEY_NAME">DISPLAY_KEY_NAME</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_DISPLAY_KEY_DESCRIPTION">DISPLAY_KEY_DESCRIPTION</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_DISPLAY_KEY_IMAGE_URL">DISPLAY_KEY_IMAGE_URL</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_DISPLAY_KEY_PROJECT_URL">DISPLAY_KEY_PROJECT_URL</a>),
        ],
        vector[
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_TOKEN_DISPLAY_NAME">TOKEN_DISPLAY_NAME</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_TOKEN_DISPLAY_DESCRIPTION">TOKEN_DISPLAY_DESCRIPTION</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_TOKEN_DISPLAY_IMAGE_URL">TOKEN_DISPLAY_IMAGE_URL</a>),
            <a href="../dependencies/std/string.md#std_string_utf8">std::string::utf8</a>(<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_TOKEN_DISPLAY_PROJECT_URL">TOKEN_DISPLAY_PROJECT_URL</a>),
        ],
        ctx
    );
    // 3. Cleanup & Transfer
    <a href="../dependencies/iota/transfer.md#iota_transfer_public_transfer">iota::transfer::public_transfer</a>(publisher, <a href="../dependencies/iota/tx_context.md#iota_tx_context_sender">iota::tx_context::sender</a>(ctx));
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_create_contract"></a>

## Function `create_contract`

Creates a new LTC1 Package (NPL Fractionalization Contract)

This is the entry point for Originators to tokenize an NPL package.


<a name="@Arguments_1"></a>

### Arguments

* <code><a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a></code> - The NPLEX Registry shared object, used to verify authorization.
* <code>name</code> - The display name of the NPL Package.
* <code>notarization</code> - The IOTA SDK Notarization object bounding the off-chain documents to this contract.
* <code>total_supply</code> - The total number of token shares to emit (must be >= <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_MIN_SUPPLY">MIN_SUPPLY</a></code>).
* <code>token_price</code> - The price of a single token share in NANOS (1,000,000,000 = 1 IOTA).
* <code>nominal_value</code> - The gross book value (GBV) of the underlying NPL package.
* <code>investor_split_bps</code> - The percentage of future revenue destined to investors (in Basis Points).
* <code>metadata_uri</code> - A link (e.g., IPFS) to the prospectus or public metadata.
* <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a></code> - The Decentralized Identifier (DID) of the Originator/Servicer.
* <code>token</code> - The sender's <code>DelegationToken</code> proving their <code>ROLE_INSTITUTION</code> authority.
* <code>clock</code> - The IOTA system clock for timestamping.


<a name="@Aborts_2"></a>

### Aborts

* <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INVALID_SPLIT">E_INVALID_SPLIT</a></code> - if <code>investor_split_bps</code> > <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_MAX_INVESTOR_BPS">MAX_INVESTOR_BPS</a></code>.
* <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_SUPPLY_TOO_LOW">E_SUPPLY_TOO_LOW</a></code> - if <code>total_supply</code> < <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_MIN_SUPPLY">MIN_SUPPLY</a></code>.
* Reverts if the <code>DelegationToken</code> does not authorize the caller as an Institution.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_create_contract">create_contract</a>&lt;T&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, name: <a href="../dependencies/std/string.md#std_string_String">std::string::String</a>, notarization: &(iota_notarization=0x0)::notarization::Notarization&lt;u256&gt;, total_supply: u64, token_price: u64, nominal_value: u64, investor_split_bps: u64, metadata_uri: <a href="../dependencies/std/string.md#std_string_String">std::string::String</a>, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a>: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, token: &(iota_identity=0x0)::controller::DelegationToken, clock: &<a href="../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_create_contract">create_contract</a>&lt;T&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> NPLEXRegistry,
    name: String,
    notarization: &Notarization&lt;u256&gt;,
    total_supply: u64,
    token_price: u64,
    nominal_value: u64,
    investor_split_bps: u64,
    metadata_uri: String,
    <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a>: ID,
    token: &DelegationToken,
    clock: &Clock,
    ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>
) {
    // Verify caller <b>has</b> approved Institution DID
    <a href="../nplex/registry.md#(nplex=0x0)_registry_verify_identity">registry::verify_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, token, <a href="../nplex/registry.md#(nplex=0x0)_registry_role_institution">registry::role_institution</a>());
    <b>let</b> owner = <a href="../dependencies/iota/tx_context.md#iota_tx_context_sender">iota::tx_context::sender</a>(ctx); // Owner is the creator
    // 0. Extract hash and ID from Notarization
    <b>let</b> state = notarization::state(notarization);
    <b>let</b> document_hash = *notarization::data(state);
    <b>let</b> notary_object_id = <a href="../dependencies/iota/object.md#iota_object_id">iota::object::id</a>(notarization);
    // 0. Validate Split
    <b>assert</b>!(investor_split_bps &lt;= <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_MAX_INVESTOR_BPS">MAX_INVESTOR_BPS</a>, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INVALID_SPLIT">E_INVALID_SPLIT</a>);
    // 1. Validate Total Supply
    <b>assert</b>!(total_supply &gt;= <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_MIN_SUPPLY">MIN_SUPPLY</a>, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_SUPPLY_TOO_LOW">E_SUPPLY_TOO_LOW</a>);
    // 2. Claim notarization
    <b>let</b> claim = <a href="../nplex/registry.md#(nplex=0x0)_registry_claim_notarization">registry::claim_notarization</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, notary_object_id, document_hash, ctx);
    // 3. Create UID <b>for</b> Package
    <b>let</b> package_uid = <a href="../dependencies/iota/object.md#iota_object_new">iota::object::new</a>(ctx);
    <b>let</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a> = <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&package_uid);
    // Calculate limits
    <b>let</b> max_sellable_supply = (((total_supply <b>as</b> u256) * (investor_split_bps <b>as</b> u256)) / (<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_SPLIT_DENOMINATOR">SPLIT_DENOMINATOR</a> <b>as</b> u256)) <b>as</b> u64;
    // 4. Create the Package (Shared Object)
    <b>let</b> package = <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>&lt;T&gt; {
        id: package_uid,
        name,
        document_hash,
        notary_object_id,
        // Supply & Pricing
        total_supply,
        max_sellable_supply,
        tokens_sold: 0,
        token_price,
        nominal_value,
        // Pools
        funding_pool: balance::zero&lt;T&gt;(),
        revenue_pool: balance::zero&lt;T&gt;(),
        total_revenue_deposited: 0,
        owner_legacy_revenue: 0,
        // Metadata & Admin
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a>,
        owner_claimed_revenue: 0,
        creation_timestamp: clock::timestamp_ms(clock),
        metadata_uri,
        sales_open: <b>false</b>,
    };
    // 5. Bind hash with Witness
    <a href="../nplex/registry.md#(nplex=0x0)_registry_bind_executor">registry::bind_executor</a>(
        <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>,
        claim,
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a>,
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Witness">LTC1Witness</a> {}
    );
    // 6. Publish
    // Share the package so ANYONE can find it and interact (buy tokens, view status)
    <a href="../dependencies/iota/transfer.md#iota_transfer_share_object">iota::transfer::share_object</a>(package);
    // 7. Emit Event
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_contract_created">events::emit_contract_created</a>(
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a>,
        owner,
        nominal_value,
    );
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_buy_token"></a>

## Function `buy_token`

Purchase tokens (fractional shares) from the package

Investors use this function to finance the NPL package by acquiring <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a></code> shares.


<a name="@Arguments_3"></a>

### Arguments

* <code><a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a></code> - The NPLEX Registry to verify the investor's identity.
* <code>package</code> - The <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a></code> offering the tokens.
* <code>payment</code> - An IOTA <code>Coin</code> used to pay for the tokens. Change is refunded.
* <code>amount</code> - The number of tokens requested.
* <code>token</code> - The sender's <code>DelegationToken</code> proving their <code>ROLE_INVESTOR</code> authority.


<a name="@Logic_4"></a>

### Logic

Implements "Dividend-stripping protection" by pre-calculating the <code>initial_claimed</code>
revenue. This ensures the new investor cannot claim past revenue that was generated
before they bought the token. The past revenue is credited to the Originator.


<a name="@Aborts_5"></a>

### Aborts

* <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_SALES_CLOSED">E_SALES_CLOSED</a></code> - if the package sales are not active.
* <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INSUFFICIENT_SUPPLY">E_INSUFFICIENT_SUPPLY</a></code> - if the requested <code>amount</code> exceeds the <code>max_sellable_supply</code>.
* <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INSUFFICIENT_PAYMENT">E_INSUFFICIENT_PAYMENT</a></code> - if the <code>payment</code> coin value is lower than the required cost.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_buy_token">buy_token</a>&lt;T&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, package: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">ltc1::LTC1Package</a>&lt;T&gt;, payment: <a href="../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;T&gt;, amount: u64, token: &(iota_identity=0x0)::controller::DelegationToken, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_buy_token">buy_token</a>&lt;T&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &NPLEXRegistry,
    package: &<b>mut</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>&lt;T&gt;,
    <b>mut</b> payment: Coin&lt;T&gt;,
    amount: u64,
    token: &DelegationToken,
    ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>
) {
    // Verify caller <b>has</b> approved Investor DID
    <a href="../nplex/registry.md#(nplex=0x0)_registry_verify_identity">registry::verify_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, token, <a href="../nplex/registry.md#(nplex=0x0)_registry_role_investor">registry::role_investor</a>());
    // 0. Verify Contract Status (not revoked)
    <b>assert</b>!(<a href="../nplex/registry.md#(nplex=0x0)_registry_is_valid_notarization">registry::is_valid_notarization</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, package.notary_object_id), <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_CONTRACT_REVOKED">E_CONTRACT_REVOKED</a>);
    // 0.1. amount must be greater than 0
    <b>assert</b>!(amount &gt; 0, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INVALID_AMOUNT">E_INVALID_AMOUNT</a>);
    // 0.5. Verify Sales are Open
    <b>assert</b>!(package.sales_open, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_SALES_CLOSED">E_SALES_CLOSED</a>);
    // 1. Check supply
    <b>assert</b>!(amount &lt;= package.max_sellable_supply - package.tokens_sold, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INSUFFICIENT_SUPPLY">E_INSUFFICIENT_SUPPLY</a>);
    // 2. Calculate cost
    <b>let</b> cost = (((amount <b>as</b> u256) * (package.token_price <b>as</b> u256)) <b>as</b> u64);
    <b>assert</b>!(<a href="../dependencies/iota/coin.md#iota_coin_value">iota::coin::value</a>(&payment) &gt;= cost, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INSUFFICIENT_PAYMENT">E_INSUFFICIENT_PAYMENT</a>);
    // 3. Handle Payment
    <b>let</b> coin_value = <a href="../dependencies/iota/coin.md#iota_coin_value">iota::coin::value</a>(&payment);
    <b>let</b> paid_balance = <b>if</b> (coin_value == cost) {
        <a href="../dependencies/iota/coin.md#iota_coin_into_balance">iota::coin::into_balance</a>(payment)
    } <b>else</b> {
        <b>let</b> split = <a href="../dependencies/iota/coin.md#iota_coin_split">iota::coin::split</a>(&<b>mut</b> payment, cost, ctx);
        <a href="../dependencies/iota/transfer.md#iota_transfer_public_transfer">iota::transfer::public_transfer</a>(payment, <a href="../dependencies/iota/tx_context.md#iota_tx_context_sender">iota::tx_context::sender</a>(ctx)); // Return change
        <a href="../dependencies/iota/coin.md#iota_coin_into_balance">iota::coin::into_balance</a>(split)
    };
    balance::join(&<b>mut</b> package.funding_pool, paid_balance);
    // 4. Calculate Claims
    // When buying new tokens, we must prevent "buying into" past revenue.
    // The revenue attached to these tokens *up to this point* belongs to the Owner (old owner).
    // "Dividend Stripping" protection turned into "Back Pay" <b>for</b> Owner.
    <b>let</b> initial_claimed = (((amount <b>as</b> u256) * (package.total_revenue_deposited <b>as</b> u256)) / (package.total_supply <b>as</b> u256) <b>as</b> u64);
    // 5. Mint Token
    package.tokens_sold = package.tokens_sold + amount;
    <b>let</b> token = <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a> {
        id: <a href="../dependencies/iota/object.md#iota_object_new">iota::object::new</a>(ctx),
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>: amount,
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a>: <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&package.id),
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>: initial_claimed,
    };
    // 6. Credit Owner Legacy Revenue
    // The `initial_claimed` amount is money the new buyer IS NOT entitled to.
    // Therefore, it is money the Owner WAS entitled to (<b>as</b> previous owner of unsold stock).
    package.owner_legacy_revenue = package.owner_legacy_revenue + initial_claimed;
    <a href="../dependencies/iota/transfer.md#iota_transfer_transfer">iota::transfer::transfer</a>(token, <a href="../dependencies/iota/tx_context.md#iota_tx_context_sender">iota::tx_context::sender</a>(ctx));
    // 7. Emit Event
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_token_purchased">events::emit_token_purchased</a>(
        <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&package.id),
        <a href="../dependencies/iota/tx_context.md#iota_tx_context_sender">iota::tx_context::sender</a>(ctx),
        amount,
        cost,
    );
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_withdraw_funding"></a>

## Function `withdraw_funding`

Withdraw Funding from the package (Owner Only)
Verified via DelegationToken matching package.owner_identity


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_withdraw_funding">withdraw_funding</a>&lt;T&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, package: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">ltc1::LTC1Package</a>&lt;T&gt;, amount: u64, token: &(iota_identity=0x0)::controller::DelegationToken, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_withdraw_funding">withdraw_funding</a>&lt;T&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &NPLEXRegistry,
    package: &<b>mut</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>&lt;T&gt;,
    amount: u64,
    token: &DelegationToken,
    ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>
) {
    // Verify caller <b>has</b> approved Institution DID
    <a href="../nplex/registry.md#(nplex=0x0)_registry_verify_identity">registry::verify_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, token, <a href="../nplex/registry.md#(nplex=0x0)_registry_role_institution">registry::role_institution</a>());
    // 0. Verify Contract Status (not revoked)
    <b>assert</b>!(<a href="../nplex/registry.md#(nplex=0x0)_registry_is_valid_notarization">registry::is_valid_notarization</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, package.notary_object_id), <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_CONTRACT_REVOKED">E_CONTRACT_REVOKED</a>);
    // 1. Verify caller's DID matches package owner
    <b>let</b> caller_identity = <a href="../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_delegation_token_controller_of">iota_identity::controller::delegation_token_controller_of</a>(token);
    <b>assert</b>!(caller_identity == package.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a>, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_WRONG_BOND">E_WRONG_BOND</a>);
    // 2. Withdraw
    <b>let</b> funding = <a href="../dependencies/iota/coin.md#iota_coin_take">iota::coin::take</a>(&<b>mut</b> package.funding_pool, amount, ctx); // Aborts <b>if</b> amount &gt; funding_pool.value
    <a href="../dependencies/iota/transfer.md#iota_transfer_public_transfer">iota::transfer::public_transfer</a>(funding, <a href="../dependencies/iota/tx_context.md#iota_tx_context_sender">iota::tx_context::sender</a>(ctx));
    // 3. Emit Event
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_funding_withdrawn">events::emit_funding_withdrawn</a>(
        <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&package.id),
        amount,
        <a href="../dependencies/iota/tx_context.md#iota_tx_context_sender">iota::tx_context::sender</a>(ctx),
    );
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_deposit_revenue"></a>

## Function `deposit_revenue`

Deposit revenue into the package (Owner Only)
Verified via DelegationToken matching package.owner_identity


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_deposit_revenue">deposit_revenue</a>&lt;T&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, package: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">ltc1::LTC1Package</a>&lt;T&gt;, payment: <a href="../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;T&gt;, token: &(iota_identity=0x0)::controller::DelegationToken, _ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_deposit_revenue">deposit_revenue</a>&lt;T&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &NPLEXRegistry,
    package: &<b>mut</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>&lt;T&gt;,
    payment: Coin&lt;T&gt;,
    token: &DelegationToken,
    _ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>
) {
    // Verify caller <b>has</b> approved Institution DID
    <a href="../nplex/registry.md#(nplex=0x0)_registry_verify_identity">registry::verify_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, token, <a href="../nplex/registry.md#(nplex=0x0)_registry_role_institution">registry::role_institution</a>());
    // 0. Verify Contract Status (not revoked)
    <b>assert</b>!(<a href="../nplex/registry.md#(nplex=0x0)_registry_is_valid_notarization">registry::is_valid_notarization</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, package.notary_object_id), <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_CONTRACT_REVOKED">E_CONTRACT_REVOKED</a>);
    // 1. Verify caller's DID matches package owner
    <b>let</b> caller_identity = <a href="../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_delegation_token_controller_of">iota_identity::controller::delegation_token_controller_of</a>(token);
    <b>assert</b>!(caller_identity == package.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a>, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_WRONG_BOND">E_WRONG_BOND</a>);
    // 2. Update Metadata
    <b>let</b> amount = <a href="../dependencies/iota/coin.md#iota_coin_value">iota::coin::value</a>(&payment);
    package.total_revenue_deposited = package.total_revenue_deposited + amount;
    // 3. Deposit to Revenue Pool
    balance::join(&<b>mut</b> package.revenue_pool, <a href="../dependencies/iota/coin.md#iota_coin_into_balance">iota::coin::into_balance</a>(payment));
    // 4. Emit Event
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_revenue_deposited">events::emit_revenue_deposited</a>(
        <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&package.id),
        amount,
    );
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_claim_revenue_owner"></a>

## Function `claim_revenue_owner`

Claim Revenue for Owner
Owner is entitled to:
1. The revenue share of the currently UNSOLD tokens.
2. The "Legacy Revenue" accumulated from tokens they owned in the past but then sold.
Verified via DelegationToken matching package.owner_identity


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claim_revenue_owner">claim_revenue_owner</a>&lt;T&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, package: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">ltc1::LTC1Package</a>&lt;T&gt;, token: &(iota_identity=0x0)::controller::DelegationToken, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claim_revenue_owner">claim_revenue_owner</a>&lt;T&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &NPLEXRegistry,
    package: &<b>mut</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>&lt;T&gt;,
    token: &DelegationToken,
    ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>
) {
    // Verify caller <b>has</b> approved Institution DID
    <a href="../nplex/registry.md#(nplex=0x0)_registry_verify_identity">registry::verify_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, token, <a href="../nplex/registry.md#(nplex=0x0)_registry_role_institution">registry::role_institution</a>());
    // Verify Contract Status (not revoked)
    <b>assert</b>!(<a href="../nplex/registry.md#(nplex=0x0)_registry_is_valid_notarization">registry::is_valid_notarization</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, package.notary_object_id), <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_CONTRACT_REVOKED">E_CONTRACT_REVOKED</a>);
    // 1. Verify caller's DID matches package owner
    <b>let</b> caller_identity = <a href="../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_delegation_token_controller_of">iota_identity::controller::delegation_token_controller_of</a>(token);
    <b>assert</b>!(caller_identity == package.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a>, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_WRONG_BOND">E_WRONG_BOND</a>);
    // 2. Calculate Current Entitlement (Unsold Tokens)
    <b>let</b> unsold_supply = package.total_supply - package.tokens_sold;
    <b>let</b> current_share = (((unsold_supply <b>as</b> u256) * (package.total_revenue_deposited <b>as</b> u256)) / (package.total_supply <b>as</b> u256) <b>as</b> u64);
    // 3. Calculate Total Entitlement (Current + Legacy)
    <b>let</b> total_entitled = current_share + package.owner_legacy_revenue;
    // 4. Calculate Due
    <b>let</b> due = total_entitled - package.owner_claimed_revenue;
    // In the rare case due is 0 (double claim), we just <b>return</b>.
    <b>if</b> (due == 0) {
        <b>return</b>
    };
    // 5. Update Package State
    package.owner_claimed_revenue = package.owner_claimed_revenue + due;
    // 6. Payout
    <b>let</b> payment = <a href="../dependencies/iota/coin.md#iota_coin_take">iota::coin::take</a>(&<b>mut</b> package.revenue_pool, due, ctx);
    <a href="../dependencies/iota/transfer.md#iota_transfer_public_transfer">iota::transfer::public_transfer</a>(payment, <a href="../dependencies/iota/tx_context.md#iota_tx_context_sender">iota::tx_context::sender</a>(ctx));
    // 7. Emit Event
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_revenue_claimed_owner">events::emit_revenue_claimed_owner</a>(
        <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&package.id),
        due,
        <a href="../dependencies/iota/tx_context.md#iota_tx_context_sender">iota::tx_context::sender</a>(ctx),
    );
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_transfer_ownership"></a>

## Function `transfer_ownership`

Transfer ownership of the package to a new owner (DID-based)
Requires prior authorization from NPLEX via Registry


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_transfer_ownership">transfer_ownership</a>&lt;T&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, package: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">ltc1::LTC1Package</a>&lt;T&gt;, new_owner: <b>address</b>, new_owner_identity: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, sender_token: &(iota_identity=0x0)::controller::DelegationToken, _ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_transfer_ownership">transfer_ownership</a>&lt;T&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> NPLEXRegistry,
    package: &<b>mut</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>&lt;T&gt;,
    new_owner: <b>address</b>,
    new_owner_identity: ID,
    sender_token: &DelegationToken,
    _ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>
) {
    // Verify sender <b>has</b> approved Institution DID
    <a href="../nplex/registry.md#(nplex=0x0)_registry_verify_identity">registry::verify_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, sender_token, <a href="../nplex/registry.md#(nplex=0x0)_registry_role_institution">registry::role_institution</a>());
    // Verify caller's DID matches current package owner
    <b>let</b> caller_identity = <a href="../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_delegation_token_controller_of">iota_identity::controller::delegation_token_controller_of</a>(sender_token);
    <b>assert</b>!(caller_identity == package.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a>, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_WRONG_BOND">E_WRONG_BOND</a>);
    // 1. Validate and Consume Ticket from Registry
    <b>let</b> pkg_id = <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&package.id);
    <a href="../nplex/registry.md#(nplex=0x0)_registry_consume_transfer_ticket">registry::consume_transfer_ticket</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, pkg_id, new_owner, new_owner_identity, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Witness">LTC1Witness</a> {});
    // 2. Update ownership on package
    package.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a> = new_owner_identity;
    // 3. Emit Event
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_ownership_transferred">events::emit_ownership_transferred</a>(pkg_id, new_owner_identity);
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_transfer_token"></a>

## Function `transfer_token`

Transfer an LTC1Token to another address (DID-gated sender)
Sender must be a whitelisted Investor. Recipient is not verified on-chain —
the real gate is at the point of USE (claim_revenue, transfer_token, etc.)


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_transfer_token">transfer_token</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, token: (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">ltc1::LTC1Token</a>, recipient: <b>address</b>, sender_did: &(iota_identity=0x0)::controller::DelegationToken)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_transfer_token">transfer_token</a>(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &NPLEXRegistry,
    token: <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>,
    recipient: <b>address</b>,
    sender_did: &DelegationToken,
) {
    // Verify sender is whitelisted Investor
    <a href="../nplex/registry.md#(nplex=0x0)_registry_verify_identity">registry::verify_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, sender_did, <a href="../nplex/registry.md#(nplex=0x0)_registry_role_investor">registry::role_investor</a>());
    <b>let</b> token_id = <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&token.id);
    <a href="../dependencies/iota/transfer.md#iota_transfer_transfer">iota::transfer::transfer</a>(token, recipient);
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_transfer_token">events::emit_transfer_token</a>(token_id, recipient);
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_send_token_to"></a>

## Function `send_token_to`

Package-internal helper: transfer a LTC1Token to an address.
Used by sibling modules (e.g. fractional::redeem) that cannot call
the private <code><a href="../dependencies/iota/transfer.md#iota_transfer_transfer">iota::transfer::transfer</a></code> directly on LTC1Token.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_send_token_to">send_token_to</a>(token: (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">ltc1::LTC1Token</a>, recipient: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_send_token_to">send_token_to</a>(token: <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>, recipient: <b>address</b>) {
    <a href="../dependencies/iota/transfer.md#iota_transfer_transfer">iota::transfer::transfer</a>(token, recipient);
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_toggle_sales"></a>

## Function `toggle_sales`

Toggle sales state for the package
Requires prior authorization from NPLEX via Registry


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_toggle_sales">toggle_sales</a>&lt;T&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, package: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">ltc1::LTC1Package</a>&lt;T&gt;, token: &(iota_identity=0x0)::controller::DelegationToken, _ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_toggle_sales">toggle_sales</a>&lt;T&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &<b>mut</b> NPLEXRegistry,
    package: &<b>mut</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>&lt;T&gt;,
    token: &DelegationToken,
    _ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>
) {
    // Verify caller <b>has</b> approved Institution DID
    <a href="../nplex/registry.md#(nplex=0x0)_registry_verify_identity">registry::verify_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, token, <a href="../nplex/registry.md#(nplex=0x0)_registry_role_institution">registry::role_institution</a>());
    // 1. Consume Ticket from Registry (validates executor + authorization)
    <b>let</b> new_state = <a href="../nplex/registry.md#(nplex=0x0)_registry_consume_sales_toggle_ticket">registry::consume_sales_toggle_ticket</a>(
        <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>,
        <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&package.id),
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Witness">LTC1Witness</a> {}
    );
    // 2. Update Sales State
    package.sales_open = new_state;
    // 3. Emit Event
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_sales_toggled">events::emit_sales_toggled</a>(
        <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&package.id),
        new_state,
    );
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_claim_revenue"></a>

## Function `claim_revenue`

Claim Revenue for Investors
Investors can claim their share of the revenue based on their token balance.
Maybe should be allowed even if the contract is revoked (so investors can exit), to check later when a better control over permissions is implemented.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claim_revenue">claim_revenue</a>&lt;T&gt;(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &(nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry_NPLEXRegistry">registry::NPLEXRegistry</a>, package: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">ltc1::LTC1Package</a>&lt;T&gt;, token: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">ltc1::LTC1Token</a>, did_token: &(iota_identity=0x0)::controller::DelegationToken, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claim_revenue">claim_revenue</a>&lt;T&gt;(
    <a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>: &NPLEXRegistry,
    package: &<b>mut</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>&lt;T&gt;,
    token: &<b>mut</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>,
    did_token: &DelegationToken,
    ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>
) {
    // Verify caller <b>has</b> approved Investor DID
    <a href="../nplex/registry.md#(nplex=0x0)_registry_verify_identity">registry::verify_identity</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, did_token, <a href="../nplex/registry.md#(nplex=0x0)_registry_role_investor">registry::role_investor</a>());
    // Verify Contract Status (not revoked)
    // TODO this <b>has</b> to be checked in the future when we have a more granular control over permissions
    <b>assert</b>!(<a href="../nplex/registry.md#(nplex=0x0)_registry_is_valid_notarization">registry::is_valid_notarization</a>(<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>, package.notary_object_id), <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_CONTRACT_REVOKED">E_CONTRACT_REVOKED</a>);
    // 1. Verify Token belongs to this package
    <b>assert</b>!(token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a> == <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&package.id), <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INVALID_TOKEN">E_INVALID_TOKEN</a>);
    // 2. Calculate Entitlement
    // Formula: (<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a> * total_revenue_deposited) / total_supply
    <b>let</b> total_entitled = (((token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a> <b>as</b> u256) * (package.total_revenue_deposited <b>as</b> u256)) / (package.total_supply <b>as</b> u256) <b>as</b> u64);
    // 3. Calculate Due
    <b>let</b> due = total_entitled - token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>;
    <b>if</b> (due == 0) {
        <b>return</b>
    };
    // 4. Update Token
    token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a> = token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a> + due;
    // 5. Payout
    <b>let</b> payment = <a href="../dependencies/iota/coin.md#iota_coin_take">iota::coin::take</a>(&<b>mut</b> package.revenue_pool, due, ctx);
    <a href="../dependencies/iota/transfer.md#iota_transfer_public_transfer">iota::transfer::public_transfer</a>(payment, <a href="../dependencies/iota/tx_context.md#iota_tx_context_sender">iota::tx_context::sender</a>(ctx));
    // 6. Emit Event
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_revenue_claimed_investor">events::emit_revenue_claimed_investor</a>(
        <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&package.id),
        <a href="../dependencies/iota/object.md#iota_object_uid_to_inner">iota::object::uid_to_inner</a>(&token.id),
        due,
        <a href="../dependencies/iota/tx_context.md#iota_tx_context_sender">iota::tx_context::sender</a>(ctx),
    );
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_balance"></a>

## Function `balance`

Accessor for <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a></code>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>(token: &(nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">ltc1::LTC1Token</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>(token: &<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>): u64 {
    token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_claimed_revenue"></a>

## Function `claimed_revenue`

Accessor for <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a></code>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>(token: &(nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">ltc1::LTC1Token</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>(token: &<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>): u64 {
    token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_package_id"></a>

## Function `package_id`

Accessor for <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a></code>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a>(token: &(nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">ltc1::LTC1Token</a>): <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a>(token: &<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>): ID {
    token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a>
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_verify_document"></a>

## Function `verify_document`

Verify if a proposed document hash matches the package's registered hash
Returns true if <code>document_hash</code> equals <code>package.document_hash</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_verify_document">verify_document</a>&lt;T&gt;(package: &(nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">ltc1::LTC1Package</a>&lt;T&gt;, document_hash: u256): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_verify_document">verify_document</a>&lt;T&gt;(package: &<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>&lt;T&gt;, document_hash: u256): bool {
    package.document_hash == document_hash
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_owner_identity"></a>

## Function `owner_identity`

Accessor for <code><a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a></code>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a>&lt;T&gt;(package: &(nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">ltc1::LTC1Package</a>&lt;T&gt;): <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a>&lt;T&gt;(package: &<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">LTC1Package</a>&lt;T&gt;): ID {
    package.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_owner_identity">owner_identity</a>
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_subtract_balance"></a>

## Function `subtract_balance`

Subtract <code>amount</code> from a token's balance, splitting claimed_revenue proportionally.
Returns (balance_removed, claimed_revenue_removed).
Asserts amount > 0 and amount < token.balance (cannot fractionalize entire token).


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_subtract_balance">subtract_balance</a>(token: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">ltc1::LTC1Token</a>, amount: u64): (u64, u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_subtract_balance">subtract_balance</a>(token: &<b>mut</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>, amount: u64): (u64, u64) {
    <b>assert</b>!(amount &gt; 0, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_ZERO_AMOUNT">E_ZERO_AMOUNT</a>);
    <b>assert</b>!(amount &lt; token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_E_INSUFFICIENT_BALANCE">E_INSUFFICIENT_BALANCE</a>);
    // Split <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a> proportionally
    <b>let</b> claimed_split = (((token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a> <b>as</b> u256) * (amount <b>as</b> u256)) / (token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a> <b>as</b> u256) <b>as</b> u64);
    token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a> = token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a> - amount;
    token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a> = token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a> - claimed_split;
    (amount, claimed_split)
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_create_token_from_fraction"></a>

## Function `create_token_from_fraction`

Create a new LTC1Token with exact values. Used during fraction redemption.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_create_token_from_fraction">create_token_from_fraction</a>(<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a>: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>: u64, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>: u64, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">ltc1::LTC1Token</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_create_token_from_fraction">create_token_from_fraction</a>(
    <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a>: ID,
    <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>: u64,
    <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>: u64,
    ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>
): <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a> {
    <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a> {
        id: <a href="../dependencies/iota/object.md#iota_object_new">iota::object::new</a>(ctx),
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>,
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">package_id</a>,
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>,
    }
}
</code></pre>



</details>

<a name="(nplex=0x0)_ltc1_add_fraction_balance"></a>

## Function `add_fraction_balance`

Add balance and claimed_revenue from a fraction back to an existing token.
Used by fractional::merge().


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_add_fraction_balance">add_fraction_balance</a>(token: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">ltc1::LTC1Token</a>, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>: u64, <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_add_fraction_balance">add_fraction_balance</a>(
    token: &<b>mut</b> <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">LTC1Token</a>,
    <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>: u64,
    <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>: u64,
) {
    token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a> = token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a> + <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_balance">balance</a>;
    token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a> = token.<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a> + <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_claimed_revenue">claimed_revenue</a>;
}
</code></pre>



</details>
