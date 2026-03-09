
<a name="iota_auth_context"></a>

# Module `iota::auth_context`



-  [Struct `AuthContext`](#iota_auth_context_AuthContext)
-  [Function `digest`](#iota_auth_context_digest)
-  [Function `tx_inputs`](#iota_auth_context_tx_inputs)
-  [Function `tx_commands`](#iota_auth_context_tx_commands)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg">iota::ptb_call_arg</a>;
<b>use</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command">iota::ptb_command</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_auth_context_AuthContext"></a>

## Struct `AuthContext`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/auth_context.md#iota_auth_context_AuthContext">AuthContext</a> <b>has</b> drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>auth_digest: vector&lt;u8&gt;</code>
</dt>
<dd>
 The digest of the MoveAuthenticator
</dd>
<dt>
<code><a href="../../dependencies/iota/auth_context.md#iota_auth_context_tx_inputs">tx_inputs</a>: vector&lt;<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">iota::ptb_call_arg::CallArg</a>&gt;</code>
</dt>
<dd>
 The transaction input objects or primitive values
</dd>
<dt>
<code><a href="../../dependencies/iota/auth_context.md#iota_auth_context_tx_commands">tx_commands</a>: vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>&gt;</code>
</dt>
<dd>
 The transaction commands to be executed sequentially.
</dd>
</dl>


</details>

<a name="iota_auth_context_digest"></a>

## Function `digest`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/auth_context.md#iota_auth_context_digest">digest</a>(ctx: &<a href="../../dependencies/iota/auth_context.md#iota_auth_context_AuthContext">iota::auth_context::AuthContext</a>): &vector&lt;u8&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/auth_context.md#iota_auth_context_digest">digest</a>(ctx: &<a href="../../dependencies/iota/auth_context.md#iota_auth_context_AuthContext">AuthContext</a>): &vector&lt;u8&gt; {
    &ctx.auth_digest
}
</code></pre>



</details>

<a name="iota_auth_context_tx_inputs"></a>

## Function `tx_inputs`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/auth_context.md#iota_auth_context_tx_inputs">tx_inputs</a>(ctx: &<a href="../../dependencies/iota/auth_context.md#iota_auth_context_AuthContext">iota::auth_context::AuthContext</a>): &vector&lt;<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">iota::ptb_call_arg::CallArg</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/auth_context.md#iota_auth_context_tx_inputs">tx_inputs</a>(ctx: &<a href="../../dependencies/iota/auth_context.md#iota_auth_context_AuthContext">AuthContext</a>): &vector&lt;CallArg&gt; {
    &ctx.<a href="../../dependencies/iota/auth_context.md#iota_auth_context_tx_inputs">tx_inputs</a>
}
</code></pre>



</details>

<a name="iota_auth_context_tx_commands"></a>

## Function `tx_commands`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/auth_context.md#iota_auth_context_tx_commands">tx_commands</a>(ctx: &<a href="../../dependencies/iota/auth_context.md#iota_auth_context_AuthContext">iota::auth_context::AuthContext</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/auth_context.md#iota_auth_context_tx_commands">tx_commands</a>(ctx: &<a href="../../dependencies/iota/auth_context.md#iota_auth_context_AuthContext">AuthContext</a>): &vector&lt;Command&gt; {
    &ctx.<a href="../../dependencies/iota/auth_context.md#iota_auth_context_tx_commands">tx_commands</a>
}
</code></pre>



</details>
