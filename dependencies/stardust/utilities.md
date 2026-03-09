
<a name="stardust_utilities"></a>

# Module `stardust::utilities`



-  [Constants](#@Constants_0)
-  [Function `extract_and_send_to`](#stardust_utilities_extract_and_send_to)
-  [Function `extract`](#stardust_utilities_extract)
-  [Function `extract_`](#stardust_utilities_extract_)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../../dependencies/iota/coin.md#iota_coin">iota::coin</a>;
<b>use</b> <a href="../../dependencies/iota/config.md#iota_config">iota::config</a>;
<b>use</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list">iota::deny_list</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="@Constants_0"></a>

## Constants


<a name="stardust_utilities_EZeroNativeTokenBalance"></a>

Returned when trying to extract a <code>Balance&lt;T&gt;</code> from a <code>Bag</code> and the balance is zero.


<pre><code><b>const</b> <a href="../../dependencies/stardust/utilities.md#stardust_utilities_EZeroNativeTokenBalance">EZeroNativeTokenBalance</a>: u64 = 0;
</code></pre>



<a name="stardust_utilities_extract_and_send_to"></a>

## Function `extract_and_send_to`

Extract a <code>Balance&lt;T&gt;</code> from a <code>Bag</code>, create a <code>Coin</code> out of it and send it to the address.
NOTE: We return the <code>Bag</code> by value so the function can be called repeatedly in a PTB.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/utilities.md#stardust_utilities_extract_and_send_to">extract_and_send_to</a>&lt;T&gt;(bag: <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a>, to: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/utilities.md#stardust_utilities_extract_and_send_to">extract_and_send_to</a>&lt;T&gt;(<b>mut</b> bag: Bag, to: <b>address</b>, ctx: &<b>mut</b> TxContext): Bag {
    <b>let</b> coin = coin::from_balance(<a href="../../dependencies/stardust/utilities.md#stardust_utilities_extract_">extract_</a>&lt;T&gt;(&<b>mut</b> bag), ctx);
    transfer::public_transfer(coin, to);
    bag
}
</code></pre>



</details>

<a name="stardust_utilities_extract"></a>

## Function `extract`

Extract a <code>Balance&lt;T&gt;</code> from a <code>Bag</code> and return it. Caller can decide what to do with it.
NOTE: We return the <code>Bag</code> by value so the function can be called repeatedly in a PTB.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/utilities.md#stardust_utilities_extract">extract</a>&lt;T&gt;(bag: <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a>): (<a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a>, <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/utilities.md#stardust_utilities_extract">extract</a>&lt;T&gt;(<b>mut</b> bag: Bag): (Bag, Balance&lt;T&gt;) {
    <b>let</b> balance = <a href="../../dependencies/stardust/utilities.md#stardust_utilities_extract_">extract_</a>&lt;T&gt;(&<b>mut</b> bag);
    (bag, balance)
}
</code></pre>



</details>

<a name="stardust_utilities_extract_"></a>

## Function `extract_`

Get a <code>Balance&lt;T&gt;</code> from a <code>Bag</code>.
Aborts if the balance is zero or if there is no balance for the type <code>T</code>.


<pre><code><b>fun</b> <a href="../../dependencies/stardust/utilities.md#stardust_utilities_extract_">extract_</a>&lt;T&gt;(bag: &<b>mut</b> <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a>): <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/stardust/utilities.md#stardust_utilities_extract_">extract_</a>&lt;T&gt;(bag: &<b>mut</b> Bag): Balance&lt;T&gt; {
    <b>let</b> key = type_name::get&lt;T&gt;().into_string();
    // This call aborts <b>if</b> the key doesn't exist.
    <b>let</b> balance: Balance&lt;T&gt; = bag.remove(key);
    <b>assert</b>!(balance.value() != 0, <a href="../../dependencies/stardust/utilities.md#stardust_utilities_EZeroNativeTokenBalance">EZeroNativeTokenBalance</a>);
    balance
}
</code></pre>



</details>
