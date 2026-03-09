
<a name="(iota_notarization=0x0)_method"></a>

# Module `(iota_notarization=0x0)::method`

This module provides enum NotarizationMethod used to distinguish programmatically
between Notarization methods.


-  [Enum `NotarizationMethod`](#(iota_notarization=0x0)_method_NotarizationMethod)
-  [Function `new_dynamic`](#(iota_notarization=0x0)_method_new_dynamic)
-  [Function `new_locked`](#(iota_notarization=0x0)_method_new_locked)
-  [Function `is_dynamic`](#(iota_notarization=0x0)_method_is_dynamic)
-  [Function `is_locked`](#(iota_notarization=0x0)_method_is_locked)
-  [Function `to_str`](#(iota_notarization=0x0)_method_to_str)


<pre><code><b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="(iota_notarization=0x0)_method_NotarizationMethod"></a>

## Enum `NotarizationMethod`



<pre><code><b>public</b> <b>enum</b> <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_NotarizationMethod">NotarizationMethod</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Variants</summary>


<dl>
<dt>
Variant <code>Dynamic</code>
</dt>
<dd>
</dd>
<dt>
Variant <code>Locked</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_notarization=0x0)_method_new_dynamic"></a>

## Function `new_dynamic`

Returns a new NotarizationMethod::Dynamic.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_new_dynamic">new_dynamic</a>(): (iota_notarization=0x0)::method::NotarizationMethod
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_new_dynamic">new_dynamic</a>(): <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_NotarizationMethod">NotarizationMethod</a> {
    NotarizationMethod::Dynamic
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_method_new_locked"></a>

## Function `new_locked`

Returns a new NotarizationMethod::Locked.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_new_locked">new_locked</a>(): (iota_notarization=0x0)::method::NotarizationMethod
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_new_locked">new_locked</a>(): <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_NotarizationMethod">NotarizationMethod</a> {
    NotarizationMethod::Locked
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_method_is_dynamic"></a>

## Function `is_dynamic`

Returns true if the NotarizationMethod is Dynamic


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_is_dynamic">is_dynamic</a>(method: &(iota_notarization=0x0)::method::NotarizationMethod): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_is_dynamic">is_dynamic</a>(method: &<a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_NotarizationMethod">NotarizationMethod</a>): bool {
    match (method) {
        NotarizationMethod::Dynamic =&gt; <b>true</b>,
        NotarizationMethod::Locked =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_method_is_locked"></a>

## Function `is_locked`

Returns true if the NotarizationMethod is Locked


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_is_locked">is_locked</a>(method: &(iota_notarization=0x0)::method::NotarizationMethod): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_is_locked">is_locked</a>(method: &<a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_NotarizationMethod">NotarizationMethod</a>): bool {
    match (method) {
        NotarizationMethod::Dynamic =&gt; <b>false</b>,
        NotarizationMethod::Locked =&gt; <b>true</b>,
    }
}
</code></pre>



</details>

<a name="(iota_notarization=0x0)_method_to_str"></a>

## Function `to_str`

Returns the Notarization method as String


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_to_str">to_str</a>(method: &(iota_notarization=0x0)::method::NotarizationMethod): <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_to_str">to_str</a>(method: &<a href="../../dependencies/nplex/method.md#(iota_notarization=0x0)_method_NotarizationMethod">NotarizationMethod</a>): String {
    match (method) {
        NotarizationMethod::Dynamic =&gt; {
            string::utf8(b"DynamicNotarization")
        },
        NotarizationMethod::Locked =&gt; {
            string::utf8(b"LockedNotarization")
        },
    }
}
</code></pre>



</details>
