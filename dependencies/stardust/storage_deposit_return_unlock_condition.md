
<a name="stardust_storage_deposit_return_unlock_condition"></a>

# Module `stardust::storage_deposit_return_unlock_condition`



-  [Struct `StorageDepositReturnUnlockCondition`](#stardust_storage_deposit_return_unlock_condition_StorageDepositReturnUnlockCondition)
-  [Function `unlock`](#stardust_storage_deposit_return_unlock_condition_unlock)
-  [Function `return_address`](#stardust_storage_deposit_return_unlock_condition_return_address)
-  [Function `return_amount`](#stardust_storage_deposit_return_unlock_condition_return_amount)


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



<a name="stardust_storage_deposit_return_unlock_condition_StorageDepositReturnUnlockCondition"></a>

## Struct `StorageDepositReturnUnlockCondition`

The Stardust storage deposit return unlock condition.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_StorageDepositReturnUnlockCondition">StorageDepositReturnUnlockCondition</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_address">return_address</a>: <b>address</b></code>
</dt>
<dd>
 The address to which the consuming transaction should deposit the amount defined in Return Amount.
</dd>
<dt>
<code><a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_amount">return_amount</a>: u64</code>
</dt>
<dd>
 The amount of coins the consuming transaction should deposit to the address defined in Return Address.
</dd>
</dl>


</details>

<a name="stardust_storage_deposit_return_unlock_condition_unlock"></a>

## Function `unlock`

Check the unlock condition.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_unlock">unlock</a>&lt;T&gt;(condition: <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_StorageDepositReturnUnlockCondition">stardust::storage_deposit_return_unlock_condition::StorageDepositReturnUnlockCondition</a>, funding: &<b>mut</b> <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_unlock">unlock</a>&lt;T&gt;(
    condition: <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_StorageDepositReturnUnlockCondition">StorageDepositReturnUnlockCondition</a>,
    funding: &<b>mut</b> Balance&lt;T&gt;,
    ctx: &<b>mut</b> TxContext,
) {
    // Aborts <b>if</b> `funding` is not enough.
    <b>let</b> return_balance = funding.split(condition.<a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_amount">return_amount</a>());
    // Recipient will need to transfer the coin to a normal ed25519 <b>address</b> instead of legacy.
    public_transfer(from_balance(return_balance, ctx), condition.<a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_address">return_address</a>());
    <b>let</b> <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_StorageDepositReturnUnlockCondition">StorageDepositReturnUnlockCondition</a> {
        <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_address">return_address</a>: _,
        <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_amount">return_amount</a>: _,
    } = condition;
}
</code></pre>



</details>

<a name="stardust_storage_deposit_return_unlock_condition_return_address"></a>

## Function `return_address`

Get the unlock condition's <code><a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_address">return_address</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_address">return_address</a>(condition: &<a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_StorageDepositReturnUnlockCondition">stardust::storage_deposit_return_unlock_condition::StorageDepositReturnUnlockCondition</a>): <b>address</b>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_address">return_address</a>(condition: &<a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_StorageDepositReturnUnlockCondition">StorageDepositReturnUnlockCondition</a>): <b>address</b> {
    condition.<a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_address">return_address</a>
}
</code></pre>



</details>

<a name="stardust_storage_deposit_return_unlock_condition_return_amount"></a>

## Function `return_amount`

Get the unlock condition's <code><a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_amount">return_amount</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_amount">return_amount</a>(condition: &<a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_StorageDepositReturnUnlockCondition">stardust::storage_deposit_return_unlock_condition::StorageDepositReturnUnlockCondition</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_amount">return_amount</a>(condition: &<a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_StorageDepositReturnUnlockCondition">StorageDepositReturnUnlockCondition</a>): u64 {
    condition.<a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition_return_amount">return_amount</a>
}
</code></pre>



</details>
