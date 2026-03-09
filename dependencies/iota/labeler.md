
<a name="iota_labeler"></a>

# Module `iota::labeler`

Defines a LabelerCap used for creating labels in a ```iota::timelock::Timelock``` object.
The LabelerCap can be created only be consuming an OTW, making then labels unique for each cap.


-  [Struct `LabelerCap`](#iota_labeler_LabelerCap)
-  [Constants](#@Constants_0)
-  [Function `create_labeler_cap`](#iota_labeler_create_labeler_cap)
-  [Function `destroy_labeler_cap`](#iota_labeler_destroy_labeler_cap)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_labeler_LabelerCap"></a>

## Struct `LabelerCap`

<code><a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">LabelerCap</a></code> allows to create labels of the specific type <code>L</code>.
Can be publicly transferred like any other object.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">LabelerCap</a>&lt;<b>phantom</b> L&gt; <b>has</b> key, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_labeler_ENotOneTimeWitness"></a>

Error code for when a type passed to the <code><a href="../../dependencies/iota/labeler.md#iota_labeler_create_labeler_cap">create_labeler_cap</a></code> function is not a one-time witness.


<pre><code><b>const</b> <a href="../../dependencies/iota/labeler.md#iota_labeler_ENotOneTimeWitness">ENotOneTimeWitness</a>: u64 = 0;
</code></pre>



<a name="iota_labeler_create_labeler_cap"></a>

## Function `create_labeler_cap`

Create a <code><a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">LabelerCap</a></code> instance.
Can be created only by consuming a one time witness.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/labeler.md#iota_labeler_create_labeler_cap">create_labeler_cap</a>&lt;L: drop&gt;(witness: L, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">iota::labeler::LabelerCap</a>&lt;L&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/labeler.md#iota_labeler_create_labeler_cap">create_labeler_cap</a>&lt;L: drop&gt;(witness: L, ctx: &<b>mut</b> TxContext): <a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">LabelerCap</a>&lt;L&gt; {
    <b>assert</b>!(<a href="../../dependencies/iota/types.md#iota_types_is_one_time_witness">iota::types::is_one_time_witness</a>(&witness), <a href="../../dependencies/iota/labeler.md#iota_labeler_ENotOneTimeWitness">ENotOneTimeWitness</a>);
    <a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">LabelerCap</a>&lt;L&gt; {
        id: object::new(ctx),
    }
}
</code></pre>



</details>

<a name="iota_labeler_destroy_labeler_cap"></a>

## Function `destroy_labeler_cap`

Delete a <code><a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">LabelerCap</a></code> instance.
If a capability is destroyed, it is impossible to add the related labels.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/labeler.md#iota_labeler_destroy_labeler_cap">destroy_labeler_cap</a>&lt;L&gt;(cap: <a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">iota::labeler::LabelerCap</a>&lt;L&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/labeler.md#iota_labeler_destroy_labeler_cap">destroy_labeler_cap</a>&lt;L&gt;(cap: <a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">LabelerCap</a>&lt;L&gt;) {
    <b>let</b> <a href="../../dependencies/iota/labeler.md#iota_labeler_LabelerCap">LabelerCap</a>&lt;L&gt; {
        id,
    } = cap;
    object::delete(id);
}
</code></pre>



</details>
