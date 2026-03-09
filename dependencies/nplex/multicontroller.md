
<a name="(iota_identity=0x0)_multicontroller"></a>

# Module `(iota_identity=0x0)::multicontroller`



-  [Struct `Multicontroller`](#(iota_identity=0x0)_multicontroller_Multicontroller)
-  [Struct `Proposal`](#(iota_identity=0x0)_multicontroller_Proposal)
-  [Struct `Action`](#(iota_identity=0x0)_multicontroller_Action)
-  [Constants](#@Constants_0)
-  [Function `new`](#(iota_identity=0x0)_multicontroller_new)
-  [Function `new_with_controller`](#(iota_identity=0x0)_multicontroller_new_with_controller)
-  [Function `new_with_controllers`](#(iota_identity=0x0)_multicontroller_new_with_controllers)
-  [Function `is_expired`](#(iota_identity=0x0)_multicontroller_is_expired)
-  [Function `unwrap`](#(iota_identity=0x0)_multicontroller_unwrap)
-  [Function `borrow`](#(iota_identity=0x0)_multicontroller_borrow)
-  [Function `borrow_mut`](#(iota_identity=0x0)_multicontroller_borrow_mut)
-  [Function `assert_is_member`](#(iota_identity=0x0)_multicontroller_assert_is_member)
-  [Function `create_proposal`](#(iota_identity=0x0)_multicontroller_create_proposal)
-  [Function `approve_proposal`](#(iota_identity=0x0)_multicontroller_approve_proposal)
-  [Function `execute_proposal`](#(iota_identity=0x0)_multicontroller_execute_proposal)
-  [Function `remove_approval`](#(iota_identity=0x0)_multicontroller_remove_approval)
-  [Function `delete_proposal`](#(iota_identity=0x0)_multicontroller_delete_proposal)
-  [Function `value`](#(iota_identity=0x0)_multicontroller_value)
-  [Function `controllers`](#(iota_identity=0x0)_multicontroller_controllers)
-  [Function `threshold`](#(iota_identity=0x0)_multicontroller_threshold)
-  [Function `voting_power`](#(iota_identity=0x0)_multicontroller_voting_power)
-  [Function `set_voting_power`](#(iota_identity=0x0)_multicontroller_set_voting_power)
-  [Function `max_votes`](#(iota_identity=0x0)_multicontroller_max_votes)
-  [Function `revoke_token`](#(iota_identity=0x0)_multicontroller_revoke_token)
-  [Function `unrevoke_token`](#(iota_identity=0x0)_multicontroller_unrevoke_token)
-  [Function `destroy_controller_cap`](#(iota_identity=0x0)_multicontroller_destroy_controller_cap)
-  [Function `remove_and_destroy_controller`](#(iota_identity=0x0)_multicontroller_remove_and_destroy_controller)
-  [Function `destroy_delegation_token`](#(iota_identity=0x0)_multicontroller_destroy_delegation_token)
-  [Function `delete`](#(iota_identity=0x0)_multicontroller_delete)
-  [Function `unpack_action`](#(iota_identity=0x0)_multicontroller_unpack_action)
-  [Function `is_proposal_approved`](#(iota_identity=0x0)_multicontroller_is_proposal_approved)
-  [Function `add_members`](#(iota_identity=0x0)_multicontroller_add_members)
-  [Function `owner`](#(iota_identity=0x0)_multicontroller_owner)
-  [Function `remove_members`](#(iota_identity=0x0)_multicontroller_remove_members)
-  [Function `update_members`](#(iota_identity=0x0)_multicontroller_update_members)
-  [Function `set_threshold`](#(iota_identity=0x0)_multicontroller_set_threshold)
-  [Function `set_controlled_value`](#(iota_identity=0x0)_multicontroller_set_controlled_value)
-  [Function `force_delete_proposal`](#(iota_identity=0x0)_multicontroller_force_delete_proposal)


<pre><code><b>use</b> (iota_identity=0x0)::controller;
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



<a name="(iota_identity=0x0)_multicontroller_Multicontroller"></a>

## Struct `Multicontroller`

Shares control of a value <code>V</code> with multiple entities called controllers.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt; <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>: u64</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, u64&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>controlled_value: V</code>
</dt>
<dd>
</dd>
<dt>
<code>active_proposals: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>proposals: <a href="../../dependencies/iota/object_bag.md#iota_object_bag_ObjectBag">iota::object_bag::ObjectBag</a></code>
</dt>
<dd>
</dd>
<dt>
<code>revoked_tokens: <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_multicontroller_Proposal"></a>

## Struct `Proposal`

Structure that encapsulates the logic required to make changes
to a multicontrolled value.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a>&lt;T: store&gt; <b>has</b> key, store
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
<code>votes: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>voters: <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>expiration_epoch: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>action: T</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_multicontroller_Action"></a>

## Struct `Action`

Structure that encapsulate the kind of change that will be performed
when a proposal is carried out.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Action">Action</a>&lt;T: store&gt;
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>inner: T</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(iota_identity=0x0)_multicontroller_EInvalidController"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EInvalidController">EInvalidController</a>: u64 = 0;
</code></pre>



<a name="(iota_identity=0x0)_multicontroller_EControllerAlreadyVoted"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EControllerAlreadyVoted">EControllerAlreadyVoted</a>: u64 = 1;
</code></pre>



<a name="(iota_identity=0x0)_multicontroller_EThresholdNotReached"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EThresholdNotReached">EThresholdNotReached</a>: u64 = 2;
</code></pre>



<a name="(iota_identity=0x0)_multicontroller_EInvalidThreshold"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EInvalidThreshold">EInvalidThreshold</a>: u64 = 3;
</code></pre>



<a name="(iota_identity=0x0)_multicontroller_EExpiredProposal"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EExpiredProposal">EExpiredProposal</a>: u64 = 4;
</code></pre>



<a name="(iota_identity=0x0)_multicontroller_ENotVotedYet"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_ENotVotedYet">ENotVotedYet</a>: u64 = 5;
</code></pre>



<a name="(iota_identity=0x0)_multicontroller_EProposalNotFound"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EProposalNotFound">EProposalNotFound</a>: u64 = 6;
</code></pre>



<a name="(iota_identity=0x0)_multicontroller_ECannotDelete"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_ECannotDelete">ECannotDelete</a>: u64 = 7;
</code></pre>



<a name="(iota_identity=0x0)_multicontroller_new"></a>

## Function `new`

Wraps a <code>V</code> in <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a></code>, making the tx's sender a controller with
voting power 1.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_new">new</a>&lt;V&gt;(controlled_value: V, can_delegate: bool, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_new">new</a>&lt;V&gt;(
    controlled_value: V,
    can_delegate: bool,
    <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>: ID,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt; {
    <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_new_with_controller">new_with_controller</a>(controlled_value, ctx.sender(), can_delegate, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>, ctx)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_new_with_controller"></a>

## Function `new_with_controller`

Wraps a <code>V</code> in <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a></code> and sends <code>controller</code> a <code>ControllerCap</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_new_with_controller">new_with_controller</a>&lt;V&gt;(controlled_value: V, controller: <b>address</b>, can_delegate: bool, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_new_with_controller">new_with_controller</a>&lt;V&gt;(
    controlled_value: V,
    controller: <b>address</b>,
    can_delegate: bool,
    <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>: ID,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt; {
    <b>let</b> <b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a> = vec_map::empty();
    <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.insert(controller, 1);
    <b>if</b> (can_delegate) {
        <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_new_with_controllers">new_with_controllers</a>(controlled_value, vec_map::empty(), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>, 1, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>, ctx)
    } <b>else</b> {
        <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_new_with_controllers">new_with_controllers</a>(controlled_value, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>, vec_map::empty(), 1, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>, ctx)
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_new_with_controllers"></a>

## Function `new_with_controllers`

Wraps a <code>V</code> in <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a></code>, settings <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a></code> as the threshold,
and using <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a></code> to set controllers: i.e. each <code>(recipient, voting power)</code>
in <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a></code> results in <code>recipient</code> obtaining a <code>ControllerCap</code> with the
specified voting power.
Controllers that are able to delegate their access, should be passed through
<code>controllers_that_can_delegate</code> parameter.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_new_with_controllers">new_with_controllers</a>&lt;V&gt;(controlled_value: V, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;, controllers_that_can_delegate: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>: u64, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_new_with_controllers">new_with_controllers</a>&lt;V&gt;(
    controlled_value: V,
    <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>: VecMap&lt;<b>address</b>, u64&gt;,
    controllers_that_can_delegate: VecMap&lt;<b>address</b>, u64&gt;,
    <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>: u64,
    <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>: ID,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt; {
    <b>let</b> (addrs, vps) = <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.into_keys_values();
    <b>let</b> <b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a> = vec_map::empty();
    vector::zip_do!(addrs, vps, |addr, vp| {
        <b>let</b> cap = controller::new(<b>false</b>, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>, ctx);
        <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.insert(cap.id().to_inner(), vp);
        cap.transfer(addr);
    });
    <b>let</b> (addrs, vps) = controllers_that_can_delegate.into_keys_values();
    vector::zip_do!(addrs, vps, |addr, vp| {
        <b>let</b> cap = controller::new(<b>true</b>, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>, ctx);
        <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.insert(cap.id().to_inner(), vp);
        cap.transfer(addr)
    });
    <b>let</b> <b>mut</b> multi = <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a> {
        controlled_value,
        <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>,
        <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>,
        <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>,
        active_proposals: vector[],
        proposals: object_bag::new(ctx),
        revoked_tokens: vec_set::empty(),
    };
    multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_set_threshold">set_threshold</a>(<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>);
    multi
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_is_expired"></a>

## Function `is_expired`

Returns <code><b>true</b></code> if <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a></code> <code>self</code> is expired.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_is_expired">is_expired</a>&lt;T: store&gt;(self: &(iota_identity=0x0)::multicontroller::Proposal&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_is_expired">is_expired</a>&lt;T: store&gt;(self: &<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a>&lt;T&gt;, ctx: &<b>mut</b> TxContext): bool {
    <b>if</b> (self.expiration_epoch.is_some()) {
        <b>let</b> expiration = *self.expiration_epoch.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_borrow">borrow</a>();
        expiration &lt; ctx.epoch()
    } <b>else</b> {
        <b>false</b>
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_unwrap"></a>

## Function `unwrap`

Consumes <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Action">Action</a></code> returning the inner value.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_unwrap">unwrap</a>&lt;T: store&gt;(action: (iota_identity=0x0)::multicontroller::Action&lt;T&gt;): T
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_unwrap">unwrap</a>&lt;T: store&gt;(action: <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Action">Action</a>&lt;T&gt;): T {
    <b>let</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Action">Action</a> { inner } = action;
    inner
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_borrow"></a>

## Function `borrow`

Borrows the content of <code>action</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_borrow">borrow</a>&lt;T: store&gt;(action: &(iota_identity=0x0)::multicontroller::Action&lt;T&gt;): &T
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_borrow">borrow</a>&lt;T: store&gt;(action: &<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Action">Action</a>&lt;T&gt;): &T {
    &action.inner
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_borrow_mut"></a>

## Function `borrow_mut`

Mutably borrows the content of <code>action</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_borrow_mut">borrow_mut</a>&lt;T: store&gt;(action: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;T&gt;): &<b>mut</b> T
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_borrow_mut">borrow_mut</a>&lt;T: store&gt;(action: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Action">Action</a>&lt;T&gt;): &<b>mut</b> T {
    &<b>mut</b> action.inner
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_assert_is_member"></a>

## Function `assert_is_member`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_assert_is_member">assert_is_member</a>&lt;V&gt;(multi: &(iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_assert_is_member">assert_is_member</a>&lt;V&gt;(multi: &<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;, cap: &DelegationToken) {
    <b>assert</b>!(multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.contains(&cap.controller()), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EInvalidController">EInvalidController</a>);
    // Make sure the presented token hasn't been revoked.
    <b>assert</b>!(!multi.revoked_tokens.contains(&cap.id()), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EInvalidController">EInvalidController</a>);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_create_proposal"></a>

## Function `create_proposal`

Creates a new proposal for <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a></code> <code>multi</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_create_proposal">create_proposal</a>&lt;V, T: store&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken, action: T, expiration_epoch: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_create_proposal">create_proposal</a>&lt;V, T: store&gt;(
    multi: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;,
    cap: &DelegationToken,
    action: T,
    expiration_epoch: Option&lt;u64&gt;,
    ctx: &<b>mut</b> TxContext,
): ID {
    multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_assert_is_member">assert_is_member</a>(cap);
    cap.assert_has_permission(permissions::can_create_proposal());
    <b>let</b> cap_id = cap.controller();
    <b>let</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_voting_power">voting_power</a> = multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_voting_power">voting_power</a>(cap_id);
    <b>let</b> proposal = <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a> {
        id: object::new(ctx),
        votes: <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_voting_power">voting_power</a>,
        voters: vec_set::singleton(cap_id),
        expiration_epoch,
        action,
    };
    <b>let</b> proposal_id = object::id(&proposal);
    multi.proposals.add(proposal_id, proposal);
    multi.active_proposals.push_back(proposal_id);
    proposal_id
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_approve_proposal"></a>

## Function `approve_proposal`

Approves an active <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a></code> in <code>multi</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_approve_proposal">approve_proposal</a>&lt;V, T: store&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_approve_proposal">approve_proposal</a>&lt;V, T: store&gt;(
    multi: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;,
    cap: &DelegationToken,
    proposal_id: ID,
) {
    multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_assert_is_member">assert_is_member</a>(cap);
    cap.assert_has_permission(permissions::can_approve_proposal());
    <b>let</b> cap_id = cap.controller();
    <b>let</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_voting_power">voting_power</a> = multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_voting_power">voting_power</a>(cap_id);
    <b>let</b> proposal = multi.proposals.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_borrow_mut">borrow_mut</a>&lt;ID, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a>&lt;T&gt;&gt;(proposal_id);
    <b>assert</b>!(!proposal.voters.contains(&cap_id), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EControllerAlreadyVoted">EControllerAlreadyVoted</a>);
    proposal.votes = proposal.votes + <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_voting_power">voting_power</a>;
    proposal.voters.insert(cap_id);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_execute_proposal"></a>

## Function `execute_proposal`

Consumes the <code>multi</code>'s active <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a></code> with id <code>proposal_id</code>,
returning its inner <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Action">Action</a></code>.
This call fails if <code>multi</code>'s threshold has not been reached.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_execute_proposal">execute_proposal</a>&lt;V, T: store&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (iota_identity=0x0)::multicontroller::Action&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_execute_proposal">execute_proposal</a>&lt;V, T: store&gt;(
    multi: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;,
    cap: &DelegationToken,
    proposal_id: ID,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Action">Action</a>&lt;T&gt; {
    multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_assert_is_member">assert_is_member</a>(cap);
    cap.assert_has_permission(permissions::can_execute_proposal());
    <b>let</b> proposal = multi.proposals.remove&lt;ID, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a>&lt;T&gt;&gt;(proposal_id);
    <b>assert</b>!(proposal.votes &gt;= multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EThresholdNotReached">EThresholdNotReached</a>);
    <b>assert</b>!(!proposal.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_is_expired">is_expired</a>(ctx), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EExpiredProposal">EExpiredProposal</a>);
    <b>let</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a> {
        id,
        votes: _,
        voters: _,
        expiration_epoch: _,
        action: inner,
    } = proposal;
    id.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_delete">delete</a>();
    <b>let</b> (present, i) = multi.active_proposals.index_of(&proposal_id);
    <b>assert</b>!(present, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EProposalNotFound">EProposalNotFound</a>);
    multi.active_proposals.remove(i);
    <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Action">Action</a> { inner }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_remove_approval"></a>

## Function `remove_approval`

Removes the approval given by the controller owning <code>cap</code> on <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a></code>
<code>proposal_id</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_remove_approval">remove_approval</a>&lt;V, T: store&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_remove_approval">remove_approval</a>&lt;V, T: store&gt;(
    multi: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;,
    cap: &DelegationToken,
    proposal_id: ID,
) {
    cap.assert_has_permission(permissions::can_remove_approval());
    <b>let</b> cap_id = cap.controller();
    <b>let</b> vp = multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_voting_power">voting_power</a>(cap_id);
    <b>let</b> proposal = multi.proposals.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_borrow_mut">borrow_mut</a>&lt;ID, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a>&lt;T&gt;&gt;(proposal_id);
    <b>assert</b>!(proposal.voters.contains(&cap_id), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_ENotVotedYet">ENotVotedYet</a>);
    proposal.voters.remove(&cap_id);
    proposal.votes = proposal.votes - vp;
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_delete_proposal"></a>

## Function `delete_proposal`

Removes a proposal no one has voted for.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_delete_proposal">delete_proposal</a>&lt;V, T: drop, store&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_delete_proposal">delete_proposal</a>&lt;V, T: store + drop&gt;(
    multi: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;,
    cap: &DelegationToken,
    proposal_id: ID,
    ctx: &<b>mut</b> TxContext,
) {
    cap.assert_has_permission(permissions::can_delete_proposal());
    <b>let</b> proposal = multi.proposals.remove&lt;ID, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a>&lt;T&gt;&gt;(proposal_id);
    <b>assert</b>!(proposal.votes == 0 || proposal.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_is_expired">is_expired</a>(ctx), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_ECannotDelete">ECannotDelete</a>);
    <b>let</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a> {
        id,
        votes: _,
        voters: _,
        expiration_epoch: _,
        action: _,
    } = proposal;
    id.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_delete">delete</a>();
    <b>let</b> (present, i) = multi.active_proposals.index_of(&proposal_id);
    <b>assert</b>!(present, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EProposalNotFound">EProposalNotFound</a>);
    multi.active_proposals.remove(i);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_value"></a>

## Function `value`

Returns a reference to <code>multi</code>'s value.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_value">value</a>&lt;V: store&gt;(multi: &(iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;): &V
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_value">value</a>&lt;V: store&gt;(multi: &<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;): &V {
    &multi.controlled_value
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_controllers"></a>

## Function `controllers`

Returns the list of <code>multi</code>'s controllers - i.e. the <code>ID</code> of its <code>ControllerCap</code>s.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>&lt;V&gt;(multi: &(iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;): vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>&lt;V&gt;(multi: &<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;): vector&lt;ID&gt; {
    multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.keys()
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_threshold"></a>

## Function `threshold`

Returns <code>multi</code>'s threshold.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>&lt;V&gt;(multi: &(iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>&lt;V&gt;(multi: &<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;): u64 {
    multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_voting_power"></a>

## Function `voting_power`

Returns the voting power of a given controller, identified by its <code>ID</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_voting_power">voting_power</a>&lt;V&gt;(multi: &(iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, controller_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_voting_power">voting_power</a>&lt;V&gt;(multi: &<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;, controller_id: ID): u64 {
    *multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.get(&controller_id)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_set_voting_power"></a>

## Function `set_voting_power`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_set_voting_power">set_voting_power</a>&lt;V&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, controller_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, vp: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_set_voting_power">set_voting_power</a>&lt;V&gt;(
    multi: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;,
    controller_id: ID,
    vp: u64,
) {
    <b>assert</b>!(multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>().contains(&controller_id), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EInvalidController">EInvalidController</a>);
    *multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.get_mut(&controller_id) = vp;
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_max_votes"></a>

## Function `max_votes`

Returns the sum of all controllers voting powers.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_max_votes">max_votes</a>&lt;V&gt;(multi: &(iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_max_votes">max_votes</a>&lt;V&gt;(multi: &<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;): u64 {
    <b>let</b> (_, <b>mut</b> values) = multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.into_keys_values();
    <b>let</b> <b>mut</b> sum = 0;
    <b>while</b> (!values.is_empty()) {
        sum = sum + values.pop_back();
    };
    sum
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_revoke_token"></a>

## Function `revoke_token`

Revoke the <code>DelegationToken</code> with <code>ID</code> <code>deny_id</code>. Only controllers can perform this operation.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_revoke_token">revoke_token</a>&lt;V&gt;(self: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::ControllerCap, deny_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_revoke_token">revoke_token</a>&lt;V&gt;(self: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;, cap: &ControllerCap, deny_id: ID) {
    <b>assert</b>!(self.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.contains(object::borrow_id(cap)), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EInvalidController">EInvalidController</a>);
    self.revoked_tokens.insert(deny_id);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_unrevoke_token"></a>

## Function `unrevoke_token`

Un-revoke a <code>DelegationToken</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_unrevoke_token">unrevoke_token</a>&lt;V&gt;(self: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::ControllerCap, token_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_unrevoke_token">unrevoke_token</a>&lt;V&gt;(self: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;, cap: &ControllerCap, token_id: ID) {
    <b>assert</b>!(self.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.contains(object::borrow_id(cap)), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EInvalidController">EInvalidController</a>);
    self.revoked_tokens.remove(&token_id);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_destroy_controller_cap"></a>

## Function `destroy_controller_cap`

Destroys a <code>ControllerCap</code>. Can only be used after a controller has been removed from
the controller committee.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_destroy_controller_cap">destroy_controller_cap</a>&lt;V&gt;(self: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: (iota_identity=0x0)::controller::ControllerCap)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_destroy_controller_cap">destroy_controller_cap</a>&lt;V&gt;(self: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;, cap: ControllerCap) {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.contains(&cap.id().to_inner()), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EInvalidController">EInvalidController</a>);
    <b>assert</b>!(cap.controller_of() == self.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EInvalidController">EInvalidController</a>);
    cap.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_delete">delete</a>();
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_remove_and_destroy_controller"></a>

## Function `remove_and_destroy_controller`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_remove_and_destroy_controller">remove_and_destroy_controller</a>&lt;V&gt;(self: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: (iota_identity=0x0)::controller::ControllerCap)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_remove_and_destroy_controller">remove_and_destroy_controller</a>&lt;V&gt;(self: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;, cap: ControllerCap) {
    <b>assert</b>!(cap.controller_of() == self.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EInvalidController">EInvalidController</a>);
    <b>let</b> controller_id = object::id(&cap);
    <b>if</b> (self.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.contains(&controller_id)) {
        self.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.remove(&controller_id);
    };
    cap.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_delete">delete</a>();
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_destroy_delegation_token"></a>

## Function `destroy_delegation_token`

Destroys a <code>DelegationToken</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_destroy_delegation_token">destroy_delegation_token</a>&lt;V&gt;(self: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, token: (iota_identity=0x0)::controller::DelegationToken)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_destroy_delegation_token">destroy_delegation_token</a>&lt;V&gt;(self: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;, token: DelegationToken) {
    <b>let</b> token_id = object::id(&token);
    <b>let</b> is_revoked = self.revoked_tokens.contains(&token_id);
    <b>if</b> (is_revoked) {
        self.revoked_tokens.remove(&token_id);
    };
    token.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_delete">delete</a>();
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_delete"></a>

## Function `delete`

Deletes this <code><a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a></code> returning the wrapped value.
This function can only be called if there are no active proposals.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_delete">delete</a>&lt;V&gt;(self: (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;): V
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_delete">delete</a>&lt;V&gt;(self: <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;): V {
    <b>assert</b>!(self.active_proposals.is_empty(), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_ECannotDelete">ECannotDelete</a>);
    <b>let</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a> {
        controlled_value,
        proposals,
        ..,
    } = self;
    proposals.destroy_empty();
    controlled_value
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_unpack_action"></a>

## Function `unpack_action`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_unpack_action">unpack_action</a>&lt;T: store&gt;(action: (iota_identity=0x0)::multicontroller::Action&lt;T&gt;): T
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_unpack_action">unpack_action</a>&lt;T: store&gt;(action: <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Action">Action</a>&lt;T&gt;): T {
    <b>let</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Action">Action</a> { inner } = action;
    inner
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_is_proposal_approved"></a>

## Function `is_proposal_approved`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_is_proposal_approved">is_proposal_approved</a>&lt;V, A: store&gt;(multi: &(iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_is_proposal_approved">is_proposal_approved</a>&lt;V, A: store&gt;(
    multi: &<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;,
    proposal_id: ID,
): bool {
    <b>let</b> proposal = multi.proposals.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_borrow">borrow</a>&lt;ID, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a>&lt;A&gt;&gt;(proposal_id);
    proposal.votes &gt;= multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_add_members"></a>

## Function `add_members`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_add_members">add_members</a>&lt;V&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, to_add: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_add_members">add_members</a>&lt;V&gt;(
    multi: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;,
    to_add: VecMap&lt;<b>address</b>, u64&gt;,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; to_add.size()) {
        <b>let</b> (addr, vp) = to_add.get_entry_by_idx(i);
        <b>let</b> new_cap = controller::new(<b>false</b>, multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>, ctx);
        multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.insert(new_cap.id().to_inner(), *vp);
        new_cap.transfer(*addr);
        i = i + 1;
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_owner"></a>

## Function `owner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>&lt;V&gt;(multi: &(iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>&lt;V&gt;(multi: &<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;): ID {
    multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_owner">owner</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_remove_members"></a>

## Function `remove_members`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_remove_members">remove_members</a>&lt;V&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, to_remove: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_remove_members">remove_members</a>&lt;V&gt;(multi: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;, <b>mut</b> to_remove: vector&lt;ID&gt;) {
    <b>while</b> (!to_remove.is_empty()) {
        <b>let</b> id = to_remove.pop_back();
        multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_controllers">controllers</a>.remove(&id);
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_update_members"></a>

## Function `update_members`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_update_members">update_members</a>&lt;V&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, to_update: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, u64&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_update_members">update_members</a>&lt;V&gt;(
    multi: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;,
    <b>mut</b> to_update: VecMap&lt;ID, u64&gt;,
) {
    <b>while</b> (!to_update.is_empty()) {
        <b>let</b> (controller, vp) = to_update.pop();
        multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_set_voting_power">set_voting_power</a>(controller, vp);
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_set_threshold"></a>

## Function `set_threshold`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_set_threshold">set_threshold</a>&lt;V&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_set_threshold">set_threshold</a>&lt;V&gt;(multi: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>: u64) {
    <b>assert</b>!(<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a> &lt;= multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_max_votes">max_votes</a>(), <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_EInvalidThreshold">EInvalidThreshold</a>);
    multi.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a> = <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_threshold">threshold</a>;
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_set_controlled_value"></a>

## Function `set_controlled_value`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_set_controlled_value">set_controlled_value</a>&lt;V: drop, store&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, controlled_value: V)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_set_controlled_value">set_controlled_value</a>&lt;V: store + drop&gt;(
    multi: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;,
    controlled_value: V,
) {
    multi.controlled_value = controlled_value;
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_multicontroller_force_delete_proposal"></a>

## Function `force_delete_proposal`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_force_delete_proposal">force_delete_proposal</a>&lt;V, T: drop, store&gt;(self: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_force_delete_proposal">force_delete_proposal</a>&lt;V, T: drop + store&gt;(
    self: &<b>mut</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Multicontroller">Multicontroller</a>&lt;V&gt;,
    proposal_id: ID,
) {
    <b>let</b> proposal = self.proposals.remove&lt;ID, <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a>&lt;T&gt;&gt;(proposal_id);
    <b>let</b> <a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_Proposal">Proposal</a>&lt;T&gt; {
        id,
        ..,
    } = proposal;
    id.<a href="../../dependencies/nplex/multicontroller.md#(iota_identity=0x0)_multicontroller_delete">delete</a>();
}
</code></pre>



</details>
