
<a name="iota_deny_list"></a>

# Module `iota::deny_list`

Defines the <code><a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a></code> type. The <code><a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a></code> shared object is used to restrict access to
instances of certain core types from being used as inputs by specified addresses in the deny
list.


-  [Struct `DenyList`](#iota_deny_list_DenyList)
-  [Struct `ConfigWriteCap`](#iota_deny_list_ConfigWriteCap)
-  [Struct `ConfigKey`](#iota_deny_list_ConfigKey)
-  [Struct `AddressKey`](#iota_deny_list_AddressKey)
-  [Struct `GlobalPauseKey`](#iota_deny_list_GlobalPauseKey)
-  [Struct `PerTypeConfigCreated`](#iota_deny_list_PerTypeConfigCreated)
-  [Constants](#@Constants_0)
-  [Function `add`](#iota_deny_list_add)
-  [Function `remove`](#iota_deny_list_remove)
-  [Function `contains_current_epoch`](#iota_deny_list_contains_current_epoch)
-  [Function `contains_next_epoch`](#iota_deny_list_contains_next_epoch)
-  [Function `enable_global_pause`](#iota_deny_list_enable_global_pause)
-  [Function `disable_global_pause`](#iota_deny_list_disable_global_pause)
-  [Function `is_global_pause_enabled_current_epoch`](#iota_deny_list_is_global_pause_enabled_current_epoch)
-  [Function `is_global_pause_enabled_next_epoch`](#iota_deny_list_is_global_pause_enabled_next_epoch)
-  [Function `add_per_type_config`](#iota_deny_list_add_per_type_config)
-  [Function `borrow_per_type_config_mut`](#iota_deny_list_borrow_per_type_config_mut)
-  [Function `borrow_per_type_config`](#iota_deny_list_borrow_per_type_config)
-  [Function `per_type_exists`](#iota_deny_list_per_type_exists)
-  [Macro function `per_type_config_entry`](#iota_deny_list_per_type_config_entry)
-  [Function `create`](#iota_deny_list_create)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../../dependencies/iota/config.md#iota_config">iota::config</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_deny_list_DenyList"></a>

## Struct `DenyList`

A shared object that stores the addresses that are blocked for a given core type.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a> <b>has</b> key
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>lists: <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a></code>
</dt>
<dd>
 The individual deny lists.
</dd>
</dl>


</details>

<a name="iota_deny_list_ConfigWriteCap"></a>

## Struct `ConfigWriteCap`

The capability used to write to the deny list config. Ensures that the Configs for the
DenyList are modified only by this module.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">ConfigWriteCap</a> <b>has</b> drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="iota_deny_list_ConfigKey"></a>

## Struct `ConfigKey`

The dynamic object field key used to store the <code>Config</code> for a given type, essentially a
<code>(per_type_index, per_type_key)</code> pair.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigKey">ConfigKey</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>per_type_index: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>per_type_key: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_deny_list_AddressKey"></a>

## Struct `AddressKey`

The setting key used to store the deny list for a given address in the <code>Config</code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_AddressKey">AddressKey</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>0: <b>address</b></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_deny_list_GlobalPauseKey"></a>

## Struct `GlobalPauseKey`

The setting key used to store the global pause setting in the <code>Config</code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_GlobalPauseKey">GlobalPauseKey</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="iota_deny_list_PerTypeConfigCreated"></a>

## Struct `PerTypeConfigCreated`

The event emitted when a new <code>Config</code> is created for a given type. This can be useful for
tracking the <code>ID</code> of a type's <code>Config</code> object.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_PerTypeConfigCreated">PerTypeConfigCreated</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>key: <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigKey">iota::deny_list::ConfigKey</a></code>
</dt>
<dd>
</dd>
<dt>
<code>config_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_deny_list_ENotSystemAddress"></a>

Trying to create a deny list object when not called by the system address.


<pre><code><b>const</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ENotSystemAddress">ENotSystemAddress</a>: u64 = 0;
</code></pre>



<a name="iota_deny_list_add"></a>

## Function `add`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_add">add</a>(deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;, addr: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_add">add</a>(
    deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    per_type_index: u64,
    per_type_key: vector&lt;u8&gt;,
    addr: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> per_type_config = deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_config_entry">per_type_config_entry</a>!(per_type_index, per_type_key, ctx);
    <b>let</b> setting_name = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_AddressKey">AddressKey</a>(addr);
    <b>let</b> next_epoch_entry = per_type_config.<b>entry</b>!&lt;_, <a href="../../dependencies/iota/deny_list.md#iota_deny_list_AddressKey">AddressKey</a>, bool&gt;(
        &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">ConfigWriteCap</a>(),
        setting_name,
        |_deny_list, _cap, _ctx| <b>true</b>,
        ctx,
    );
    *next_epoch_entry = <b>true</b>;
}
</code></pre>



</details>

<a name="iota_deny_list_remove"></a>

## Function `remove`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_remove">remove</a>(deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;, addr: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_remove">remove</a>(
    deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    per_type_index: u64,
    per_type_key: vector&lt;u8&gt;,
    addr: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> per_type_config = deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_config_entry">per_type_config_entry</a>!(per_type_index, per_type_key, ctx);
    <b>let</b> setting_name = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_AddressKey">AddressKey</a>(addr);
    per_type_config.remove_for_next_epoch&lt;_, <a href="../../dependencies/iota/deny_list.md#iota_deny_list_AddressKey">AddressKey</a>, bool&gt;(
        &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">ConfigWriteCap</a>(),
        setting_name,
        ctx,
    );
}
</code></pre>



</details>

<a name="iota_deny_list_contains_current_epoch"></a>

## Function `contains_current_epoch`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_contains_current_epoch">contains_current_epoch</a>(deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;, addr: <b>address</b>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_contains_current_epoch">contains_current_epoch</a>(
    deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    per_type_index: u64,
    per_type_key: vector&lt;u8&gt;,
    addr: <b>address</b>,
    ctx: &TxContext,
): bool {
    <b>if</b> (!deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_exists">per_type_exists</a>(per_type_index, per_type_key)) <b>return</b> <b>false</b>;
    <b>let</b> per_type_config = deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_borrow_per_type_config">borrow_per_type_config</a>(per_type_index, per_type_key);
    <b>let</b> setting_name = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_AddressKey">AddressKey</a>(addr);
    config::read_setting(object::id(per_type_config), setting_name, ctx).destroy_or!(<b>false</b>)
}
</code></pre>



</details>

<a name="iota_deny_list_contains_next_epoch"></a>

## Function `contains_next_epoch`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_contains_next_epoch">contains_next_epoch</a>(deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;, addr: <b>address</b>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_contains_next_epoch">contains_next_epoch</a>(
    deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    per_type_index: u64,
    per_type_key: vector&lt;u8&gt;,
    addr: <b>address</b>,
): bool {
    <b>if</b> (!deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_exists">per_type_exists</a>(per_type_index, per_type_key)) <b>return</b> <b>false</b>;
    <b>let</b> per_type_config = deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_borrow_per_type_config">borrow_per_type_config</a>(per_type_index, per_type_key);
    <b>let</b> setting_name = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_AddressKey">AddressKey</a>(addr);
    per_type_config.read_setting_for_next_epoch(setting_name).destroy_or!(<b>false</b>)
}
</code></pre>



</details>

<a name="iota_deny_list_enable_global_pause"></a>

## Function `enable_global_pause`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_enable_global_pause">enable_global_pause</a>(deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_enable_global_pause">enable_global_pause</a>(
    deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    per_type_index: u64,
    per_type_key: vector&lt;u8&gt;,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> per_type_config = deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_config_entry">per_type_config_entry</a>!(per_type_index, per_type_key, ctx);
    <b>let</b> setting_name = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_GlobalPauseKey">GlobalPauseKey</a>();
    <b>let</b> next_epoch_entry = per_type_config.<b>entry</b>!&lt;_, <a href="../../dependencies/iota/deny_list.md#iota_deny_list_GlobalPauseKey">GlobalPauseKey</a>, bool&gt;(
        &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">ConfigWriteCap</a>(),
        setting_name,
        |_deny_list, _cap, _ctx| <b>true</b>,
        ctx,
    );
    *next_epoch_entry = <b>true</b>;
}
</code></pre>



</details>

<a name="iota_deny_list_disable_global_pause"></a>

## Function `disable_global_pause`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_disable_global_pause">disable_global_pause</a>(deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_disable_global_pause">disable_global_pause</a>(
    deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    per_type_index: u64,
    per_type_key: vector&lt;u8&gt;,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> per_type_config = deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_config_entry">per_type_config_entry</a>!(per_type_index, per_type_key, ctx);
    <b>let</b> setting_name = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_GlobalPauseKey">GlobalPauseKey</a>();
    per_type_config.remove_for_next_epoch&lt;_, <a href="../../dependencies/iota/deny_list.md#iota_deny_list_GlobalPauseKey">GlobalPauseKey</a>, bool&gt;(
        &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">ConfigWriteCap</a>(),
        setting_name,
        ctx,
    );
}
</code></pre>



</details>

<a name="iota_deny_list_is_global_pause_enabled_current_epoch"></a>

## Function `is_global_pause_enabled_current_epoch`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_is_global_pause_enabled_current_epoch">is_global_pause_enabled_current_epoch</a>(deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_is_global_pause_enabled_current_epoch">is_global_pause_enabled_current_epoch</a>(
    deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    per_type_index: u64,
    per_type_key: vector&lt;u8&gt;,
    ctx: &TxContext,
): bool {
    <b>if</b> (!deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_exists">per_type_exists</a>(per_type_index, per_type_key)) <b>return</b> <b>false</b>;
    <b>let</b> per_type_config = deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_borrow_per_type_config">borrow_per_type_config</a>(per_type_index, per_type_key);
    <b>let</b> setting_name = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_GlobalPauseKey">GlobalPauseKey</a>();
    config::read_setting(object::id(per_type_config), setting_name, ctx).destroy_or!(<b>false</b>)
}
</code></pre>



</details>

<a name="iota_deny_list_is_global_pause_enabled_next_epoch"></a>

## Function `is_global_pause_enabled_next_epoch`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_is_global_pause_enabled_next_epoch">is_global_pause_enabled_next_epoch</a>(deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_is_global_pause_enabled_next_epoch">is_global_pause_enabled_next_epoch</a>(
    deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    per_type_index: u64,
    per_type_key: vector&lt;u8&gt;,
): bool {
    <b>if</b> (!deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_exists">per_type_exists</a>(per_type_index, per_type_key)) <b>return</b> <b>false</b>;
    <b>let</b> per_type_config = deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_borrow_per_type_config">borrow_per_type_config</a>(per_type_index, per_type_key);
    <b>let</b> setting_name = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_GlobalPauseKey">GlobalPauseKey</a>();
    per_type_config.read_setting_for_next_epoch(setting_name).destroy_or!(<b>false</b>)
}
</code></pre>



</details>

<a name="iota_deny_list_add_per_type_config"></a>

## Function `add_per_type_config`



<pre><code><b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_add_per_type_config">add_per_type_config</a>(deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_add_per_type_config">add_per_type_config</a>(
    deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    per_type_index: u64,
    per_type_key: vector&lt;u8&gt;,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> key = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigKey">ConfigKey</a> { per_type_index, per_type_key };
    <b>let</b> config = config::new(&<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">ConfigWriteCap</a>(), ctx);
    <b>let</b> config_id = object::id(&config);
    ofield::internal_add(&<b>mut</b> deny_list.id, key, config);
    <a href="../../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../../dependencies/iota/deny_list.md#iota_deny_list_PerTypeConfigCreated">PerTypeConfigCreated</a> { key, config_id });
}
</code></pre>



</details>

<a name="iota_deny_list_borrow_per_type_config_mut"></a>

## Function `borrow_per_type_config_mut`



<pre><code><b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_borrow_per_type_config_mut">borrow_per_type_config_mut</a>(deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;): &<b>mut</b> <a href="../../dependencies/iota/config.md#iota_config_Config">iota::config::Config</a>&lt;<a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">iota::deny_list::ConfigWriteCap</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_borrow_per_type_config_mut">borrow_per_type_config_mut</a>(
    deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    per_type_index: u64,
    per_type_key: vector&lt;u8&gt;,
): &<b>mut</b> Config&lt;<a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">ConfigWriteCap</a>&gt; {
    <b>let</b> key = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigKey">ConfigKey</a> { per_type_index, per_type_key };
    ofield::internal_borrow_mut(&<b>mut</b> deny_list.id, key)
}
</code></pre>



</details>

<a name="iota_deny_list_borrow_per_type_config"></a>

## Function `borrow_per_type_config`



<pre><code><b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_borrow_per_type_config">borrow_per_type_config</a>(deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;): &<a href="../../dependencies/iota/config.md#iota_config_Config">iota::config::Config</a>&lt;<a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">iota::deny_list::ConfigWriteCap</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_borrow_per_type_config">borrow_per_type_config</a>(
    deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    per_type_index: u64,
    per_type_key: vector&lt;u8&gt;,
): &Config&lt;<a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">ConfigWriteCap</a>&gt; {
    <b>let</b> key = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigKey">ConfigKey</a> { per_type_index, per_type_key };
    ofield::internal_borrow(&deny_list.id, key)
}
</code></pre>



</details>

<a name="iota_deny_list_per_type_exists"></a>

## Function `per_type_exists`



<pre><code><b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_exists">per_type_exists</a>(deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_exists">per_type_exists</a>(deny_list: &<a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>, per_type_index: u64, per_type_key: vector&lt;u8&gt;): bool {
    <b>let</b> key = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigKey">ConfigKey</a> { per_type_index, per_type_key };
    ofield::exists_(&deny_list.id, key)
}
</code></pre>



</details>

<a name="iota_deny_list_per_type_config_entry"></a>

## Macro function `per_type_config_entry`



<pre><code><b>macro</b> <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_config_entry">per_type_config_entry</a>($deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">iota::deny_list::DenyList</a>, $per_type_index: u64, $per_type_key: vector&lt;u8&gt;, $ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): &<b>mut</b> <a href="../../dependencies/iota/config.md#iota_config_Config">iota::config::Config</a>&lt;<a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">iota::deny_list::ConfigWriteCap</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>macro</b> <b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_config_entry">per_type_config_entry</a>(
    $deny_list: &<b>mut</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a>,
    $per_type_index: u64,
    $per_type_key: vector&lt;u8&gt;,
    $ctx: &<b>mut</b> TxContext,
): &<b>mut</b> Config&lt;<a href="../../dependencies/iota/deny_list.md#iota_deny_list_ConfigWriteCap">ConfigWriteCap</a>&gt; {
    <b>let</b> deny_list = $deny_list;
    <b>let</b> per_type_index = $per_type_index;
    <b>let</b> per_type_key = $per_type_key;
    <b>let</b> ctx = $ctx;
    <b>if</b> (!deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_per_type_exists">per_type_exists</a>(per_type_index, per_type_key)) {
        deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_add_per_type_config">add_per_type_config</a>(per_type_index, per_type_key, ctx);
    };
    deny_list.<a href="../../dependencies/iota/deny_list.md#iota_deny_list_borrow_per_type_config_mut">borrow_per_type_config_mut</a>(per_type_index, per_type_key)
}
</code></pre>



</details>

<a name="iota_deny_list_create"></a>

## Function `create`

Creation of the deny list object is restricted to the system address
via a system transaction.


<pre><code><b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_create">create</a>(ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list_create">create</a>(ctx: &<b>mut</b> TxContext) {
    <b>assert</b>!(ctx.sender() == @0x0, <a href="../../dependencies/iota/deny_list.md#iota_deny_list_ENotSystemAddress">ENotSystemAddress</a>);
    <b>let</b> deny_list_object = <a href="../../dependencies/iota/deny_list.md#iota_deny_list_DenyList">DenyList</a> {
        id: object::iota_deny_list_object_id(),
        lists: bag::new(ctx),
    };
    transfer::share_object(deny_list_object);
}
</code></pre>



</details>
