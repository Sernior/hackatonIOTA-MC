
<a name="stardust_nft_output"></a>

# Module `stardust::nft_output`



-  [Struct `NftOutput`](#stardust_nft_output_NftOutput)
-  [Constants](#@Constants_0)
-  [Function `extract_assets`](#stardust_nft_output_extract_assets)
-  [Function `load_nft`](#stardust_nft_output_load_nft)
-  [Function `attach_nft`](#stardust_nft_output_attach_nft)
-  [Function `receive`](#stardust_nft_output_receive)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../../dependencies/iota/coin.md#iota_coin">iota::coin</a>;
<b>use</b> <a href="../../dependencies/iota/config.md#iota_config">iota::config</a>;
<b>use</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list">iota::deny_list</a>;
<b>use</b> <a href="../../dependencies/iota/display.md#iota_display">iota::display</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/package.md#iota_package">iota::package</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/stardust/expiration_unlock_condition.md#stardust_expiration_unlock_condition">stardust::expiration_unlock_condition</a>;
<b>use</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27">stardust::irc27</a>;
<b>use</b> <a href="../../dependencies/stardust/nft.md#stardust_nft">stardust::nft</a>;
<b>use</b> <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition">stardust::storage_deposit_return_unlock_condition</a>;
<b>use</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition">stardust::timelock_unlock_condition</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/fixed_point32.md#std_fixed_point32">std::fixed_point32</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="stardust_nft_output_NftOutput"></a>

## Struct `NftOutput`

The Stardust NFT output representation.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">NftOutput</a>&lt;<b>phantom</b> T&gt; <b>has</b> key
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
 This is a "random" UID, not the NFTID from Stardust.
</dd>
<dt>
<code>balance: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;</code>
</dt>
<dd>
 The amount of coins held by the output.
</dd>
<dt>
<code>native_tokens: <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a></code>
</dt>
<dd>
 The <code>Bag</code> holds native tokens, key-ed by the stringified type of the asset.
 Example: key: "0xabcded::soon::SOON", value: Balance<0xabcded::soon::SOON>.
</dd>
<dt>
<code>storage_deposit_return_uc: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_StorageDepositReturnUnlockCondition">stardust::storage_deposit_return_unlock_condition::StorageDepositReturnUnlockCondition</a>&gt;</code>
</dt>
<dd>
 The storage deposit return unlock condition.
</dd>
<dt>
<code>timelock_uc: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_TimelockUnlockCondition">stardust::timelock_unlock_condition::TimelockUnlockCondition</a>&gt;</code>
</dt>
<dd>
 The timelock unlock condition.
</dd>
<dt>
<code>expiration_uc: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/stardust/expiration_unlock_condition.md#stardust_expiration_unlock_condition_ExpirationUnlockCondition">stardust::expiration_unlock_condition::ExpirationUnlockCondition</a>&gt;</code>
</dt>
<dd>
 The expiration unlock condition.
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="stardust_nft_output_NFT_NAME"></a>

The NFT dynamic field name.


<pre><code><b>const</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NFT_NAME">NFT_NAME</a>: vector&lt;u8&gt; = vector[110, 102, 116];
</code></pre>



<a name="stardust_nft_output_extract_assets"></a>

## Function `extract_assets`

The function extracts assets from a legacy NFT output.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_extract_assets">extract_assets</a>&lt;T&gt;(output: <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">stardust::nft_output::NftOutput</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;, <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a>, <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_extract_assets">extract_assets</a>&lt;T&gt;(
    <b>mut</b> output: <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">NftOutput</a>&lt;T&gt;,
    ctx: &<b>mut</b> TxContext,
): (Balance&lt;T&gt;, Bag, Nft) {
    // Load the related Nft object.
    <b>let</b> nft = <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_load_nft">load_nft</a>(&<b>mut</b> output);
    // Unpuck the output.
    <b>let</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">NftOutput</a> {
        id,
        balance: <b>mut</b> balance,
        native_tokens,
        storage_deposit_return_uc: <b>mut</b> storage_deposit_return_uc,
        timelock_uc: <b>mut</b> timelock_uc,
        expiration_uc: <b>mut</b> expiration_uc,
    } = output;
    // If the output <b>has</b> a timelock unlock condition, then we need to check <b>if</b> the timelock_uc <b>has</b> expired.
    <b>if</b> (timelock_uc.is_some()) {
        timelock_uc.extract().unlock(ctx);
    };
    // If the output <b>has</b> an expiration unlock condition, then we need to check who can unlock the output.
    <b>if</b> (expiration_uc.is_some()) {
        expiration_uc.extract().unlock(ctx);
    };
    // If the output <b>has</b> a storage deposit <b>return</b> unlock condition, then we need to <b>return</b> the deposit.
    <b>if</b> (storage_deposit_return_uc.is_some()) {
        storage_deposit_return_uc.extract().unlock(&<b>mut</b> balance, ctx);
    };
    // Destroy the output.
    option::destroy_none(timelock_uc);
    option::destroy_none(expiration_uc);
    option::destroy_none(storage_deposit_return_uc);
    object::delete(id);
    <b>return</b> (balance, native_tokens, nft)
}
</code></pre>



</details>

<a name="stardust_nft_output_load_nft"></a>

## Function `load_nft`

Loads the related <code>Nft</code> object.


<pre><code><b>fun</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_load_nft">load_nft</a>&lt;T&gt;(output: &<b>mut</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">stardust::nft_output::NftOutput</a>&lt;T&gt;): <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_load_nft">load_nft</a>&lt;T&gt;(output: &<b>mut</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">NftOutput</a>&lt;T&gt;): Nft {
    dynamic_object_field::remove(&<b>mut</b> output.id, <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NFT_NAME">NFT_NAME</a>)
}
</code></pre>



</details>

<a name="stardust_nft_output_attach_nft"></a>

## Function `attach_nft`

Utility function to attach an <code>Nft</code> to an <code><a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">NftOutput</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_attach_nft">attach_nft</a>&lt;T&gt;(output: &<b>mut</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">stardust::nft_output::NftOutput</a>&lt;T&gt;, nft: <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_attach_nft">attach_nft</a>&lt;T&gt;(output: &<b>mut</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">NftOutput</a>&lt;T&gt;, nft: Nft) {
    dynamic_object_field::add(&<b>mut</b> output.id, <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NFT_NAME">NFT_NAME</a>, nft)
}
</code></pre>



</details>

<a name="stardust_nft_output_receive"></a>

## Function `receive`

Utility function to receive an <code><a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">NftOutput</a></code> in other Stardust modules.
Other modules in the stardust package can call this function to receive an <code><a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">NftOutput</a></code> (alias).


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_receive">receive</a>&lt;T&gt;(parent: &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>, nft: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;<a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">stardust::nft_output::NftOutput</a>&lt;T&gt;&gt;): <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">stardust::nft_output::NftOutput</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_receive">receive</a>&lt;T&gt;(parent: &<b>mut</b> UID, nft: Receiving&lt;<a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">NftOutput</a>&lt;T&gt;&gt;): <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">NftOutput</a>&lt;T&gt; {
    transfer::receive(parent, nft)
}
</code></pre>



</details>
