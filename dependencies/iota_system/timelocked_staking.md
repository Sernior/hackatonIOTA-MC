
<a name="iota_system_timelocked_staking"></a>

# Module `iota_system::timelocked_staking`



-  [Struct `TimelockedStakedIota`](#iota_system_timelocked_staking_TimelockedStakedIota)
-  [Constants](#@Constants_0)
-  [Function `request_add_stake`](#iota_system_timelocked_staking_request_add_stake)
-  [Function `request_add_stake_mul_bal`](#iota_system_timelocked_staking_request_add_stake_mul_bal)
-  [Function `request_withdraw_stake`](#iota_system_timelocked_staking_request_withdraw_stake)
-  [Function `request_add_stake_non_entry`](#iota_system_timelocked_staking_request_add_stake_non_entry)
-  [Function `request_add_stake_mul_bal_non_entry`](#iota_system_timelocked_staking_request_add_stake_mul_bal_non_entry)
-  [Function `request_withdraw_stake_non_entry`](#iota_system_timelocked_staking_request_withdraw_stake_non_entry)
-  [Function `unlock`](#iota_system_timelocked_staking_unlock)
-  [Function `unlock_with_clock`](#iota_system_timelocked_staking_unlock_with_clock)
-  [Function `split`](#iota_system_timelocked_staking_split)
-  [Function `split_staked_iota`](#iota_system_timelocked_staking_split_staked_iota)
-  [Function `join_staked_iota`](#iota_system_timelocked_staking_join_staked_iota)
-  [Function `transfer_to_sender`](#iota_system_timelocked_staking_transfer_to_sender)
-  [Function `transfer_to_sender_multiple`](#iota_system_timelocked_staking_transfer_to_sender_multiple)
-  [Function `is_equal_staking_metadata`](#iota_system_timelocked_staking_is_equal_staking_metadata)
-  [Function `pool_id`](#iota_system_timelocked_staking_pool_id)
-  [Function `staked_iota_amount`](#iota_system_timelocked_staking_staked_iota_amount)
-  [Function `stake_activation_epoch`](#iota_system_timelocked_staking_stake_activation_epoch)
-  [Function `expiration_timestamp_ms`](#iota_system_timelocked_staking_expiration_timestamp_ms)
-  [Function `label`](#iota_system_timelocked_staking_label)
-  [Function `is_labeled_with`](#iota_system_timelocked_staking_is_labeled_with)
-  [Function `unpack`](#iota_system_timelocked_staking_unpack)
-  [Function `transfer`](#iota_system_timelocked_staking_transfer)
-  [Function `transfer_multiple`](#iota_system_timelocked_staking_transfer_multiple)
-  [Function `request_add_stake_at_genesis`](#iota_system_timelocked_staking_request_add_stake_at_genesis)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../../dependencies/iota/clock.md#iota_clock">iota::clock</a>;
<b>use</b> <a href="../../dependencies/iota/coin.md#iota_coin">iota::coin</a>;
<b>use</b> <a href="../../dependencies/iota/config.md#iota_config">iota::config</a>;
<b>use</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list">iota::deny_list</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/iota.md#iota_iota">iota::iota</a>;
<b>use</b> <a href="../../dependencies/iota/labeler.md#iota_labeler">iota::labeler</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/pay.md#iota_pay">iota::pay</a>;
<b>use</b> <a href="../../dependencies/iota/priority_queue.md#iota_priority_queue">iota::priority_queue</a>;
<b>use</b> <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap">iota::system_admin_cap</a>;
<b>use</b> <a href="../../dependencies/iota/table.md#iota_table">iota::table</a>;
<b>use</b> <a href="../../dependencies/iota/table_vec.md#iota_table_vec">iota::table_vec</a>;
<b>use</b> <a href="../../dependencies/iota/timelock.md#iota_timelock">iota::timelock</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/iota/vec_set.md#iota_vec_set">iota::vec_set</a>;
<b>use</b> <a href="../../dependencies/iota/versioned.md#iota_versioned">iota::versioned</a>;
<b>use</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system">iota_system::iota_system</a>;
<b>use</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner">iota_system::iota_system_state_inner</a>;
<b>use</b> <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool">iota_system::staking_pool</a>;
<b>use</b> <a href="../../dependencies/iota_system/storage_fund.md#iota_system_storage_fund">iota_system::storage_fund</a>;
<b>use</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator">iota_system::validator</a>;
<b>use</b> <a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap">iota_system::validator_cap</a>;
<b>use</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set">iota_system::validator_set</a>;
<b>use</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper">iota_system::validator_wrapper</a>;
<b>use</b> <a href="../../dependencies/iota_system/voting_power.md#iota_system_voting_power">iota_system::voting_power</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/u64.md#std_u64">std::u64</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_system_timelocked_staking_TimelockedStakedIota"></a>

## Struct `TimelockedStakedIota`

A self-custodial object holding the timelocked staked IOTA tokens.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a> <b>has</b> key
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
<code>staked_iota: <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a></code>
</dt>
<dd>
 A self-custodial object holding the staked IOTA tokens.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64</code>
</dt>
<dd>
 This is the epoch time stamp of when the lock expires.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
 Timelock related label.
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_system_timelocked_staking_ETimeLockShouldNotBeExpired"></a>

For when trying to stake an expired time-locked balance.


<pre><code><b>const</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_ETimeLockShouldNotBeExpired">ETimeLockShouldNotBeExpired</a>: u64 = 0;
</code></pre>



<a name="iota_system_timelocked_staking_EIncompatibleTimelockedStakedIota"></a>

Incompatible objects when joining <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code>.


<pre><code><b>const</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_EIncompatibleTimelockedStakedIota">EIncompatibleTimelockedStakedIota</a>: u64 = 1;
</code></pre>



<a name="iota_system_timelocked_staking_ETimelockedStakedIotaShouldBeExpired"></a>



<pre><code>#[error]
<b>const</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_ETimelockedStakedIotaShouldBeExpired">ETimelockedStakedIotaShouldBeExpired</a>: vector&lt;u8&gt; = b"<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a> is not expired.";
</code></pre>



<a name="iota_system_timelocked_staking_request_add_stake"></a>

## Function `request_add_stake`

Add a time-locked stake to a validator's staking pool.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake">request_add_stake</a>(iota_system: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, timelocked_balance: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;&gt;, validator_address: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake">request_add_stake</a>(
    iota_system: &<b>mut</b> IotaSystemState,
    timelocked_balance: TimeLock&lt;Balance&lt;IOTA&gt;&gt;,
    validator_address: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
) {
    // Stake the time-locked balance.
    <b>let</b> timelocked_staked_iota = <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_non_entry">request_add_stake_non_entry</a>(
        iota_system,
        timelocked_balance,
        validator_address,
        ctx,
    );
    // Transfer the receipt to the sender.
    timelocked_staked_iota.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer_to_sender">transfer_to_sender</a>(ctx);
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_request_add_stake_mul_bal"></a>

## Function `request_add_stake_mul_bal`

Add a time-locked stake to a validator's staking pool using multiple time-locked balances.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_mul_bal">request_add_stake_mul_bal</a>(iota_system: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, timelocked_balances: vector&lt;<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;&gt;&gt;, validator_address: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_mul_bal">request_add_stake_mul_bal</a>(
    iota_system: &<b>mut</b> IotaSystemState,
    timelocked_balances: vector&lt;TimeLock&lt;Balance&lt;IOTA&gt;&gt;&gt;,
    validator_address: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
) {
    // Stake the time-locked balances.
    <b>let</b> <b>mut</b> receipts = <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_mul_bal_non_entry">request_add_stake_mul_bal_non_entry</a>(
        iota_system,
        timelocked_balances,
        validator_address,
        ctx,
    );
    // Create useful variables.
    <b>let</b> (<b>mut</b> i, len) = (0, receipts.length());
    // Send all the receipts to the sender.
    <b>while</b> (i &lt; len) {
        // Take a receipt.
        <b>let</b> receipt = receipts.pop_back();
        // Transfer the receipt to the sender.
        receipt.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer_to_sender">transfer_to_sender</a>(ctx);
        i = i + 1
    };
    // Destroy the empty vector.
    vector::destroy_empty(receipts)
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_request_withdraw_stake"></a>

## Function `request_withdraw_stake`

Withdraw a time-locked stake from a validator's staking pool.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_withdraw_stake">request_withdraw_stake</a>(iota_system: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, timelocked_staked_iota: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_withdraw_stake">request_withdraw_stake</a>(
    iota_system: &<b>mut</b> IotaSystemState,
    timelocked_staked_iota: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>,
    ctx: &<b>mut</b> TxContext,
) {
    // Withdraw the time-locked balance.
    <b>let</b> (timelocked_balance, reward) = <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_withdraw_stake_non_entry">request_withdraw_stake_non_entry</a>(
        iota_system,
        timelocked_staked_iota,
        ctx,
    );
    // Transfer the withdrawn time-locked balance to the sender.
    timelocked_balance.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer_to_sender">transfer_to_sender</a>(ctx);
    // Send coins only <b>if</b> the reward is not zero.
    <b>if</b> (reward.value() &gt; 0) {
        transfer::public_transfer(reward.into_coin(ctx), ctx.sender());
    } <b>else</b> {
        balance::destroy_zero(reward);
    }
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_request_add_stake_non_entry"></a>

## Function `request_add_stake_non_entry`

The non-entry version of <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake">request_add_stake</a></code>, which returns the time-locked staked IOTA instead of transferring it to the sender.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_non_entry">request_add_stake_non_entry</a>(iota_system: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, timelocked_balance: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;&gt;, validator_address: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_non_entry">request_add_stake_non_entry</a>(
    iota_system: &<b>mut</b> IotaSystemState,
    timelocked_balance: TimeLock&lt;Balance&lt;IOTA&gt;&gt;,
    validator_address: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a> {
    // Check the preconditions.
    <b>assert</b>!(timelocked_balance.is_locked(ctx), <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_ETimeLockShouldNotBeExpired">ETimeLockShouldNotBeExpired</a>);
    // Unpack the time-locked balance.
    <b>let</b> sys_admin_cap = iota_system.load_iota_system_admin_cap();
    <b>let</b> (balance, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>) = timelock::system_unpack(
        sys_admin_cap,
        timelocked_balance,
    );
    // Stake the time-locked balance.
    <b>let</b> staked_iota = iota_system.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_non_entry">request_add_stake_non_entry</a>(
        balance.into_coin(ctx),
        validator_address,
        ctx,
    );
    // Create and <b>return</b> a receipt.
    <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a> {
        id: object::new(ctx),
        staked_iota,
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>,
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>,
    }
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_request_add_stake_mul_bal_non_entry"></a>

## Function `request_add_stake_mul_bal_non_entry`

The non-entry version of <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_mul_bal">request_add_stake_mul_bal</a></code>,
which returns a list of the time-locked staked IOTAs instead of transferring them to the sender.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_mul_bal_non_entry">request_add_stake_mul_bal_non_entry</a>(iota_system: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, timelocked_balances: vector&lt;<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;&gt;&gt;, validator_address: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): vector&lt;<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_mul_bal_non_entry">request_add_stake_mul_bal_non_entry</a>(
    iota_system: &<b>mut</b> IotaSystemState,
    <b>mut</b> timelocked_balances: vector&lt;TimeLock&lt;Balance&lt;IOTA&gt;&gt;&gt;,
    validator_address: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
): vector&lt;<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>&gt; {
    // Create a vector to store the results.
    <b>let</b> <b>mut</b> result = vector[];
    // Create useful variables.
    <b>let</b> (<b>mut</b> i, len) = (0, timelocked_balances.length());
    // Stake all the time-locked balances.
    <b>while</b> (i &lt; len) {
        // Take a time-locked balance.
        <b>let</b> timelocked_balance = timelocked_balances.pop_back();
        // Stake the time-locked balance.
        <b>let</b> timelocked_staked_iota = <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_non_entry">request_add_stake_non_entry</a>(
            iota_system,
            timelocked_balance,
            validator_address,
            ctx,
        );
        // Store the created receipt.
        result.push_back(timelocked_staked_iota);
        i = i + 1
    };
    // Destroy the empty vector.
    vector::destroy_empty(timelocked_balances);
    result
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_request_withdraw_stake_non_entry"></a>

## Function `request_withdraw_stake_non_entry`

Non-entry version of <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_withdraw_stake">request_withdraw_stake</a></code> that returns the withdrawn time-locked IOTA and reward
instead of transferring it to the sender.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_withdraw_stake_non_entry">request_withdraw_stake_non_entry</a>(iota_system: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, timelocked_staked_iota: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;&gt;, <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_withdraw_stake_non_entry">request_withdraw_stake_non_entry</a>(
    iota_system: &<b>mut</b> IotaSystemState,
    timelocked_staked_iota: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>,
    ctx: &<b>mut</b> TxContext,
): (TimeLock&lt;Balance&lt;IOTA&gt;&gt;, Balance&lt;IOTA&gt;) {
    // Unpack the `<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>` instance.
    <b>let</b> (staked_iota, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>) = timelocked_staked_iota.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_unpack">unpack</a>();
    // Store the original stake amount.
    <b>let</b> principal = staked_iota.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_staked_iota_amount">staked_iota_amount</a>();
    // Withdraw the balance.
    <b>let</b> <b>mut</b> withdraw_stake = iota_system.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_withdraw_stake_non_entry">request_withdraw_stake_non_entry</a>(staked_iota, ctx);
    // The iota_system withdraw functions <b>return</b> a balance that consists of the original staked amount plus the reward amount;
    // In here, it splits the original staked balance to timelock it again.
    <b>let</b> principal = withdraw_stake.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_split">split</a>(principal);
    // Pack and <b>return</b> a time-locked balance, and the reward.
    <b>let</b> sys_admin_cap = iota_system.load_iota_system_admin_cap();
    (
        timelock::system_pack(sys_admin_cap, principal, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>, ctx),
        withdraw_stake,
    )
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_unlock"></a>

## Function `unlock`

Unlock the <code>StakedIota</code> from a <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code>  based on the epoch start time.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_unlock">unlock</a>(self: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_unlock">unlock</a>(self: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>, ctx: &TxContext): StakedIota {
    // Unpack the `<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>`.
    <b>let</b> (staked, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>, _) = <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_unpack">unpack</a>(self);
    // Check <b>if</b> the lock <b>has</b> expired.
    <b>assert</b>!(
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a> &lt;= ctx.epoch_timestamp_ms(),
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_ETimelockedStakedIotaShouldBeExpired">ETimelockedStakedIotaShouldBeExpired</a>,
    );
    staked
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_unlock_with_clock"></a>

## Function `unlock_with_clock`

Unlock the <code>StakedIota</code> from a <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code> based on the <code>Clock</code> object.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_unlock_with_clock">unlock_with_clock</a>(self: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_unlock_with_clock">unlock_with_clock</a>(self: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>, clock: &Clock): StakedIota {
    // Unpack the `<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>`.
    <b>let</b> (staked, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>, _) = <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_unpack">unpack</a>(self);
    // Check <b>if</b> the lock <b>has</b> expired.
    <b>assert</b>!(<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a> &lt;= clock.timestamp_ms(), <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_ETimelockedStakedIotaShouldBeExpired">ETimelockedStakedIotaShouldBeExpired</a>);
    staked
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_split"></a>

## Function `split`

Split <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code> into two parts, one with principal <code>split_amount</code>,
and the remaining principal is left in <code>self</code>.
All the other parameters of the <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code> like <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_stake_activation_epoch">stake_activation_epoch</a></code> or <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_pool_id">pool_id</a></code> remain the same.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_split">split</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>, split_amount: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_split">split</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>,
    split_amount: u64,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a> {
    <b>let</b> split_stake = self.staked_iota.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_split">split</a>(split_amount, ctx);
    <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a> {
        id: object::new(ctx),
        staked_iota: split_stake,
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>: self.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>,
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>: self.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>,
    }
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_split_staked_iota"></a>

## Function `split_staked_iota`

Split the given <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code> to the two parts, one with principal <code>split_amount</code>,
transfer the newly split part to the sender address.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_split_staked_iota">split_staked_iota</a>(stake: &<b>mut</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>, split_amount: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_split_staked_iota">split_staked_iota</a>(
    stake: &<b>mut</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>,
    split_amount: u64,
    ctx: &<b>mut</b> TxContext,
) {
    <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_split">split</a>(stake, split_amount, ctx).<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer_to_sender">transfer_to_sender</a>(ctx);
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_join_staked_iota"></a>

## Function `join_staked_iota`

Consume the staked iota <code>other</code> and add its value to <code>self</code>.
Aborts if some of the staking parameters are incompatible (pool id, stake activation epoch, etc.)


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_join_staked_iota">join_staked_iota</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>, other: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_join_staked_iota">join_staked_iota</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>, other: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>) {
    <b>assert</b>!(self.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_is_equal_staking_metadata">is_equal_staking_metadata</a>(&other), <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_EIncompatibleTimelockedStakedIota">EIncompatibleTimelockedStakedIota</a>);
    <b>let</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a> {
        id,
        staked_iota,
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>: _,
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>: _,
    } = other;
    id.delete();
    self.staked_iota.join(staked_iota);
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_transfer_to_sender"></a>

## Function `transfer_to_sender`

A utility function to transfer a <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer_to_sender">transfer_to_sender</a>(stake: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer_to_sender">transfer_to_sender</a>(stake: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>, ctx: &TxContext) {
    <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer">transfer</a>(stake, ctx.sender())
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_transfer_to_sender_multiple"></a>

## Function `transfer_to_sender_multiple`

A utility function to transfer multiple <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer_to_sender_multiple">transfer_to_sender_multiple</a>(stakes: vector&lt;<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer_to_sender_multiple">transfer_to_sender_multiple</a>(stakes: vector&lt;<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>&gt;, ctx: &TxContext) {
    <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer_multiple">transfer_multiple</a>(stakes, ctx.sender())
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_is_equal_staking_metadata"></a>

## Function `is_equal_staking_metadata`

A utility function that returns true if all the staking parameters
of the staked iota except the principal are identical


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_is_equal_staking_metadata">is_equal_staking_metadata</a>(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>, other: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_is_equal_staking_metadata">is_equal_staking_metadata</a>(
    self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>,
    other: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>,
): bool {
    self.staked_iota.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_is_equal_staking_metadata">is_equal_staking_metadata</a>(&other.staked_iota) &&
        (self.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a> == other.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>) &&
        (self.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>() == other.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>())
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_pool_id"></a>

## Function `pool_id`

Function to get the pool id of a <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_pool_id">pool_id</a>(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_pool_id">pool_id</a>(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>): ID { self.staked_iota.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_pool_id">pool_id</a>() }
</code></pre>



</details>

<a name="iota_system_timelocked_staking_staked_iota_amount"></a>

## Function `staked_iota_amount`

Function to get the staked iota amount of a <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_staked_iota_amount">staked_iota_amount</a>(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_staked_iota_amount">staked_iota_amount</a>(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>): u64 {
    self.staked_iota.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_staked_iota_amount">staked_iota_amount</a>()
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_stake_activation_epoch"></a>

## Function `stake_activation_epoch`

Function to get the stake activation epoch of a <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_stake_activation_epoch">stake_activation_epoch</a>(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_stake_activation_epoch">stake_activation_epoch</a>(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>): u64 {
    self.staked_iota.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_stake_activation_epoch">stake_activation_epoch</a>()
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_expiration_timestamp_ms"></a>

## Function `expiration_timestamp_ms`

Function to get the expiration timestamp of a <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>): u64 {
    self.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_label"></a>

## Function `label`

Function to get the label of a <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>): Option&lt;String&gt; {
    self.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_is_labeled_with"></a>

## Function `is_labeled_with`

Check if a <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code> is labeled with the type <code>L</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_is_labeled_with">is_labeled_with</a>&lt;L&gt;(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_is_labeled_with">is_labeled_with</a>&lt;L&gt;(self: &<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>): bool {
    <b>if</b> (self.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>.is_some()) {
        self.<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>.borrow() == timelock::type_name&lt;L&gt;()
    } <b>else</b> {
        <b>false</b>
    }
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_unpack"></a>

## Function `unpack`

A utility function to destroy a <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code>.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_unpack">unpack</a>(self: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>): (<a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a>, u64, <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_unpack">unpack</a>(self: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>): (StakedIota, u64, Option&lt;String&gt;) {
    <b>let</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a> {
        id,
        staked_iota,
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>,
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>,
    } = self;
    object::delete(id);
    (staked_iota, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>)
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_transfer"></a>

## Function `transfer`

A utility function to transfer a <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code> to a receiver.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer">transfer</a>(stake: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>, receiver: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer">transfer</a>(stake: <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>, receiver: <b>address</b>) {
    transfer::transfer(stake, receiver);
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_transfer_multiple"></a>

## Function `transfer_multiple`

A utility function to transfer a vector of <code><a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a></code> to a receiver.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer_multiple">transfer_multiple</a>(stakes: vector&lt;<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">iota_system::timelocked_staking::TimelockedStakedIota</a>&gt;, receiver: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer_multiple">transfer_multiple</a>(<b>mut</b> stakes: vector&lt;<a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a>&gt;, receiver: <b>address</b>) {
    // Transfer all the time-locked stakes to the recipient.
    <b>while</b> (!stakes.is_empty()) {
        <b>let</b> stake = stakes.pop_back();
        transfer::transfer(stake, receiver);
    };
    // Destroy the empty vector.
    vector::destroy_empty(stakes);
}
</code></pre>



</details>

<a name="iota_system_timelocked_staking_request_add_stake_at_genesis"></a>

## Function `request_add_stake_at_genesis`

Request to add timelocked stake to the validator's staking pool at genesis


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_at_genesis">request_add_stake_at_genesis</a>(validator: &<b>mut</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>, stake: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, staker_address: <b>address</b>, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64, <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_request_add_stake_at_genesis">request_add_stake_at_genesis</a>(
    validator: &<b>mut</b> ValidatorV1,
    stake: Balance&lt;IOTA&gt;,
    staker_address: <b>address</b>,
    <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64,
    <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>: Option&lt;String&gt;,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> staked_iota = validator.request_add_stake_at_genesis_with_receipt(stake, ctx);
    <b>let</b> timelocked_staked_iota = <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_TimelockedStakedIota">TimelockedStakedIota</a> {
        id: object::new(ctx),
        staked_iota,
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_expiration_timestamp_ms">expiration_timestamp_ms</a>,
        <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_label">label</a>,
    };
    <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking_transfer">transfer</a>(timelocked_staked_iota, staker_address);
}
</code></pre>



</details>
