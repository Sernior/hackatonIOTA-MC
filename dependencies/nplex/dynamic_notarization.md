
<a name="(iota_notarization=0x0)_dynamic_notarization"></a>

# Module `(iota_notarization=0x0)::dynamic_notarization`

This module provides dynamic notarization capabilities that can be freely updated by its owner


-  [Struct `DynamicNotarizationCreated`](#(iota_notarization=0x0)_dynamic_notarization_DynamicNotarizationCreated)
-  [Struct `DynamicNotarizationTransferred`](#(iota_notarization=0x0)_dynamic_notarization_DynamicNotarizationTransferred)
-  [Constants](#@Constants_0)
-  [Function `new`](#(iota_notarization=0x0)_dynamic_notarization_new)
-  [Function `create`](#(iota_notarization=0x0)_dynamic_notarization_create)
-  [Function `transfer`](#(iota_notarization=0x0)_dynamic_notarization_transfer)
-  [Function `is_transferable`](#(iota_notarization=0x0)_dynamic_notarization_is_transferable)


<pre><code><b>use</b> (iota_notarization=0x0)::method;
<b>use</b> (iota_notarization=0x0)::notarization;
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



<a name="(iota_notarization=0x0)_dynamic_notarization_DynamicNotarizationCreated"></a>

## Struct `DynamicNotarizationCreated`

Event emitted when a dynamic notarization is created


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_DynamicNotarizationCreated">DynamicNotarizationCreated</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>notarization_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 ID of the <code>Notarization</code> object that was created
</dd>
</dl>


</details>

<a name="(iota_notarization=0x0)_dynamic_notarization_DynamicNotarizationTransferred"></a>

## Struct `DynamicNotarizationTransferred`

Event emitted when a dynamic notarization is transferred


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_DynamicNotarizationTransferred">DynamicNotarizationTransferred</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>notarization_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 ID of the <code>Notarization</code> object that was transferred
</dd>
<dt>
<code>recipient: <b>address</b></code>
</dt>
<dd>
 Address of the new owner
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(iota_notarization=0x0)_dynamic_notarization_ECannotTransferLocked"></a>

Cannot transfer a locked notarization


<pre><code><b>const</b> <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_ECannotTransferLocked">ECannotTransferLocked</a>: u64 = 0;
</code></pre>



<a name="(iota_notarization=0x0)_dynamic_notarization_new"></a>

## Function `new`

Create a new dynamic <code>Notarization</code>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_new">new</a>&lt;D: <b>copy</b>, drop, store&gt;(state: (iota_notarization=0x0)::notarization::State&lt;D&gt;, immutable_description: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, updatable_metadata: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, transfer_lock: (iota_notarization=0x0)::timelock::TimeLock, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (iota_notarization=0x0)::notarization::Notarization&lt;D&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_new">new</a>&lt;D: store + drop + <b>copy</b>&gt;(
    state: notarization::State&lt;D&gt;,
    immutable_description: Option&lt;String&gt;,
    updatable_metadata: Option&lt;String&gt;,
    transfer_lock: TimeLock,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
): notarization::Notarization&lt;D&gt; {
    notarization::new_dynamic_notarization(
        state,
        immutable_description,
        updatable_metadata,
        transfer_lock,
        clock,
        ctx,
    )
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_dynamic_notarization_create"></a>

## Function `create`

Create and transfer a new dynamic <code>Notarization</code> to the sender


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_create">create</a>&lt;D: <b>copy</b>, drop, store&gt;(state: (iota_notarization=0x0)::notarization::State&lt;D&gt;, immutable_description: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, updatable_metadata: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, transfer_lock: (iota_notarization=0x0)::timelock::TimeLock, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_create">create</a>&lt;D: store + drop + <b>copy</b>&gt;(
    state: notarization::State&lt;D&gt;,
    immutable_description: Option&lt;String&gt;,
    updatable_metadata: Option&lt;String&gt;,
    transfer_lock: TimeLock,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
) {
    // Use the core <b>module</b> to <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_create">create</a> and <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_transfer">transfer</a> the notarization
    <b>let</b> notarization = <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_new">new</a>(
        state,
        immutable_description,
        updatable_metadata,
        transfer_lock,
        clock,
        ctx,
    );
    <b>let</b> id = object::uid_to_inner(notarization.id());
    event::emit(<a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_DynamicNotarizationCreated">DynamicNotarizationCreated</a> { notarization_id: id });
    notarization::transfer_notarization(notarization, tx_context::sender(ctx));
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_dynamic_notarization_transfer"></a>

## Function `transfer`

Transfer a dynamic notarization to a new owner
Only works for dynamic notarizations that are marked as transferrable


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_transfer">transfer</a>&lt;D: <b>copy</b>, drop, store&gt;(self: (iota_notarization=0x0)::notarization::Notarization&lt;D&gt;, recipient: <b>address</b>, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, _: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_transfer">transfer</a>&lt;D: store + drop + <b>copy</b>&gt;(
    self: notarization::Notarization&lt;D&gt;,
    recipient: <b>address</b>,
    clock: &Clock,
    _: &<b>mut</b> TxContext,
) {
    // Ensure this notarization is transferrable
    <b>assert</b>!(<a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_is_transferable">is_transferable</a>(&self, clock), <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_ECannotTransferLocked">ECannotTransferLocked</a>);
    notarization::transfer_notarization(self, recipient);
    <b>let</b> id = object::id_from_address(recipient);
    event::emit(<a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_DynamicNotarizationTransferred">DynamicNotarizationTransferred</a> {
        notarization_id: id,
        recipient,
    });
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_dynamic_notarization_is_transferable"></a>

## Function `is_transferable`

Check if the notarization is transferable


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_is_transferable">is_transferable</a>&lt;D: <b>copy</b>, drop, store&gt;(self: &(iota_notarization=0x0)::notarization::Notarization&lt;D&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/dynamic_notarization.md#(iota_notarization=0x0)_dynamic_notarization_is_transferable">is_transferable</a>&lt;D: store + drop + <b>copy</b>&gt;(
    self: &notarization::Notarization&lt;D&gt;,
    clock: &Clock,
): bool {
    self.lock_metadata().is_none() || !self.is_transfer_locked(clock)
}
</code></pre>



</details>
