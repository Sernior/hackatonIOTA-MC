
<a name="stardust_irc27"></a>

# Module `stardust::irc27`



-  [Struct `Irc27Metadata`](#stardust_irc27_Irc27Metadata)
-  [Function `version`](#stardust_irc27_version)
-  [Function `media_type`](#stardust_irc27_media_type)
-  [Function `uri`](#stardust_irc27_uri)
-  [Function `name`](#stardust_irc27_name)
-  [Function `collection_name`](#stardust_irc27_collection_name)
-  [Function `royalties`](#stardust_irc27_royalties)
-  [Function `issuer_name`](#stardust_irc27_issuer_name)
-  [Function `description`](#stardust_irc27_description)
-  [Function `attributes`](#stardust_irc27_attributes)
-  [Function `non_standard_fields`](#stardust_irc27_non_standard_fields)
-  [Function `destroy`](#stardust_irc27_destroy)


<pre><code><b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/fixed_point32.md#std_fixed_point32">std::fixed_point32</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="stardust_irc27_Irc27Metadata"></a>

## Struct `Irc27Metadata`

The IRC27 NFT metadata standard schema.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_version">version</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a></code>
</dt>
<dd>
 Version of the metadata standard.
</dd>
<dt>
<code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_media_type">media_type</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a></code>
</dt>
<dd>
 The media type (MIME) of the asset.
 ## Examples
 - Image files: <code>image/jpeg</code>, <code>image/png</code>, <code>image/gif</code>, etc.
 - Video files: <code>video/x-msvideo</code> (avi), <code>video/mp4</code>, <code>video/mpeg</code>, etc.
 - Audio files: <code>audio/mpeg</code>, <code>audio/wav</code>, etc.
 - 3D Assets: <code>model/obj</code>, <code>model/u3d</code>, etc.
 - Documents: <code>application/pdf</code>, <code>text/plain</code>, etc.
</dd>
<dt>
<code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_uri">uri</a>: <a href="../../dependencies/iota/url.md#iota_url_Url">iota::url::Url</a></code>
</dt>
<dd>
 URL pointing to the NFT file location.
</dd>
<dt>
<code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_name">name</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a></code>
</dt>
<dd>
 Alphanumeric text string defining the human identifiable name for the NFT.
</dd>
<dt>
<code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_collection_name">collection_name</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
 The human-readable collection name of the NFT.
</dd>
<dt>
<code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_royalties">royalties</a>: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/std/fixed_point32.md#std_fixed_point32_FixedPoint32">std::fixed_point32::FixedPoint32</a>&gt;</code>
</dt>
<dd>
 Royalty payment addresses mapped to the payout percentage.
 Contains a hash of the 32 bytes parsed from the BECH32 encoded IOTA address in the metadata, it is a legacy address.
 Royalties are not supported by the protocol and needed to be processed by an integrator.
</dd>
<dt>
<code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_issuer_name">issuer_name</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
 The human-readable name of the NFT creator.
</dd>
<dt>
<code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_description">description</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
 The human-readable description of the NFT.
</dd>
<dt>
<code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_attributes">attributes</a>: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
 Additional attributes which follow [OpenSea Metadata standards](https://docs.opensea.io/docs/metadata-standards).
</dd>
<dt>
<code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_non_standard_fields">non_standard_fields</a>: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
 Legacy non-standard metadata fields.
</dd>
</dl>


</details>

<a name="stardust_irc27_version"></a>

## Function `version`

Get the metadata's <code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_version">version</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_version">version</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>): &<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_version">version</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a>): &String {
    &irc27.<a href="../../dependencies/stardust/irc27.md#stardust_irc27_version">version</a>
}
</code></pre>



</details>

<a name="stardust_irc27_media_type"></a>

## Function `media_type`

Get the metadata's <code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_media_type">media_type</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_media_type">media_type</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>): &<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_media_type">media_type</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a>): &String {
    &irc27.<a href="../../dependencies/stardust/irc27.md#stardust_irc27_media_type">media_type</a>
}
</code></pre>



</details>

<a name="stardust_irc27_uri"></a>

## Function `uri`

Get the metadata's <code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_uri">uri</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_uri">uri</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>): &<a href="../../dependencies/iota/url.md#iota_url_Url">iota::url::Url</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_uri">uri</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a>): &Url {
    &irc27.<a href="../../dependencies/stardust/irc27.md#stardust_irc27_uri">uri</a>
}
</code></pre>



</details>

<a name="stardust_irc27_name"></a>

## Function `name`

Get the metadata's <code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_name">name</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_name">name</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>): &<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_name">name</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a>): &String {
    &irc27.<a href="../../dependencies/stardust/irc27.md#stardust_irc27_name">name</a>
}
</code></pre>



</details>

<a name="stardust_irc27_collection_name"></a>

## Function `collection_name`

Get the metadata's <code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_collection_name">collection_name</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_collection_name">collection_name</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_collection_name">collection_name</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a>): &Option&lt;String&gt; {
    &irc27.<a href="../../dependencies/stardust/irc27.md#stardust_irc27_collection_name">collection_name</a>
}
</code></pre>



</details>

<a name="stardust_irc27_royalties"></a>

## Function `royalties`

Get the metadata's <code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_royalties">royalties</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_royalties">royalties</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>): &<a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/std/fixed_point32.md#std_fixed_point32_FixedPoint32">std::fixed_point32::FixedPoint32</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_royalties">royalties</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a>): &VecMap&lt;<b>address</b>, FixedPoint32&gt; {
    &irc27.<a href="../../dependencies/stardust/irc27.md#stardust_irc27_royalties">royalties</a>
}
</code></pre>



</details>

<a name="stardust_irc27_issuer_name"></a>

## Function `issuer_name`

Get the metadata's <code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_issuer_name">issuer_name</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_issuer_name">issuer_name</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_issuer_name">issuer_name</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a>): &Option&lt;String&gt; {
    &irc27.<a href="../../dependencies/stardust/irc27.md#stardust_irc27_issuer_name">issuer_name</a>
}
</code></pre>



</details>

<a name="stardust_irc27_description"></a>

## Function `description`

Get the metadata's <code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_description">description</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_description">description</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_description">description</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a>): &Option&lt;String&gt; {
    &irc27.<a href="../../dependencies/stardust/irc27.md#stardust_irc27_description">description</a>
}
</code></pre>



</details>

<a name="stardust_irc27_attributes"></a>

## Function `attributes`

Get the metadata's <code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_attributes">attributes</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_attributes">attributes</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>): &<a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_attributes">attributes</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a>): &VecMap&lt;String, String&gt; {
    &irc27.<a href="../../dependencies/stardust/irc27.md#stardust_irc27_attributes">attributes</a>
}
</code></pre>



</details>

<a name="stardust_irc27_non_standard_fields"></a>

## Function `non_standard_fields`

Get the metadata's <code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_non_standard_fields">non_standard_fields</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_non_standard_fields">non_standard_fields</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>): &<a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_non_standard_fields">non_standard_fields</a>(irc27: &<a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a>): &VecMap&lt;String, String&gt; {
    &irc27.<a href="../../dependencies/stardust/irc27.md#stardust_irc27_non_standard_fields">non_standard_fields</a>
}
</code></pre>



</details>

<a name="stardust_irc27_destroy"></a>

## Function `destroy`

Permanently destroy a <code><a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a></code> object.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_destroy">destroy</a>(irc27: <a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">stardust::irc27::Irc27Metadata</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_destroy">destroy</a>(irc27: <a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a>) {
    <b>let</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27_Irc27Metadata">Irc27Metadata</a> {
        <a href="../../dependencies/stardust/irc27.md#stardust_irc27_version">version</a>: _,
        <a href="../../dependencies/stardust/irc27.md#stardust_irc27_media_type">media_type</a>: _,
        <a href="../../dependencies/stardust/irc27.md#stardust_irc27_uri">uri</a>: _,
        <a href="../../dependencies/stardust/irc27.md#stardust_irc27_name">name</a>: _,
        <a href="../../dependencies/stardust/irc27.md#stardust_irc27_collection_name">collection_name</a>: _,
        <a href="../../dependencies/stardust/irc27.md#stardust_irc27_royalties">royalties</a>: _,
        <a href="../../dependencies/stardust/irc27.md#stardust_irc27_issuer_name">issuer_name</a>: _,
        <a href="../../dependencies/stardust/irc27.md#stardust_irc27_description">description</a>: _,
        <a href="../../dependencies/stardust/irc27.md#stardust_irc27_attributes">attributes</a>: _,
        <a href="../../dependencies/stardust/irc27.md#stardust_irc27_non_standard_fields">non_standard_fields</a>: _,
    } = irc27;
}
</code></pre>



</details>
