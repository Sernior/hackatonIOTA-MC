
<a name="(iota_identity=0x0)_access_sub_entity_proposal"></a>

# Module `(iota_identity=0x0)::access_sub_entity_proposal`



-  [Struct `AccessSubEntity`](#(iota_identity=0x0)_access_sub_entity_proposal_AccessSubEntity)
-  [Constants](#@Constants_0)
-  [Function `new`](#(iota_identity=0x0)_access_sub_entity_proposal_new)
-  [Function `borrow_controller_cap`](#(iota_identity=0x0)_access_sub_entity_proposal_borrow_controller_cap)
-  [Function `borrow_delegation_token`](#(iota_identity=0x0)_access_sub_entity_proposal_borrow_delegation_token)
-  [Function `put_back_controller_cap`](#(iota_identity=0x0)_access_sub_entity_proposal_put_back_controller_cap)
-  [Function `put_back_delegation_token`](#(iota_identity=0x0)_access_sub_entity_proposal_put_back_delegation_token)


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



<a name="(iota_identity=0x0)_access_sub_entity_proposal_AccessSubEntity"></a>

## Struct `AccessSubEntity`

An action that let its executor borrow either a <code>ControllerCap</code>
or a <code>DelegationToken</code> from the executing entity in order to
access another entity <code>sub_entity</code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_AccessSubEntity">AccessSubEntity</a> <b>has</b> drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>entity: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 The entity which has control over <code>sub_entity</code>.
</dd>
<dt>
<code>sub_entity: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 The entity we want to access by using <code>entity</code>'s access token.
</dd>
<dt>
<code>borrowed_token: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;</code>
</dt>
<dd>
 Borrowed <code>entity</code>'s token.
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(iota_identity=0x0)_access_sub_entity_proposal_ETokenAlreadyBorrowed"></a>

A token has already been borrowed.


<pre><code><b>const</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_ETokenAlreadyBorrowed">ETokenAlreadyBorrowed</a>: u64 = 0;
</code></pre>



<a name="(iota_identity=0x0)_access_sub_entity_proposal_EInvalidTokenToSubEntity"></a>

The received token doesn't grant access to the specified sub-entity.


<pre><code><b>const</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_EInvalidTokenToSubEntity">EInvalidTokenToSubEntity</a>: u64 = 1;
</code></pre>



<a name="(iota_identity=0x0)_access_sub_entity_proposal_ENothingToReturn"></a>

Trying to return a token that has never been borrowed to begin with.


<pre><code><b>const</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_ENothingToReturn">ENothingToReturn</a>: u64 = 2;
</code></pre>



<a name="(iota_identity=0x0)_access_sub_entity_proposal_ETokenReturnMismatch"></a>

The returned token doesn't match the borrowed token.


<pre><code><b>const</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_ETokenReturnMismatch">ETokenReturnMismatch</a>: u64 = 3;
</code></pre>



<a name="(iota_identity=0x0)_access_sub_entity_proposal_EEntityMismatch"></a>

The provided entity doesn't match the one defined in this action.


<pre><code><b>const</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_EEntityMismatch">EEntityMismatch</a>: u64 = 4;
</code></pre>



<a name="(iota_identity=0x0)_access_sub_entity_proposal_new"></a>

## Function `new`

Creates a proposal to access the sub-entity <code>sub_entity</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_new">new</a>(entity: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, sub_entity: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): (iota_identity=0x0)::access_sub_entity_proposal::AccessSubEntity
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_new">new</a>(entity: ID, sub_entity: ID): <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_AccessSubEntity">AccessSubEntity</a> {
    <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_AccessSubEntity">AccessSubEntity</a> {
        entity,
        sub_entity,
        borrowed_token: option::none(),
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_access_sub_entity_proposal_borrow_controller_cap"></a>

## Function `borrow_controller_cap`

Borrows from <code>entity</code> a <code>ControllerCap</code> granting access to <code>sub_entity</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_borrow_controller_cap">borrow_controller_cap</a>(action: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::access_sub_entity_proposal::AccessSubEntity&gt;, entity: &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>, recv: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;(iota_identity=0x0)::controller::ControllerCap&gt;): (iota_identity=0x0)::controller::ControllerCap
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_borrow_controller_cap">borrow_controller_cap</a>(
    action: &<b>mut</b> Action&lt;<a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_AccessSubEntity">AccessSubEntity</a>&gt;,
    entity: &<b>mut</b> UID,
    recv: Receiving&lt;ControllerCap&gt;,
): ControllerCap {
    <b>let</b> config = action.borrow_mut();
    // Make sure no token <b>has</b> been borrowed yet.
    <b>assert</b>!(config.borrowed_token.is_none(), <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_ETokenAlreadyBorrowed">ETokenAlreadyBorrowed</a>);
    // Make sure provided entity matches action's one.
    <b>assert</b>!(config.entity == entity.to_inner(), <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_EEntityMismatch">EEntityMismatch</a>);
    // Receive the token from the executing entity.
    <b>let</b> token = controller::receive(entity, recv);
    // Make sure the received token grants access to sub_entity.
    <b>assert</b>!(token.controller_of() == config.sub_entity, <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_EInvalidTokenToSubEntity">EInvalidTokenToSubEntity</a>);
    // Enforce borrowing only once.
    config.borrowed_token = option::some(token.id().to_inner());
    token
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_access_sub_entity_proposal_borrow_delegation_token"></a>

## Function `borrow_delegation_token`

Borrows from <code>entity</code> a <code>DelegationToken</code> granting access to <code>sub_entity</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_borrow_delegation_token">borrow_delegation_token</a>(action: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::access_sub_entity_proposal::AccessSubEntity&gt;, entity: &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>, recv: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;(iota_identity=0x0)::controller::DelegationToken&gt;): (iota_identity=0x0)::controller::DelegationToken
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_borrow_delegation_token">borrow_delegation_token</a>(
    action: &<b>mut</b> Action&lt;<a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_AccessSubEntity">AccessSubEntity</a>&gt;,
    entity: &<b>mut</b> UID,
    recv: Receiving&lt;DelegationToken&gt;,
): DelegationToken {
    <b>let</b> config = action.borrow_mut();
    // Make sure no token <b>has</b> been borrowed yet.
    <b>assert</b>!(config.borrowed_token.is_none(), <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_ETokenAlreadyBorrowed">ETokenAlreadyBorrowed</a>);
    // Make sure provided entity matches action's one.
    <b>assert</b>!(config.entity == entity.to_inner(), <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_EEntityMismatch">EEntityMismatch</a>);
    // Receive the token from the executing entity.
    <b>let</b> token = transfer::public_receive(entity, recv);
    // Make sure the received token grants access to sub_entity.
    <b>assert</b>!(token.controller_of() == config.sub_entity, <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_EInvalidTokenToSubEntity">EInvalidTokenToSubEntity</a>);
    // Enforce borrowing only once.
    config.borrowed_token = option::some(token.id());
    token
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_access_sub_entity_proposal_put_back_controller_cap"></a>

## Function `put_back_controller_cap`

Returns the borrowed <code>ControllerCap</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_put_back_controller_cap">put_back_controller_cap</a>(action: (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::access_sub_entity_proposal::AccessSubEntity&gt;, token: (iota_identity=0x0)::controller::ControllerCap)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_put_back_controller_cap">put_back_controller_cap</a>(action: Action&lt;<a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_AccessSubEntity">AccessSubEntity</a>&gt;, token: ControllerCap) {
    <b>let</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_AccessSubEntity">AccessSubEntity</a> { borrowed_token, entity, .. } = action.unwrap();
    // Make sure a token <b>has</b> been borrowed.
    <b>assert</b>!(borrowed_token.is_some(), <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_ENothingToReturn">ENothingToReturn</a>);
    // Make sure the presented token is the one that had been borrowed.
    <b>assert</b>!(token.id().as_inner() == borrowed_token.borrow(), <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_ETokenReturnMismatch">ETokenReturnMismatch</a>);
    token.transfer(entity.to_address())
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_access_sub_entity_proposal_put_back_delegation_token"></a>

## Function `put_back_delegation_token`

Returns the borrowed <code>DelegationToken</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_put_back_delegation_token">put_back_delegation_token</a>(action: (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::access_sub_entity_proposal::AccessSubEntity&gt;, token: (iota_identity=0x0)::controller::DelegationToken)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_put_back_delegation_token">put_back_delegation_token</a>(action: Action&lt;<a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_AccessSubEntity">AccessSubEntity</a>&gt;, token: DelegationToken) {
    <b>let</b> <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_AccessSubEntity">AccessSubEntity</a> { borrowed_token, entity, .. } = action.unwrap();
    // Make sure a token <b>has</b> been borrowed.
    <b>assert</b>!(borrowed_token.is_some(), <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_ENothingToReturn">ENothingToReturn</a>);
    // Make sure the presented token is the one that had been borrowed.
    <b>assert</b>!(token.id() == *borrowed_token.borrow(), <a href="../../dependencies/nplex/access_sub_entity.md#(iota_identity=0x0)_access_sub_entity_proposal_ETokenReturnMismatch">ETokenReturnMismatch</a>);
    transfer::public_transfer(token, entity.to_address())
}
</code></pre>



</details>
