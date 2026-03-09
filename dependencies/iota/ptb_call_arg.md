
<a name="iota_ptb_call_arg"></a>

# Module `iota::ptb_call_arg`



-  [Struct `ObjectRef`](#iota_ptb_call_arg_ObjectRef)
-  [Enum `CallArg`](#iota_ptb_call_arg_CallArg)
-  [Enum `ObjectArg`](#iota_ptb_call_arg_ObjectArg)
-  [Function `is_pure_data`](#iota_ptb_call_arg_is_pure_data)
-  [Function `is_object_data`](#iota_ptb_call_arg_is_object_data)
-  [Function `as_pure_data`](#iota_ptb_call_arg_as_pure_data)
-  [Function `as_object_data`](#iota_ptb_call_arg_as_object_data)
-  [Function `is_shared_object`](#iota_ptb_call_arg_is_shared_object)
-  [Function `is_imm_or_owned_object`](#iota_ptb_call_arg_is_imm_or_owned_object)
-  [Function `is_receiving_object`](#iota_ptb_call_arg_is_receiving_object)
-  [Function `object_id`](#iota_ptb_call_arg_object_id)
-  [Function `object_version`](#iota_ptb_call_arg_object_version)
-  [Function `object_digest`](#iota_ptb_call_arg_object_digest)
-  [Function `object_ref`](#iota_ptb_call_arg_object_ref)
-  [Function `is_mutable_shared_object`](#iota_ptb_call_arg_is_mutable_shared_object)
-  [Function `id`](#iota_ptb_call_arg_id)
-  [Function `sequence_number`](#iota_ptb_call_arg_sequence_number)
-  [Function `digest`](#iota_ptb_call_arg_digest)


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



<a name="iota_ptb_call_arg_ObjectRef"></a>

## Struct `ObjectRef`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectRef">ObjectRef</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_id">object_id</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_sequence_number">sequence_number</a>: u64</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_digest">object_digest</a>: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_ptb_call_arg_CallArg"></a>

## Enum `CallArg`



<pre><code><b>public</b> <b>enum</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">CallArg</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Variants</summary>


<dl>
<dt>
Variant <code>PureData</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>ObjectData</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">iota::ptb_call_arg::ObjectArg</a></code>
</dt>
<dd>
</dd>
</dl>

</dl>


</details>

<a name="iota_ptb_call_arg_ObjectArg"></a>

## Enum `ObjectArg`



<pre><code><b>public</b> <b>enum</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">ObjectArg</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Variants</summary>


<dl>
<dt>
Variant <code>ImmOrOwnedObject</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectRef">iota::ptb_call_arg::ObjectRef</a></code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>SharedObject</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code><a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_id">id</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


<dl>
<dt>
<code>initial_shared_version: u64</code>
</dt>
<dd>
</dd>
</dl>


<dl>
<dt>
<code>mutable: bool</code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>ReceivingObject</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectRef">iota::ptb_call_arg::ObjectRef</a></code>
</dt>
<dd>
</dd>
</dl>

</dl>


</details>

<a name="iota_ptb_call_arg_is_pure_data"></a>

## Function `is_pure_data`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_pure_data">is_pure_data</a>(arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">iota::ptb_call_arg::CallArg</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_pure_data">is_pure_data</a>(arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">CallArg</a>): bool {
    match (arg) {
        CallArg::PureData(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_is_object_data"></a>

## Function `is_object_data`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_object_data">is_object_data</a>(arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">iota::ptb_call_arg::CallArg</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_object_data">is_object_data</a>(arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">CallArg</a>): bool {
    match (arg) {
        CallArg::ObjectData(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_as_pure_data"></a>

## Function `as_pure_data`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_as_pure_data">as_pure_data</a>(arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">iota::ptb_call_arg::CallArg</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_as_pure_data">as_pure_data</a>(arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">CallArg</a>): Option&lt;vector&lt;u8&gt;&gt; {
    match (arg) {
        CallArg::PureData(data) =&gt; some(*data),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_as_object_data"></a>

## Function `as_object_data`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_as_object_data">as_object_data</a>(arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">iota::ptb_call_arg::CallArg</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">iota::ptb_call_arg::ObjectArg</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_as_object_data">as_object_data</a>(arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">CallArg</a>): Option&lt;<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">ObjectArg</a>&gt; {
    match (arg) {
        CallArg::ObjectData(obj) =&gt; some(*obj),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_is_shared_object"></a>

## Function `is_shared_object`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_shared_object">is_shared_object</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">iota::ptb_call_arg::ObjectArg</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_shared_object">is_shared_object</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">ObjectArg</a>): bool {
    match (obj_arg) {
        ObjectArg::SharedObject { <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_id">id</a>: _, initial_shared_version: _, mutable: _ } =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_is_imm_or_owned_object"></a>

## Function `is_imm_or_owned_object`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_imm_or_owned_object">is_imm_or_owned_object</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">iota::ptb_call_arg::ObjectArg</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_imm_or_owned_object">is_imm_or_owned_object</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">ObjectArg</a>): bool {
    match (obj_arg) {
        ObjectArg::ImmOrOwnedObject(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_is_receiving_object"></a>

## Function `is_receiving_object`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_receiving_object">is_receiving_object</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">iota::ptb_call_arg::ObjectArg</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_receiving_object">is_receiving_object</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">ObjectArg</a>): bool {
    match (obj_arg) {
        ObjectArg::ReceivingObject(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_object_id"></a>

## Function `object_id`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_id">object_id</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">iota::ptb_call_arg::ObjectArg</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_id">object_id</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">ObjectArg</a>): Option&lt;ID&gt; {
    match (obj_arg) {
        ObjectArg::ImmOrOwnedObject(obj_ref) =&gt; some(obj_ref.<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_id">object_id</a>),
        ObjectArg::ReceivingObject(obj_ref) =&gt; some(obj_ref.<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_id">object_id</a>),
        ObjectArg::SharedObject { <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_id">id</a>, initial_shared_version: _, mutable: _ } =&gt; some(*<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_id">id</a>),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_object_version"></a>

## Function `object_version`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_version">object_version</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">iota::ptb_call_arg::ObjectArg</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_version">object_version</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">ObjectArg</a>): Option&lt;u64&gt; {
    match (obj_arg) {
        ObjectArg::ImmOrOwnedObject(obj_ref) =&gt; some(obj_ref.<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_sequence_number">sequence_number</a>),
        ObjectArg::ReceivingObject(obj_ref) =&gt; some(obj_ref.<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_sequence_number">sequence_number</a>),
        ObjectArg::SharedObject { <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_id">id</a>: _, initial_shared_version, mutable: _ } =&gt; some(
            *initial_shared_version,
        ),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_object_digest"></a>

## Function `object_digest`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_digest">object_digest</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">iota::ptb_call_arg::ObjectArg</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;vector&lt;u8&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_digest">object_digest</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">ObjectArg</a>): Option&lt;vector&lt;u8&gt;&gt; {
    match (obj_arg) {
        ObjectArg::ImmOrOwnedObject(obj_ref) =&gt; some(obj_ref.<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_digest">object_digest</a>),
        ObjectArg::ReceivingObject(obj_ref) =&gt; some(obj_ref.<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_digest">object_digest</a>),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_object_ref"></a>

## Function `object_ref`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_ref">object_ref</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">iota::ptb_call_arg::ObjectArg</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectRef">iota::ptb_call_arg::ObjectRef</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_ref">object_ref</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">ObjectArg</a>): Option&lt;<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectRef">ObjectRef</a>&gt; {
    match (obj_arg) {
        ObjectArg::ImmOrOwnedObject(obj_ref) =&gt; some(*obj_ref),
        ObjectArg::ReceivingObject(obj_ref) =&gt; some(*obj_ref),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_is_mutable_shared_object"></a>

## Function `is_mutable_shared_object`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_mutable_shared_object">is_mutable_shared_object</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">iota::ptb_call_arg::ObjectArg</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;bool&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_is_mutable_shared_object">is_mutable_shared_object</a>(obj_arg: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectArg">ObjectArg</a>): Option&lt;bool&gt; {
    match (obj_arg) {
        ObjectArg::SharedObject { <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_id">id</a>: _, initial_shared_version: _, mutable } =&gt; some(*mutable),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_id"></a>

## Function `id`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_id">id</a>(obj_ref: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectRef">iota::ptb_call_arg::ObjectRef</a>): &<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_id">id</a>(obj_ref: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectRef">ObjectRef</a>): &ID {
    &obj_ref.<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_id">object_id</a>
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_sequence_number"></a>

## Function `sequence_number`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_sequence_number">sequence_number</a>(obj_ref: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectRef">iota::ptb_call_arg::ObjectRef</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_sequence_number">sequence_number</a>(obj_ref: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectRef">ObjectRef</a>): u64 {
    obj_ref.<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_sequence_number">sequence_number</a>
}
</code></pre>



</details>

<a name="iota_ptb_call_arg_digest"></a>

## Function `digest`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_digest">digest</a>(obj_ref: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectRef">iota::ptb_call_arg::ObjectRef</a>): &vector&lt;u8&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_digest">digest</a>(obj_ref: &<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_ObjectRef">ObjectRef</a>): &vector&lt;u8&gt; {
    &obj_ref.<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_object_digest">object_digest</a>
}
</code></pre>



</details>
