
<a name="stardust_alias_output"></a>

# Module `stardust::alias_output`



-  [Struct `AliasOutput`](#stardust_alias_output_AliasOutput)
-  [Constants](#@Constants_0)
-  [Function `extract_assets`](#stardust_alias_output_extract_assets)
-  [Function `receive`](#stardust_alias_output_receive)
-  [Function `attach_alias`](#stardust_alias_output_attach_alias)
-  [Function `load_alias`](#stardust_alias_output_load_alias)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/stardust/alias.md#stardust_alias">stardust::alias</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="stardust_alias_output_AliasOutput"></a>

## Struct `AliasOutput`

Owned Object controlled by the Governor Address.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">AliasOutput</a>&lt;<b>phantom</b> T&gt; <b>has</b> key
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
 This is a "random" UID, not the AliasID from Stardust.
</dd>
<dt>
<code>balance: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;</code>
</dt>
<dd>
 The amount of coins held by the output.
</dd>
<dt>
<code>native_tokens: <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a></code>
</dt>
<dd>
 The <code>Bag</code> holds native tokens, key-ed by the stringified type of the asset.
 Example: key: "0xabcded::soon::SOON", value: Balance<0xabcded::soon::SOON>.
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="stardust_alias_output_ALIAS_NAME"></a>

The Alias dynamic object field name.


<pre><code><b>const</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_ALIAS_NAME">ALIAS_NAME</a>: vector&lt;u8&gt; = vector[97, 108, 105, 97, 115];
</code></pre>



<a name="stardust_alias_output_extract_assets"></a>

## Function `extract_assets`

The function extracts assets from a legacy <code><a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">AliasOutput</a></code>.
- returns the coin Balance,
- the native tokens Bag,
- and the <code>Alias</code> object that persists the AliasID=ObjectID from Stardust.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_extract_assets">extract_assets</a>&lt;T&gt;(output: <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">stardust::alias_output::AliasOutput</a>&lt;T&gt;): (<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;, <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a>, <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_extract_assets">extract_assets</a>&lt;T&gt;(<b>mut</b> output: <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">AliasOutput</a>&lt;T&gt;): (Balance&lt;T&gt;, Bag, Alias) {
    // Load the related alias object.
    <b>let</b> alias = <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_load_alias">load_alias</a>(&<b>mut</b> output);
    // Unpack the output into its basic part.
    <b>let</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">AliasOutput</a> {
        id,
        balance,
        native_tokens,
    } = output;
    // Delete the output.
    object::delete(id);
    (balance, native_tokens, alias)
}
</code></pre>



</details>

<a name="stardust_alias_output_receive"></a>

## Function `receive`

Utility function to receive an <code><a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">AliasOutput</a></code> object in other Stardust modules.
Other modules in the Stardust package can call this function to receive an <code><a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">AliasOutput</a></code> object (nft).


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_receive">receive</a>&lt;T&gt;(parent: &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>, output: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;<a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">stardust::alias_output::AliasOutput</a>&lt;T&gt;&gt;): <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">stardust::alias_output::AliasOutput</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_receive">receive</a>&lt;T&gt;(
    parent: &<b>mut</b> UID,
    output: Receiving&lt;<a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">AliasOutput</a>&lt;T&gt;&gt;,
): <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">AliasOutput</a>&lt;T&gt; {
    transfer::receive(parent, output)
}
</code></pre>



</details>

<a name="stardust_alias_output_attach_alias"></a>

## Function `attach_alias`

Utility function to attach an <code>Alias</code> to an <code><a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">AliasOutput</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_attach_alias">attach_alias</a>&lt;T&gt;(output: &<b>mut</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">stardust::alias_output::AliasOutput</a>&lt;T&gt;, alias: <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_attach_alias">attach_alias</a>&lt;T&gt;(output: &<b>mut</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">AliasOutput</a>&lt;T&gt;, alias: Alias) {
    dynamic_object_field::add(&<b>mut</b> output.id, <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_ALIAS_NAME">ALIAS_NAME</a>, alias)
}
</code></pre>



</details>

<a name="stardust_alias_output_load_alias"></a>

## Function `load_alias`

Loads the <code>Alias</code> object from the dynamic object field.


<pre><code><b>fun</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_load_alias">load_alias</a>&lt;T&gt;(output: &<b>mut</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">stardust::alias_output::AliasOutput</a>&lt;T&gt;): <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_load_alias">load_alias</a>&lt;T&gt;(output: &<b>mut</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">AliasOutput</a>&lt;T&gt;): Alias {
    dynamic_object_field::remove(&<b>mut</b> output.id, <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_ALIAS_NAME">ALIAS_NAME</a>)
}
</code></pre>



</details>
