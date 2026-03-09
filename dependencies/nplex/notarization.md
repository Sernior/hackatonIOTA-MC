
<a name="(iota_notarization=0x0)_notarization"></a>

# Module `(iota_notarization=0x0)::notarization`

This module provides core notarization capabilities to be used by
locked_notarization and dynamic_notarization modules


-  [Struct `Notarization`](#(iota_notarization=0x0)_notarization_Notarization)
-  [Struct `ImmutableMetadata`](#(iota_notarization=0x0)_notarization_ImmutableMetadata)
-  [Struct `LockMetadata`](#(iota_notarization=0x0)_notarization_LockMetadata)
-  [Struct `State`](#(iota_notarization=0x0)_notarization_State)
-  [Struct `NotarizationUpdated`](#(iota_notarization=0x0)_notarization_NotarizationUpdated)
-  [Struct `NotarizationDestroyed`](#(iota_notarization=0x0)_notarization_NotarizationDestroyed)
-  [Constants](#@Constants_0)
-  [Function `update_lock`](#(iota_notarization=0x0)_notarization_update_lock)
-  [Function `delete_lock`](#(iota_notarization=0x0)_notarization_delete_lock)
-  [Function `transfer_lock`](#(iota_notarization=0x0)_notarization_transfer_lock)
-  [Function `data`](#(iota_notarization=0x0)_notarization_data)
-  [Function `metadata`](#(iota_notarization=0x0)_notarization_metadata)
-  [Function `new_state_from_bytes`](#(iota_notarization=0x0)_notarization_new_state_from_bytes)
-  [Function `new_state_from_string`](#(iota_notarization=0x0)_notarization_new_state_from_string)
-  [Function `new_state_from_generic`](#(iota_notarization=0x0)_notarization_new_state_from_generic)
-  [Function `new_lock_metadata`](#(iota_notarization=0x0)_notarization_new_lock_metadata)
-  [Function `new_immutable_metadata`](#(iota_notarization=0x0)_notarization_new_immutable_metadata)
-  [Function `new_dynamic_notarization`](#(iota_notarization=0x0)_notarization_new_dynamic_notarization)
-  [Function `new_locked_notarization`](#(iota_notarization=0x0)_notarization_new_locked_notarization)
-  [Function `update_state`](#(iota_notarization=0x0)_notarization_update_state)
-  [Function `destroy`](#(iota_notarization=0x0)_notarization_destroy)
-  [Function `transfer_notarization`](#(iota_notarization=0x0)_notarization_transfer_notarization)
-  [Function `update_metadata`](#(iota_notarization=0x0)_notarization_update_metadata)
-  [Function `id`](#(iota_notarization=0x0)_notarization_id)
-  [Function `state`](#(iota_notarization=0x0)_notarization_state)
-  [Function `created_at`](#(iota_notarization=0x0)_notarization_created_at)
-  [Function `last_change`](#(iota_notarization=0x0)_notarization_last_change)
-  [Function `version_count`](#(iota_notarization=0x0)_notarization_version_count)
-  [Function `description`](#(iota_notarization=0x0)_notarization_description)
-  [Function `updatable_metadata`](#(iota_notarization=0x0)_notarization_updatable_metadata)
-  [Function `notarization_method`](#(iota_notarization=0x0)_notarization_notarization_method)
-  [Function `lock_metadata`](#(iota_notarization=0x0)_notarization_lock_metadata)
-  [Function `is_update_locked`](#(iota_notarization=0x0)_notarization_is_update_locked)
-  [Function `is_delete_locked`](#(iota_notarization=0x0)_notarization_is_delete_locked)
-  [Function `is_transfer_locked`](#(iota_notarization=0x0)_notarization_is_transfer_locked)
-  [Function `is_destroy_allowed`](#(iota_notarization=0x0)_notarization_is_destroy_allowed)
-  [Function `assert_method_specific_invariants`](#(iota_notarization=0x0)_notarization_assert_method_specific_invariants)
-  [Function `are_locked_notarization_invariants_ok`](#(iota_notarization=0x0)_notarization_are_locked_notarization_invariants_ok)
-  [Function `are_dynamic_notarization_invariants_ok`](#(iota_notarization=0x0)_notarization_are_dynamic_notarization_invariants_ok)


<pre><code><b>use</b> (iota_notarization=0x0)::method;
<b>use</b> (iota_notarization=0x0)::timelock;
<b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/clock.md#iota_clock">iota::clock</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
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



<a name="(iota_notarization=0x0)_notarization_Notarization"></a>

## Struct `Notarization`

A unified notarization type that can be either dynamic or locked


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D: <b>copy</b>, drop, store&gt; <b>has</b> key
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_id">id</a>: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a>: (iota_notarization=0x0)::notarization::State&lt;D&gt;</code>
</dt>
<dd>
 The state of the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> containing the notarized data
 <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a></code> can be updated depending on the <code>NotarizationMethod</code>:
 - Dynamic: Can be updated anytime after creation
 - Locked: Immutable after creation
 Use <code>Notarization::update_state()</code> for <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a></code> updates.
</dd>
<dt>
<code>immutable_metadata: (iota_notarization=0x0)::notarization::ImmutableMetadata</code>
</dt>
<dd>
 Immutable metadata, defined at creation time
 Provides immutable information, assertions and guaranties for third parties.
 <code>immutable_metadata</code> are automatically created at creation time
 and cannot be updated thereafter.
</dd>
<dt>
<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
 Provides context or additional information for third parties
 <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a></code> can be updated depending on the <code>NotarizationMethod</code>:
 - Dynamic: Can be updated anytime after creation
 - Locked: Immutable after creation
 NOTE:
 - <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a></code> can be updated independently of <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a></code>
 - Updating <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a></code> does not increase the <code>state_version_count</code>
 - Updating <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a></code> does not change the <code>last_state_change_at</code> timestamp
 - Use <code>Notarization::update_metadata()</code> for <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a></code> updates.
</dd>
<dt>
<code>last_state_change_at: u64</code>
</dt>
<dd>
 Timestamp of the last <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a></code> change (milliseconds since UNIX epoch)
</dd>
<dt>
<code>state_version_count: u64</code>
</dt>
<dd>
 Counter for the number of <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a></code> updates
</dd>
<dt>
<code>method: (iota_notarization=0x0)::method::NotarizationMethod</code>
</dt>
<dd>
 Notarization Method defining the overall behavior of the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code>
</dd>
</dl>


</details>

<a name="(iota_notarization=0x0)_notarization_ImmutableMetadata"></a>

## Struct `ImmutableMetadata`

Gathers immutable fields defined when the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> object is created


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ImmutableMetadata">ImmutableMetadata</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_created_at">created_at</a>: u64</code>
</dt>
<dd>
 Timestamp when the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> was created
</dd>
<dt>
<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_description">description</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
 Description of the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code>
</dd>
<dt>
<code>locking: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;(iota_notarization=0x0)::notarization::LockMetadata&gt;</code>
</dt>
<dd>
 Optional lock metadata for <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code>
</dd>
</dl>


</details>

<a name="(iota_notarization=0x0)_notarization_LockMetadata"></a>

## Struct `LockMetadata`

Defines how a <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> is locked.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_LockMetadata">LockMetadata</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>: (iota_notarization=0x0)::timelock::TimeLock</code>
</dt>
<dd>
 Update lock condition
</dd>
<dt>
<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>: (iota_notarization=0x0)::timelock::TimeLock</code>
</dt>
<dd>
 Lock condition for deletion
 NOTE: delete_lock cannot be TimeLock::UntilDestroyed
</dd>
<dt>
<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>: (iota_notarization=0x0)::timelock::TimeLock</code>
</dt>
<dd>
 Transfer lock
 NOTE: Only dynamic notarizations can be transferable
</dd>
</dl>


</details>

<a name="(iota_notarization=0x0)_notarization_State"></a>

## Struct `State`

Represents the state of a <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> containing the notarized <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a></code> and its <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a></code>

The <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a></code> can be updated by the owner depending on the used <code>NotarizationMethod</code>:
- Dynamic: <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a></code> and <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a></code> of the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a></code> can be updated anytime after creation
- Locked: The <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a></code> is immutable after <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> creation

<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a></code> <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a></code> and <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a></code> can only be updated at once, using method <code>Notarization::update_state()</code>
which will increase the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> <code>state_version_count</code> and update the <code>last_state_change_at</code>
timestamp even if only the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a></code> are altered.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a>&lt;D: <b>copy</b>, drop, store&gt; <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>: D</code>
</dt>
<dd>
 The data being notarized
</dd>
<dt>
<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
 State-associated metadata
</dd>
</dl>


</details>

<a name="(iota_notarization=0x0)_notarization_NotarizationUpdated"></a>

## Struct `NotarizationUpdated`

Event emitted when the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a></code> of a <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> is updated


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_NotarizationUpdated">NotarizationUpdated</a>&lt;D: <b>copy</b>, drop, store&gt; <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>notarization_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 ID of the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> object that was updated
</dd>
<dt>
<code>state_version_count: u64</code>
</dt>
<dd>
 New version number after the update
</dd>
<dt>
<code>updated_state: (iota_notarization=0x0)::notarization::State&lt;D&gt;</code>
</dt>
<dd>
 Updated State
</dd>
</dl>


</details>

<a name="(iota_notarization=0x0)_notarization_NotarizationDestroyed"></a>

## Struct `NotarizationDestroyed`

Event emitted when a <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> is destroyed


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_NotarizationDestroyed">NotarizationDestroyed</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>notarization_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 ID of the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> object that was destroyed
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(iota_notarization=0x0)_notarization_EUpdateWhileLocked"></a>

Cannot update state while notarization is locked for updates


<pre><code><b>const</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_EUpdateWhileLocked">EUpdateWhileLocked</a>: u64 = 0;
</code></pre>



<a name="(iota_notarization=0x0)_notarization_EDestroyWhileLocked"></a>

Cannot destroy while notarization is locked for deletion


<pre><code><b>const</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_EDestroyWhileLocked">EDestroyWhileLocked</a>: u64 = 1;
</code></pre>



<a name="(iota_notarization=0x0)_notarization_ELockTimeNotSatisfied"></a>

A lock time is not satisfied


<pre><code><b>const</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ELockTimeNotSatisfied">ELockTimeNotSatisfied</a>: u64 = 2;
</code></pre>



<a name="(iota_notarization=0x0)_notarization_EUntilDestroyedLockNotAllowed"></a>

Delete lock cannot be TimeLock::UntilDestroyed


<pre><code><b>const</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_EUntilDestroyedLockNotAllowed">EUntilDestroyedLockNotAllowed</a>: u64 = 3;
</code></pre>



<a name="(iota_notarization=0x0)_notarization_EDynamicNotarizationInvariants"></a>

Invariants for dynamic notarization are broken by the specified
Notarization configuration


<pre><code><b>const</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_EDynamicNotarizationInvariants">EDynamicNotarizationInvariants</a>: u64 = 4;
</code></pre>



<a name="(iota_notarization=0x0)_notarization_ELockedNotarizationInvariants"></a>

Invariants for locked notarization are broken by the specified
Notarization configuration


<pre><code><b>const</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ELockedNotarizationInvariants">ELockedNotarizationInvariants</a>: u64 = 5;
</code></pre>



<a name="(iota_notarization=0x0)_notarization_update_lock"></a>

## Function `update_lock`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>(self: &(iota_notarization=0x0)::notarization::LockMetadata): &(iota_notarization=0x0)::timelock::TimeLock
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_LockMetadata">LockMetadata</a>): &TimeLock {
    &self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_delete_lock"></a>

## Function `delete_lock`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>(self: &(iota_notarization=0x0)::notarization::LockMetadata): &(iota_notarization=0x0)::timelock::TimeLock
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_LockMetadata">LockMetadata</a>): &TimeLock {
    &self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_transfer_lock"></a>

## Function `transfer_lock`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>(self: &(iota_notarization=0x0)::notarization::LockMetadata): &(iota_notarization=0x0)::timelock::TimeLock
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_LockMetadata">LockMetadata</a>): &TimeLock {
    &self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_data"></a>

## Function `data`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::State&lt;D&gt;): &D
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a>&lt;D&gt;): &D {
    &self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_metadata"></a>

## Function `metadata`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::State&lt;D&gt;): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a>&lt;D&gt;): &Option&lt;String&gt; {
    &self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a>
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_new_state_from_bytes"></a>

## Function `new_state_from_bytes`

Create a new state from a vector<u8> data


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_state_from_bytes">new_state_from_bytes</a>(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>: vector&lt;u8&gt;, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;): (iota_notarization=0x0)::notarization::State&lt;vector&lt;u8&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_state_from_bytes">new_state_from_bytes</a>(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>: vector&lt;u8&gt;, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a>: Option&lt;String&gt;): <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a>&lt;vector&lt;u8&gt;&gt; {
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a> { <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a> }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_new_state_from_string"></a>

## Function `new_state_from_string`

Create state from a string data


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_state_from_string">new_state_from_string</a>(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;): (iota_notarization=0x0)::notarization::State&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_state_from_string">new_state_from_string</a>(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>: String, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a>: Option&lt;String&gt;): <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a>&lt;String&gt; {
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a> { <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a> }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_new_state_from_generic"></a>

## Function `new_state_from_generic`

Create state from generic data


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_state_from_generic">new_state_from_generic</a>&lt;D: <b>copy</b>, drop, store&gt;(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>: D, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;): (iota_notarization=0x0)::notarization::State&lt;D&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_state_from_generic">new_state_from_generic</a>&lt;D: store + drop + <b>copy</b>&gt;(
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>: D,
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a>: Option&lt;String&gt;,
): <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a>&lt;D&gt; {
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a> { <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_data">data</a>, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a> }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_new_lock_metadata"></a>

## Function `new_lock_metadata`

Create lock metadata


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_lock_metadata">new_lock_metadata</a>(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>: (iota_notarization=0x0)::timelock::TimeLock, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>: (iota_notarization=0x0)::timelock::TimeLock, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>: (iota_notarization=0x0)::timelock::TimeLock): (iota_notarization=0x0)::notarization::LockMetadata
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_lock_metadata">new_lock_metadata</a>(
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>: TimeLock,
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>: TimeLock,
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>: TimeLock,
): <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_LockMetadata">LockMetadata</a> {
    <b>assert</b>!(!<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>.is_until_destroyed(), <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_EUntilDestroyedLockNotAllowed">EUntilDestroyedLockNotAllowed</a>);
    <b>if</b> (<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>.is_unlock_at()) {
        <b>let</b> delete_lock_time = <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>.get_unlock_time().destroy_some();
        <b>if</b> (<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>.is_unlock_at()) {
            <b>let</b> update_lock_time = <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>.get_unlock_time().destroy_some();
            <b>assert</b>!(delete_lock_time &gt;= update_lock_time, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ELockTimeNotSatisfied">ELockTimeNotSatisfied</a>)
        };
        <b>if</b> (<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>.is_unlock_at()) {
            <b>let</b> transfer_lock_time = <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>.get_unlock_time().destroy_some();
            <b>assert</b>!(delete_lock_time &gt;= transfer_lock_time, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ELockTimeNotSatisfied">ELockTimeNotSatisfied</a>)
        };
    };
    // In the current implementation the combination of locks in <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_LockMetadata">LockMetadata</a>
    // is restricted by the notarization-method specific lock invariants which are guaranteed
    // by function `<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_assert_method_specific_invariants">assert_method_specific_invariants</a>()` and the constructor functions
    // `<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_locked_notarization">new_locked_notarization</a>()` and `<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_dynamic_notarization">new_dynamic_notarization</a>()`.
    //
    // According to these invariants we don't need to handle the edge cases where
    // <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>.is_none() and other locks are `TimeLock::UnlockAt`.
    //
    // These edge cases must be handled here, once new notarization-methods will
    // be added in future versions of iota_notarization, having different invariants.
    //
    // To avoid malicious or at least very surprising behavior
    // the <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a> must always exceed all other locks (<b>as</b> been asserted above
    // <b>for</b> `<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>.is_unlock_at()`).
    //
    // In case <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>.is_none() and one of the other locks is TimeLock::UnlockAt,
    // <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a> needs to be set to the same lock_time <b>as</b> the lock, having the greatest
    // lock_time.
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_LockMetadata">LockMetadata</a> {
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>,
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>,
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>,
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_new_immutable_metadata"></a>

## Function `new_immutable_metadata`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_immutable_metadata">new_immutable_metadata</a>(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_created_at">created_at</a>: u64, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_description">description</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, locking: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;(iota_notarization=0x0)::notarization::LockMetadata&gt;): (iota_notarization=0x0)::notarization::ImmutableMetadata
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_immutable_metadata">new_immutable_metadata</a>(
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_created_at">created_at</a>: u64,
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_description">description</a>: Option&lt;String&gt;,
    locking: Option&lt;<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_LockMetadata">LockMetadata</a>&gt;,
): <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ImmutableMetadata">ImmutableMetadata</a> {
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ImmutableMetadata">ImmutableMetadata</a> {
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_created_at">created_at</a>,
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_description">description</a>,
        locking,
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_new_dynamic_notarization"></a>

## Function `new_dynamic_notarization`

Create a new dynamic <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_dynamic_notarization">new_dynamic_notarization</a>&lt;D: <b>copy</b>, drop, store&gt;(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a>: (iota_notarization=0x0)::notarization::State&lt;D&gt;, immutable_description: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>: (iota_notarization=0x0)::timelock::TimeLock, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (iota_notarization=0x0)::notarization::Notarization&lt;D&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_dynamic_notarization">new_dynamic_notarization</a>&lt;D: store + drop + <b>copy</b>&gt;(
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a>: <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a>&lt;D&gt;,
    immutable_description: Option&lt;String&gt;,
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a>: Option&lt;String&gt;,
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>: TimeLock,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt; {
    <b>let</b> locking = <b>if</b> (timelock::is_none(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>)) {
        timelock::destroy(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>, clock);
        option::none()
    } <b>else</b> {
        option::some(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_lock_metadata">new_lock_metadata</a>(timelock::none(), timelock::none(), <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>))
    };
    <b>let</b> immutable_metadata = <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ImmutableMetadata">ImmutableMetadata</a> {
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_created_at">created_at</a>: clock::timestamp_ms(clock),
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_description">description</a>: immutable_description,
        locking,
    };
    <b>assert</b>!(
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_are_dynamic_notarization_invariants_ok">are_dynamic_notarization_invariants_ok</a>(&immutable_metadata),
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_EDynamicNotarizationInvariants">EDynamicNotarizationInvariants</a>,
    );
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt; {
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_id">id</a>: object::new(ctx),
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a>,
        immutable_metadata,
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a>,
        last_state_change_at: clock::timestamp_ms(clock),
        state_version_count: 0,
        method: new_dynamic(),
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_new_locked_notarization"></a>

## Function `new_locked_notarization`

Create a new locked <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_locked_notarization">new_locked_notarization</a>&lt;D: <b>copy</b>, drop, store&gt;(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a>: (iota_notarization=0x0)::notarization::State&lt;D&gt;, immutable_description: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>: (iota_notarization=0x0)::timelock::TimeLock, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (iota_notarization=0x0)::notarization::Notarization&lt;D&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_locked_notarization">new_locked_notarization</a>&lt;D: store + drop + <b>copy</b>&gt;(
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a>: <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a>&lt;D&gt;,
    immutable_description: Option&lt;String&gt;,
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a>: Option&lt;String&gt;,
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>: TimeLock,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt; {
    <b>let</b> immutable_metadata = <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ImmutableMetadata">ImmutableMetadata</a> {
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_created_at">created_at</a>: clock::timestamp_ms(clock),
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_description">description</a>: immutable_description,
        locking: option::some(
            <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_new_lock_metadata">new_lock_metadata</a>(
                timelock::until_destroyed(),
                <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>,
                timelock::until_destroyed(),
            ),
        ),
    };
    <b>assert</b>!(
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_are_locked_notarization_invariants_ok">are_locked_notarization_invariants_ok</a>(&immutable_metadata),
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ELockedNotarizationInvariants">ELockedNotarizationInvariants</a>,
    );
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt; {
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_id">id</a>: object::new(ctx),
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a>,
        immutable_metadata,
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a>,
        last_state_change_at: clock::timestamp_ms(clock),
        state_version_count: 0,
        method: new_locked(),
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_update_state"></a>

## Function `update_state`

Update the state of a <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code>

Using this function will:
- set the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a></code> to the <code>new_state</code>
- increase the <code>state_version_count</code> by 1
- set the <code>last_state_change_at</code> timestamp to the current <code>clock::timestamp_ms</code>
- emit a <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_NotarizationUpdated">NotarizationUpdated</a></code> event in case of success
- fail if the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> uses <code>NotarizationMethod::Locked</code> or is update-locked
(<code>Notarization::is_update_locked()</code> is true) by other means


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_state">update_state</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &<b>mut</b> (iota_notarization=0x0)::notarization::Notarization&lt;D&gt;, new_state: (iota_notarization=0x0)::notarization::State&lt;D&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_state">update_state</a>&lt;D: store + drop + <b>copy</b>&gt;(
    self: &<b>mut</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;,
    new_state: <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a>&lt;D&gt;,
    clock: &Clock,
) {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_is_update_locked">is_update_locked</a>(clock), <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_EUpdateWhileLocked">EUpdateWhileLocked</a>);
    self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a> = new_state;
    self.last_state_change_at = clock::timestamp_ms(clock);
    self.state_version_count = self.state_version_count + 1;
    event::emit(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_NotarizationUpdated">NotarizationUpdated</a> {
        notarization_id: object::uid_to_inner(&self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_id">id</a>),
        state_version_count: self.state_version_count,
        updated_state: new_state,
    });
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_destroy"></a>

## Function `destroy`

Destroy a <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_destroy">destroy</a>&lt;D: <b>copy</b>, drop, store&gt;(self: (iota_notarization=0x0)::notarization::Notarization&lt;D&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_destroy">destroy</a>&lt;D: drop + store + <b>copy</b>&gt;(self: <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;, clock: &Clock) {
    <b>assert</b>!(self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_is_destroy_allowed">is_destroy_allowed</a>(clock), <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_EDestroyWhileLocked">EDestroyWhileLocked</a>);
    <b>let</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a> {
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_id">id</a>,
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a>: _,
        immutable_metadata: <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ImmutableMetadata">ImmutableMetadata</a> {
            <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_created_at">created_at</a>: _,
            <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_description">description</a>: _,
            locking,
        },
        <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a>: _,
        last_state_change_at: _,
        state_version_count: _,
        method: _,
    } = self;
    <b>if</b> (locking.is_some()) {
        <b>let</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_LockMetadata">LockMetadata</a> { <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>, <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a> } = option::destroy_some(
            locking,
        );
        // <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_destroy">destroy</a> the locks
        timelock::destroy(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>, clock);
        timelock::destroy(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>, clock);
        timelock::destroy(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>, clock);
    } <b>else</b> {
        // We know dynamic Notarizations have no lock <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_metadata">metadata</a>
        option::destroy_none(locking);
    };
    <b>let</b> id_inner = object::uid_to_inner(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_id">id</a>);
    object::delete(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_id">id</a>);
    event::emit(<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_NotarizationDestroyed">NotarizationDestroyed</a> { notarization_id: id_inner });
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_transfer_notarization"></a>

## Function `transfer_notarization`

Re-exports the transfer function from the core module

Workaround for transferability


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_notarization">transfer_notarization</a>&lt;D: <b>copy</b>, drop, store&gt;(self: (iota_notarization=0x0)::notarization::Notarization&lt;D&gt;, recipient: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_notarization">transfer_notarization</a>&lt;D: store + drop + <b>copy</b>&gt;(
    self: <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;,
    recipient: <b>address</b>,
) {
    transfer::transfer(self, recipient);
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_update_metadata"></a>

## Function `update_metadata`

Update the updatable metadata of a <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code>

NOTE:
- does not affect the state version count or the <code>last_state_change_at</code> timestamp
- will fail if the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> uses <code>NotarizationMethod::Locked</code> or is update-locked
(<code>Notarization::is_update_locked()</code> is true) by other means
- Only the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a></code> can be changed; the <code>immutable_metadata::description</code>
remains fixed


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_metadata">update_metadata</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &<b>mut</b> (iota_notarization=0x0)::notarization::Notarization&lt;D&gt;, new_metadata: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_metadata">update_metadata</a>&lt;D: store + drop + <b>copy</b>&gt;(
    self: &<b>mut</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;,
    new_metadata: Option&lt;String&gt;,
    clock: &Clock,
) {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_is_update_locked">is_update_locked</a>(clock), <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_EUpdateWhileLocked">EUpdateWhileLocked</a>);
    self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a> = new_metadata;
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_id"></a>

## Function `id`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_id">id</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;): &<a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_id">id</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;): &UID { &self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_id">id</a> }
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_state"></a>

## Function `state`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;): &(iota_notarization=0x0)::notarization::State&lt;D&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;): &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_State">State</a>&lt;D&gt; { &self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_state">state</a> }
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_created_at"></a>

## Function `created_at`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_created_at">created_at</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_created_at">created_at</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;): u64 {
    self.immutable_metadata.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_created_at">created_at</a>
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_last_change"></a>

## Function `last_change`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_last_change">last_change</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_last_change">last_change</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;): u64 {
    self.last_state_change_at
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_version_count"></a>

## Function `version_count`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_version_count">version_count</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_version_count">version_count</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;): u64 {
    self.state_version_count
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_description"></a>

## Function `description`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_description">description</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_description">description</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;): Option&lt;String&gt; {
    self.immutable_metadata.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_description">description</a>
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_updatable_metadata"></a>

## Function `updatable_metadata`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;): Option&lt;String&gt; {
    self.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_updatable_metadata">updatable_metadata</a>
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_notarization_method"></a>

## Function `notarization_method`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_notarization_method">notarization_method</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;): (iota_notarization=0x0)::method::NotarizationMethod
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_notarization_method">notarization_method</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;): NotarizationMethod {
    self.method
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_lock_metadata"></a>

## Function `lock_metadata`

Get the lock metadata if this is a locked Notarization


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;(iota_notarization=0x0)::notarization::LockMetadata&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;): &Option&lt;<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_LockMetadata">LockMetadata</a>&gt; {
    &self.immutable_metadata.locking
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_is_update_locked"></a>

## Function `is_update_locked`

Check if the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> is locked for updates (always false for dynamic variant)


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_is_update_locked">is_update_locked</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_is_update_locked">is_update_locked</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;, clock: &Clock): bool {
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_assert_method_specific_invariants">assert_method_specific_invariants</a>(self);
    <b>if</b> (self.method.is_dynamic()) {
        <b>false</b>
    } <b>else</b> {
        <b>let</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a> = option::borrow(&self.immutable_metadata.locking);
        timelock::is_timelocked(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>, clock)
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_is_delete_locked"></a>

## Function `is_delete_locked`

Check if the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> is locked for deletion (always false for dynamic variant)


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_is_delete_locked">is_delete_locked</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_is_delete_locked">is_delete_locked</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;, clock: &Clock): bool {
    <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_assert_method_specific_invariants">assert_method_specific_invariants</a>(self);
    <b>if</b> (self.method.is_dynamic()) {
        <b>false</b>
    } <b>else</b> {
        <b>let</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a> = option::borrow(&self.immutable_metadata.locking);
        timelock::is_timelocked(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>, clock)
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_is_transfer_locked"></a>

## Function `is_transfer_locked`

Check if the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> is locked for transfer


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_is_transfer_locked">is_transfer_locked</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_is_transfer_locked">is_transfer_locked</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;, clock: &Clock): bool {
    option::is_some_and!(&self.immutable_metadata.locking, |<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>| {
        timelock::is_timelocked(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>, clock)
    })
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_is_destroy_allowed"></a>

## Function `is_destroy_allowed`

Check if the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a></code> can be destroyed


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_is_destroy_allowed">is_destroy_allowed</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_is_destroy_allowed">is_destroy_allowed</a>&lt;D: store + drop + <b>copy</b>&gt;(self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;, clock: &Clock): bool {
    <b>if</b> (self.method.is_dynamic()) {
        !option::is_some_and!(
            &self.immutable_metadata.locking,
            |<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>| timelock::is_timelocked_unlock_at(
                &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>,
                clock,
            ),
        )
    } <b>else</b> {
        <b>let</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a> = option::borrow(&self.immutable_metadata.locking);
        !(
            timelock::is_timelocked_unlock_at(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>, clock) ||
        timelock::is_timelocked_unlock_at(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>, clock) ||
        timelock::is_timelocked_unlock_at(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>, clock),
        )
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_assert_method_specific_invariants"></a>

## Function `assert_method_specific_invariants`

Ensures that the NotarizationMethod specific invariants are hold
See fun <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_are_locked_notarization_invariants_ok">are_locked_notarization_invariants_ok</a>()</code> and
<code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_are_dynamic_notarization_invariants_ok">are_dynamic_notarization_invariants_ok</a>()</code>
for more details.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_assert_method_specific_invariants">assert_method_specific_invariants</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_assert_method_specific_invariants">assert_method_specific_invariants</a>&lt;D: store + drop + <b>copy</b>&gt;(
    self: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_Notarization">Notarization</a>&lt;D&gt;,
) {
    <b>if</b> (self.method.is_dynamic()) {
        <b>assert</b>!(
            <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_are_dynamic_notarization_invariants_ok">are_dynamic_notarization_invariants_ok</a>(&self.immutable_metadata),
            <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_EDynamicNotarizationInvariants">EDynamicNotarizationInvariants</a>,
        );
    } <b>else</b> <b>if</b> (self.method.is_locked()) {
        <b>assert</b>!(
            <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_are_locked_notarization_invariants_ok">are_locked_notarization_invariants_ok</a>(&self.immutable_metadata),
            <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ELockedNotarizationInvariants">ELockedNotarizationInvariants</a>,
        );
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_are_locked_notarization_invariants_ok"></a>

## Function `are_locked_notarization_invariants_ok`

Indicates if the invariants for <code>NotarizationMethod::Locked</code> are satisfied:

- <code>self.immutable_metadata.locking</code> must exist.
- <code>updated_lock</code> and <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a></code> must be <code>TimeLock::UntilDestroyed</code>.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_are_locked_notarization_invariants_ok">are_locked_notarization_invariants_ok</a>(immutable_metadata: &(iota_notarization=0x0)::notarization::ImmutableMetadata): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_are_locked_notarization_invariants_ok">are_locked_notarization_invariants_ok</a>(
    immutable_metadata: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ImmutableMetadata">ImmutableMetadata</a>,
): bool {
    <b>if</b> (immutable_metadata.locking.is_some()) {
        <b>let</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a> = option::borrow(&immutable_metadata.locking);
        timelock::is_until_destroyed(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>) && timelock::is_until_destroyed(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>)
    } <b>else</b> {
        <b>false</b>
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_notarization_are_dynamic_notarization_invariants_ok"></a>

## Function `are_dynamic_notarization_invariants_ok`

Indicates if the invariants for <code>NotarizationMethod::Dynamic</code> are satisfied:

- Dynamic notarization can only have transfer locking or no
<code>immutable_metadata.locking</code>.
If <code>immutable_metadata.locking</code> exists, all locks except <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a></code>
must be <code>TimeLock::None</code>
and the <code><a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a></code> must not be <code>TimeLock::None</code>.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_are_dynamic_notarization_invariants_ok">are_dynamic_notarization_invariants_ok</a>(immutable_metadata: &(iota_notarization=0x0)::notarization::ImmutableMetadata): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_are_dynamic_notarization_invariants_ok">are_dynamic_notarization_invariants_ok</a>(
    immutable_metadata: &<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_ImmutableMetadata">ImmutableMetadata</a>,
): bool {
    <b>if</b> (immutable_metadata.locking.is_some()) {
        <b>let</b> <a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a> = option::borrow(&immutable_metadata.locking);
        timelock::is_none(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_delete_lock">delete_lock</a>) &&
        timelock::is_none(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_update_lock">update_lock</a>) &&
        !timelock::is_none(&<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_lock_metadata">lock_metadata</a>.<a href="../../dependencies/nplex/notarization.md#(iota_notarization=0x0)_notarization_transfer_lock">transfer_lock</a>)
    } <b>else</b> {
        <b>true</b>
    }
}
</code></pre>



</details>
