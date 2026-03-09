
<a name="(iota_identity=0x0)_transfer_proposal"></a>

# Module `(iota_identity=0x0)::transfer_proposal`



-  [Struct `Send`](#(iota_identity=0x0)_transfer_proposal_Send)
-  [Constants](#@Constants_0)
-  [Function `propose_send`](#(iota_identity=0x0)_transfer_proposal_propose_send)
-  [Function `send`](#(iota_identity=0x0)_transfer_proposal_send)
-  [Function `complete_send`](#(iota_identity=0x0)_transfer_proposal_complete_send)


<pre><code><b>use</b> (iota_identity=0x0)::controller;
<b>use</b> (iota_identity=0x0)::multicontroller;
<b>use</b> (iota_identity=0x0)::permissions;
<b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/borrow.md#iota_borrow">iota::borrow</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/object_bag.md#iota_object_bag">iota::object_bag</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/iota/vec_set.md#iota_vec_set">iota::vec_set</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="(iota_identity=0x0)_transfer_proposal_Send"></a>

## Struct `Send`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_Send">Send</a> <b>has</b> drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>objects: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>recipients: vector&lt;<b>address</b>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(iota_identity=0x0)_transfer_proposal_EDifferentLength"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_EDifferentLength">EDifferentLength</a>: u64 = 0;
</code></pre>



<a name="(iota_identity=0x0)_transfer_proposal_EUnsentAssets"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_EUnsentAssets">EUnsentAssets</a>: u64 = 1;
</code></pre>



<a name="(iota_identity=0x0)_transfer_proposal_EInvalidObject"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_EInvalidObject">EInvalidObject</a>: u64 = 2;
</code></pre>



<a name="(iota_identity=0x0)_transfer_proposal_propose_send"></a>

## Function `propose_send`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_propose_send">propose_send</a>&lt;V&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, objects: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;, recipients: vector&lt;<b>address</b>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_propose_send">propose_send</a>&lt;V&gt;(
    multi: &<b>mut</b> Multicontroller&lt;V&gt;,
    cap: &DelegationToken,
    expiration: Option&lt;u64&gt;,
    objects: vector&lt;ID&gt;,
    recipients: vector&lt;<b>address</b>&gt;,
    ctx: &<b>mut</b> TxContext,
): ID {
    <b>assert</b>!(objects.length() == recipients.length(), <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_EDifferentLength">EDifferentLength</a>);
    <b>let</b> action = <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_Send">Send</a> { objects, recipients };
    multi.create_proposal(cap, action, expiration, ctx)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_transfer_proposal_send"></a>

## Function `send`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_send">send</a>&lt;T: key, store&gt;(action: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::transfer_proposal::Send&gt;, controllee: &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>, received: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_send">send</a>&lt;T: key + store&gt;(
    action: &<b>mut</b> Action&lt;<a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_Send">Send</a>&gt;,
    controllee: &<b>mut</b> UID,
    received: Receiving&lt;T&gt;,
) {
    <b>let</b> send_action = action.borrow_mut();
    <b>let</b> object_id = received.receiving_object_id();
    <b>let</b> (object_exists, object_idx) = send_action.objects.index_of(&object_id);
    // Check that the received object is among the objects that are actually supposed to be sent.
    <b>assert</b>!(object_exists, <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_EInvalidObject">EInvalidObject</a>);
    <b>let</b> object = transfer::public_receive(controllee, received);
    // Get the corresponding recipient.
    <b>let</b> recipient = send_action.recipients.swap_remove(object_idx);
    transfer::public_transfer(object, recipient);
    // Update the list of objects that have not been sent yet.
    send_action.objects.swap_remove(object_idx);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_transfer_proposal_complete_send"></a>

## Function `complete_send`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_complete_send">complete_send</a>(action: (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::transfer_proposal::Send&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_complete_send">complete_send</a>(action: Action&lt;<a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_Send">Send</a>&gt;) {
    <b>let</b> <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_Send">Send</a> { objects, recipients } = action.unpack_action();
    <b>assert</b>!(recipients.is_empty() && objects.is_empty(), <a href="../../dependencies/nplex/transfer.md#(iota_identity=0x0)_transfer_proposal_EUnsentAssets">EUnsentAssets</a>);
    recipients.destroy_empty();
    objects.destroy_empty();
}
</code></pre>



</details>
