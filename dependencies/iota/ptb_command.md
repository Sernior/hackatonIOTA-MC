
<a name="iota_ptb_command"></a>

# Module `iota::ptb_command`



-  [Struct `ProgrammableMoveCall`](#iota_ptb_command_ProgrammableMoveCall)
-  [Struct `TransferObjectsData`](#iota_ptb_command_TransferObjectsData)
-  [Struct `SplitCoinsData`](#iota_ptb_command_SplitCoinsData)
-  [Struct `MergeCoinsData`](#iota_ptb_command_MergeCoinsData)
-  [Struct `PublishData`](#iota_ptb_command_PublishData)
-  [Struct `MakeMoveVecData`](#iota_ptb_command_MakeMoveVecData)
-  [Struct `UpgradeData`](#iota_ptb_command_UpgradeData)
-  [Enum `Command`](#iota_ptb_command_Command)
-  [Enum `Argument`](#iota_ptb_command_Argument)
-  [Function `is_move_call`](#iota_ptb_command_is_move_call)
-  [Function `is_transfer_objects`](#iota_ptb_command_is_transfer_objects)
-  [Function `is_split_coins`](#iota_ptb_command_is_split_coins)
-  [Function `is_merge_coins`](#iota_ptb_command_is_merge_coins)
-  [Function `is_publish`](#iota_ptb_command_is_publish)
-  [Function `is_make_move_vec`](#iota_ptb_command_is_make_move_vec)
-  [Function `is_upgrade`](#iota_ptb_command_is_upgrade)
-  [Function `as_move_call`](#iota_ptb_command_as_move_call)
-  [Function `as_transfer_objects`](#iota_ptb_command_as_transfer_objects)
-  [Function `as_split_coins`](#iota_ptb_command_as_split_coins)
-  [Function `as_merge_coins`](#iota_ptb_command_as_merge_coins)
-  [Function `as_publish`](#iota_ptb_command_as_publish)
-  [Function `as_make_move_vec`](#iota_ptb_command_as_make_move_vec)
-  [Function `as_upgrade`](#iota_ptb_command_as_upgrade)
-  [Function `is_gas_coin`](#iota_ptb_command_is_gas_coin)
-  [Function `is_input`](#iota_ptb_command_is_input)
-  [Function `is_result`](#iota_ptb_command_is_result)
-  [Function `is_nested_result`](#iota_ptb_command_is_nested_result)
-  [Function `input_index`](#iota_ptb_command_input_index)
-  [Function `result_command_index`](#iota_ptb_command_result_command_index)
-  [Function `nested_result_command_index`](#iota_ptb_command_nested_result_command_index)
-  [Function `nested_result_inner_index`](#iota_ptb_command_nested_result_inner_index)
-  [Function `package`](#iota_ptb_command_package)
-  [Function `module_name`](#iota_ptb_command_module_name)
-  [Function `function`](#iota_ptb_command_function)
-  [Function `type_arguments`](#iota_ptb_command_type_arguments)
-  [Function `arguments`](#iota_ptb_command_arguments)
-  [Function `objects`](#iota_ptb_command_objects)
-  [Function `recipient`](#iota_ptb_command_recipient)
-  [Function `coin`](#iota_ptb_command_coin)
-  [Function `amounts`](#iota_ptb_command_amounts)
-  [Function `target_coin`](#iota_ptb_command_target_coin)
-  [Function `source_coins`](#iota_ptb_command_source_coins)
-  [Function `modules`](#iota_ptb_command_modules)
-  [Function `dependencies`](#iota_ptb_command_dependencies)
-  [Function `type_arg`](#iota_ptb_command_type_arg)
-  [Function `elements`](#iota_ptb_command_elements)
-  [Function `upgrade_modules`](#iota_ptb_command_upgrade_modules)
-  [Function `upgrade_dependencies`](#iota_ptb_command_upgrade_dependencies)
-  [Function `upgrade_package`](#iota_ptb_command_upgrade_package)
-  [Function `upgrade_ticket`](#iota_ptb_command_upgrade_ticket)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_ptb_command_ProgrammableMoveCall"></a>

## Struct `ProgrammableMoveCall`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">ProgrammableMoveCall</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_package">package</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_module_name">module_name</a>: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_function">function</a>: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_type_arguments">type_arguments</a>: vector&lt;<a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_arguments">arguments</a>: vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_ptb_command_TransferObjectsData"></a>

## Struct `TransferObjectsData`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_TransferObjectsData">TransferObjectsData</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_objects">objects</a>: vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_recipient">recipient</a>: <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_ptb_command_SplitCoinsData"></a>

## Struct `SplitCoinsData`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_SplitCoinsData">SplitCoinsData</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_coin">coin</a>: <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_amounts">amounts</a>: vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_ptb_command_MergeCoinsData"></a>

## Struct `MergeCoinsData`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MergeCoinsData">MergeCoinsData</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_target_coin">target_coin</a>: <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_source_coins">source_coins</a>: vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_ptb_command_PublishData"></a>

## Struct `PublishData`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_PublishData">PublishData</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_modules">modules</a>: vector&lt;vector&lt;u8&gt;&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_dependencies">dependencies</a>: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_ptb_command_MakeMoveVecData"></a>

## Struct `MakeMoveVecData`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MakeMoveVecData">MakeMoveVecData</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_type_arg">type_arg</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_elements">elements</a>: vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_ptb_command_UpgradeData"></a>

## Struct `UpgradeData`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">UpgradeData</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_modules">modules</a>: vector&lt;vector&lt;u8&gt;&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_dependencies">dependencies</a>: vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_package">package</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_upgrade_ticket">upgrade_ticket</a>: <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_ptb_command_Command"></a>

## Enum `Command`



<pre><code><b>public</b> <b>enum</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Variants</summary>


<dl>
<dt>
Variant <code>MoveCall</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">iota::ptb_command::ProgrammableMoveCall</a></code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>TransferObjects</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_TransferObjectsData">iota::ptb_command::TransferObjectsData</a></code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>SplitCoins</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_SplitCoinsData">iota::ptb_command::SplitCoinsData</a></code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>MergeCoins</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MergeCoinsData">iota::ptb_command::MergeCoinsData</a></code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>Publish</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_PublishData">iota::ptb_command::PublishData</a></code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>MakeMoveVec</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MakeMoveVecData">iota::ptb_command::MakeMoveVecData</a></code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>Upgrade</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">iota::ptb_command::UpgradeData</a></code>
</dt>
<dd>
</dd>
</dl>

</dl>


</details>

<a name="iota_ptb_command_Argument"></a>

## Enum `Argument`



<pre><code><b>public</b> <b>enum</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Variants</summary>


<dl>
<dt>
Variant <code>GasCoin</code>
</dt>
<dd>
</dd>
<dt>
Variant <code>Input</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: u16</code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>Result</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: u16</code>
</dt>
<dd>
</dd>
</dl>

<dt>
Variant <code>NestedResult</code>
</dt>
<dd>
</dd>

<dl>
<dt>
<code>0: u16</code>
</dt>
<dd>
</dd>
</dl>


<dl>
<dt>
<code>1: u16</code>
</dt>
<dd>
</dd>
</dl>

</dl>


</details>

<a name="iota_ptb_command_is_move_call"></a>

## Function `is_move_call`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_move_call">is_move_call</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_move_call">is_move_call</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): bool {
    match (command) {
        Command::MoveCall(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_is_transfer_objects"></a>

## Function `is_transfer_objects`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_transfer_objects">is_transfer_objects</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_transfer_objects">is_transfer_objects</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): bool {
    match (command) {
        Command::TransferObjects(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_is_split_coins"></a>

## Function `is_split_coins`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_split_coins">is_split_coins</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_split_coins">is_split_coins</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): bool {
    match (command) {
        Command::SplitCoins(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_is_merge_coins"></a>

## Function `is_merge_coins`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_merge_coins">is_merge_coins</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_merge_coins">is_merge_coins</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): bool {
    match (command) {
        Command::MergeCoins(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_is_publish"></a>

## Function `is_publish`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_publish">is_publish</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_publish">is_publish</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): bool {
    match (command) {
        Command::Publish(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_is_make_move_vec"></a>

## Function `is_make_move_vec`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_make_move_vec">is_make_move_vec</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_make_move_vec">is_make_move_vec</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): bool {
    match (command) {
        Command::MakeMoveVec(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_is_upgrade"></a>

## Function `is_upgrade`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_upgrade">is_upgrade</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_upgrade">is_upgrade</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): bool {
    match (command) {
        Command::Upgrade(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_as_move_call"></a>

## Function `as_move_call`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_move_call">as_move_call</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">iota::ptb_command::ProgrammableMoveCall</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_move_call">as_move_call</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): Option&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">ProgrammableMoveCall</a>&gt; {
    match (command) {
        Command::MoveCall(call) =&gt; some(*call),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_as_transfer_objects"></a>

## Function `as_transfer_objects`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_transfer_objects">as_transfer_objects</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_TransferObjectsData">iota::ptb_command::TransferObjectsData</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_transfer_objects">as_transfer_objects</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): Option&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_TransferObjectsData">TransferObjectsData</a>&gt; {
    match (command) {
        Command::TransferObjects(data) =&gt; some(*data),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_as_split_coins"></a>

## Function `as_split_coins`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_split_coins">as_split_coins</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_SplitCoinsData">iota::ptb_command::SplitCoinsData</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_split_coins">as_split_coins</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): Option&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_SplitCoinsData">SplitCoinsData</a>&gt; {
    match (command) {
        Command::SplitCoins(data) =&gt; some(*data),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_as_merge_coins"></a>

## Function `as_merge_coins`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_merge_coins">as_merge_coins</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MergeCoinsData">iota::ptb_command::MergeCoinsData</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_merge_coins">as_merge_coins</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): Option&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MergeCoinsData">MergeCoinsData</a>&gt; {
    match (command) {
        Command::MergeCoins(data) =&gt; some(*data),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_as_publish"></a>

## Function `as_publish`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_publish">as_publish</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_PublishData">iota::ptb_command::PublishData</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_publish">as_publish</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): Option&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_PublishData">PublishData</a>&gt; {
    match (command) {
        Command::Publish(data) =&gt; some(*data),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_as_make_move_vec"></a>

## Function `as_make_move_vec`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_make_move_vec">as_make_move_vec</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MakeMoveVecData">iota::ptb_command::MakeMoveVecData</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_make_move_vec">as_make_move_vec</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): Option&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MakeMoveVecData">MakeMoveVecData</a>&gt; {
    match (command) {
        Command::MakeMoveVec(data) =&gt; some(*data),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_as_upgrade"></a>

## Function `as_upgrade`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_upgrade">as_upgrade</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">iota::ptb_command::Command</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">iota::ptb_command::UpgradeData</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_as_upgrade">as_upgrade</a>(command: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Command">Command</a>): Option&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">UpgradeData</a>&gt; {
    match (command) {
        Command::Upgrade(data) =&gt; some(*data),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_is_gas_coin"></a>

## Function `is_gas_coin`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_gas_coin">is_gas_coin</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_gas_coin">is_gas_coin</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>): bool {
    match (arg) {
        Argument::GasCoin =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_is_input"></a>

## Function `is_input`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_input">is_input</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_input">is_input</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>): bool {
    match (arg) {
        Argument::Input(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_is_result"></a>

## Function `is_result`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_result">is_result</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_result">is_result</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>): bool {
    match (arg) {
        Argument::Result(_) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_is_nested_result"></a>

## Function `is_nested_result`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_nested_result">is_nested_result</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_is_nested_result">is_nested_result</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>): bool {
    match (arg) {
        Argument::NestedResult(_, _) =&gt; <b>true</b>,
        _ =&gt; <b>false</b>,
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_input_index"></a>

## Function `input_index`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_input_index">input_index</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u16&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_input_index">input_index</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>): Option&lt;u16&gt; {
    match (arg) {
        Argument::Input(index) =&gt; some(*index),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_result_command_index"></a>

## Function `result_command_index`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_result_command_index">result_command_index</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u16&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_result_command_index">result_command_index</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>): Option&lt;u16&gt; {
    match (arg) {
        Argument::Result(command_index) =&gt; some(*command_index),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_nested_result_command_index"></a>

## Function `nested_result_command_index`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_nested_result_command_index">nested_result_command_index</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u16&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_nested_result_command_index">nested_result_command_index</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>): Option&lt;u16&gt; {
    match (arg) {
        Argument::NestedResult(command_index, _) =&gt; some(*command_index),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_nested_result_inner_index"></a>

## Function `nested_result_inner_index`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_nested_result_inner_index">nested_result_inner_index</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u16&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_nested_result_inner_index">nested_result_inner_index</a>(arg: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>): Option&lt;u16&gt; {
    match (arg) {
        Argument::NestedResult(_, inner_index) =&gt; some(*inner_index),
        _ =&gt; none(),
    }
}
</code></pre>



</details>

<a name="iota_ptb_command_package"></a>

## Function `package`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_package">package</a>(call: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">iota::ptb_command::ProgrammableMoveCall</a>): &<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_package">package</a>(call: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">ProgrammableMoveCall</a>): &ID {
    &call.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_package">package</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_module_name"></a>

## Function `module_name`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_module_name">module_name</a>(call: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">iota::ptb_command::ProgrammableMoveCall</a>): &<a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_module_name">module_name</a>(call: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">ProgrammableMoveCall</a>): &String {
    &call.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_module_name">module_name</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_function"></a>

## Function `function`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_function">function</a>(call: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">iota::ptb_command::ProgrammableMoveCall</a>): &<a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_function">function</a>(call: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">ProgrammableMoveCall</a>): &String {
    &call.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_function">function</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_type_arguments"></a>

## Function `type_arguments`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_type_arguments">type_arguments</a>(call: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">iota::ptb_command::ProgrammableMoveCall</a>): &vector&lt;<a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_type_arguments">type_arguments</a>(call: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">ProgrammableMoveCall</a>): &vector&lt;TypeName&gt; {
    &call.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_type_arguments">type_arguments</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_arguments"></a>

## Function `arguments`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_arguments">arguments</a>(call: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">iota::ptb_command::ProgrammableMoveCall</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_arguments">arguments</a>(call: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_ProgrammableMoveCall">ProgrammableMoveCall</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>&gt; {
    &call.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_arguments">arguments</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_objects"></a>

## Function `objects`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_objects">objects</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_TransferObjectsData">iota::ptb_command::TransferObjectsData</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_objects">objects</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_TransferObjectsData">TransferObjectsData</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>&gt; {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_objects">objects</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_recipient"></a>

## Function `recipient`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_recipient">recipient</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_TransferObjectsData">iota::ptb_command::TransferObjectsData</a>): &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_recipient">recipient</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_TransferObjectsData">TransferObjectsData</a>): &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a> {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_recipient">recipient</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_coin"></a>

## Function `coin`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_coin">coin</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_SplitCoinsData">iota::ptb_command::SplitCoinsData</a>): &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_coin">coin</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_SplitCoinsData">SplitCoinsData</a>): &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a> {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_coin">coin</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_amounts"></a>

## Function `amounts`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_amounts">amounts</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_SplitCoinsData">iota::ptb_command::SplitCoinsData</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_amounts">amounts</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_SplitCoinsData">SplitCoinsData</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>&gt; {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_amounts">amounts</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_target_coin"></a>

## Function `target_coin`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_target_coin">target_coin</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MergeCoinsData">iota::ptb_command::MergeCoinsData</a>): &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_target_coin">target_coin</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MergeCoinsData">MergeCoinsData</a>): &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a> {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_target_coin">target_coin</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_source_coins"></a>

## Function `source_coins`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_source_coins">source_coins</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MergeCoinsData">iota::ptb_command::MergeCoinsData</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_source_coins">source_coins</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MergeCoinsData">MergeCoinsData</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>&gt; {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_source_coins">source_coins</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_modules"></a>

## Function `modules`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_modules">modules</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_PublishData">iota::ptb_command::PublishData</a>): &vector&lt;vector&lt;u8&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_modules">modules</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_PublishData">PublishData</a>): &vector&lt;vector&lt;u8&gt;&gt; {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_modules">modules</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_dependencies"></a>

## Function `dependencies`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_dependencies">dependencies</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_PublishData">iota::ptb_command::PublishData</a>): &vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_dependencies">dependencies</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_PublishData">PublishData</a>): &vector&lt;ID&gt; {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_dependencies">dependencies</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_type_arg"></a>

## Function `type_arg`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_type_arg">type_arg</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MakeMoveVecData">iota::ptb_command::MakeMoveVecData</a>): &<a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_type_arg">type_arg</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MakeMoveVecData">MakeMoveVecData</a>): &Option&lt;TypeName&gt; {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_type_arg">type_arg</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_elements"></a>

## Function `elements`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_elements">elements</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MakeMoveVecData">iota::ptb_command::MakeMoveVecData</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_elements">elements</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_MakeMoveVecData">MakeMoveVecData</a>): &vector&lt;<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a>&gt; {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_elements">elements</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_upgrade_modules"></a>

## Function `upgrade_modules`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_upgrade_modules">upgrade_modules</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">iota::ptb_command::UpgradeData</a>): &vector&lt;vector&lt;u8&gt;&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_upgrade_modules">upgrade_modules</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">UpgradeData</a>): &vector&lt;vector&lt;u8&gt;&gt; {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_modules">modules</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_upgrade_dependencies"></a>

## Function `upgrade_dependencies`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_upgrade_dependencies">upgrade_dependencies</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">iota::ptb_command::UpgradeData</a>): &vector&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_upgrade_dependencies">upgrade_dependencies</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">UpgradeData</a>): &vector&lt;ID&gt; {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_dependencies">dependencies</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_upgrade_package"></a>

## Function `upgrade_package`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_upgrade_package">upgrade_package</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">iota::ptb_command::UpgradeData</a>): &<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_upgrade_package">upgrade_package</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">UpgradeData</a>): &ID {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_package">package</a>
}
</code></pre>



</details>

<a name="iota_ptb_command_upgrade_ticket"></a>

## Function `upgrade_ticket`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_upgrade_ticket">upgrade_ticket</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">iota::ptb_command::UpgradeData</a>): &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">iota::ptb_command::Argument</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_upgrade_ticket">upgrade_ticket</a>(data: &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_UpgradeData">UpgradeData</a>): &<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_Argument">Argument</a> {
    &data.<a href="../../dependencies/iota/ptb_command.md#iota_ptb_command_upgrade_ticket">upgrade_ticket</a>
}
</code></pre>



</details>
