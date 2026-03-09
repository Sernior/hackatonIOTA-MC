
<a name="stardust_nft"></a>

# Module `stardust::nft`



-  [Struct `NFT`](#stardust_nft_NFT)
-  [Struct `Nft`](#stardust_nft_Nft)
-  [Function `init`](#stardust_nft_init)
-  [Function `destroy`](#stardust_nft_destroy)
-  [Function `legacy_sender`](#stardust_nft_legacy_sender)
-  [Function `metadata`](#stardust_nft_metadata)
-  [Function `tag`](#stardust_nft_tag)
-  [Function `immutable_issuer`](#stardust_nft_immutable_issuer)
-  [Function `immutable_metadata`](#stardust_nft_immutable_metadata)
-  [Function `id`](#stardust_nft_id)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/display.md#iota_display">iota::display</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/package.md#iota_package">iota::package</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27">stardust::irc27</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/fixed_point32.md#std_fixed_point32">std::fixed_point32</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="stardust_nft_NFT"></a>

## Struct `NFT`

One Time Witness.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_NFT">NFT</a> <b>has</b> drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="stardust_nft_Nft"></a>

## Struct `Nft`

The Stardust NFT representation.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a> <b>has</b> key, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/stardust/nft.md#stardust_nft_id">id</a>: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
 The Nft's ID is nested from Stardust.
</dd>
<dt>
<code><a href="../../dependencies/stardust/nft.md#stardust_nft_legacy_sender">legacy_sender</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;</code>
</dt>
<dd>
 The sender feature holds the last sender address assigned before the migration and
 is not supported by the protocol after it.
</dd>
<dt>
<code><a href="../../dependencies/stardust/nft.md#stardust_nft_metadata">metadata</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;</code>
</dt>
<dd>
 The metadata feature.
</dd>
<dt>
<code><a href="../../dependencies/stardust/nft.md#stardust_nft_tag">tag</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;</code>
</dt>
<dd>
 The tag feature.
</dd>
<dt>
<code><a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_issuer">immutable_issuer</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;</code>
</dt>
<dd>
 The immutable issuer feature.
</dd>
<dt>
<code><a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>: <a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a></code>
</dt>
<dd>
 The immutable metadata feature.
</dd>
</dl>


</details>

<a name="stardust_nft_init"></a>

## Function `init`

The <code><a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a></code> module initializer.


<pre><code><b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_init">init</a>(otw: <a href="../../dependencies/stardust/nft.md#stardust_nft_NFT">stardust::nft::NFT</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_init">init</a>(otw: <a href="../../dependencies/stardust/nft.md#stardust_nft_NFT">NFT</a>, ctx: &<b>mut</b> TxContext) {
    // Claim the <b>module</b> publisher.
    <b>let</b> publisher = package::claim(otw, ctx);
    // Build a `Display` object.
    <b>let</b> keys = vector[
        // The IOTA standard fields.
        string::utf8(b"name"),
        string::utf8(b"image_url"),
        string::utf8(b"description"),
        string::utf8(b"creator"),
        // The extra IRC27-nested fields.
        string::utf8(b"version"),
        string::utf8(b"media_type"),
        string::utf8(b"collection_name"),
        // The issuer of the <a href="../../dependencies/stardust/nft.md#stardust_nft_NFT">NFT</a>. Equivalent to IRC-27 `collectionId`.
        string::utf8(b"<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_issuer">immutable_issuer</a>"),
    ];
    <b>let</b> values = vector[
        // The IOTA standard fields.
        string::utf8(b"{<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>.name}"),
        string::utf8(b"{<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>.uri}"),
        string::utf8(b"{<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>.description}"),
        string::utf8(b"{<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>.issuer_name}"),
        // The extra IRC27-nested fields.
        string::utf8(b"{<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>.version}"),
        string::utf8(b"{<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>.media_type}"),
        string::utf8(b"{<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>.collection_name}"),
        // The issuer of the <a href="../../dependencies/stardust/nft.md#stardust_nft_NFT">NFT</a>. Equivalent to IRC-27 `collectionId`.
        string::utf8(b"{<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_issuer">immutable_issuer</a>}"),
    ];
    <b>let</b> <b>mut</b> display = display::new_with_fields&lt;<a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a>&gt;(
        &publisher,
        keys,
        values,
        ctx,
    );
    // Commit the first version of `Display` to apply changes.
    display.update_version();
    // Burn the publisher object.
    package::burn_publisher(publisher);
    // Freeze the display object.
    <a href="../../dependencies/iota/transfer.md#iota_transfer_public_freeze_object">iota::transfer::public_freeze_object</a>(display);
}
</code></pre>



</details>

<a name="stardust_nft_destroy"></a>

## Function `destroy`

Permanently destroy an <code><a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a></code> object.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_destroy">destroy</a>(nft: <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_destroy">destroy</a>(nft: <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a>) {
    <b>let</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a> {
        <a href="../../dependencies/stardust/nft.md#stardust_nft_id">id</a>,
        <a href="../../dependencies/stardust/nft.md#stardust_nft_legacy_sender">legacy_sender</a>: _,
        <a href="../../dependencies/stardust/nft.md#stardust_nft_metadata">metadata</a>: _,
        <a href="../../dependencies/stardust/nft.md#stardust_nft_tag">tag</a>: _,
        <a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_issuer">immutable_issuer</a>: _,
        <a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>,
    } = nft;
    irc27::destroy(<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>);
    object::delete(<a href="../../dependencies/stardust/nft.md#stardust_nft_id">id</a>);
}
</code></pre>



</details>

<a name="stardust_nft_legacy_sender"></a>

## Function `legacy_sender`

Get the Nft's <code><a href="../../dependencies/stardust/nft.md#stardust_nft_legacy_sender">legacy_sender</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_legacy_sender">legacy_sender</a>(nft: &<a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_legacy_sender">legacy_sender</a>(nft: &<a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a>): &Option&lt;<b>address</b>&gt; {
    &nft.<a href="../../dependencies/stardust/nft.md#stardust_nft_legacy_sender">legacy_sender</a>
}
</code></pre>



</details>

<a name="stardust_nft_metadata"></a>

## Function `metadata`

Get the Nft's <code><a href="../../dependencies/stardust/nft.md#stardust_nft_metadata">metadata</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_metadata">metadata</a>(nft: &<a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_metadata">metadata</a>(nft: &<a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a>): &Option&lt;vector&lt;u8&gt;&gt; {
    &nft.<a href="../../dependencies/stardust/nft.md#stardust_nft_metadata">metadata</a>
}
</code></pre>



</details>

<a name="stardust_nft_tag"></a>

## Function `tag`

Get the Nft's <code><a href="../../dependencies/stardust/nft.md#stardust_nft_tag">tag</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_tag">tag</a>(nft: &<a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_tag">tag</a>(nft: &<a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a>): &Option&lt;vector&lt;u8&gt;&gt; {
    &nft.<a href="../../dependencies/stardust/nft.md#stardust_nft_tag">tag</a>
}
</code></pre>



</details>

<a name="stardust_nft_immutable_issuer"></a>

## Function `immutable_issuer`

Get the Nft's <code>immutable_sender</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_issuer">immutable_issuer</a>(nft: &<a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_issuer">immutable_issuer</a>(nft: &<a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a>): &Option&lt;<b>address</b>&gt; {
    &nft.<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_issuer">immutable_issuer</a>
}
</code></pre>



</details>

<a name="stardust_nft_immutable_metadata"></a>

## Function `immutable_metadata`

Get the Nft's <code><a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>(nft: &<a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>): &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>(nft: &<a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a>): &Irc27Metadata {
    &nft.<a href="../../dependencies/stardust/nft.md#stardust_nft_immutable_metadata">immutable_metadata</a>
}
</code></pre>



</details>

<a name="stardust_nft_id"></a>

## Function `id`

Get the Nft's id.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_id">id</a>(self: &<b>mut</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>): &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_id">id</a>(self: &<b>mut</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">Nft</a>): &<b>mut</b> UID {
    &<b>mut</b> self.<a href="../../dependencies/stardust/nft.md#stardust_nft_id">id</a>
}
</code></pre>



</details>
