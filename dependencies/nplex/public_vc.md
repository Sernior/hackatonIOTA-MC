
<a name="(iota_identity=0x0)_public_vc"></a>

# Module `(iota_identity=0x0)::public_vc`



-  [Struct `PublicVc`](#(iota_identity=0x0)_public_vc_PublicVc)
-  [Function `new`](#(iota_identity=0x0)_public_vc_new)
-  [Function `data`](#(iota_identity=0x0)_public_vc_data)
-  [Function `set_data`](#(iota_identity=0x0)_public_vc_set_data)


<pre><code></code></pre>



<a name="(iota_identity=0x0)_public_vc_PublicVc"></a>

## Struct `PublicVc`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_PublicVc">PublicVc</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_data">data</a>: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_public_vc_new"></a>

## Function `new`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_new">new</a>(<a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_data">data</a>: vector&lt;u8&gt;): (iota_identity=0x0)::public_vc::PublicVc
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_new">new</a>(<a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_data">data</a>: vector&lt;u8&gt;): <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_PublicVc">PublicVc</a> {
    <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_PublicVc">PublicVc</a> { <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_data">data</a> }
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_public_vc_data"></a>

## Function `data`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_data">data</a>(self: &(iota_identity=0x0)::public_vc::PublicVc): &vector&lt;u8&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_data">data</a>(self: &<a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_PublicVc">PublicVc</a>): &vector&lt;u8&gt; {
    &self.<a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_data">data</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_public_vc_set_data"></a>

## Function `set_data`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_set_data">set_data</a>(self: &<b>mut</b> (iota_identity=0x0)::public_vc::PublicVc, <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_data">data</a>: vector&lt;u8&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_set_data">set_data</a>(self: &<b>mut</b> <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_PublicVc">PublicVc</a>, <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_data">data</a>: vector&lt;u8&gt;) {
    self.<a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_data">data</a> = <a href="../../dependencies/nplex/public_vc.md#(iota_identity=0x0)_public_vc_data">data</a>
}
</code></pre>



</details>
