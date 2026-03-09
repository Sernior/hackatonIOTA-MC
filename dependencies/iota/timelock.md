
<a name="iota_timelock"></a>

# Module `iota::timelock`

A timelock implementation.


-  [Struct `TimeLock`](#iota_timelock_TimeLock)
-  [Constants](#@Constants_0)
-  [Function `lock`](#iota_timelock_lock)
-  [Function `lock_with_label`](#iota_timelock_lock_with_label)
-  [Function `lock_and_transfer`](#iota_timelock_lock_and_transfer)
-  [Function `lock_with_label_and_transfer`](#iota_timelock_lock_with_label_and_transfer)
-  [Function `unlock`](#iota_timelock_unlock)
-  [Function `unlock_with_clock`](#iota_timelock_unlock_with_clock)
-  [Function `join`](#iota_timelock_join)
-  [Function `join_vec`](#iota_timelock_join_vec)
-  [Function `split`](#iota_timelock_split)
-  [Function `split_balance`](#iota_timelock_split_balance)
-  [Function `transfer_to_sender`](#iota_timelock_transfer_to_sender)
-  [Function `system_pack`](#iota_timelock_system_pack)
-  [Function `system_unpack`](#iota_timelock_system_unpack)
-  [Function `type_name`](#iota_timelock_type_name)
-  [Function `expiration_timestamp_ms`](#iota_timelock_expiration_timestamp_ms)
-  [Function `is_locked`](#iota_timelock_is_locked)
-  [Function `remaining_time`](#iota_timelock_remaining_time)
-  [Function `is_locked_with_clock`](#iota_timelock_is_locked_with_clock)
-  [Function `remaining_time_with_clock`](#iota_timelock_remaining_time_with_clock)
-  [Function `locked`](#iota_timelock_locked)
-  [Function `label`](#iota_timelock_label)
-  [Function `is_labeled_with`](#iota_timelock_is_labeled_with)
-  [Function `pack`](#iota_timelock_pack)
-  [Function `unpack`](#iota_timelock_unpack)
-  [Function `transfer`](#iota_timelock_transfer)
-  [Function `remaining_time_with_timestamp`](#iota_timelock_remaining_time_with_timestamp)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../../dependencies/iota/clock.md#iota_clock">iota::clock</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/labeler.md#iota_labeler">iota::labeler</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap">iota::system_admin_cap</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_timelock_TimeLock"></a>

## Struct `TimeLock`

<code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> struct that holds a locked object.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T: store&gt; <b>has</b> key
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
<code><a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>: T</code>
</dt>
<dd>
 The locked object.
</dd>
<dt>
<code><a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64</code>
</dt>
<dd>
 This is the epoch time stamp of when the lock expires.
</dd>
<dt>
<code><a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
 Timelock related label.
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_timelock_ENotExpiredYet"></a>

The lock has not expired yet.


<pre><code><b>const</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_ENotExpiredYet">ENotExpiredYet</a>: u64 = 1;
</code></pre>



<a name="iota_timelock_EDifferentExpirationTime"></a>

For when trying to join two time-locked balances with different expiration time.


<pre><code><b>const</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_EDifferentExpirationTime">EDifferentExpirationTime</a>: u64 = 2;
</code></pre>



<a name="iota_timelock_EDifferentLabels"></a>

For when trying to join two time-locked balances with different labels.


<pre><code><b>const</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_EDifferentLabels">EDifferentLabels</a>: u64 = 3;
</code></pre>



<a name="iota_timelock_lock"></a>

## Function `lock`

Function to lock an object till a unix timestamp in milliseconds.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>&lt;T: store&gt;(<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>: T, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>&lt;T: store&gt;(
    <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>: T,
    <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt; {
    // Create a timelock.
    <a href="../../dependencies/iota/timelock.md#iota_timelock_pack">pack</a>(<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>, option::none(), ctx)
}
</code></pre>



</details>

<a name="iota_timelock_lock_with_label"></a>

## Function `lock_with_label`

Function to lock a labeled object till a unix timestamp in milliseconds.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_lock_with_label">lock_with_label</a>&lt;T: store, L&gt;(_: &<a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">iota::labeler::LabelerCap</a>&lt;L&gt;, <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>: T, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_lock_with_label">lock_with_label</a>&lt;T: store, L&gt;(
    _: &LabelerCap&lt;L&gt;,
    <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>: T,
    <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt; {
    // Calculate a <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a> value.
    <b>let</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a> = <a href="../../dependencies/iota/timelock.md#iota_timelock_type_name">type_name</a>&lt;L&gt;();
    // Create a labeled timelock.
    <a href="../../dependencies/iota/timelock.md#iota_timelock_pack">pack</a>(<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>, option::some(<a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>), ctx)
}
</code></pre>



</details>

<a name="iota_timelock_lock_and_transfer"></a>

## Function `lock_and_transfer`

Function to lock an object <code>obj</code> until <code><a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a></code> and transfer it to address <code>to</code>.
Since <code>Timelock&lt;T&gt;</code> does not support public transfer, use this function to lock an object to an address.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_lock_and_transfer">lock_and_transfer</a>&lt;T: store&gt;(obj: T, to: <b>address</b>, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_lock_and_transfer">lock_and_transfer</a>&lt;T: store&gt;(
    obj: T,
    to: <b>address</b>,
    <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64,
    ctx: &<b>mut</b> TxContext,
) {
    <a href="../../dependencies/iota/timelock.md#iota_timelock_transfer">transfer</a>(<a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>(obj, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>, ctx), to);
}
</code></pre>



</details>

<a name="iota_timelock_lock_with_label_and_transfer"></a>

## Function `lock_with_label_and_transfer`

Function to lock a labeled object <code>obj</code> until <code><a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a></code> and transfer it to address <code>to</code>.
Since <code>Timelock&lt;T&gt;</code> does not support public transfer, use this function to lock a labeled object to an address.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_lock_with_label_and_transfer">lock_with_label_and_transfer</a>&lt;T: store, L&gt;(labeler: &<a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">iota::labeler::LabelerCap</a>&lt;L&gt;, obj: T, to: <b>address</b>, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_lock_with_label_and_transfer">lock_with_label_and_transfer</a>&lt;T: store, L&gt;(
    labeler: &LabelerCap&lt;L&gt;,
    obj: T,
    to: <b>address</b>,
    <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64,
    ctx: &<b>mut</b> TxContext,
) {
    <a href="../../dependencies/iota/timelock.md#iota_timelock_transfer">transfer</a>(<a href="../../dependencies/iota/timelock.md#iota_timelock_lock_with_label">lock_with_label</a>(labeler, obj, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>, ctx), to);
}
</code></pre>



</details>

<a name="iota_timelock_unlock"></a>

## Function `unlock`

Function to unlock the object from a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> based on the epoch start time.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_unlock">unlock</a>&lt;T: store&gt;(self: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): T
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_unlock">unlock</a>&lt;T: store&gt;(self: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;, ctx: &TxContext): T {
    // Unpack the timelock.
    <b>let</b> (<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>, _) = <a href="../../dependencies/iota/timelock.md#iota_timelock_unpack">unpack</a>(self);
    // Check <b>if</b> the <a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a> <b>has</b> expired.
    <b>assert</b>!(<a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a> &lt;= ctx.epoch_timestamp_ms(), <a href="../../dependencies/iota/timelock.md#iota_timelock_ENotExpiredYet">ENotExpiredYet</a>);
    <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>
}
</code></pre>



</details>

<a name="iota_timelock_unlock_with_clock"></a>

## Function `unlock_with_clock`

Function to unlock the object from a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> based on the <code>Clock</code> object.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_unlock_with_clock">unlock_with_clock</a>&lt;T: store&gt;(self: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): T
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_unlock_with_clock">unlock_with_clock</a>&lt;T: store&gt;(self: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;, clock: &Clock): T {
    // Unpack the timelock.
    <b>let</b> (<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>, _) = <a href="../../dependencies/iota/timelock.md#iota_timelock_unpack">unpack</a>(self);
    // Check <b>if</b> the <a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a> <b>has</b> expired.
    <b>assert</b>!(<a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a> &lt;= clock.timestamp_ms(), <a href="../../dependencies/iota/timelock.md#iota_timelock_ENotExpiredYet">ENotExpiredYet</a>);
    <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>
}
</code></pre>



</details>

<a name="iota_timelock_join"></a>

## Function `join`

Join two <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;Balance&lt;T&gt;&gt;</code> together.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_join">join</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;&gt;, other: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_join">join</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;Balance&lt;T&gt;&gt;, other: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;Balance&lt;T&gt;&gt;) {
    // Check the preconditions.
    <b>assert</b>!(
        self.<a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>() == other.<a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>(),
        <a href="../../dependencies/iota/timelock.md#iota_timelock_EDifferentExpirationTime">EDifferentExpirationTime</a>,
    );
    <b>assert</b>!(self.<a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>() == other.<a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>(), <a href="../../dependencies/iota/timelock.md#iota_timelock_EDifferentLabels">EDifferentLabels</a>);
    // Unpack the time-<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a> balance.
    <b>let</b> (value, _, _) = <a href="../../dependencies/iota/timelock.md#iota_timelock_unpack">unpack</a>(other);
    // Join the balances.
    self.<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>.<a href="../../dependencies/iota/timelock.md#iota_timelock_join">join</a>(value);
}
</code></pre>



</details>

<a name="iota_timelock_join_vec"></a>

## Function `join_vec`

Join everything in <code>others</code> with <code>self</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_join_vec">join_vec</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;&gt;, others: vector&lt;<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;&gt;&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_join_vec">join_vec</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;Balance&lt;T&gt;&gt;, <b>mut</b> others: vector&lt;<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;Balance&lt;T&gt;&gt;&gt;) {
    // Create useful variables.
    <b>let</b> (<b>mut</b> i, len) = (0, others.length());
    // Join all the balances.
    <b>while</b> (i &lt; len) {
        <b>let</b> other = others.pop_back();
        <a href="../../dependencies/iota/timelock.md#iota_timelock_join">Self::join</a>(self, other);
        i = i + 1
    };
    // Destroy the empty vector.
    vector::destroy_empty(others)
}
</code></pre>



</details>

<a name="iota_timelock_split"></a>

## Function `split`

Split a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;Balance&lt;T&gt;&gt;</code> and take a sub balance from it.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_split">split</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;&gt;, value: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_split">split</a>&lt;T&gt;(
    self: &<b>mut</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;Balance&lt;T&gt;&gt;,
    value: u64,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;Balance&lt;T&gt;&gt; {
    // Split the <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a> balance.
    <b>let</b> value = self.<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>.<a href="../../dependencies/iota/timelock.md#iota_timelock_split">split</a>(value);
    // Pack the <a href="../../dependencies/iota/timelock.md#iota_timelock_split">split</a> balance into a timelock.
    <a href="../../dependencies/iota/timelock.md#iota_timelock_pack">pack</a>(value, self.<a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>(), self.<a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>(), ctx)
}
</code></pre>



</details>

<a name="iota_timelock_split_balance"></a>

## Function `split_balance`

Split the given <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;Balance&lt;T&gt;&gt;</code> into two parts, one with principal <code>value</code>,
and transfer the newly split part to the sender address.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_split_balance">split_balance</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;&gt;, value: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_split_balance">split_balance</a>&lt;T&gt;(
    self: &<b>mut</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;Balance&lt;T&gt;&gt;,
    value: u64,
    ctx: &<b>mut</b> TxContext,
) {
    <a href="../../dependencies/iota/timelock.md#iota_timelock_split">split</a>(self, value, ctx).<a href="../../dependencies/iota/timelock.md#iota_timelock_transfer_to_sender">transfer_to_sender</a>(ctx)
}
</code></pre>



</details>

<a name="iota_timelock_transfer_to_sender"></a>

## Function `transfer_to_sender`

A utility function to transfer a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> to the sender.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_transfer_to_sender">transfer_to_sender</a>&lt;T: store&gt;(<a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_transfer_to_sender">transfer_to_sender</a>&lt;T: store&gt;(<a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;, ctx: &TxContext) {
    <a href="../../dependencies/iota/timelock.md#iota_timelock_transfer">transfer</a>(<a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>, ctx.sender())
}
</code></pre>



</details>

<a name="iota_timelock_system_pack"></a>

## Function `system_pack`

A utility function to pack a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> that can be invoked only by a system package.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_system_pack">system_pack</a>&lt;T: store&gt;(_: &<a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">iota::system_admin_cap::IotaSystemAdminCap</a>, <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>: T, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64, <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_system_pack">system_pack</a>&lt;T: store&gt;(
    _: &IotaSystemAdminCap,
    <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>: T,
    <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64,
    <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>: Option&lt;String&gt;,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt; {
    <a href="../../dependencies/iota/timelock.md#iota_timelock_pack">pack</a>(<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>, <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>, ctx)
}
</code></pre>



</details>

<a name="iota_timelock_system_unpack"></a>

## Function `system_unpack`

An utility function to unpack a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> that can be invoked only by a system package.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_system_unpack">system_unpack</a>&lt;T: store&gt;(_: &<a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">iota::system_admin_cap::IotaSystemAdminCap</a>, <a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;): (T, u64, <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_system_unpack">system_unpack</a>&lt;T: store&gt;(
    _: &IotaSystemAdminCap,
    <a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;,
): (T, u64, Option&lt;String&gt;) {
    <a href="../../dependencies/iota/timelock.md#iota_timelock_unpack">unpack</a>(<a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>)
}
</code></pre>



</details>

<a name="iota_timelock_type_name"></a>

## Function `type_name`

Return a fully qualified type name with the original package IDs
that is used as type related a label value.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_type_name">type_name</a>&lt;L&gt;(): <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_type_name">type_name</a>&lt;L&gt;(): String {
    string::from_ascii(<a href="../../dependencies/std/type_name.md#std_type_name_get_with_original_ids">std::type_name::get_with_original_ids</a>&lt;L&gt;().into_string())
}
</code></pre>



</details>

<a name="iota_timelock_expiration_timestamp_ms"></a>

## Function `expiration_timestamp_ms`

Function to get the expiration timestamp of a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;): u64 {
    self.<a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>
}
</code></pre>



</details>

<a name="iota_timelock_is_locked"></a>

## Function `is_locked`

Function to check if a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> is locked based on the epoch start time.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_is_locked">is_locked</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_is_locked">is_locked</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;, ctx: &TxContext): bool {
    self.<a href="../../dependencies/iota/timelock.md#iota_timelock_remaining_time">remaining_time</a>(ctx) &gt; 0
}
</code></pre>



</details>

<a name="iota_timelock_remaining_time"></a>

## Function `remaining_time`

Function to get the remaining time of a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> based on the epoch start time.
Returns 0 if the lock has expired.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_remaining_time">remaining_time</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_remaining_time">remaining_time</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;, ctx: &TxContext): u64 {
    // Get the epoch timestamp.
    <b>let</b> current_timestamp_ms = ctx.epoch_timestamp_ms();
    self.<a href="../../dependencies/iota/timelock.md#iota_timelock_remaining_time_with_timestamp">remaining_time_with_timestamp</a>(current_timestamp_ms)
}
</code></pre>



</details>

<a name="iota_timelock_is_locked_with_clock"></a>

## Function `is_locked_with_clock`

Function to check if a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> is locked based on the <code>Clock</code> object.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_is_locked_with_clock">is_locked_with_clock</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_is_locked_with_clock">is_locked_with_clock</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;, clock: &Clock): bool {
    self.<a href="../../dependencies/iota/timelock.md#iota_timelock_remaining_time_with_clock">remaining_time_with_clock</a>(clock) &gt; 0
}
</code></pre>



</details>

<a name="iota_timelock_remaining_time_with_clock"></a>

## Function `remaining_time_with_clock`

Function to get the remaining time of a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> based on the <code>Clock</code> object.
Returns 0 if the lock has expired.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_remaining_time_with_clock">remaining_time_with_clock</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_remaining_time_with_clock">remaining_time_with_clock</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;, clock: &Clock): u64 {
    // Get the clock's timestamp.
    <b>let</b> current_timestamp_ms = clock.timestamp_ms();
    self.<a href="../../dependencies/iota/timelock.md#iota_timelock_remaining_time_with_timestamp">remaining_time_with_timestamp</a>(current_timestamp_ms)
}
</code></pre>



</details>

<a name="iota_timelock_locked"></a>

## Function `locked`

Function to get the locked object of a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;): &T
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;): &T {
    &self.<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>
}
</code></pre>



</details>

<a name="iota_timelock_label"></a>

## Function `label`

Function to get the label of a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;): Option&lt;String&gt; {
    self.<a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>
}
</code></pre>



</details>

<a name="iota_timelock_is_labeled_with"></a>

## Function `is_labeled_with`

Check if a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> is labeled with the type <code>L</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_is_labeled_with">is_labeled_with</a>&lt;T: store, L&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_is_labeled_with">is_labeled_with</a>&lt;T: store, L&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;): bool {
    <b>if</b> (self.<a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>.is_some()) {
        self.<a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>.borrow() == <a href="../../dependencies/iota/timelock.md#iota_timelock_type_name">type_name</a>&lt;L&gt;()
    } <b>else</b> {
        <b>false</b>
    }
}
</code></pre>



</details>

<a name="iota_timelock_pack"></a>

## Function `pack`

A utility function to pack a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code>.


<pre><code><b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_pack">pack</a>&lt;T: store&gt;(<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>: T, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64, <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_pack">pack</a>&lt;T: store&gt;(
    <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>: T,
    <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>: u64,
    <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>: Option&lt;String&gt;,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt; {
    // Create a timelock.
    <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a> {
        id: object::new(ctx),
        <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>,
        <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>,
        <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>,
    }
}
</code></pre>



</details>

<a name="iota_timelock_unpack"></a>

## Function `unpack`

An utility function to unpack a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code>.


<pre><code><b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_unpack">unpack</a>&lt;T: store&gt;(<a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;): (T, u64, <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_unpack">unpack</a>&lt;T: store&gt;(<a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;): (T, u64, Option&lt;String&gt;) {
    // Unpack the timelock.
    <b>let</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a> {
        id,
        <a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>,
        <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>,
        <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>,
    } = <a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>;
    // Delete the timelock.
    object::delete(id);
    (<a href="../../dependencies/iota/timelock.md#iota_timelock_locked">locked</a>, <a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a>, <a href="../../dependencies/iota/timelock.md#iota_timelock_label">label</a>)
}
</code></pre>



</details>

<a name="iota_timelock_transfer"></a>

## Function `transfer`

A utility function to transfer a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code> to a receiver.


<pre><code><b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_transfer">transfer</a>&lt;T: store&gt;(<a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;, receiver: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_transfer">transfer</a>&lt;T: store&gt;(<a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>: <a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;, receiver: <b>address</b>) {
    transfer::transfer(<a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a>, receiver);
}
</code></pre>



</details>

<a name="iota_timelock_remaining_time_with_timestamp"></a>

## Function `remaining_time_with_timestamp`

An utility function to get the remaining time of a <code><a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a></code>.


<pre><code><b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_remaining_time_with_timestamp">remaining_time_with_timestamp</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">iota::timelock::TimeLock</a>&lt;T&gt;, current_timestamp_ms: u64): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/timelock.md#iota_timelock_remaining_time_with_timestamp">remaining_time_with_timestamp</a>&lt;T: store&gt;(self: &<a href="../../dependencies/iota/timelock.md#iota_timelock_TimeLock">TimeLock</a>&lt;T&gt;, current_timestamp_ms: u64): u64 {
    // Check <b>if</b> the <a href="../../dependencies/iota/timelock.md#iota_timelock_lock">lock</a> <b>has</b> expired.
    <b>if</b> (self.<a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a> &lt; current_timestamp_ms) {
        <b>return</b> 0
    };
    // Calculate the remaining time.
    self.<a href="../../dependencies/iota/timelock.md#iota_timelock_expiration_timestamp_ms">expiration_timestamp_ms</a> - current_timestamp_ms
}
</code></pre>



</details>
