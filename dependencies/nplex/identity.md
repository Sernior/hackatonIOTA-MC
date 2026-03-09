
<a name="(iota_identity=0x0)_identity"></a>

# Module `(iota_identity=0x0)::identity`



-  [Struct `ProposalEvent`](#(iota_identity=0x0)_identity_ProposalEvent)
-  [Struct `ProposalApproved`](#(iota_identity=0x0)_identity_ProposalApproved)
-  [Struct `Identity`](#(iota_identity=0x0)_identity_Identity)
-  [Constants](#@Constants_0)
-  [Function `new`](#(iota_identity=0x0)_identity_new)
-  [Function `new_with_migration_data`](#(iota_identity=0x0)_identity_new_with_migration_data)
-  [Function `new_with_controller`](#(iota_identity=0x0)_identity_new_with_controller)
-  [Function `new_with_controllers`](#(iota_identity=0x0)_identity_new_with_controllers)
-  [Function `id`](#(iota_identity=0x0)_identity_id)
-  [Function `legacy_id`](#(iota_identity=0x0)_identity_legacy_id)
-  [Function `created`](#(iota_identity=0x0)_identity_created)
-  [Function `updated`](#(iota_identity=0x0)_identity_updated)
-  [Function `deleted`](#(iota_identity=0x0)_identity_deleted)
-  [Function `deleted_did`](#(iota_identity=0x0)_identity_deleted_did)
-  [Function `threshold`](#(iota_identity=0x0)_identity_threshold)
-  [Function `approve_proposal`](#(iota_identity=0x0)_identity_approve_proposal)
-  [Function `propose_deletion`](#(iota_identity=0x0)_identity_propose_deletion)
-  [Function `execute_deletion`](#(iota_identity=0x0)_identity_execute_deletion)
-  [Function `propose_access_to_sub_identity`](#(iota_identity=0x0)_identity_propose_access_to_sub_identity)
-  [Function `borrow_controller_cap_to_sub_identity`](#(iota_identity=0x0)_identity_borrow_controller_cap_to_sub_identity)
-  [Function `borrow_delegation_token_to_sub_identity`](#(iota_identity=0x0)_identity_borrow_delegation_token_to_sub_identity)
-  [Function `propose_controller_execution`](#(iota_identity=0x0)_identity_propose_controller_execution)
-  [Function `borrow_controller_cap`](#(iota_identity=0x0)_identity_borrow_controller_cap)
-  [Function `propose_upgrade`](#(iota_identity=0x0)_identity_propose_upgrade)
-  [Function `execute_upgrade`](#(iota_identity=0x0)_identity_execute_upgrade)
-  [Function `migrate`](#(iota_identity=0x0)_identity_migrate)
-  [Function `propose_update`](#(iota_identity=0x0)_identity_propose_update)
-  [Function `execute_update`](#(iota_identity=0x0)_identity_execute_update)
-  [Function `propose_config_change`](#(iota_identity=0x0)_identity_propose_config_change)
-  [Function `execute_config_change`](#(iota_identity=0x0)_identity_execute_config_change)
-  [Function `propose_send`](#(iota_identity=0x0)_identity_propose_send)
-  [Function `execute_send`](#(iota_identity=0x0)_identity_execute_send)
-  [Function `propose_borrow`](#(iota_identity=0x0)_identity_propose_borrow)
-  [Function `execute_borrow`](#(iota_identity=0x0)_identity_execute_borrow)
-  [Function `propose_new_controller`](#(iota_identity=0x0)_identity_propose_new_controller)
-  [Function `execute_proposal`](#(iota_identity=0x0)_identity_execute_proposal)
-  [Function `delete_proposal`](#(iota_identity=0x0)_identity_delete_proposal)
-  [Function `revoke_token`](#(iota_identity=0x0)_identity_revoke_token)
-  [Function `unrevoke_token`](#(iota_identity=0x0)_identity_unrevoke_token)
-  [Function `destroy_controller_cap`](#(iota_identity=0x0)_identity_destroy_controller_cap)
-  [Function `destroy_delegation_token`](#(iota_identity=0x0)_identity_destroy_delegation_token)
-  [Function `delete`](#(iota_identity=0x0)_identity_delete)
-  [Function `uid_mut`](#(iota_identity=0x0)_identity_uid_mut)
-  [Function `is_did_output`](#(iota_identity=0x0)_identity_is_did_output)
-  [Function `did_doc`](#(iota_identity=0x0)_identity_did_doc)
-  [Function `emit_proposal_event`](#(iota_identity=0x0)_identity_emit_proposal_event)


<pre><code><b>use</b> (iota_identity=0x0)::access_sub_entity_proposal;
<b>use</b> (iota_identity=0x0)::borrow_proposal;
<b>use</b> (iota_identity=0x0)::config_proposal;
<b>use</b> (iota_identity=0x0)::controller;
<b>use</b> (iota_identity=0x0)::controller_proposal;
<b>use</b> (iota_identity=0x0)::<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_delete_proposal">delete_proposal</a>;
<b>use</b> (iota_identity=0x0)::multicontroller;
<b>use</b> (iota_identity=0x0)::permissions;
<b>use</b> (iota_identity=0x0)::transfer_proposal;
<b>use</b> (iota_identity=0x0)::update_value_proposal;
<b>use</b> (iota_identity=0x0)::upgrade_proposal;
<b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/borrow.md#iota_borrow">iota::borrow</a>;
<b>use</b> <a href="../../dependencies/iota/clock.md#iota_clock">iota::clock</a>;
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



<a name="(iota_identity=0x0)_identity_ProposalEvent"></a>

## Struct `ProposalEvent`

Event emitted when an <code>identity</code>'s <code>Proposal</code> with <code>ID</code> <code>proposal</code> is created or executed by <code>controller</code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_ProposalEvent">ProposalEvent</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>identity: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>controller: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>proposal: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>executed: bool</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_identity_ProposalApproved"></a>

## Struct `ProposalApproved`

Event emitted when a <code>Proposal</code> has reached the AC threshold and
can now be executed.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_ProposalApproved">ProposalApproved</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>identity: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 ID of the <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code> owning the proposal.
</dd>
<dt>
<code>proposal: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 ID of the created <code>Proposal</code>.
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_identity_Identity"></a>

## Struct `Identity`

On-chain Identity.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a> <b>has</b> key
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>: (iota_identity=0x0)::multicontroller::Multicontroller&lt;<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;&gt;</code>
</dt>
<dd>
 Same as stardust <code>state_metadata</code>.
</dd>
<dt>
<code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_legacy_id">legacy_id</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;</code>
</dt>
<dd>
 If this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code> has been migrated from a Stardust
 AliasOutput, this field must be set with its AliasID.
</dd>
<dt>
<code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_created">created</a>: u64</code>
</dt>
<dd>
 Timestamp of this Identity's creation.
</dd>
<dt>
<code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_updated">updated</a>: u64</code>
</dt>
<dd>
 Timestamp of this Identity's last update.
</dd>
<dt>
<code>version: u64</code>
</dt>
<dd>
 Package version used by this object.
</dd>
<dt>
<code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>: bool</code>
</dt>
<dd>
 Flag to verify if this Identity has been deleted.
 Once an Identity has been deleted it CANNOT be activated again.
</dd>
<dt>
<code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted_did">deleted_did</a>: bool</code>
</dt>
<dd>
 Set when the DID Document of this Identity has been deleted.
 Once a DID Document has been deleted it CANNOT be activated again.
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(iota_identity=0x0)_identity_ENotADidDocument"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_ENotADidDocument">ENotADidDocument</a>: u64 = 0;
</code></pre>



<a name="(iota_identity=0x0)_identity_EInvalidTimestamp"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EInvalidTimestamp">EInvalidTimestamp</a>: u64 = 1;
</code></pre>



<a name="(iota_identity=0x0)_identity_EInvalidThreshold"></a>

The threshold specified upon document creation was not valid.
Threshold must be greater than or equal to 1.


<pre><code><b>const</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EInvalidThreshold">EInvalidThreshold</a>: u64 = 2;
</code></pre>



<a name="(iota_identity=0x0)_identity_EInvalidControllersList"></a>

The controller list must contain at least 1 element.


<pre><code><b>const</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EInvalidControllersList">EInvalidControllersList</a>: u64 = 3;
</code></pre>



<a name="(iota_identity=0x0)_identity_ENoUpgrade"></a>

There's no upgrade available for this identity.


<pre><code><b>const</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_ENoUpgrade">ENoUpgrade</a>: u64 = 4;
</code></pre>



<a name="(iota_identity=0x0)_identity_ECannotDelete"></a>

Cannot delete identity.


<pre><code><b>const</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_ECannotDelete">ECannotDelete</a>: u64 = 5;
</code></pre>



<a name="(iota_identity=0x0)_identity_EDeletedIdentity"></a>

Identity had been deleted.


<pre><code><b>const</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>: u64 = 6;
</code></pre>



<a name="(iota_identity=0x0)_identity_PACKAGE_VERSION"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_PACKAGE_VERSION">PACKAGE_VERSION</a>: u64 = 0;
</code></pre>



<a name="(iota_identity=0x0)_identity_new"></a>

## Function `new`

Creates an <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code> with a single controller.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_new">new</a>(doc: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_new">new</a>(doc: Option&lt;vector&lt;u8&gt;&gt;, clock: &Clock, ctx: &<b>mut</b> TxContext): ID {
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_new_with_controller">new_with_controller</a>(doc, ctx.sender(), <b>false</b>, clock, ctx)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_new_with_migration_data"></a>

## Function `new_with_migration_data`

Creates an identity specifying its <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_created">created</a></code> timestamp.
Should only be used for migration!


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_new_with_migration_data">new_with_migration_data</a>(doc: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;, creation_timestamp: u64, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_legacy_id">legacy_id</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_new_with_migration_data">new_with_migration_data</a>(
    doc: Option&lt;vector&lt;u8&gt;&gt;,
    creation_timestamp: u64,
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_legacy_id">legacy_id</a>: ID,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
): ID {
    <b>let</b> now = clock.timestamp_ms();
    <b>assert</b>!(now &gt;= creation_timestamp, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EInvalidTimestamp">EInvalidTimestamp</a>);
    <b>let</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a> = object::new(ctx);
    <b>let</b> identity_id = <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>.to_inner();
    <b>let</b> identity = <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a> {
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>: multicontroller::new_with_controller(
            doc,
            ctx.sender(),
            <b>false</b>,
            identity_id,
            ctx,
        ),
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_legacy_id">legacy_id</a>: option::some(<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_legacy_id">legacy_id</a>),
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_created">created</a>: creation_timestamp,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_updated">updated</a>: now,
        version: <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_PACKAGE_VERSION">PACKAGE_VERSION</a>,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>: <b>false</b>,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted_did">deleted_did</a>: <b>false</b>,
    };
    <b>let</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a> = object::id(&identity);
    transfer::share_object(identity);
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_new_with_controller"></a>

## Function `new_with_controller`

Creates a new <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code> wrapping DID DOC <code>doc</code> and controller by
a single address <code>controller</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_new_with_controller">new_with_controller</a>(doc: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;, controller: <b>address</b>, can_delegate: bool, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_new_with_controller">new_with_controller</a>(
    doc: Option&lt;vector&lt;u8&gt;&gt;,
    controller: <b>address</b>,
    can_delegate: bool,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
): ID {
    <b>let</b> now = clock.timestamp_ms();
    <b>let</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a> = object::new(ctx);
    <b>let</b> identity_id = <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>.to_inner();
    <b>let</b> identity = <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a> {
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>: multicontroller::new_with_controller(
            doc,
            controller,
            can_delegate,
            identity_id,
            ctx,
        ),
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_legacy_id">legacy_id</a>: option::none(),
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_created">created</a>: now,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_updated">updated</a>: now,
        version: <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_PACKAGE_VERSION">PACKAGE_VERSION</a>,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>: <b>false</b>,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted_did">deleted_did</a>: <b>false</b>,
    };
    <b>let</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a> = object::id(&identity);
    transfer::share_object(identity);
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_new_with_controllers"></a>

## Function `new_with_controllers`

Creates an [<code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>] controlled by multiple controllers.
The <code>weights</code> vectors is used to create a vector of <code>ControllerCap</code>s <code>controller_caps</code>,
where <code>controller_caps[i].weight = weights[i]</code> for all <code>i</code>s in <code>[0, weights.length())</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_new_with_controllers">new_with_controllers</a>(doc: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;, controllers: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;, controllers_that_can_delegate: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_threshold">threshold</a>: u64, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_new_with_controllers">new_with_controllers</a>(
    doc: Option&lt;vector&lt;u8&gt;&gt;,
    controllers: VecMap&lt;<b>address</b>, u64&gt;,
    controllers_that_can_delegate: VecMap&lt;<b>address</b>, u64&gt;,
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_threshold">threshold</a>: u64,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
): ID {
    <b>assert</b>!(<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_threshold">threshold</a> &gt;= 1, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EInvalidThreshold">EInvalidThreshold</a>);
    <b>assert</b>!(controllers.size() &gt; 0, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EInvalidControllersList">EInvalidControllersList</a>);
    <b>if</b> (doc.is_some()) {
        <b>assert</b>!(<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_is_did_output">is_did_output</a>(doc.borrow()), <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_ENotADidDocument">ENotADidDocument</a>);
    };
    <b>let</b> now = clock.timestamp_ms();
    <b>let</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a> = object::new(ctx);
    <b>let</b> identity_id = <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>.to_inner();
    <b>let</b> identity = <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a> {
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>: multicontroller::new_with_controllers(
            doc,
            controllers,
            controllers_that_can_delegate,
            <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_threshold">threshold</a>,
            identity_id,
            ctx,
        ),
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_legacy_id">legacy_id</a>: option::none(),
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_created">created</a>: now,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_updated">updated</a>: now,
        version: <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_PACKAGE_VERSION">PACKAGE_VERSION</a>,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>: <b>false</b>,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted_did">deleted_did</a>: <b>false</b>,
    };
    <b>let</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a> = object::id(&identity);
    transfer::share_object(identity);
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_id"></a>

## Function `id`

Returns a reference to the <code>UID</code> of an <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(self: &(iota_identity=0x0)::identity::Identity): &<a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(self: &<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>): &UID {
    &self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_legacy_id"></a>

## Function `legacy_id`

Returns a reference to the optional legacy ID of this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>.
Only <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>s that had been migrated from Stardust AliasOutputs
will have <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_legacy_id">legacy_id</a></code> set.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_legacy_id">legacy_id</a>(self: &(iota_identity=0x0)::identity::Identity): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_legacy_id">legacy_id</a>(self: &<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>): &Option&lt;ID&gt; {
    &self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_legacy_id">legacy_id</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_created"></a>

## Function `created`

Returns the unsigned amount of milliseconds
that passed from the UNIX epoch to the creation of this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_created">created</a>(self: &(iota_identity=0x0)::identity::Identity): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_created">created</a>(self: &<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>): u64 {
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_created">created</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_updated"></a>

## Function `updated`

Returns the unsigned amount of milliseconds
that passed from the UNIX epoch to the last update on this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_updated">updated</a>(self: &(iota_identity=0x0)::identity::Identity): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_updated">updated</a>(self: &<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>): u64 {
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_updated">updated</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_deleted"></a>

## Function `deleted`

Returns the value of the flag <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>(self: &(iota_identity=0x0)::identity::Identity): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>(self: &<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>): bool {
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_deleted_did"></a>

## Function `deleted_did`

Returns the value of the flag <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted_did">deleted_did</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted_did">deleted_did</a>(self: &(iota_identity=0x0)::identity::Identity): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted_did">deleted_did</a>(self: &<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>): bool {
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted_did">deleted_did</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_threshold"></a>

## Function `threshold`

Returns this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>'s threshold.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_threshold">threshold</a>(self: &(iota_identity=0x0)::identity::Identity): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_threshold">threshold</a>(self: &<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>): u64 {
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_threshold">threshold</a>()
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_approve_proposal"></a>

## Function `approve_proposal`

Approve an <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>'s <code>Proposal</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_approve_proposal">approve_proposal</a>&lt;T: store&gt;(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_approve_proposal">approve_proposal</a>&lt;T: store&gt;(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    proposal_id: ID,
) {
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_approve_proposal">approve_proposal</a>&lt;_, T&gt;(cap, proposal_id);
    // If proposal is ready to be executed send an event.
    <b>if</b> (self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.is_proposal_approved&lt;_, T&gt;(proposal_id)) {
        <a href="../../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_ProposalApproved">ProposalApproved</a> {
            identity: self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(),
            proposal: proposal_id,
        })
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_propose_deletion"></a>

## Function `propose_deletion`

Proposes the deletion of this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_deletion">propose_deletion</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_deletion">propose_deletion</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    expiration: Option&lt;u64&gt;,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
): Option&lt;ID&gt; {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <b>let</b> proposal_id = self
        .<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>
        .create_proposal(
            cap,
            delete_proposal::new(),
            expiration,
            ctx,
        );
    <b>let</b> is_approved = self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.is_proposal_approved&lt;_, Delete&gt;(proposal_id);
    <b>if</b> (is_approved) {
        self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_deletion">execute_deletion</a>(cap, proposal_id, clock, ctx);
        option::none()
    } <b>else</b> {
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>false</b>);
        option::some(proposal_id)
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_execute_deletion"></a>

## Function `execute_deletion`

Executes a proposal to delete this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>'s DID document.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_deletion">execute_deletion</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_deletion">execute_deletion</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    proposal_id: ID,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
) {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <b>let</b> _ = self
        .<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_proposal">execute_proposal</a>&lt;Delete&gt;(
            cap,
            proposal_id,
            ctx,
        )
        .unwrap();
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a> = <b>true</b>;
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.set_controlled_value(option::none());
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_updated">updated</a> = clock.timestamp_ms();
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>true</b>);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_propose_access_to_sub_identity"></a>

## Function `propose_access_to_sub_identity`

Creates a new <code>AccessSubEntity</code> proposal to access a sub-identity.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_access_to_sub_identity">propose_access_to_sub_identity</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, sub_identity: &(iota_identity=0x0)::identity::Identity, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_access_to_sub_identity">propose_access_to_sub_identity</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    sub_identity: &<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    expiration: Option&lt;u64&gt;,
    ctx: &<b>mut</b> TxContext,
): ID {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <b>let</b> proposal_id = self
        .<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>
        .create_proposal(
            cap,
            access_sub_entity_proposal::new(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>.to_inner(), sub_identity.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>.to_inner()),
            expiration,
            ctx,
        );
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>false</b>);
    proposal_id
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_borrow_controller_cap_to_sub_identity"></a>

## Function `borrow_controller_cap_to_sub_identity`

Borrows the <code>ControllerCap</code> specified in this <code>AccessSubEntity</code> action.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_borrow_controller_cap_to_sub_identity">borrow_controller_cap_to_sub_identity</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, action: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::access_sub_entity_proposal::AccessSubEntity&gt;, receiving: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;(iota_identity=0x0)::controller::ControllerCap&gt;): (iota_identity=0x0)::controller::ControllerCap
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_borrow_controller_cap_to_sub_identity">borrow_controller_cap_to_sub_identity</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    action: &<b>mut</b> Action&lt;AccessSubEntity&gt;,
    receiving: Receiving&lt;ControllerCap&gt;,
): ControllerCap {
    access_sub_entity_proposal::borrow_controller_cap(action, self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_uid_mut">uid_mut</a>(), receiving)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_borrow_delegation_token_to_sub_identity"></a>

## Function `borrow_delegation_token_to_sub_identity`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_borrow_delegation_token_to_sub_identity">borrow_delegation_token_to_sub_identity</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, action: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::access_sub_entity_proposal::AccessSubEntity&gt;, receiving: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;(iota_identity=0x0)::controller::DelegationToken&gt;): (iota_identity=0x0)::controller::DelegationToken
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_borrow_delegation_token_to_sub_identity">borrow_delegation_token_to_sub_identity</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    action: &<b>mut</b> Action&lt;AccessSubEntity&gt;,
    receiving: Receiving&lt;DelegationToken&gt;,
): DelegationToken {
    access_sub_entity_proposal::borrow_delegation_token(action, self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_uid_mut">uid_mut</a>(), receiving)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_propose_controller_execution"></a>

## Function `propose_controller_execution`

Creates a new <code>ControllerExecution</code> proposal.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_controller_execution">propose_controller_execution</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, controller_cap_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_controller_execution">propose_controller_execution</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    controller_cap_id: ID,
    expiration: Option&lt;u64&gt;,
    ctx: &<b>mut</b> TxContext,
): ID {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <b>let</b> identity_address = self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_address();
    <b>let</b> proposal_id = self
        .<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>
        .create_proposal(
            cap,
            controller_proposal::new(controller_cap_id, identity_address),
            expiration,
            ctx,
        );
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>false</b>);
    proposal_id
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_borrow_controller_cap"></a>

## Function `borrow_controller_cap`

Borrow the identity-owned controller cap specified in <code>ControllerExecution</code>.
The borrowed cap must be put back by calling <code>controller_proposal::put_back</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_borrow_controller_cap">borrow_controller_cap</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, action: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::controller_proposal::ControllerExecution&gt;, receiving: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;(iota_identity=0x0)::controller::ControllerCap&gt;): (iota_identity=0x0)::controller::ControllerCap
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_borrow_controller_cap">borrow_controller_cap</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    action: &<b>mut</b> Action&lt;ControllerExecution&gt;,
    receiving: Receiving&lt;ControllerCap&gt;,
): ControllerCap {
    controller_proposal::receive(action, &<b>mut</b> self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>, receiving)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_propose_upgrade"></a>

## Function `propose_upgrade`

Proposes to upgrade this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code> to this package's version.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_upgrade">propose_upgrade</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_upgrade">propose_upgrade</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    expiration: Option&lt;u64&gt;,
    ctx: &<b>mut</b> TxContext,
): Option&lt;ID&gt; {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <b>assert</b>!(self.version &lt; <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_PACKAGE_VERSION">PACKAGE_VERSION</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_ENoUpgrade">ENoUpgrade</a>);
    <b>let</b> proposal_id = self
        .<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>
        .create_proposal(
            cap,
            upgrade_proposal::new(),
            expiration,
            ctx,
        );
    <b>let</b> is_approved = self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.is_proposal_approved&lt;_, Upgrade&gt;(proposal_id);
    <b>if</b> (is_approved) {
        self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_upgrade">execute_upgrade</a>(cap, proposal_id, ctx);
        option::none()
    } <b>else</b> {
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>false</b>);
        option::some(proposal_id)
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_execute_upgrade"></a>

## Function `execute_upgrade`

Consumes a <code>Proposal&lt;Upgrade&gt;</code> that migrates <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code> to this
package's version.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_upgrade">execute_upgrade</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_upgrade">execute_upgrade</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    proposal_id: ID,
    ctx: &<b>mut</b> TxContext,
) {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_proposal">execute_proposal</a>&lt;Upgrade&gt;(cap, proposal_id, ctx).unwrap();
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_migrate">migrate</a>();
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>true</b>);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_migrate"></a>

## Function `migrate`

Migrates this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code> to this package's version.


<pre><code><b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_migrate">migrate</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_migrate">migrate</a>(self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>) {
    // ADD migration logic when needed!
    self.version = <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_PACKAGE_VERSION">PACKAGE_VERSION</a>;
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_propose_update"></a>

## Function `propose_update`

Proposes an update to the DID Document contained in this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>.
This function can update the DID Document right away if <code>cap</code> has
enough voting power.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_update">propose_update</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, updated_doc: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_update">propose_update</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    updated_doc: Option&lt;vector&lt;u8&gt;&gt;,
    expiration: Option&lt;u64&gt;,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
): Option&lt;ID&gt; {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a> && !self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted_did">deleted_did</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <b>if</b> (updated_doc.is_some()) {
        <b>let</b> doc = updated_doc.borrow();
        <b>assert</b>!(doc.is_empty() || <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_is_did_output">is_did_output</a>(doc), <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_ENotADidDocument">ENotADidDocument</a>);
    };
    <b>let</b> proposal_id = update_value_proposal::propose_update(
        &<b>mut</b> self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>,
        cap,
        updated_doc,
        expiration,
        ctx,
    );
    <b>let</b> is_approved = self
        .<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>
        .is_proposal_approved&lt;_, update_value_proposal::UpdateValue&lt;Option&lt;vector&lt;u8&gt;&gt;&gt;&gt;(
            proposal_id,
        );
    <b>if</b> (is_approved) {
        self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_update">execute_update</a>(cap, proposal_id, clock, ctx);
        option::none()
    } <b>else</b> {
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>false</b>);
        option::some(proposal_id)
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_execute_update"></a>

## Function `execute_update`

Executes a proposal to update the DID Document contained in this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_update">execute_update</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_update">execute_update</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    proposal_id: ID,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
) {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a> && !self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted_did">deleted_did</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <b>let</b> updated_did_value = self
        .<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_proposal">execute_proposal</a>&lt;UpdateValue&lt;Option&lt;vector&lt;u8&gt;&gt;&gt;&gt;(cap, proposal_id, ctx)
        .unpack_action()
        .into_inner();
    <b>if</b> (updated_did_value.is_none()) {
        self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted_did">deleted_did</a> = <b>true</b>;
    };
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.set_controlled_value(updated_did_value);
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_updated">updated</a> = clock.timestamp_ms();
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>true</b>);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_propose_config_change"></a>

## Function `propose_config_change`

Proposes to update this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>'s AC.
This operation might be carried out right away if <code>cap</code>
has enough voting power.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_config_change">propose_config_change</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_threshold">threshold</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, controllers_to_add: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;, controllers_to_remove: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;, controllers_to_update: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, u64&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_config_change">propose_config_change</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    expiration: Option&lt;u64&gt;,
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_threshold">threshold</a>: Option&lt;u64&gt;,
    controllers_to_add: VecMap&lt;<b>address</b>, u64&gt;,
    controllers_to_remove: vector&lt;ID&gt;,
    controllers_to_update: VecMap&lt;ID, u64&gt;,
    ctx: &<b>mut</b> TxContext,
): Option&lt;ID&gt; {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <b>let</b> proposal_id = config_proposal::propose_modify(
        &<b>mut</b> self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>,
        cap,
        expiration,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_threshold">threshold</a>,
        controllers_to_add,
        controllers_to_remove,
        controllers_to_update,
        ctx,
    );
    <b>let</b> is_approved = self
        .<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>
        .is_proposal_approved&lt;_, config_proposal::Modify&gt;(proposal_id);
    <b>if</b> (is_approved) {
        self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_config_change">execute_config_change</a>(cap, proposal_id, ctx);
        option::none()
    } <b>else</b> {
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>false</b>);
        option::some(proposal_id)
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_execute_config_change"></a>

## Function `execute_config_change`

Execute a proposal to change this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>'s AC.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_config_change">execute_config_change</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_config_change">execute_config_change</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    proposal_id: ID,
    ctx: &<b>mut</b> TxContext,
) {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    config_proposal::execute_modify(
        &<b>mut</b> self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>,
        cap,
        proposal_id,
        ctx,
    );
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>true</b>);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_propose_send"></a>

## Function `propose_send`

Proposes the transfer of a set of objects owned by this <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_send">propose_send</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, objects: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;, recipients: vector&lt;<b>address</b>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_send">propose_send</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    expiration: Option&lt;u64&gt;,
    objects: vector&lt;ID&gt;,
    recipients: vector&lt;<b>address</b>&gt;,
    ctx: &<b>mut</b> TxContext,
): ID {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <b>let</b> proposal_id = transfer_proposal::propose_send(
        &<b>mut</b> self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>,
        cap,
        expiration,
        objects,
        recipients,
        ctx,
    );
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>false</b>);
    proposal_id
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_execute_send"></a>

## Function `execute_send`

Sends one object among the one specified in a <code>Send</code> proposal.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_send">execute_send</a>&lt;T: key, store&gt;(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, send_action: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::transfer_proposal::Send&gt;, receiving: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_send">execute_send</a>&lt;T: key + store&gt;(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    send_action: &<b>mut</b> Action&lt;Send&gt;,
    receiving: Receiving&lt;T&gt;,
) {
    transfer_proposal::send(send_action, &<b>mut</b> self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>, receiving);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_propose_borrow"></a>

## Function `propose_borrow`

Requests the borrowing of a set of assets
in order to use them in a transaction. Borrowed assets must be returned.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_borrow">propose_borrow</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, objects: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_borrow">propose_borrow</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    expiration: Option&lt;u64&gt;,
    objects: vector&lt;ID&gt;,
    ctx: &<b>mut</b> TxContext,
): ID {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <b>let</b> identity_address = self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_address();
    <b>let</b> proposal_id = borrow_proposal::propose_borrow(
        &<b>mut</b> self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>,
        cap,
        expiration,
        objects,
        identity_address,
        ctx,
    );
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>false</b>);
    proposal_id
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_execute_borrow"></a>

## Function `execute_borrow`

Takes one of the borrowed assets.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_borrow">execute_borrow</a>&lt;T: key, store&gt;(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, borrow_action: &<b>mut</b> (iota_identity=0x0)::multicontroller::Action&lt;(iota_identity=0x0)::borrow_proposal::Borrow&gt;, receiving: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;T&gt;): T
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_borrow">execute_borrow</a>&lt;T: key + store&gt;(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    borrow_action: &<b>mut</b> Action&lt;Borrow&gt;,
    receiving: Receiving&lt;T&gt;,
): T {
    borrow_proposal::borrow(borrow_action, &<b>mut</b> self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>, receiving)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_propose_new_controller"></a>

## Function `propose_new_controller`

Simplified version of <code>Identity::propose_config_change</code> that allows
to add a new controller.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_new_controller">propose_new_controller</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, new_controller_addr: <b>address</b>, voting_power: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_new_controller">propose_new_controller</a>(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    expiration: Option&lt;u64&gt;,
    new_controller_addr: <b>address</b>,
    voting_power: u64,
    ctx: &<b>mut</b> TxContext,
): Option&lt;ID&gt; {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <b>let</b> <b>mut</b> new_controllers = vec_map::empty();
    new_controllers.insert(new_controller_addr, voting_power);
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_propose_config_change">propose_config_change</a>(
        cap,
        expiration,
        option::none(),
        new_controllers,
        vector[],
        vec_map::empty(),
        ctx,
    )
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_execute_proposal"></a>

## Function `execute_proposal`

Executes an <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>'s proposal.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_proposal">execute_proposal</a>&lt;T: store&gt;(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (iota_identity=0x0)::multicontroller::Action&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_proposal">execute_proposal</a>&lt;T: store&gt;(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    proposal_id: ID,
    ctx: &<b>mut</b> TxContext,
): Action&lt;T&gt; {
    <b>assert</b>!(!self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>, <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_EDeletedIdentity">EDeletedIdentity</a>);
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>().to_inner(), cap.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>(), proposal_id, <b>true</b>);
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_execute_proposal">execute_proposal</a>(cap, proposal_id, ctx)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_delete_proposal"></a>

## Function `delete_proposal`

Deletes an <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>'s proposal. Proposals can only be deleted if they have no votes, if they are expired,
or if the identity is deleted.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_delete_proposal">delete_proposal</a>&lt;T: drop, store&gt;(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_delete_proposal">delete_proposal</a>&lt;T: store + drop&gt;(
    self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>,
    cap: &DelegationToken,
    proposal_id: ID,
    ctx: &<b>mut</b> TxContext,
) {
    <b>if</b> (self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>) {
        self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.force_delete_proposal&lt;_, T&gt;(proposal_id);
    } <b>else</b> {
        self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_delete_proposal">delete_proposal</a>&lt;_, T&gt;(cap, proposal_id, ctx);
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_revoke_token"></a>

## Function `revoke_token`

revoke the <code>DelegationToken</code> with <code>ID</code> <code>deny_id</code>. Only controllers can perform this operation.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_revoke_token">revoke_token</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::ControllerCap, deny_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_revoke_token">revoke_token</a>(self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>, cap: &ControllerCap, deny_id: ID) {
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_revoke_token">revoke_token</a>(cap, deny_id);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_unrevoke_token"></a>

## Function `unrevoke_token`

Un-revoke a <code>DelegationToken</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_unrevoke_token">unrevoke_token</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: &(iota_identity=0x0)::controller::ControllerCap, token_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_unrevoke_token">unrevoke_token</a>(self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>, cap: &ControllerCap, token_id: ID) {
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_unrevoke_token">unrevoke_token</a>(cap, token_id);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_destroy_controller_cap"></a>

## Function `destroy_controller_cap`

Destroys a <code>ControllerCap</code>. Can only be used after a controller has been removed from
the controller committee OR if <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code>'s <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a></code> flag is set.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_destroy_controller_cap">destroy_controller_cap</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, cap: (iota_identity=0x0)::controller::ControllerCap)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_destroy_controller_cap">destroy_controller_cap</a>(self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>, cap: ControllerCap) {
    <b>if</b> (self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a>) {
        self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.remove_and_destroy_controller(cap);
    } <b>else</b> {
        self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_destroy_controller_cap">destroy_controller_cap</a>(cap);
    }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_destroy_delegation_token"></a>

## Function `destroy_delegation_token`

Destroys a <code>DelegationToken</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_destroy_delegation_token">destroy_delegation_token</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity, token: (iota_identity=0x0)::controller::DelegationToken)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_destroy_delegation_token">destroy_delegation_token</a>(self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>, token: DelegationToken) {
    self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_destroy_delegation_token">destroy_delegation_token</a>(token);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_delete"></a>

## Function `delete`

Deletes this Identity.
Calls to this method will succeed only if
the <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a></code> has no controllers left and its <code><a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a></code> flag had been
set to <code><b>true</b></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_delete">delete</a>(self: (iota_identity=0x0)::identity::Identity)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_delete">delete</a>(self: <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>) {
    <b>assert</b>!(self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_deleted">deleted</a> && self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.controllers().is_empty(), <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_ECannotDelete">ECannotDelete</a>);
    <b>let</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a> {
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>,
        <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>,
        ..,
    } = self;
    object::delete(<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>);
    <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_delete">delete</a>();
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_uid_mut"></a>

## Function `uid_mut`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_uid_mut">uid_mut</a>(self: &<b>mut</b> (iota_identity=0x0)::identity::Identity): &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_uid_mut">uid_mut</a>(self: &<b>mut</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>): &<b>mut</b> UID {
    &<b>mut</b> self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_id">id</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_is_did_output"></a>

## Function `is_did_output`

Checks if <code>data</code> is a state metadata representing a DID.
i.e. starts with the bytes b"DID".


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_is_did_output">is_did_output</a>(data: &vector&lt;u8&gt;): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_is_did_output">is_did_output</a>(data: &vector&lt;u8&gt;): bool {
    data[0] == 0x44 &&      // b'D'
        data[1] == 0x49 &&  // b'I'
        data[2] == 0x44 // b'D'
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_did_doc"></a>

## Function `did_doc`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>(self: &(iota_identity=0x0)::identity::Identity): &(iota_identity=0x0)::multicontroller::Multicontroller&lt;<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>(self: &<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_Identity">Identity</a>): &Multicontroller&lt;Option&lt;vector&lt;u8&gt;&gt;&gt; {
    &self.<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_did_doc">did_doc</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_identity_emit_proposal_event"></a>

## Function `emit_proposal_event`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(identity: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, controller: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, proposal: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, executed: bool)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_emit_proposal_event">emit_proposal_event</a>(
    identity: ID,
    controller: ID,
    proposal: ID,
    executed: bool,
) {
    <a href="../../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../../dependencies/nplex/identity.md#(iota_identity=0x0)_identity_ProposalEvent">ProposalEvent</a> {
        identity,
        controller,
        proposal,
        executed,
    })
}
</code></pre>



</details>
