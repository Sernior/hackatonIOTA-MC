
<a name="iota_system_validator_wrapper"></a>

# Module `iota_system::validator_wrapper`



-  [Struct `Validator`](#iota_system_validator_wrapper_Validator)
-  [Constants](#@Constants_0)
-  [Function `create_v1`](#iota_system_validator_wrapper_create_v1)
-  [Function `load_validator_maybe_upgrade`](#iota_system_validator_wrapper_load_validator_maybe_upgrade)
-  [Function `destroy`](#iota_system_validator_wrapper_destroy)
-  [Function `upgrade_to_latest`](#iota_system_validator_wrapper_upgrade_to_latest)
-  [Function `version`](#iota_system_validator_wrapper_version)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../../dependencies/iota/coin.md#iota_coin">iota::coin</a>;
<b>use</b> <a href="../../dependencies/iota/config.md#iota_config">iota::config</a>;
<b>use</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list">iota::deny_list</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/iota.md#iota_iota">iota::iota</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/table.md#iota_table">iota::table</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/iota/versioned.md#iota_versioned">iota::versioned</a>;
<b>use</b> <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool">iota_system::staking_pool</a>;
<b>use</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator">iota_system::validator</a>;
<b>use</b> <a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap">iota_system::validator_cap</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/u64.md#std_u64">std::u64</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_system_validator_wrapper_Validator"></a>

## Struct `Validator`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">Validator</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>inner: <a href="../../dependencies/iota/versioned.md#iota_versioned_Versioned">iota::versioned::Versioned</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_system_validator_wrapper_EInvalidVersion"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_EInvalidVersion">EInvalidVersion</a>: u64 = 0;
</code></pre>



<a name="iota_system_validator_wrapper_create_v1"></a>

## Function `create_v1`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_create_v1">create_v1</a>(validator: <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">iota_system::validator_wrapper::Validator</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_create_v1">create_v1</a>(validator: ValidatorV1, ctx: &<b>mut</b> TxContext): <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">Validator</a> {
    <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">Validator</a> {
        inner: versioned::create(1, validator, ctx),
    }
}
</code></pre>



</details>

<a name="iota_system_validator_wrapper_load_validator_maybe_upgrade"></a>

## Function `load_validator_maybe_upgrade`

This function should always return the latest supported version.
If the inner version is old, we upgrade it lazily in-place.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_load_validator_maybe_upgrade">load_validator_maybe_upgrade</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">iota_system::validator_wrapper::Validator</a>): &<b>mut</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_load_validator_maybe_upgrade">load_validator_maybe_upgrade</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">Validator</a>): &<b>mut</b> ValidatorV1 {
    <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_upgrade_to_latest">upgrade_to_latest</a>(self);
    versioned::load_value_mut(&<b>mut</b> self.inner)
}
</code></pre>



</details>

<a name="iota_system_validator_wrapper_destroy"></a>

## Function `destroy`

Destroy the wrapper and retrieve the inner validator object.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_destroy">destroy</a>(self: <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">iota_system::validator_wrapper::Validator</a>): <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_destroy">destroy</a>(self: <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">Validator</a>): ValidatorV1 {
    <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_upgrade_to_latest">upgrade_to_latest</a>(&self);
    <b>let</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">Validator</a> { inner } = self;
    versioned::destroy(inner)
}
</code></pre>



</details>

<a name="iota_system_validator_wrapper_upgrade_to_latest"></a>

## Function `upgrade_to_latest`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_upgrade_to_latest">upgrade_to_latest</a>(self: &<a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">iota_system::validator_wrapper::Validator</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_upgrade_to_latest">upgrade_to_latest</a>(self: &<a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">Validator</a>) {
    <b>let</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_version">version</a> = <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_version">version</a>(self);
    // TODO: When new versions are added, we need to explicitly upgrade here.
    <b>assert</b>!(<a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_version">version</a> == 1, <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_EInvalidVersion">EInvalidVersion</a>);
}
</code></pre>



</details>

<a name="iota_system_validator_wrapper_version"></a>

## Function `version`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_version">version</a>(self: &<a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">iota_system::validator_wrapper::Validator</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_version">version</a>(self: &<a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">Validator</a>): u64 {
    versioned::version(&self.inner)
}
</code></pre>



</details>
