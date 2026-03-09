
<a name="(iota_identity=0x0)_utils"></a>

# Module `(iota_identity=0x0)::utils`



-  [Function `vec_map_from_keys_values`](#(iota_identity=0x0)_utils_vec_map_from_keys_values)


<pre><code><b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="(iota_identity=0x0)_utils_vec_map_from_keys_values"></a>

## Function `vec_map_from_keys_values`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/utils.md#(iota_identity=0x0)_utils_vec_map_from_keys_values">vec_map_from_keys_values</a>&lt;K: <b>copy</b>, store, V: store&gt;(keys: vector&lt;K&gt;, values: vector&lt;V&gt;): <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;K, V&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/utils.md#(iota_identity=0x0)_utils_vec_map_from_keys_values">vec_map_from_keys_values</a>&lt;K: store + <b>copy</b>, V: store&gt;(
    keys: vector&lt;K&gt;,
    values: vector&lt;V&gt;,
): VecMap&lt;K, V&gt; {
    vec_map::from_keys_values(keys, values)
}
</code></pre>



</details>
