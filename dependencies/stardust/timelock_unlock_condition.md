
<a name="stardust_timelock_unlock_condition"></a>

# Module `stardust::timelock_unlock_condition`



-  [Struct `TimelockUnlockCondition`](#stardust_timelock_unlock_condition_TimelockUnlockCondition)
-  [Constants](#@Constants_0)
-  [Function `unlock`](#stardust_timelock_unlock_condition_unlock)
-  [Function `is_timelocked`](#stardust_timelock_unlock_condition_is_timelocked)
-  [Function `unix_time`](#stardust_timelock_unlock_condition_unix_time)


<pre><code><b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
</code></pre>



<a name="stardust_timelock_unlock_condition_TimelockUnlockCondition"></a>

## Struct `TimelockUnlockCondition`

The Stardust timelock unlock condition.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_TimelockUnlockCondition">TimelockUnlockCondition</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_unix_time">unix_time</a>: u32</code>
</dt>
<dd>
 The unix time (seconds since Unix epoch) starting from which the output can be consumed.
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="stardust_timelock_unlock_condition_ETimelockNotExpired"></a>

The timelock is not expired error.


<pre><code><b>const</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_ETimelockNotExpired">ETimelockNotExpired</a>: u64 = 0;
</code></pre>



<a name="stardust_timelock_unlock_condition_unlock"></a>

## Function `unlock`

Check the unlock condition.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_unlock">unlock</a>(condition: <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_TimelockUnlockCondition">stardust::timelock_unlock_condition::TimelockUnlockCondition</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_unlock">unlock</a>(condition: <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_TimelockUnlockCondition">TimelockUnlockCondition</a>, ctx: &TxContext) {
    <b>assert</b>!(!<a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_is_timelocked">is_timelocked</a>(&condition, ctx), <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_ETimelockNotExpired">ETimelockNotExpired</a>);
    <b>let</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_TimelockUnlockCondition">TimelockUnlockCondition</a> {
        <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_unix_time">unix_time</a>: _,
    } = condition;
}
</code></pre>



</details>

<a name="stardust_timelock_unlock_condition_is_timelocked"></a>

## Function `is_timelocked`

Check if the output is locked by the <code>Timelock</code> condition.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_is_timelocked">is_timelocked</a>(condition: &<a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_TimelockUnlockCondition">stardust::timelock_unlock_condition::TimelockUnlockCondition</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_is_timelocked">is_timelocked</a>(condition: &<a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_TimelockUnlockCondition">TimelockUnlockCondition</a>, ctx: &TxContext): bool {
    condition.<a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_unix_time">unix_time</a>() &gt; ((tx_context::epoch_timestamp_ms(ctx) / 1000) <b>as</b> u32)
}
</code></pre>



</details>

<a name="stardust_timelock_unlock_condition_unix_time"></a>

## Function `unix_time`

Get the unlock condition's <code><a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_unix_time">unix_time</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_unix_time">unix_time</a>(condition: &<a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_TimelockUnlockCondition">stardust::timelock_unlock_condition::TimelockUnlockCondition</a>): u32
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_unix_time">unix_time</a>(condition: &<a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_TimelockUnlockCondition">TimelockUnlockCondition</a>): u32 {
    condition.<a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition_unix_time">unix_time</a>
}
</code></pre>



</details>
