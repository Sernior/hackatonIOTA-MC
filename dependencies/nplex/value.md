
<a name="(iota_identity=0x0)_update_value_proposal"></a>

# Module `(iota_identity=0x0)::update_value_proposal`



-  [Struct `UpdateValue`](#(iota_identity=0x0)_update_value_proposal_UpdateValue)
-  [Function `propose_update`](#(iota_identity=0x0)_update_value_proposal_propose_update)
-  [Function `execute_update`](#(iota_identity=0x0)_update_value_proposal_execute_update)
-  [Function `into_inner`](#(iota_identity=0x0)_update_value_proposal_into_inner)


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



<a name="(iota_identity=0x0)_update_value_proposal_UpdateValue"></a>

## Struct `UpdateValue`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/value.md#(iota_identity=0x0)_update_value_proposal_UpdateValue">UpdateValue</a>&lt;V: store&gt; <b>has</b> drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>new_value: V</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_update_value_proposal_propose_update"></a>

## Function `propose_update`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/value.md#(iota_identity=0x0)_update_value_proposal_propose_update">propose_update</a>&lt;V: store&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken, new_value: V, expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/value.md#(iota_identity=0x0)_update_value_proposal_propose_update">propose_update</a>&lt;V: store&gt;(
    multi: &<b>mut</b> Multicontroller&lt;V&gt;,
    cap: &DelegationToken,
    new_value: V,
    expiration: Option&lt;u64&gt;,
    ctx: &<b>mut</b> TxContext,
): ID {
    <b>let</b> update_action = <a href="../../dependencies/nplex/value.md#(iota_identity=0x0)_update_value_proposal_UpdateValue">UpdateValue</a> { new_value };
    multi.create_proposal(cap, update_action, expiration, ctx)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_update_value_proposal_execute_update"></a>

## Function `execute_update`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/value.md#(iota_identity=0x0)_update_value_proposal_execute_update">execute_update</a>&lt;V: drop, store&gt;(multi: &<b>mut</b> (iota_identity=0x0)::multicontroller::Multicontroller&lt;V&gt;, cap: &(iota_identity=0x0)::controller::DelegationToken, proposal_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/value.md#(iota_identity=0x0)_update_value_proposal_execute_update">execute_update</a>&lt;V: store + drop&gt;(
    multi: &<b>mut</b> Multicontroller&lt;V&gt;,
    cap: &DelegationToken,
    proposal_id: ID,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> action = multi.execute_proposal(cap, proposal_id, ctx);
    <b>let</b> <a href="../../dependencies/nplex/value.md#(iota_identity=0x0)_update_value_proposal_UpdateValue">UpdateValue</a> { new_value } = action.unpack_action();
    multi.set_controlled_value(new_value)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_update_value_proposal_into_inner"></a>

## Function `into_inner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/value.md#(iota_identity=0x0)_update_value_proposal_into_inner">into_inner</a>&lt;V: store&gt;(self: (iota_identity=0x0)::update_value_proposal::UpdateValue&lt;V&gt;): V
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/value.md#(iota_identity=0x0)_update_value_proposal_into_inner">into_inner</a>&lt;V: store&gt;(self: <a href="../../dependencies/nplex/value.md#(iota_identity=0x0)_update_value_proposal_UpdateValue">UpdateValue</a>&lt;V&gt;): V {
    <b>let</b> <a href="../../dependencies/nplex/value.md#(iota_identity=0x0)_update_value_proposal_UpdateValue">UpdateValue</a> { new_value } = self;
    new_value
}
</code></pre>



</details>
