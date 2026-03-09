
<a name="(iota_identity=0x0)_controller_proposal"></a>

# Module `(iota_identity=0x0)::controller_proposal`



-  [Struct `ControllerExecution`](#(iota_identity=0x0)_controller_proposal_ControllerExecution)
-  [Constants](#@Constants_0)
-  [Function `new`](#(iota_identity=0x0)_controller_proposal_new)
-  [Function `receive`](#(iota_identity=0x0)_controller_proposal_receive)
-  [Function `put_back`](#(iota_identity=0x0)_controller_proposal_put_back)


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



<a name="(iota_identity=0x0)_controller_proposal_ControllerExecution"></a>

## Struct `ControllerExecution`

Borrow a given <code>ControllerCap</code> from an <code>Identity</code> for
a single transaction.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_ControllerExecution">ControllerExecution</a> <b>has</b> drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>controller_cap: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 ID of the <code>ControllerCap</code> to borrow.
</dd>
<dt>
<code>identity: <b>address</b></code>
</dt>
<dd>
 The address of the <code>Identity</code> that owns
 the <code>ControllerCap</code> we are borrowing.
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(iota_identity=0x0)_controller_proposal_EControllerCapMismatch"></a>

The received <code>ControllerCap</code> does not match the one
specified in the <code><a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_ControllerExecution">ControllerExecution</a></code> action.


<pre><code><b>const</b> <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_EControllerCapMismatch">EControllerCapMismatch</a>: u64 = 0;
</code></pre>



<a name="(iota_identity=0x0)_controller_proposal_EInvalidIdentityUID"></a>

The provided <code>UID</code> is not the <code>UID</code> of the <code>Identity</code>
specified in the action.


<pre><code><b>const</b> <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_EInvalidIdentityUID">EInvalidIdentityUID</a>: u64 = 1;
</code></pre>



<a name="(iota_identity=0x0)_controller_proposal_new"></a>

## Function `new`

Returns a new <code><a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_ControllerExecution">ControllerExecution</a></code> that - in a Proposal - allows whoever
executes it to receive <code>identity</code>'s <code>ControllerCap</code> (the one that has ID <code>controller_cap</code>)
for the duration of a single transaction.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_new">new</a>(controller_cap: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, identity: <b>address</b>): (iota_identity=0x0)::controller_proposal::ControllerExecution
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_new">new</a>(controller_cap: ID, identity: <b>address</b>): <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_ControllerExecution">ControllerExecution</a> {
    <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_ControllerExecution">ControllerExecution</a> {
        controller_cap,
        identity,
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_controller_proposal_receive"></a>

## Function `receive`

Returns the <code>ControllerCap</code> specified in this action.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_receive">receive</a>(self: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::controller_proposal::ControllerExecution&gt;, identity: &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>, cap: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;(iota_identity=0x0)::controller::ControllerCap&gt;): (iota_identity=0x0)::controller::ControllerCap
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_receive">receive</a>(
    self: &<b>mut</b> Action&lt;<a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_ControllerExecution">ControllerExecution</a>&gt;,
    identity: &<b>mut</b> UID,
    cap: Receiving&lt;ControllerCap&gt;,
): ControllerCap {
    <b>assert</b>!(identity.to_address() == self.borrow().identity, <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_EInvalidIdentityUID">EInvalidIdentityUID</a>);
    <b>assert</b>!(cap.receiving_object_id() == self.borrow().controller_cap, <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_EControllerCapMismatch">EControllerCapMismatch</a>);
    controller::receive(identity, cap)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_controller_proposal_put_back"></a>

## Function `put_back`

Consumes a <code><a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_ControllerExecution">ControllerExecution</a></code> action by returning the borrowed <code>ControllerCap</code>
to the corresponding <code>Identity</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_put_back">put_back</a>(action: (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::controller_proposal::ControllerExecution&gt;, cap: (iota_identity=0x0)::controller::ControllerCap)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_put_back">put_back</a>(action: Action&lt;<a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_ControllerExecution">ControllerExecution</a>&gt;, cap: ControllerCap) {
    <b>let</b> <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_ControllerExecution">ControllerExecution</a> { identity, controller_cap } = action.unwrap();
    <b>assert</b>!(object::id(&cap) == controller_cap, <a href="../../dependencies/nplex/controller.md#(iota_identity=0x0)_controller_proposal_EControllerCapMismatch">EControllerCapMismatch</a>);
    cap.transfer(identity);
}
</code></pre>



</details>
