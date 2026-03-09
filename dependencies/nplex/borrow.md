
<a name="(iota_identity=0x0)_borrow_proposal"></a>

# Module `(iota_identity=0x0)::borrow_proposal`



-  [Struct `Borrow`](#(iota_identity=0x0)_borrow_proposal_Borrow)
-  [Constants](#@Constants_0)
-  [Function `propose_borrow`](#(iota_identity=0x0)_borrow_proposal_propose_borrow)
-  [Function `borrow`](#(iota_identity=0x0)_borrow_proposal_borrow)
-  [Function `put_back`](#(iota_identity=0x0)_borrow_proposal_put_back)
-  [Function `conclude_borrow`](#(iota_identity=0x0)_borrow_proposal_conclude_borrow)


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



<a name="(iota_identity=0x0)_borrow_proposal_Borrow"></a>

## Struct `Borrow`

Action used to "borrow" assets in a transaction - enforcing their return.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_Borrow">Borrow</a> <b>has</b> drop, store
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
<code>objects_to_return: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>owner: <b>address</b></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(iota_identity=0x0)_borrow_proposal_EInvalidObject"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_EInvalidObject">EInvalidObject</a>: u64 = 0;
</code></pre>



<a name="(iota_identity=0x0)_borrow_proposal_EInvalidOwner"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_EInvalidOwner">EInvalidOwner</a>: u64 = 1;
</code></pre>



<a name="(iota_identity=0x0)_borrow_proposal_EUnreturnedObjects"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_EUnreturnedObjects">EUnreturnedObjects</a>: u64 = 2;
</code></pre>



<a name="(iota_identity=0x0)_borrow_proposal_propose_borrow"></a>

## Function `propose_borrow`

Propose the borrowing of a set of assets owned by this multicontroller.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_propose_borrow">propose_borrow</a>&lt;V&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, objects: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;, owner: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_propose_borrow">propose_borrow</a>&lt;V&gt;(
    multi: &<b>mut</b> Multicontroller&lt;V&gt;,
    cap: &DelegationToken,
    expiration: Option&lt;u64&gt;,
    objects: vector&lt;ID&gt;,
    owner: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
): ID {
    <b>let</b> action = <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_Borrow">Borrow</a> { objects, objects_to_return: vector::empty(), owner };
    multi.create_proposal(cap, action, expiration, ctx)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_borrow_proposal_borrow"></a>

## Function `borrow`

Borrows an asset from this action. This function will fail if:
- the received object is not among <code>Borrow::objects</code>;
- controllee does not have the same address as <code>Borrow::owner</code>;


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_borrow">borrow</a>&lt;T: key, store&gt;(action: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::borrow_proposal::Borrow&gt;, controllee: &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>, receiving: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;T&gt;): T
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_borrow">borrow</a>&lt;T: key + store&gt;(
    action: &<b>mut</b> Action&lt;<a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_Borrow">Borrow</a>&gt;,
    controllee: &<b>mut</b> UID,
    receiving: Receiving&lt;T&gt;,
): T {
    <b>let</b> borrow_action = action.borrow_mut();
    <b>assert</b>!(borrow_action.owner == controllee.to_address(), <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_EInvalidOwner">EInvalidOwner</a>);
    <b>let</b> receiving_object_id = receiving.receiving_object_id();
    <b>let</b> (obj_exists, obj_idx) = borrow_action.objects.index_of(&receiving_object_id);
    <b>assert</b>!(obj_exists, <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_EInvalidObject">EInvalidObject</a>);
    borrow_action.objects.swap_remove(obj_idx);
    borrow_action.objects_to_return.push_back(receiving_object_id);
    transfer::public_receive(controllee, receiving)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_borrow_proposal_put_back"></a>

## Function `put_back`

Transfer a borrowed object back to its original owner.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_put_back">put_back</a>&lt;T: key, store&gt;(action: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::borrow_proposal::Borrow&gt;, obj: T)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_put_back">put_back</a>&lt;T: key + store&gt;(action: &<b>mut</b> Action&lt;<a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_Borrow">Borrow</a>&gt;, obj: T) {
    <b>let</b> borrow_action = action.borrow_mut();
    <b>let</b> object_id = object::id(&obj);
    <b>let</b> (contains, obj_idx) = borrow_action.objects_to_return.index_of(&object_id);
    <b>assert</b>!(contains, <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_EInvalidObject">EInvalidObject</a>);
    borrow_action.objects_to_return.swap_remove(obj_idx);
    transfer::public_transfer(obj, borrow_action.owner);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_borrow_proposal_conclude_borrow"></a>

## Function `conclude_borrow`

Consumes a borrow action.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_conclude_borrow">conclude_borrow</a>(action: (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::borrow_proposal::Borrow&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_conclude_borrow">conclude_borrow</a>(action: Action&lt;<a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_Borrow">Borrow</a>&gt;) {
    <b>let</b> <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_Borrow">Borrow</a> { objects: _, objects_to_return, owner: _ } = action.unpack_action();
    <b>assert</b>!(objects_to_return.is_empty(), <a href="../../dependencies/nplex/borrow.md#(iota_identity=0x0)_borrow_proposal_EUnreturnedObjects">EUnreturnedObjects</a>);
}
</code></pre>



</details>
