
<a name="iota_coin_manager"></a>

# Module `iota::coin_manager`

The purpose of a CoinManager is to allow access to all
properties of a Coin on-chain from within a single shared object
This includes access to the total supply and metadata
In addition a optional maximum supply can be set and a custom
additional Metadata field can be added.


-  [Struct `CoinManager`](#iota_coin_manager_CoinManager)
-  [Struct `CoinManagerTreasuryCap`](#iota_coin_manager_CoinManagerTreasuryCap)
-  [Struct `CoinManagerMetadataCap`](#iota_coin_manager_CoinManagerMetadataCap)
-  [Struct `ImmutableCoinMetadata`](#iota_coin_manager_ImmutableCoinMetadata)
-  [Struct `CoinManaged`](#iota_coin_manager_CoinManaged)
-  [Struct `TreasuryOwnershipRenounced`](#iota_coin_manager_TreasuryOwnershipRenounced)
-  [Struct `MetadataOwnershipRenounced`](#iota_coin_manager_MetadataOwnershipRenounced)
-  [Constants](#@Constants_0)
-  [Function `new`](#iota_coin_manager_new)
-  [Function `new_with_immutable_metadata`](#iota_coin_manager_new_with_immutable_metadata)
-  [Function `create`](#iota_coin_manager_create)
-  [Function `add_additional_metadata`](#iota_coin_manager_add_additional_metadata)
-  [Function `replace_additional_metadata`](#iota_coin_manager_replace_additional_metadata)
-  [Function `additional_metadata`](#iota_coin_manager_additional_metadata)
-  [Function `get_additional_metadata`](#iota_coin_manager_get_additional_metadata)
-  [Function `enforce_maximum_supply`](#iota_coin_manager_enforce_maximum_supply)
-  [Function `renounce_treasury_ownership`](#iota_coin_manager_renounce_treasury_ownership)
-  [Function `renounce_metadata_ownership`](#iota_coin_manager_renounce_metadata_ownership)
-  [Function `supply_is_immutable`](#iota_coin_manager_supply_is_immutable)
-  [Function `metadata_is_immutable`](#iota_coin_manager_metadata_is_immutable)
-  [Function `metadata`](#iota_coin_manager_metadata)
-  [Function `immutable_metadata`](#iota_coin_manager_immutable_metadata)
-  [Function `total_supply`](#iota_coin_manager_total_supply)
-  [Function `maximum_supply`](#iota_coin_manager_maximum_supply)
-  [Function `available_supply`](#iota_coin_manager_available_supply)
-  [Function `has_maximum_supply`](#iota_coin_manager_has_maximum_supply)
-  [Function `supply_immut`](#iota_coin_manager_supply_immut)
-  [Function `mint`](#iota_coin_manager_mint)
-  [Function `mint_balance`](#iota_coin_manager_mint_balance)
-  [Function `burn`](#iota_coin_manager_burn)
-  [Function `mint_and_transfer`](#iota_coin_manager_mint_and_transfer)
-  [Function `update_name`](#iota_coin_manager_update_name)
-  [Function `update_symbol`](#iota_coin_manager_update_symbol)
-  [Function `update_description`](#iota_coin_manager_update_description)
-  [Function `update_icon_url`](#iota_coin_manager_update_icon_url)
-  [Function `decimals`](#iota_coin_manager_decimals)
-  [Function `name`](#iota_coin_manager_name)
-  [Function `symbol`](#iota_coin_manager_symbol)
-  [Function `description`](#iota_coin_manager_description)
-  [Function `icon_url`](#iota_coin_manager_icon_url)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../../dependencies/iota/coin.md#iota_coin">iota::coin</a>;
<b>use</b> <a href="../../dependencies/iota/config.md#iota_config">iota::config</a>;
<b>use</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list">iota::deny_list</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_coin_manager_CoinManager"></a>

## Struct `CoinManager`

Holds all the related objects to the coin of type <code>T</code> in a convenient shared function.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;<b>phantom</b> T&gt; <b>has</b> key, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>treasury_cap: <a href="../../dependencies/iota/coin.md#iota_coin_TreasuryCap">iota::coin::TreasuryCap</a>&lt;T&gt;</code>
</dt>
<dd>
 The original <code>TreasuryCap</code> object as returned by <code>create_currency</code>.
</dd>
<dt>
<code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/coin.md#iota_coin_CoinMetadata">iota::coin::CoinMetadata</a>&lt;T&gt;&gt;</code>
</dt>
<dd>
 Metadata object, original one from the <code>coin</code> module, if available.
</dd>
<dt>
<code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ImmutableCoinMetadata">iota::coin_manager::ImmutableCoinMetadata</a>&lt;T&gt;&gt;</code>
</dt>
<dd>
 Immutable Metadata object, only to be used as a last resort if the original metadata is frozen.
</dd>
<dt>
<code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;</code>
</dt>
<dd>
 Optional maximum supply, if set you can't mint more as this number - can only be set once.
</dd>
<dt>
<code>supply_immutable: bool</code>
</dt>
<dd>
 Flag indicating if the supply is considered immutable (TreasuryCap is exchanged for this).
</dd>
<dt>
<code>metadata_immutable: bool</code>
</dt>
<dd>
 Flag indicating if the metadata is considered immutable (MetadataCap is exchanged for this).
</dd>
</dl>


</details>

<a name="iota_coin_manager_CoinManagerTreasuryCap"></a>

## Struct `CoinManagerTreasuryCap`

Like <code>TreasuryCap</code>, but for dealing with <code>TreasuryCap</code> inside <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a></code> objects.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;<b>phantom</b> T&gt; <b>has</b> key, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_coin_manager_CoinManagerMetadataCap"></a>

## Struct `CoinManagerMetadataCap`

Metadata has it's own Cap, independent of the <code>TreasuryCap</code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a>&lt;<b>phantom</b> T&gt; <b>has</b> key, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_coin_manager_ImmutableCoinMetadata"></a>

## Struct `ImmutableCoinMetadata`

The immutable version of <code>CoinMetadata</code>, used in case of migrating from frozen objects
to a <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a></code> holding the metadata.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ImmutableCoinMetadata">ImmutableCoinMetadata</a>&lt;<b>phantom</b> T&gt; <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_decimals">decimals</a>: u8</code>
</dt>
<dd>
 Number of decimal places the coin uses.
 A coin with <code>value</code> N and <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_decimals">decimals</a></code> D should be shown as N / 10^D
 E.g., a coin with <code>value</code> 7002 and decimals 3 should be displayed as 7.002
 This is metadata for display usage only.
</dd>
<dt>
<code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a></code>
</dt>
<dd>
 Name for the token.
</dd>
<dt>
<code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a>: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
 Symbol for the token.
</dd>
<dt>
<code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a></code>
</dt>
<dd>
 Description of the token.
</dd>
<dt>
<code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_icon_url">icon_url</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/url.md#iota_url_Url">iota::url::Url</a>&gt;</code>
</dt>
<dd>
 URL for the token logo.
</dd>
</dl>


</details>

<a name="iota_coin_manager_CoinManaged"></a>

## Struct `CoinManaged`

Event triggered once <code>Coin</code> ownership is transferred to a new <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a></code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManaged">CoinManaged</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>coin_name: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_coin_manager_TreasuryOwnershipRenounced"></a>

## Struct `TreasuryOwnershipRenounced`

Event triggered if the ownership of the treasury part of a <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a></code> is renounced.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_TreasuryOwnershipRenounced">TreasuryOwnershipRenounced</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>coin_name: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_coin_manager_MetadataOwnershipRenounced"></a>

## Struct `MetadataOwnershipRenounced`

Event triggered if the ownership of the metadata part of a <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a></code> is renounced.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_MetadataOwnershipRenounced">MetadataOwnershipRenounced</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>coin_name: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_coin_manager_EMaximumSupplyReached"></a>

The error returned when the maximum supply reached.


<pre><code><b>const</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EMaximumSupplyReached">EMaximumSupplyReached</a>: u64 = 0;
</code></pre>



<a name="iota_coin_manager_EMaximumSupplyAlreadySet"></a>

The error returned if an attempt is made to change the maximum supply after setting it.


<pre><code><b>const</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EMaximumSupplyAlreadySet">EMaximumSupplyAlreadySet</a>: u64 = 1;
</code></pre>



<a name="iota_coin_manager_EMaximumSupplyLowerThanTotalSupply"></a>

The error returned if an attempt is made to change the maximum supply that is lower than the total supply.


<pre><code><b>const</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EMaximumSupplyLowerThanTotalSupply">EMaximumSupplyLowerThanTotalSupply</a>: u64 = 2;
</code></pre>



<a name="iota_coin_manager_EMaximumSupplyHigherThanPossible"></a>

The error returned if an attempt is made to change the maximum supply that is higher than the maximum possible supply.


<pre><code><b>const</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EMaximumSupplyHigherThanPossible">EMaximumSupplyHigherThanPossible</a>: u64 = 3;
</code></pre>



<a name="iota_coin_manager_EAdditionalMetadataDoesNotExist"></a>

The error returned if you try to edit nonexisting additional metadata.


<pre><code><b>const</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EAdditionalMetadataDoesNotExist">EAdditionalMetadataDoesNotExist</a>: u64 = 4;
</code></pre>



<a name="iota_coin_manager_MAX_SUPPLY"></a>

The maximum supply supported by <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a></code>.


<pre><code><b>const</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_MAX_SUPPLY">MAX_SUPPLY</a>: u64 = 18446744073709551614;
</code></pre>



<a name="iota_coin_manager_ADDITIONAL_METADATA_NAME"></a>

The name of the related additional metadata dynamic field.


<pre><code><b>const</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ADDITIONAL_METADATA_NAME">ADDITIONAL_METADATA_NAME</a>: vector&lt;u8&gt; = vector[97, 100, 100, 105, 116, 105, 111, 110, 97, 108, 95, 109, 101, 116, 97, 100, 97, 116, 97];
</code></pre>



<a name="iota_coin_manager_new"></a>

## Function `new`

Wraps all important objects related to a <code>Coin</code> inside a shared object.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_new">new</a>&lt;T&gt;(treasury_cap: <a href="../../dependencies/iota/coin.md#iota_coin_TreasuryCap">iota::coin::TreasuryCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>: <a href="../../dependencies/iota/coin.md#iota_coin_CoinMetadata">iota::coin::CoinMetadata</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">iota::coin_manager::CoinManagerTreasuryCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">iota::coin_manager::CoinManagerMetadataCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_new">new</a>&lt;T&gt;(
    treasury_cap: TreasuryCap&lt;T&gt;,
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>: CoinMetadata&lt;T&gt;,
    ctx: &<b>mut</b> TxContext,
): (<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;) {
    <b>let</b> manager = <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a> {
        id: object::new(ctx),
        treasury_cap,
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>: option::some(<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>),
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>: option::none(),
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>: option::none(),
        supply_immutable: <b>false</b>,
        metadata_immutable: <b>false</b>,
    };
    event::emit(<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManaged">CoinManaged</a> {
        coin_name: type_name::into_string(type_name::get&lt;T&gt;()),
    });
    (
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;T&gt; {
            id: object::new(ctx),
        },
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a>&lt;T&gt; {
            id: object::new(ctx),
        },
        manager,
    )
}
</code></pre>



</details>

<a name="iota_coin_manager_new_with_immutable_metadata"></a>

## Function `new_with_immutable_metadata`

This function allows the same as <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_new">new</a></code> but under the assumption the Metadata can not be transferred.
This would typically be the case with <code>Coin</code> instances where the metadata is already frozen.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_new_with_immutable_metadata">new_with_immutable_metadata</a>&lt;T&gt;(treasury_cap: <a href="../../dependencies/iota/coin.md#iota_coin_TreasuryCap">iota::coin::TreasuryCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>: &<a href="../../dependencies/iota/coin.md#iota_coin_CoinMetadata">iota::coin::CoinMetadata</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">iota::coin_manager::CoinManagerTreasuryCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_new_with_immutable_metadata">new_with_immutable_metadata</a>&lt;T&gt;(
    treasury_cap: TreasuryCap&lt;T&gt;,
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>: &CoinMetadata&lt;T&gt;,
    ctx: &<b>mut</b> TxContext,
): (<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;) {
    <b>let</b> metacopy = <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ImmutableCoinMetadata">ImmutableCoinMetadata</a>&lt;T&gt; {
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_decimals">decimals</a>: <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>.get_decimals(),
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a>: <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>.get_name(),
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a>: <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>.get_symbol(),
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a>: <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>.get_description(),
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_icon_url">icon_url</a>: <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>.get_icon_url(),
    };
    <b>let</b> manager = <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a> {
        id: object::new(ctx),
        treasury_cap,
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>: option::none(),
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>: option::some(metacopy),
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>: option::none(),
        supply_immutable: <b>false</b>,
        metadata_immutable: <b>true</b>,
    };
    event::emit(<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManaged">CoinManaged</a> {
        coin_name: type_name::into_string(type_name::get&lt;T&gt;()),
    });
    (
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;T&gt; {
            id: object::new(ctx),
        },
        manager,
    )
}
</code></pre>



</details>

<a name="iota_coin_manager_create"></a>

## Function `create`

Convenience wrapper to create a new <code>Coin</code> and instantly wrap the cap inside a <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_create">create</a>&lt;T: drop&gt;(witness: T, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_decimals">decimals</a>: u8, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a>: vector&lt;u8&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a>: vector&lt;u8&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a>: vector&lt;u8&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_icon_url">icon_url</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/url.md#iota_url_Url">iota::url::Url</a>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">iota::coin_manager::CoinManagerTreasuryCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">iota::coin_manager::CoinManagerMetadataCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_create">create</a>&lt;T: drop&gt;(
    witness: T,
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_decimals">decimals</a>: u8,
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a>: vector&lt;u8&gt;,
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a>: vector&lt;u8&gt;,
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a>: vector&lt;u8&gt;,
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_icon_url">icon_url</a>: Option&lt;Url&gt;,
    ctx: &<b>mut</b> TxContext,
): (<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;) {
    <b>let</b> (cap, meta) = coin::create_currency(
        witness,
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_decimals">decimals</a>,
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a>,
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a>,
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a>,
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_icon_url">icon_url</a>,
        ctx,
    );
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_new">new</a>(cap, meta, ctx)
}
</code></pre>



</details>

<a name="iota_coin_manager_add_additional_metadata"></a>

## Function `add_additional_metadata`

Option to add an additional metadata object to the manager.
Can contain whatever you need in terms of additional metadata as a object.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_add_additional_metadata">add_additional_metadata</a>&lt;T, Value: store&gt;(_: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">iota::coin_manager::CoinManagerMetadataCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;, value: Value)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_add_additional_metadata">add_additional_metadata</a>&lt;T, Value: store&gt;(
    _: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
    value: Value,
) {
    df::add(&<b>mut</b> manager.id, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ADDITIONAL_METADATA_NAME">ADDITIONAL_METADATA_NAME</a>, value);
}
</code></pre>



</details>

<a name="iota_coin_manager_replace_additional_metadata"></a>

## Function `replace_additional_metadata`

Option to replace an additional metadata object to the manager.
Can contain whatever you need in terms of additional metadata as a object.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_replace_additional_metadata">replace_additional_metadata</a>&lt;T, Value: store, OldValue: store&gt;(_: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">iota::coin_manager::CoinManagerMetadataCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;, value: Value): OldValue
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_replace_additional_metadata">replace_additional_metadata</a>&lt;T, Value: store, OldValue: store&gt;(
    _: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
    value: Value,
): OldValue {
    <b>assert</b>!(df::exists_(&manager.id, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ADDITIONAL_METADATA_NAME">ADDITIONAL_METADATA_NAME</a>), <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EAdditionalMetadataDoesNotExist">EAdditionalMetadataDoesNotExist</a>);
    <b>let</b> old_value = df::remove&lt;vector&lt;u8&gt;, OldValue&gt;(&<b>mut</b> manager.id, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ADDITIONAL_METADATA_NAME">ADDITIONAL_METADATA_NAME</a>);
    df::add(&<b>mut</b> manager.id, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ADDITIONAL_METADATA_NAME">ADDITIONAL_METADATA_NAME</a>, value);
    old_value
}
</code></pre>



</details>

<a name="iota_coin_manager_additional_metadata"></a>

## Function `additional_metadata`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_additional_metadata">additional_metadata</a>&lt;T, Value: store&gt;(manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): &Value
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_additional_metadata">additional_metadata</a>&lt;T, Value: store&gt;(manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): &Value {
    <b>assert</b>!(df::exists_(&manager.id, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ADDITIONAL_METADATA_NAME">ADDITIONAL_METADATA_NAME</a>), <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EAdditionalMetadataDoesNotExist">EAdditionalMetadataDoesNotExist</a>);
    <b>let</b> meta: &Value = df::borrow(&manager.id, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ADDITIONAL_METADATA_NAME">ADDITIONAL_METADATA_NAME</a>);
    meta
}
</code></pre>



</details>

<a name="iota_coin_manager_get_additional_metadata"></a>

## Function `get_additional_metadata`

Immutably borrows the additional metadata.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_get_additional_metadata">get_additional_metadata</a>&lt;T, Value: store&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): &Value
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_get_additional_metadata">get_additional_metadata</a>&lt;T, Value: store&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): &Value {
    <b>assert</b>!(df::exists_(&manager.id, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ADDITIONAL_METADATA_NAME">ADDITIONAL_METADATA_NAME</a>), <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EAdditionalMetadataDoesNotExist">EAdditionalMetadataDoesNotExist</a>);
    <b>let</b> meta: &Value = df::borrow(&manager.id, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ADDITIONAL_METADATA_NAME">ADDITIONAL_METADATA_NAME</a>);
    meta
}
</code></pre>



</details>

<a name="iota_coin_manager_enforce_maximum_supply"></a>

## Function `enforce_maximum_supply`

A one-time callable function to set a maximum mintable supply on a coin.
This can only be set once and is irrevertable.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_enforce_maximum_supply">enforce_maximum_supply</a>&lt;T&gt;(_: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">iota::coin_manager::CoinManagerTreasuryCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_enforce_maximum_supply">enforce_maximum_supply</a>&lt;T&gt;(
    _: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>: u64,
) {
    <b>assert</b>!(option::is_none(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>), <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EMaximumSupplyAlreadySet">EMaximumSupplyAlreadySet</a>);
    <b>assert</b>!(<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a> &lt;= <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_MAX_SUPPLY">MAX_SUPPLY</a>, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EMaximumSupplyHigherThanPossible">EMaximumSupplyHigherThanPossible</a>);
    <b>assert</b>!(<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a>(manager) &lt;= <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EMaximumSupplyLowerThanTotalSupply">EMaximumSupplyLowerThanTotalSupply</a>);
    option::fill(&<b>mut</b> manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>);
}
</code></pre>



</details>

<a name="iota_coin_manager_renounce_treasury_ownership"></a>

## Function `renounce_treasury_ownership`

An irreversible action renouncing supply ownership which can be called if you hold the <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a></code>.
This action provides <code>Coin</code> holders with some assurances if called, namely that there will
not be any new minting or changes to the supply from this point onward. The maximum supply
will be set to the current supply and will not be changed any more afterwards.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_renounce_treasury_ownership">renounce_treasury_ownership</a>&lt;T&gt;(cap: <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">iota::coin_manager::CoinManagerTreasuryCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_renounce_treasury_ownership">renounce_treasury_ownership</a>&lt;T&gt;(
    cap: <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
) {
    // Deleting the Cap
    <b>let</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a> { id } = cap;
    object::delete(id);
    // Updating the maximum supply to the total supply
    <b>let</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a> = <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a>(manager);
    <b>if</b> (manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_has_maximum_supply">has_maximum_supply</a>()) {
        option::swap(&<b>mut</b> manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a>);
    } <b>else</b> {
        option::fill(&<b>mut</b> manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a>);
    };
    // Setting ownership renounced to <b>true</b>
    manager.supply_immutable = <b>true</b>;
    event::emit(<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_TreasuryOwnershipRenounced">TreasuryOwnershipRenounced</a> {
        coin_name: type_name::into_string(type_name::get&lt;T&gt;()),
    });
}
</code></pre>



</details>

<a name="iota_coin_manager_renounce_metadata_ownership"></a>

## Function `renounce_metadata_ownership`

An irreversible action renouncing manager ownership which can be called if you hold the <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a></code>.
This action provides <code>Coin</code> holders with some assurances if called, namely that there will
not be any changes to the metadata from this point onward.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_renounce_metadata_ownership">renounce_metadata_ownership</a>&lt;T&gt;(cap: <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">iota::coin_manager::CoinManagerMetadataCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_renounce_metadata_ownership">renounce_metadata_ownership</a>&lt;T&gt;(
    cap: <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
) {
    // Deleting the Cap
    <b>let</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a> { id } = cap;
    object::delete(id);
    // Setting ownership renounced to <b>true</b>
    manager.metadata_immutable = <b>true</b>;
    event::emit(<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_MetadataOwnershipRenounced">MetadataOwnershipRenounced</a> {
        coin_name: type_name::into_string(type_name::get&lt;T&gt;()),
    });
}
</code></pre>



</details>

<a name="iota_coin_manager_supply_is_immutable"></a>

## Function `supply_is_immutable`

Convenience function allowing users to query if the ownership of the supply of this <code>Coin</code>
and thus the ability to mint new <code>Coin</code> has been renounced.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_supply_is_immutable">supply_is_immutable</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_supply_is_immutable">supply_is_immutable</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): bool {
    manager.supply_immutable
}
</code></pre>



</details>

<a name="iota_coin_manager_metadata_is_immutable"></a>

## Function `metadata_is_immutable`

Convenience function allowing users to query if the ownership of the metadata management
and thus the ability to change any of the metadata has been renounced.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata_is_immutable">metadata_is_immutable</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata_is_immutable">metadata_is_immutable</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): bool {
    manager.metadata_immutable || option::is_some(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>)
}
</code></pre>



</details>

<a name="iota_coin_manager_metadata"></a>

## Function `metadata`

Get a read-only version of the metadata, available for everyone.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): &<a href="../../dependencies/iota/coin.md#iota_coin_CoinMetadata">iota::coin::CoinMetadata</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): &CoinMetadata&lt;T&gt; {
    option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>)
}
</code></pre>



</details>

<a name="iota_coin_manager_immutable_metadata"></a>

## Function `immutable_metadata`

Get a read-only version of the read-only metadata, available for everyone.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ImmutableCoinMetadata">iota::coin_manager::ImmutableCoinMetadata</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_ImmutableCoinMetadata">ImmutableCoinMetadata</a>&lt;T&gt; {
    option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>)
}
</code></pre>



</details>

<a name="iota_coin_manager_total_supply"></a>

## Function `total_supply`

Get the total supply as a number.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): u64 {
    coin::total_supply(&manager.treasury_cap)
}
</code></pre>



</details>

<a name="iota_coin_manager_maximum_supply"></a>

## Function `maximum_supply`

Get the maximum supply possible as a number.
If no maximum set it's the maximum u64 possible.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): u64 {
    option::get_with_default(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_MAX_SUPPLY">MAX_SUPPLY</a>)
}
</code></pre>



</details>

<a name="iota_coin_manager_available_supply"></a>

## Function `available_supply`

Convenience function returning the remaining supply that can be minted still.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_available_supply">available_supply</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_available_supply">available_supply</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): u64 {
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>(manager) - <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a>(manager)
}
</code></pre>



</details>

<a name="iota_coin_manager_has_maximum_supply"></a>

## Function `has_maximum_supply`

Returns if a maximum supply has been set for this Coin or not.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_has_maximum_supply">has_maximum_supply</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_has_maximum_supply">has_maximum_supply</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): bool {
    option::is_some(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>)
}
</code></pre>



</details>

<a name="iota_coin_manager_supply_immut"></a>

## Function `supply_immut`

Get immutable reference to the treasury's <code>Supply</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_supply_immut">supply_immut</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): &<a href="../../dependencies/iota/balance.md#iota_balance_Supply">iota::balance::Supply</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_supply_immut">supply_immut</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): &Supply&lt;T&gt; {
    coin::supply_immut(&manager.treasury_cap)
}
</code></pre>



</details>

<a name="iota_coin_manager_mint"></a>

## Function `mint`

Create a coin worth <code>value</code> and increase the total supply
in <code>cap</code> accordingly.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_mint">mint</a>&lt;T&gt;(_: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">iota::coin_manager::CoinManagerTreasuryCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;, value: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_mint">mint</a>&lt;T&gt;(
    _: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
    value: u64,
    ctx: &<b>mut</b> TxContext,
): Coin&lt;T&gt; {
    <b>assert</b>!(<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a>(manager) + value &lt;= <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>(manager), <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EMaximumSupplyReached">EMaximumSupplyReached</a>);
    coin::mint(&<b>mut</b> manager.treasury_cap, value, ctx)
}
</code></pre>



</details>

<a name="iota_coin_manager_mint_balance"></a>

## Function `mint_balance`

Mint some amount of T as a <code>Balance</code> and increase the total
supply in <code>cap</code> accordingly.
Aborts if <code>value</code> + <code>cap.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a></code> >= U64_MAX


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_mint_balance">mint_balance</a>&lt;T&gt;(_: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">iota::coin_manager::CoinManagerTreasuryCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;, value: u64): <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_mint_balance">mint_balance</a>&lt;T&gt;(
    _: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
    value: u64,
): Balance&lt;T&gt; {
    <b>assert</b>!(<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a>(manager) + value &lt;= <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>(manager), <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EMaximumSupplyReached">EMaximumSupplyReached</a>);
    coin::mint_balance(&<b>mut</b> manager.treasury_cap, value)
}
</code></pre>



</details>

<a name="iota_coin_manager_burn"></a>

## Function `burn`

Destroy the coin <code>c</code> and decrease the total supply in <code>cap</code>
accordingly.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_burn">burn</a>&lt;T&gt;(_: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">iota::coin_manager::CoinManagerTreasuryCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;, c: <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;T&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_burn">burn</a>&lt;T&gt;(
    _: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
    c: Coin&lt;T&gt;,
): u64 {
    coin::burn(&<b>mut</b> manager.treasury_cap, c)
}
</code></pre>



</details>

<a name="iota_coin_manager_mint_and_transfer"></a>

## Function `mint_and_transfer`

Mint <code>amount</code> of <code>Coin</code> and send it to <code>recipient</code>. Invokes <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_mint">mint</a>()</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_mint_and_transfer">mint_and_transfer</a>&lt;T&gt;(_: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">iota::coin_manager::CoinManagerTreasuryCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;, amount: u64, recipient: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_mint_and_transfer">mint_and_transfer</a>&lt;T&gt;(
    _: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">CoinManagerTreasuryCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
    amount: u64,
    recipient: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
) {
    <b>assert</b>!(<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_total_supply">total_supply</a>(manager) + amount &lt;= <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_maximum_supply">maximum_supply</a>(manager), <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_EMaximumSupplyReached">EMaximumSupplyReached</a>);
    coin::mint_and_transfer(&<b>mut</b> manager.treasury_cap, amount, recipient, ctx)
}
</code></pre>



</details>

<a name="iota_coin_manager_update_name"></a>

## Function `update_name`

Update the <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a></code> of the coin in the <code>CoinMetadata</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_update_name">update_name</a>&lt;T&gt;(_: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">iota::coin_manager::CoinManagerMetadataCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_update_name">update_name</a>&lt;T&gt;(
    _: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a>: string::String,
) {
    coin::update_name(&manager.treasury_cap, option::borrow_mut(&<b>mut</b> manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>), <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a>)
}
</code></pre>



</details>

<a name="iota_coin_manager_update_symbol"></a>

## Function `update_symbol`

Update the <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a></code> of the coin in the <code>CoinMetadata</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_update_symbol">update_symbol</a>&lt;T&gt;(_: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">iota::coin_manager::CoinManagerMetadataCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a>: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_update_symbol">update_symbol</a>&lt;T&gt;(
    _: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a>: ascii::String,
) {
    coin::update_symbol(&manager.treasury_cap, option::borrow_mut(&<b>mut</b> manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>), <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a>)
}
</code></pre>



</details>

<a name="iota_coin_manager_update_description"></a>

## Function `update_description`

Update the <code><a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a></code> of the coin in the <code>CoinMetadata</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_update_description">update_description</a>&lt;T&gt;(_: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">iota::coin_manager::CoinManagerMetadataCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;, <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_update_description">update_description</a>&lt;T&gt;(
    _: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
    <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a>: string::String,
) {
    coin::update_description(
        &manager.treasury_cap,
        option::borrow_mut(&<b>mut</b> manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>),
        <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a>,
    )
}
</code></pre>



</details>

<a name="iota_coin_manager_update_icon_url"></a>

## Function `update_icon_url`

Update the <code>url</code> of the coin in the <code>CoinMetadata</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_update_icon_url">update_icon_url</a>&lt;T&gt;(_: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">iota::coin_manager::CoinManagerMetadataCap</a>&lt;T&gt;, manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;, url: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_update_icon_url">update_icon_url</a>&lt;T&gt;(
    _: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerMetadataCap">CoinManagerMetadataCap</a>&lt;T&gt;,
    manager: &<b>mut</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;,
    url: ascii::String,
) {
    coin::update_icon_url(&manager.treasury_cap, option::borrow_mut(&<b>mut</b> manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>), url)
}
</code></pre>



</details>

<a name="iota_coin_manager_decimals"></a>

## Function `decimals`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_decimals">decimals</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): u8
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_decimals">decimals</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): u8 {
    <b>if</b> (option::is_some(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>)) {
        coin::get_decimals(option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>))
    } <b>else</b> {
        option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>).<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_decimals">decimals</a>
    }
}
</code></pre>



</details>

<a name="iota_coin_manager_name"></a>

## Function `name`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): string::String {
    <b>if</b> (option::is_some(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>)) {
        coin::get_name(option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>))
    } <b>else</b> {
        option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>).<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_name">name</a>
    }
}
</code></pre>



</details>

<a name="iota_coin_manager_symbol"></a>

## Function `symbol`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): ascii::String {
    <b>if</b> (option::is_some(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>)) {
        coin::get_symbol(option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>))
    } <b>else</b> {
        option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>).<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_symbol">symbol</a>
    }
}
</code></pre>



</details>

<a name="iota_coin_manager_description"></a>

## Function `description`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): string::String {
    <b>if</b> (option::is_some(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>)) {
        coin::get_description(option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>))
    } <b>else</b> {
        option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>).<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_description">description</a>
    }
}
</code></pre>



</details>

<a name="iota_coin_manager_icon_url"></a>

## Function `icon_url`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_icon_url">icon_url</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">iota::coin_manager::CoinManager</a>&lt;T&gt;): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/url.md#iota_url_Url">iota::url::Url</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_icon_url">icon_url</a>&lt;T&gt;(manager: &<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManager">CoinManager</a>&lt;T&gt;): Option&lt;Url&gt; {
    <b>if</b> (option::is_some(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>)) {
        coin::get_icon_url(option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_metadata">metadata</a>))
    } <b>else</b> {
        option::borrow(&manager.<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_immutable_metadata">immutable_metadata</a>).<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_icon_url">icon_url</a>
    }
}
</code></pre>



</details>
