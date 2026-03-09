
<a name="iota_ptb"></a>

# Module `iota::ptb`



-  [Struct `ProgrammableTransaction`](#iota_ptb_ProgrammableTransaction)
-  [Function `inputs`](#iota_ptb_inputs)
-  [Function `commands`](#iota_ptb_commands)
-  [Function `new_programmable_transaction_for_testing`](#iota_ptb_new_programmable_transaction_for_testing)


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



<a name="iota_ptb_ProgrammableTransaction"></a>

## Struct `ProgrammableTransaction`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/ptb.md#iota_ptb_ProgrammableTransaction">ProgrammableTransaction</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/ptb.md#iota_ptb_inputs">inputs</a>: vector&lt;<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">iota::ptb_call_arg::CallArg</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb.md#iota_ptb_commands">commands</a>: vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_ptb_inputs"></a>

## Function `inputs`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb.md#iota_ptb_inputs">inputs</a>(tx: &<a href="../../dependencies/iota/ptb.md#iota_ptb_ProgrammableTransaction">iota::ptb::ProgrammableTransaction</a>): &vector&lt;<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">iota::ptb_call_arg::CallArg</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb.md#iota_ptb_inputs">inputs</a>(tx: &<a href="../../dependencies/iota/ptb.md#iota_ptb_ProgrammableTransaction">ProgrammableTransaction</a>): &vector&lt;CallArg&gt; {
    &tx.<a href="../../dependencies/iota/ptb.md#iota_ptb_inputs">inputs</a>
}
</code></pre>



</details>

<a name="iota_ptb_commands"></a>

## Function `commands`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb.md#iota_ptb_commands">commands</a>(tx: &<a href="../../dependencies/iota/ptb.md#iota_ptb_ProgrammableTransaction">iota::ptb::ProgrammableTransaction</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb.md#iota_ptb_commands">commands</a>(tx: &<a href="../../dependencies/iota/ptb.md#iota_ptb_ProgrammableTransaction">ProgrammableTransaction</a>): &vector&lt;Command&gt; {
    &tx.<a href="../../dependencies/iota/ptb.md#iota_ptb_commands">commands</a>
}
</code></pre>



</details>

<a name="iota_ptb_new_programmable_transaction_for_testing"></a>

## Function `new_programmable_transaction_for_testing`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/ptb.md#iota_ptb_new_programmable_transaction_for_testing">new_programmable_transaction_for_testing</a>(<a href="../../dependencies/iota/ptb.md#iota_ptb_inputs">inputs</a>: vector&lt;<a href="../../dependencies/iota/ptb_call_arg.md#iota_ptb_call_arg_CallArg">iota::ptb_call_arg::CallArg</a>&gt;, <a href="../../dependencies/iota/ptb.md#iota_ptb_commands">commands</a>: vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>&gt;): <a href="../../dependencies/iota/ptb.md#iota_ptb_ProgrammableTransaction">iota::ptb::ProgrammableTransaction</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/ptb.md#iota_ptb_new_programmable_transaction_for_testing">new_programmable_transaction_for_testing</a>(
    <a href="../../dependencies/iota/ptb.md#iota_ptb_inputs">inputs</a>: vector&lt;CallArg&gt;,
    <a href="../../dependencies/iota/ptb.md#iota_ptb_commands">commands</a>: vector&lt;Command&gt;,
): <a href="../../dependencies/iota/ptb.md#iota_ptb_ProgrammableTransaction">ProgrammableTransaction</a> {
    <a href="../../dependencies/iota/ptb.md#iota_ptb_ProgrammableTransaction">ProgrammableTransaction</a> { <a href="../../dependencies/iota/ptb.md#iota_ptb_inputs">inputs</a>, <a href="../../dependencies/iota/ptb.md#iota_ptb_commands">commands</a> }
}
</code></pre>



</details>
