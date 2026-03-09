
<a name="(iota_notarization=0x0)_timelock"></a>

# Module `(iota_notarization=0x0)::timelock`


<a name="@Timelock_Unlock_Condition_Module_0"></a>

## Timelock Unlock Condition Module


This module implements a timelock mechanism that restricts access to resources
until a specified time has passed. It provides functionality to create and validate
different types of time-based locks:

- Simple time locks that unlock at a specific Unix timestamp
- UntilDestroyed lock that never unlocks until the notarization is destroyed
- None lock that is not locked


-  [Timelock Unlock Condition Module](#@Timelock_Unlock_Condition_Module_0)
-  [Enum `TimeLock`](#(iota_notarization=0x0)_timelock_TimeLock)
-  [Constants](#@Constants_1)
-  [Function `unlock_at`](#(iota_notarization=0x0)_timelock_unlock_at)
-  [Function `until_destroyed`](#(iota_notarization=0x0)_timelock_until_destroyed)
-  [Function `none`](#(iota_notarization=0x0)_timelock_none)
-  [Function `is_until_destroyed`](#(iota_notarization=0x0)_timelock_is_until_destroyed)
-  [Function `is_unlock_at`](#(iota_notarization=0x0)_timelock_is_unlock_at)
-  [Function `is_none`](#(iota_notarization=0x0)_timelock_is_none)
-  [Function `get_unlock_time`](#(iota_notarization=0x0)_timelock_get_unlock_time)
-  [Function `destroy`](#(iota_notarization=0x0)_timelock_destroy)
-  [Function `is_timelocked`](#(iota_notarization=0x0)_timelock_is_timelocked)
-  [Function `is_timelocked_unlock_at`](#(iota_notarization=0x0)_timelock_is_timelocked_unlock_at)
-  [Function `is_valid_period`](#(iota_notarization=0x0)_timelock_is_valid_period)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/clock.md#iota_clock">iota::clock</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="(iota_notarization=0x0)_timelock_TimeLock"></a>

## Enum `TimeLock`

Represents different types of time-based locks that can be applied to
notarizations.


<pre><code><b>public</b> <b>enum</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a> <b>has</b> store
</code></pre>



<details>
<summary>Variants</summary>


<dl>
<dt>
Variant <code>UnlockAt</code>
</dt>
<dd>
 A lock that unlocks at a specific Unix timestamp (seconds since epoch)
</dd>

<dl>
<dt>
<code>0: u32</code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>UntilDestroyed</code>
</dt>
<dd>
 A permanent lock that never unlocks until the notarization object is destroyed (can't be used for <code>delete_lock</code>)
</dd>
<dt>
Variant <code>None</code>
</dt>
<dd>
 No lock applied
</dd>
</dl>


</details>

<a name="@Constants_1"></a>

## Constants


<a name="(iota_notarization=0x0)_timelock_EPastTimestamp"></a>

Error when attempting to create a timelock with a timestamp in the past


<pre><code><b>const</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_EPastTimestamp">EPastTimestamp</a>: u64 = 0;
</code></pre>



<a name="(iota_notarization=0x0)_timelock_ETimelockNotExpired"></a>

Error when attempting to destroy a timelock that is still locked


<pre><code><b>const</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_ETimelockNotExpired">ETimelockNotExpired</a>: u64 = 1;
</code></pre>



<a name="(iota_notarization=0x0)_timelock_unlock_at"></a>

## Function `unlock_at`

Creates a new time lock that unlocks at a specific Unix timestamp.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_unlock_at">unlock_at</a>(unix_time: u32, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): (iota_notarization=0x0)::timelock::TimeLock
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_unlock_at">unlock_at</a>(unix_time: u32, clock: &Clock): <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a> {
    <b>let</b> now = (clock::timestamp_ms(clock) / 1000) <b>as</b> u32;
    <b>assert</b>!(<a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_valid_period">is_valid_period</a>(unix_time, now), <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_EPastTimestamp">EPastTimestamp</a>);
    TimeLock::UnlockAt(unix_time)
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_timelock_until_destroyed"></a>

## Function `until_destroyed`

Creates a new UntilDestroyed lock that never unlocks until the notarization object is destroyed.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_until_destroyed">until_destroyed</a>(): (iota_notarization=0x0)::timelock::TimeLock
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_until_destroyed">until_destroyed</a>(): <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a> {
    TimeLock::UntilDestroyed
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_timelock_none"></a>

## Function `none`

Create a new lock that is not locked.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_none">none</a>(): (iota_notarization=0x0)::timelock::TimeLock
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_none">none</a>(): <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a> {
    TimeLock::None
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_timelock_is_until_destroyed"></a>

## Function `is_until_destroyed`

Checks if the provided lock time is an UntilDestroyed lock.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_until_destroyed">is_until_destroyed</a>(lock_time: &(iota_notarization=0x0)::timelock::TimeLock): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_until_destroyed">is_until_destroyed</a>(lock_time: &<a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a>): bool {
    match (lock_time) {
        TimeLock::UntilDestroyed =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_timelock_is_unlock_at"></a>

## Function `is_unlock_at`

Checks if the provided lock time is a UnlockAt lock.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_unlock_at">is_unlock_at</a>(lock_time: &(iota_notarization=0x0)::timelock::TimeLock): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_unlock_at">is_unlock_at</a>(lock_time: &<a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a>): bool {
    match (lock_time) {
        TimeLock::UnlockAt(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_timelock_is_none"></a>

## Function `is_none`

Checks if the provided lock time is a None lock.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_none">is_none</a>(lock_time: &(iota_notarization=0x0)::timelock::TimeLock): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_none">is_none</a>(lock_time: &<a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a>): bool {
    match (lock_time) {
        TimeLock::None =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_timelock_get_unlock_time"></a>

## Function `get_unlock_time`

Gets the unlock time from a TimeLock if it is a UnixTime lock.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_get_unlock_time">get_unlock_time</a>(lock_time: &(iota_notarization=0x0)::timelock::TimeLock): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u32&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_get_unlock_time">get_unlock_time</a>(lock_time: &<a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a>): Option&lt;u32&gt; {
    match (lock_time) {
        TimeLock::UnlockAt(time) =&gt; option::some(*time),
        _ =&gt; option::none(),
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_timelock_destroy"></a>

## Function `destroy`

Destroys a TimeLock if it's either unlocked or an UntilDestroyed lock.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_destroy">destroy</a>(condition: (iota_notarization=0x0)::timelock::TimeLock, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_destroy">destroy</a>(condition: <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a>, clock: &Clock) {
    // The <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a> is always destroyed, except of those cases where an assertion is raised
    match (condition) {
        TimeLock::UnlockAt(time) =&gt; {
            <b>assert</b>!(!(time &gt; ((clock::timestamp_ms(clock) / 1000) <b>as</b> u32)), <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_ETimelockNotExpired">ETimelockNotExpired</a>);
        },
        TimeLock::UntilDestroyed =&gt; {},
        TimeLock::None =&gt; {},
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_timelock_is_timelocked"></a>

## Function `is_timelocked`

Checks if a timelock condition is currently active (locked).

This function evaluates whether a given TimeLock instance is currently in a locked state
by comparing the current time with the lock's parameters. A lock is considered active if:
1. For UnixTime locks: The current time hasn't reached the specified unlock time yet
2. For UntilDestroyed: Always returns true as these locks never unlock until the notarization is destroyed
3. For None: Always returns false as there is no lock


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_timelocked">is_timelocked</a>(condition: &(iota_notarization=0x0)::timelock::TimeLock, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_timelocked">is_timelocked</a>(condition: &<a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a>, clock: &Clock): bool {
    match (condition) {
        TimeLock::UnlockAt(unix_time) =&gt; {
            *unix_time &gt; ((clock::timestamp_ms(clock) / 1000) <b>as</b> u32)
        },
        TimeLock::UntilDestroyed =&gt; <b>true</b>,
        TimeLock::None =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_timelock_is_timelocked_unlock_at"></a>

## Function `is_timelocked_unlock_at`

Check if a timelock condition is <code>UnlockAt</code>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_timelocked_unlock_at">is_timelocked_unlock_at</a>(lock_time: &(iota_notarization=0x0)::timelock::TimeLock, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_timelocked_unlock_at">is_timelocked_unlock_at</a>(lock_time: &<a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_TimeLock">TimeLock</a>, clock: &Clock): bool {
    match (lock_time) {
        TimeLock::UnlockAt(time) =&gt; {
            *time &gt; ((clock::timestamp_ms(clock) / 1000) <b>as</b> u32)
        },
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_timelock_is_valid_period"></a>

## Function `is_valid_period`

Validates that a specified unlock time is in the future.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_valid_period">is_valid_period</a>(unix_time: u32, current_time: u32): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/timelock.md#(iota_notarization=0x0)_timelock_is_valid_period">is_valid_period</a>(unix_time: u32, current_time: u32): bool {
    unix_time &gt; current_time
}
</code></pre>



</details>
