---
layout: default
title: display_utils
parent: Nplex Smart Contracts
---


<a name="(nplex=0x0)_display_utils"></a>

# Module `(nplex=0x0)::display_utils`

NPLEX Display Utils

This contract provides the logic for the display utils.


-  [Macro function `setup_display`](#(nplex=0x0)_display_utils_setup_display)


<pre><code></code></pre>



<a name="(nplex=0x0)_display_utils_setup_display"></a>

## Macro function `setup_display`

Generic macro to setup display for any type T
Takes keys and values as arguments.
Architecture definition: package-private macro <code><a href="../nplex/display_utils.md#(nplex=0x0)_display_utils_setup_display">setup_display</a>&lt;T&gt;(Publisher, keys, values, ctx)</code>
-> creates Display, calls update_version, share_object.


<pre><code><b>public</b>(package) <b>macro</b> <b>fun</b> <a href="../nplex/display_utils.md#(nplex=0x0)_display_utils_setup_display">setup_display</a>&lt;$T&gt;($publisher: &<a href="../dependencies/iota/package.md#iota_package_Publisher">iota::package::Publisher</a>, $keys: vector&lt;<a href="../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, $values: vector&lt;<a href="../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, $ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>macro</b> <b>fun</b> <a href="../nplex/display_utils.md#(nplex=0x0)_display_utils_setup_display">setup_display</a>&lt;$T&gt;(
    $publisher: &package::Publisher,
    $keys: vector&lt;String&gt;,
    $values: vector&lt;String&gt;,
    $ctx: &<b>mut</b> TxContext
) {
    <b>let</b> <b>mut</b> display = display::new_with_fields&lt;$T&gt;(
        $publisher, $keys, $values, $ctx
    );
    display::update_version(&<b>mut</b> display);
    <a href="../dependencies/iota/transfer.md#iota_transfer_public_share_object">iota::transfer::public_share_object</a>(display);
}
</code></pre>



</details>
