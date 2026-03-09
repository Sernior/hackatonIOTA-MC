
<a name="(iota_notarization=0x0)_locked_notarization"></a>

# Module `(iota_notarization=0x0)::locked_notarization`

This module provides locked notarization capabilities with timelock controls for updates and deletion


-  [Struct `LockedNotarizationCreated`](#(iota_notarization=0x0)_locked_notarization_LockedNotarizationCreated)
-  [Function `new`](#(iota_notarization=0x0)_locked_notarization_new)
-  [Function `create`](#(iota_notarization=0x0)_locked_notarization_create)


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



<a name="(iota_notarization=0x0)_locked_notarization_LockedNotarizationCreated"></a>

## Struct `LockedNotarizationCreated`

Event emitted when a locked notarization is created


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/locked_notarization.md#(iota_notarization=0x0)_locked_notarization_LockedNotarizationCreated">LockedNotarizationCreated</a> <b>has</b> <b>copy</b>, drop
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

<a name="(iota_notarization=0x0)_locked_notarization_new"></a>

## Function `new`

Create a new locked <code>Notarization</code>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/locked_notarization.md#(iota_notarization=0x0)_locked_notarization_new">new</a>&lt;D: <b>copy</b>, drop, store&gt;(state: (iota_notarization=0x0)::notarization::State&lt;D&gt;, immutable_description: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, updatable_metadata: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, delete_lock: (iota_notarization=0x0)::timelock::TimeLock, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (iota_notarization=0x0)::notarization::Notarization&lt;D&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/locked_notarization.md#(iota_notarization=0x0)_locked_notarization_new">new</a>&lt;D: store + drop + <b>copy</b>&gt;(
    state: notarization::State&lt;D&gt;,
    immutable_description: Option&lt;String&gt;,
    updatable_metadata: Option&lt;String&gt;,
    delete_lock: TimeLock,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
): notarization::Notarization&lt;D&gt; {
    notarization::new_locked_notarization(
        state,
        immutable_description,
        updatable_metadata,
        delete_lock,
        clock,
        ctx,
    )
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_locked_notarization_create"></a>

## Function `create`

Create and transfer a new locked notarization to the sender


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/locked_notarization.md#(iota_notarization=0x0)_locked_notarization_create">create</a>&lt;D: <b>copy</b>, drop, store&gt;(state: (iota_notarization=0x0)::notarization::State&lt;D&gt;, immutable_description: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, updatable_metadata: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, delete_lock: (iota_notarization=0x0)::timelock::TimeLock, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/locked_notarization.md#(iota_notarization=0x0)_locked_notarization_create">create</a>&lt;D: store + drop + <b>copy</b>&gt;(
    state: notarization::State&lt;D&gt;,
    immutable_description: Option&lt;String&gt;,
    updatable_metadata: Option&lt;String&gt;,
    delete_lock: TimeLock,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> notarization = <a href="../../dependencies/nplex/locked_notarization.md#(iota_notarization=0x0)_locked_notarization_new">new</a>(
        state,
        immutable_description,
        updatable_metadata,
        delete_lock,
        clock,
        ctx,
    );
    <b>let</b> id = object::uid_to_inner(notarization.id());
    event::emit(<a href="../../dependencies/nplex/locked_notarization.md#(iota_notarization=0x0)_locked_notarization_LockedNotarizationCreated">LockedNotarizationCreated</a> { notarization_id: id });
    notarization::transfer_notarization(notarization, tx_context::sender(ctx));
}
</code></pre>



</details>
