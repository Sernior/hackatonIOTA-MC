
<a name="iota_iota"></a>

# Module `iota::iota`

Coin<IOTA> is the token used to pay for gas in IOTA.
It has 9 decimals, and the smallest unit (10^-9) is called "nano".


-  [Struct `IOTA`](#iota_iota_IOTA)
-  [Struct `IotaTreasuryCap`](#iota_iota_IotaTreasuryCap)
-  [Constants](#@Constants_0)
-  [Function `new`](#iota_iota_new)
-  [Function `transfer`](#iota_iota_transfer)
-  [Function `mint`](#iota_iota_mint)
-  [Function `mint_balance`](#iota_iota_mint_balance)
-  [Function `burn`](#iota_iota_burn)
-  [Function `burn_balance`](#iota_iota_burn_balance)
-  [Function `total_supply`](#iota_iota_total_supply)


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



<a name="iota_iota_IOTA"></a>

## Struct `IOTA`

Name of the coin


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/iota.md#iota_iota_IOTA">IOTA</a> <b>has</b> drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="iota_iota_IotaTreasuryCap"></a>

## Struct `IotaTreasuryCap`

The IOTA token treasury capability.
Protects the token from unauthorized changes.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">IotaTreasuryCap</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>inner: <a href="../../dependencies/iota/coin.md#iota_coin_TreasuryCap">iota::coin::TreasuryCap</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_iota_EAlreadyMinted"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota/iota.md#iota_iota_EAlreadyMinted">EAlreadyMinted</a>: u64 = 0;
</code></pre>



<a name="iota_iota_ENotSystemAddress"></a>

Sender is not @0x0 the system address.


<pre><code><b>const</b> <a href="../../dependencies/iota/iota.md#iota_iota_ENotSystemAddress">ENotSystemAddress</a>: u64 = 1;
</code></pre>



<a name="iota_iota_new"></a>

## Function `new`

Register the <code><a href="../../dependencies/iota/iota.md#iota_iota_IOTA">IOTA</a></code> Coin to acquire <code><a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">IotaTreasuryCap</a></code>.
This should be called only once during genesis creation.


<pre><code><b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_new">new</a>(ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_new">new</a>(ctx: &<b>mut</b> TxContext): <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">IotaTreasuryCap</a> {
    <b>assert</b>!(ctx.sender() == @0x0, <a href="../../dependencies/iota/iota.md#iota_iota_ENotSystemAddress">ENotSystemAddress</a>);
    <b>assert</b>!(ctx.epoch() == 0, <a href="../../dependencies/iota/iota.md#iota_iota_EAlreadyMinted">EAlreadyMinted</a>);
    <b>let</b> (treasury, metadata) = coin::create_currency(
        <a href="../../dependencies/iota/iota.md#iota_iota_IOTA">IOTA</a> {},
        9,
        b"<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">IOTA</a>",
        b"<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">IOTA</a>",
        b"The main (gas)token of the <a href="../../dependencies/iota/iota.md#iota_iota_IOTA">IOTA</a> Network.",
        option::some(url::new_unsafe_from_bytes(b"https://iota.org/logo.png")),
        ctx,
    );
    transfer::public_freeze_object(metadata);
    <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">IotaTreasuryCap</a> {
        inner: treasury,
    }
}
</code></pre>



</details>

<a name="iota_iota_transfer"></a>

## Function `transfer`



<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_transfer">transfer</a>(c: <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, recipient: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_transfer">transfer</a>(c: coin::Coin&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">IOTA</a>&gt;, recipient: <b>address</b>) {
    transfer::public_transfer(c, recipient)
}
</code></pre>



</details>

<a name="iota_iota_mint"></a>

## Function `mint`

Create an IOTA coin worth <code>value</code> and increase the total supply in <code>cap</code> accordingly.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_mint">mint</a>(cap: &<b>mut</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>, value: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_mint">mint</a>(cap: &<b>mut</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">IotaTreasuryCap</a>, value: u64, ctx: &<b>mut</b> TxContext): Coin&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">IOTA</a>&gt; {
    <b>assert</b>!(ctx.sender() == @0x0, <a href="../../dependencies/iota/iota.md#iota_iota_ENotSystemAddress">ENotSystemAddress</a>);
    cap.inner.<a href="../../dependencies/iota/iota.md#iota_iota_mint">mint</a>(value, ctx)
}
</code></pre>



</details>

<a name="iota_iota_mint_balance"></a>

## Function `mint_balance`

Mint some amount of IOTA as a <code>Balance</code> and increase the total supply in <code>cap</code> accordingly.
Aborts if <code>value</code> + <code>cap.inner.<a href="../../dependencies/iota/iota.md#iota_iota_total_supply">total_supply</a></code> >= U64_MAX


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_mint_balance">mint_balance</a>(cap: &<b>mut</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>, value: u64, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_mint_balance">mint_balance</a>(cap: &<b>mut</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">IotaTreasuryCap</a>, value: u64, ctx: &TxContext): Balance&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">IOTA</a>&gt; {
    <b>assert</b>!(ctx.sender() == @0x0, <a href="../../dependencies/iota/iota.md#iota_iota_ENotSystemAddress">ENotSystemAddress</a>);
    cap.inner.<a href="../../dependencies/iota/iota.md#iota_iota_mint_balance">mint_balance</a>(value)
}
</code></pre>



</details>

<a name="iota_iota_burn"></a>

## Function `burn`

Destroy the IOTA coin <code>c</code> and decrease the total supply in <code>cap</code> accordingly.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_burn">burn</a>(cap: &<b>mut</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>, c: <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_burn">burn</a>(cap: &<b>mut</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">IotaTreasuryCap</a>, c: Coin&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">IOTA</a>&gt;, ctx: &TxContext): u64 {
    <b>assert</b>!(ctx.sender() == @0x0, <a href="../../dependencies/iota/iota.md#iota_iota_ENotSystemAddress">ENotSystemAddress</a>);
    cap.inner.<a href="../../dependencies/iota/iota.md#iota_iota_burn">burn</a>(c)
}
</code></pre>



</details>

<a name="iota_iota_burn_balance"></a>

## Function `burn_balance`

Destroy the IOTA balance <code>b</code> and decrease the total supply in <code>cap</code> accordingly.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_burn_balance">burn_balance</a>(cap: &<b>mut</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>, b: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_burn_balance">burn_balance</a>(cap: &<b>mut</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">IotaTreasuryCap</a>, b: Balance&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">IOTA</a>&gt;, ctx: &TxContext): u64 {
    <b>assert</b>!(ctx.sender() == @0x0, <a href="../../dependencies/iota/iota.md#iota_iota_ENotSystemAddress">ENotSystemAddress</a>);
    cap.inner.supply_mut().decrease_supply(b)
}
</code></pre>



</details>

<a name="iota_iota_total_supply"></a>

## Function `total_supply`

Return the total number of IOTA's in circulation.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_total_supply">total_supply</a>(cap: &<a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/iota.md#iota_iota_total_supply">total_supply</a>(cap: &<a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">IotaTreasuryCap</a>): u64 {
    cap.inner.<a href="../../dependencies/iota/iota.md#iota_iota_total_supply">total_supply</a>()
}
</code></pre>



</details>
