
<a name="(iota_identity=0x0)_config_proposal"></a>

# Module `(iota_identity=0x0)::config_proposal`



-  [Struct `Modify`](#(iota_identity=0x0)_config_proposal_Modify)
-  [Constants](#@Constants_0)
-  [Function `propose_modify`](#(iota_identity=0x0)_config_proposal_propose_modify)
-  [Function `execute_modify`](#(iota_identity=0x0)_config_proposal_execute_modify)


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



<a name="(iota_identity=0x0)_config_proposal_Modify"></a>

## Struct `Modify`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_Modify">Modify</a> <b>has</b> drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>threshold: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>controllers_to_add: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>controllers_to_remove: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>controllers_to_update: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, u64&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(iota_identity=0x0)_config_proposal_ENotMember"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_ENotMember">ENotMember</a>: u64 = 0;
</code></pre>



<a name="(iota_identity=0x0)_config_proposal_EInvalidThreshold"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_EInvalidThreshold">EInvalidThreshold</a>: u64 = 1;
</code></pre>



<a name="(iota_identity=0x0)_config_proposal_propose_modify"></a>

## Function `propose_modify`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_propose_modify">propose_modify</a>&lt;V&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, threshold: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, controllers_to_add: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;, controllers_to_remove: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;, controllers_to_update: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, u64&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_propose_modify">propose_modify</a>&lt;V&gt;(
    multi: &<b>mut</b> Multicontroller&lt;V&gt;,
    cap: &DelegationToken,
    expiration: Option&lt;u64&gt;,
    threshold: Option&lt;u64&gt;,
    controllers_to_add: VecMap&lt;<b>address</b>, u64&gt;,
    controllers_to_remove: vector&lt;ID&gt;,
    controllers_to_update: VecMap&lt;ID, u64&gt;,
    ctx: &<b>mut</b> TxContext,
): ID {
    <b>let</b> <b>mut</b> max_votes = 0;
    <b>let</b> (cs, vps) = controllers_to_update.into_keys_values();
    vector::zip_do!(cs, vps, |c, vp| {
        <b>assert</b>!(multi.controllers().contains(&c), <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_ENotMember">ENotMember</a>);
        max_votes = max_votes + vp;
    });
    <b>let</b> (_, voting_powers) = controllers_to_add.into_keys_values();
    <b>let</b> voting_power_increase = voting_powers.fold!(0, |acc, vp| acc + vp);
    <b>let</b> voting_power_decrease = controllers_to_remove.fold!(0, |acc, controller_id| {
        <b>assert</b>!(multi.controllers().contains(&controller_id), <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_ENotMember">ENotMember</a>);
        <b>let</b> <b>mut</b> vp = multi.voting_power(controller_id);
        <b>if</b> (controllers_to_update.contains(&controller_id)) {
            vp = *controllers_to_update.get(&controller_id);
        };
        acc + vp
    });
    multi.controllers().do!(|controller_id| {
        <b>if</b> (!controllers_to_update.contains(&controller_id)) {
            max_votes = max_votes + multi.voting_power(controller_id);
        };
    });
    <b>let</b> new_max_votes = max_votes + voting_power_increase - voting_power_decrease;
    <b>let</b> threshold = threshold.destroy_or!(multi.threshold());
    <b>assert</b>!(threshold &gt; 0 && threshold &lt;= new_max_votes, <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_EInvalidThreshold">EInvalidThreshold</a>);
    <b>let</b> action = <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_Modify">Modify</a> {
        threshold: option::some(threshold),
        controllers_to_add,
        controllers_to_remove,
        controllers_to_update,
    };
    multi.create_proposal(cap, action, expiration, ctx)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_config_proposal_execute_modify"></a>

## Function `execute_modify`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_execute_modify">execute_modify</a>&lt;V&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_execute_modify">execute_modify</a>&lt;V&gt;(
    multi: &<b>mut</b> Multicontroller&lt;V&gt;,
    cap: &DelegationToken,
    proposal_id: ID,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> action = multi.execute_proposal(cap, proposal_id, ctx);
    <b>let</b> <a href="../../dependencies/nplex/config.md#(iota_identity=0x0)_config_proposal_Modify">Modify</a> {
        <b>mut</b> threshold,
        controllers_to_add,
        controllers_to_remove,
        controllers_to_update,
    } = action.unpack_action();
    <b>if</b> (threshold.is_some()) multi.set_threshold(threshold.extract());
    multi.update_members(controllers_to_update);
    multi.add_members(controllers_to_add, ctx);
    multi.remove_members(controllers_to_remove);
}
</code></pre>



</details>
