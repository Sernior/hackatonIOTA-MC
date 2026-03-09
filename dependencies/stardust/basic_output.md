
<a name="stardust_basic_output"></a>

# Module `stardust::basic_output`



-  [Struct `BasicOutput`](#stardust_basic_output_BasicOutput)
-  [Function `extract_assets`](#stardust_basic_output_extract_assets)
-  [Function `receive`](#stardust_basic_output_receive)


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
<b>use</b> <a href="../../dependencies/stardust/expiration_unlock_condition.md#stardust_expiration_unlock_condition">stardust::expiration_unlock_condition</a>;
<b>use</b> <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition">stardust::storage_deposit_return_unlock_condition</a>;
<b>use</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition">stardust::timelock_unlock_condition</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="stardust_basic_output_BasicOutput"></a>

## Struct `BasicOutput`

A basic output that has unlock conditions/features.
- basic outputs with expiration unlock condition must be a shared object, since that's the only
way to handle the two possible addresses that can unlock the output.
- notice that there is no <code>store</code> ability and there is no custom transfer function:
-  you can call <code><a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_extract_assets">extract_assets</a></code>,
-  or you can call <code><a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_receive">receive</a></code> in other models to receive a <code><a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">BasicOutput</a></code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">BasicOutput</a>&lt;<b>phantom</b> T&gt; <b>has</b> key
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
 Hash of the <code>outputId</code> that was migrated.
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
<dt>
<code>metadata: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;</code>
</dt>
<dd>
 The metadata feature.
</dd>
<dt>
<code>tag: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;</code>
</dt>
<dd>
 The tag feature.
</dd>
<dt>
<code>sender: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;</code>
</dt>
<dd>
 The sender feature.
</dd>
</dl>


</details>

<a name="stardust_basic_output_extract_assets"></a>

## Function `extract_assets`

Extract the assets stored inside the output, respecting the unlock conditions.
- The object will be deleted.
- The <code>StorageDepositReturnUnlockCondition</code> will return the deposit.
- Remaining assets (coins and native tokens) will be returned.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_extract_assets">extract_assets</a>&lt;T&gt;(output: <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">stardust::basic_output::BasicOutput</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;, <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_extract_assets">extract_assets</a>&lt;T&gt;(output: <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">BasicOutput</a>&lt;T&gt;, ctx: &<b>mut</b> TxContext): (Balance&lt;T&gt;, Bag) {
    // Unpack the output into its basic part.
    <b>let</b> <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">BasicOutput</a> {
        id,
        balance: <b>mut</b> balance,
        native_tokens,
        storage_deposit_return_uc: <b>mut</b> storage_deposit_return_uc,
        timelock_uc: <b>mut</b> timelock_uc,
        expiration_uc: <b>mut</b> expiration_uc,
        sender: _,
        metadata: _,
        tag: _,
    } = output;
    // If the output <b>has</b> a timelock unlock condition, then we need to check <b>if</b> the timelock_uc <b>has</b> expired.
    <b>if</b> (timelock_uc.is_some()) {
        timelock_uc.extract().unlock(ctx);
    };
    // If the output <b>has</b> an expiration unlock condition, then we need to check who can unlock the output.
    <b>if</b> (expiration_uc.is_some()) {
        expiration_uc.extract().unlock(ctx);
    };
    // If the output <b>has</b> an storage deposit <b>return</b> unlock condition, then we need to <b>return</b> the deposit.
    <b>if</b> (storage_deposit_return_uc.is_some()) {
        storage_deposit_return_uc.extract().unlock(&<b>mut</b> balance, ctx);
    };
    // Destroy the unlock conditions.
    option::destroy_none(timelock_uc);
    option::destroy_none(expiration_uc);
    option::destroy_none(storage_deposit_return_uc);
    // Delete the output.
    object::delete(id);
    <b>return</b> (balance, native_tokens)
}
</code></pre>



</details>

<a name="stardust_basic_output_receive"></a>

## Function `receive`

Utility function to receive a basic output in other stardust modules.
Since <code><a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">BasicOutput</a></code> only has <code>key</code>, it can not be received via <code>public_receive</code>.
The private receiver must be implemented in its defining module (here).
Other modules in the Stardust package can call this function to receive a basic output (alias, NFT).


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_receive">receive</a>&lt;T&gt;(parent: &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>, output: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;<a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">stardust::basic_output::BasicOutput</a>&lt;T&gt;&gt;): <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">stardust::basic_output::BasicOutput</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_receive">receive</a>&lt;T&gt;(
    parent: &<b>mut</b> UID,
    output: Receiving&lt;<a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">BasicOutput</a>&lt;T&gt;&gt;,
): <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">BasicOutput</a>&lt;T&gt; {
    transfer::receive(parent, output)
}
</code></pre>



</details>
