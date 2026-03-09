
<a name="stardust_alias"></a>

# Module `stardust::alias`



-  [Struct `Alias`](#stardust_alias_Alias)
-  [Function `destroy`](#stardust_alias_destroy)
-  [Function `legacy_state_controller`](#stardust_alias_legacy_state_controller)
-  [Function `state_index`](#stardust_alias_state_index)
-  [Function `state_metadata`](#stardust_alias_state_metadata)
-  [Function `sender`](#stardust_alias_sender)
-  [Function `metadata`](#stardust_alias_metadata)
-  [Function `immutable_issuer`](#stardust_alias_immutable_issuer)
-  [Function `immutable_metadata`](#stardust_alias_immutable_metadata)
-  [Function `id`](#stardust_alias_id)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="stardust_alias_Alias"></a>

## Struct `Alias`

The persisted Alias object from Stardust, without tokens and assets.
Outputs owned the AliasID/Address in Stardust will be sent to this object and
have to be received via this object once extracted from <code>AliasOutput</code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a> <b>has</b> key, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/stardust/alias.md#stardust_alias_id">id</a>: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
 The ID of the Alias = hash of the Output ID that created the Alias Output in Stardust.
 This is the AliasID from Stardust.
</dd>
<dt>
<code><a href="../../dependencies/stardust/alias.md#stardust_alias_legacy_state_controller">legacy_state_controller</a>: <b>address</b></code>
</dt>
<dd>
 The last State Controller address assigned before the migration.
</dd>
<dt>
<code><a href="../../dependencies/stardust/alias.md#stardust_alias_state_index">state_index</a>: u32</code>
</dt>
<dd>
 A counter increased by 1 every time the alias was state transitioned.
</dd>
<dt>
<code><a href="../../dependencies/stardust/alias.md#stardust_alias_state_metadata">state_metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;</code>
</dt>
<dd>
 State metadata that can be used to store additional information.
</dd>
<dt>
<code><a href="../../dependencies/stardust/alias.md#stardust_alias_sender">sender</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;</code>
</dt>
<dd>
 The sender feature.
</dd>
<dt>
<code><a href="../../dependencies/stardust/alias.md#stardust_alias_metadata">metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;</code>
</dt>
<dd>
 The metadata feature.
</dd>
<dt>
<code><a href="../../dependencies/stardust/alias.md#stardust_alias_immutable_issuer">immutable_issuer</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;</code>
</dt>
<dd>
 The immutable issuer feature.
</dd>
<dt>
<code><a href="../../dependencies/stardust/alias.md#stardust_alias_immutable_metadata">immutable_metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;</code>
</dt>
<dd>
 The immutable metadata feature.
</dd>
</dl>


</details>

<a name="stardust_alias_destroy"></a>

## Function `destroy`

Destroy the <code><a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a></code> object, equivalent to <code>burning</code> an Alias Output in Stardust.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_destroy">destroy</a>(self: <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_destroy">destroy</a>(self: <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a>) {
    <b>let</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a> {
        <a href="../../dependencies/stardust/alias.md#stardust_alias_id">id</a>,
        <a href="../../dependencies/stardust/alias.md#stardust_alias_legacy_state_controller">legacy_state_controller</a>: _,
        <a href="../../dependencies/stardust/alias.md#stardust_alias_state_index">state_index</a>: _,
        <a href="../../dependencies/stardust/alias.md#stardust_alias_state_metadata">state_metadata</a>: _,
        <a href="../../dependencies/stardust/alias.md#stardust_alias_sender">sender</a>: _,
        <a href="../../dependencies/stardust/alias.md#stardust_alias_metadata">metadata</a>: _,
        <a href="../../dependencies/stardust/alias.md#stardust_alias_immutable_issuer">immutable_issuer</a>: _,
        <a href="../../dependencies/stardust/alias.md#stardust_alias_immutable_metadata">immutable_metadata</a>: _,
    } = self;
    object::delete(<a href="../../dependencies/stardust/alias.md#stardust_alias_id">id</a>);
}
</code></pre>



</details>

<a name="stardust_alias_legacy_state_controller"></a>

## Function `legacy_state_controller`

Get the Alias's <code><a href="../../dependencies/stardust/alias.md#stardust_alias_legacy_state_controller">legacy_state_controller</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_legacy_state_controller">legacy_state_controller</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>): &<b>address</b>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_legacy_state_controller">legacy_state_controller</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a>): &<b>address</b> {
    &self.<a href="../../dependencies/stardust/alias.md#stardust_alias_legacy_state_controller">legacy_state_controller</a>
}
</code></pre>



</details>

<a name="stardust_alias_state_index"></a>

## Function `state_index`

Get the Alias's <code><a href="../../dependencies/stardust/alias.md#stardust_alias_state_index">state_index</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_state_index">state_index</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>): u32
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_state_index">state_index</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a>): u32 {
    self.<a href="../../dependencies/stardust/alias.md#stardust_alias_state_index">state_index</a>
}
</code></pre>



</details>

<a name="stardust_alias_state_metadata"></a>

## Function `state_metadata`

Get the Alias's <code><a href="../../dependencies/stardust/alias.md#stardust_alias_state_metadata">state_metadata</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_state_metadata">state_metadata</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_state_metadata">state_metadata</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a>): &Option&lt;vector&lt;u8&gt;&gt; {
    &self.<a href="../../dependencies/stardust/alias.md#stardust_alias_state_metadata">state_metadata</a>
}
</code></pre>



</details>

<a name="stardust_alias_sender"></a>

## Function `sender`

Get the Alias's <code><a href="../../dependencies/stardust/alias.md#stardust_alias_sender">sender</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_sender">sender</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_sender">sender</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a>): &Option&lt;<b>address</b>&gt; {
    &self.<a href="../../dependencies/stardust/alias.md#stardust_alias_sender">sender</a>
}
</code></pre>



</details>

<a name="stardust_alias_metadata"></a>

## Function `metadata`

Get the Alias's <code><a href="../../dependencies/stardust/alias.md#stardust_alias_metadata">metadata</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_metadata">metadata</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_metadata">metadata</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a>): &Option&lt;vector&lt;u8&gt;&gt; {
    &self.<a href="../../dependencies/stardust/alias.md#stardust_alias_metadata">metadata</a>
}
</code></pre>



</details>

<a name="stardust_alias_immutable_issuer"></a>

## Function `immutable_issuer`

Get the Alias's <code>immutable_sender</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_immutable_issuer">immutable_issuer</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_immutable_issuer">immutable_issuer</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a>): &Option&lt;<b>address</b>&gt; {
    &self.<a href="../../dependencies/stardust/alias.md#stardust_alias_immutable_issuer">immutable_issuer</a>
}
</code></pre>



</details>

<a name="stardust_alias_immutable_metadata"></a>

## Function `immutable_metadata`

Get the Alias's <code><a href="../../dependencies/stardust/alias.md#stardust_alias_immutable_metadata">immutable_metadata</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_immutable_metadata">immutable_metadata</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_immutable_metadata">immutable_metadata</a>(self: &<a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a>): &Option&lt;vector&lt;u8&gt;&gt; {
    &self.<a href="../../dependencies/stardust/alias.md#stardust_alias_immutable_metadata">immutable_metadata</a>
}
</code></pre>



</details>

<a name="stardust_alias_id"></a>

## Function `id`

Get the Alias's id.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_id">id</a>(self: &<b>mut</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>): &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_id">id</a>(self: &<b>mut</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">Alias</a>): &<b>mut</b> UID {
    &<b>mut</b> self.<a href="../../dependencies/stardust/alias.md#stardust_alias_id">id</a>
}
</code></pre>



</details>
