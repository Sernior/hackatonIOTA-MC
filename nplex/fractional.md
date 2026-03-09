---
layout: default
title: fractional
parent: Nplex Smart Contracts
---


<a name="(nplex=0x0)_fractional"></a>

# Module `(nplex=0x0)::fractional`

NPLEX Fractional - Fractionalize LTC1 Tokens into real Coins

Allows investors to split their LTC1Token balance into real fungible
Coin<F> tokens (DEX-tradeable). The TreasuryCap is locked in a shared
FractionalVault so anyone can redeem coins back into LTC1Tokens.


-  [Struct `FractionalVault`](#(nplex=0x0)_fractional_FractionalVault)
-  [Constants](#@Constants_0)
-  [Function `fractionalize`](#(nplex=0x0)_fractional_fractionalize)
-  [Function `redeem`](#(nplex=0x0)_fractional_redeem)
-  [Function `merge_back`](#(nplex=0x0)_fractional_merge_back)
-  [Function `destroy_empty_vault`](#(nplex=0x0)_fractional_destroy_empty_vault)
-  [Function `vault_package_id`](#(nplex=0x0)_fractional_vault_package_id)
-  [Function `vault_total_supply`](#(nplex=0x0)_fractional_vault_total_supply)
-  [Function `vault_total_fractionalized`](#(nplex=0x0)_fractional_vault_total_fractionalized)


<pre><code><b>use</b> (iota_identity=0x0)::controller;
<b>use</b> (iota_identity=0x0)::permissions;
<b>use</b> (iota_notarization=0x0)::method;
<b>use</b> (iota_notarization=0x0)::notarization;
<b>use</b> (iota_notarization=0x0)::timelock;
<b>use</b> (nplex=0x0)::<a href="../nplex/events.md#(nplex=0x0)_events">events</a>;
<b>use</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1">ltc1</a>;
<b>use</b> (nplex=0x0)::<a href="../nplex/registry.md#(nplex=0x0)_registry">registry</a>;
<b>use</b> <a href="../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../dependencies/iota/borrow.md#iota_borrow">iota::borrow</a>;
<b>use</b> <a href="../dependencies/iota/clock.md#iota_clock">iota::clock</a>;
<b>use</b> <a href="../dependencies/iota/coin.md#iota_coin">iota::coin</a>;
<b>use</b> <a href="../dependencies/iota/config.md#iota_config">iota::config</a>;
<b>use</b> <a href="../dependencies/iota/deny_list.md#iota_deny_list">iota::deny_list</a>;
<b>use</b> <a href="../dependencies/iota/display.md#iota_display">iota::display</a>;
<b>use</b> <a href="../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../dependencies/iota/package.md#iota_package">iota::package</a>;
<b>use</b> <a href="../dependencies/iota/table.md#iota_table">iota::table</a>;
<b>use</b> <a href="../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="(nplex=0x0)_fractional_FractionalVault"></a>

## Struct `FractionalVault`

Shared vault holding the TreasuryCap for a fractionalized LTC1Token.
Anyone can redeem Coin<F> against this vault to get a new LTC1Token.


<pre><code><b>public</b> <b>struct</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a>&lt;<b>phantom</b> F&gt; <b>has</b> key
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>package_id: <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 Which LTC1Package the fractionalized token belongs to
</dd>
<dt>
<code>treasury_cap: <a href="../dependencies/iota/coin.md#iota_coin_TreasuryCap">iota::coin::TreasuryCap</a>&lt;F&gt;</code>
</dt>
<dd>
 The locked TreasuryCap — only this contract can mint/burn
</dd>
<dt>
<code>total_claimed_snapshot: u64</code>
</dt>
<dd>
 Snapshot of claimed_revenue at fractionalization time (for proportional accounting)
</dd>
<dt>
<code>total_fractionalized: u64</code>
</dt>
<dd>
 Total balance that was fractionalized (= total coins minted)
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(nplex=0x0)_fractional_E_TREASURY_NOT_FRESH"></a>



<pre><code><b>const</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_E_TREASURY_NOT_FRESH">E_TREASURY_NOT_FRESH</a>: u64 = 2001;
</code></pre>



<a name="(nplex=0x0)_fractional_E_PACKAGE_MISMATCH"></a>



<pre><code><b>const</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_E_PACKAGE_MISMATCH">E_PACKAGE_MISMATCH</a>: u64 = 2002;
</code></pre>



<a name="(nplex=0x0)_fractional_E_ZERO_AMOUNT"></a>



<pre><code><b>const</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_E_ZERO_AMOUNT">E_ZERO_AMOUNT</a>: u64 = 2003;
</code></pre>



<a name="(nplex=0x0)_fractional_fractionalize"></a>

## Function `fractionalize`

Fractionalize: convert <code>amount</code> of an LTC1Token's balance into real Coin<F>.

Security: asserts TreasuryCap total_supply == 0 (no pre-minting allowed).
The TreasuryCap is locked in a shared FractionalVault.

Caller must own the LTC1Token and pass a fresh TreasuryCap<F>.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_fractionalize">fractionalize</a>&lt;F&gt;(token: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">ltc1::LTC1Token</a>, treasury_cap: <a href="../dependencies/iota/coin.md#iota_coin_TreasuryCap">iota::coin::TreasuryCap</a>&lt;F&gt;, amount: u64, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_fractionalize">fractionalize</a>&lt;F&gt;(
    token: &<b>mut</b> LTC1Token,
    treasury_cap: TreasuryCap&lt;F&gt;,
    amount: u64,
    ctx: &<b>mut</b> TxContext
) {
    // 1. Security: no coins must have been minted before
    <b>assert</b>!(coin::total_supply(&treasury_cap) == 0, <a href="../nplex/fractional.md#(nplex=0x0)_fractional_E_TREASURY_NOT_FRESH">E_TREASURY_NOT_FRESH</a>);
    <b>assert</b>!(amount &gt; 0, <a href="../nplex/fractional.md#(nplex=0x0)_fractional_E_ZERO_AMOUNT">E_ZERO_AMOUNT</a>);
    // 2. Subtract balance from token (handles validation + proportional claimed split)
    <b>let</b> (_balance_removed, claimed_split) = <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_subtract_balance">ltc1::subtract_balance</a>(token, amount);
    // 3. Mint coins
    <b>let</b> <b>mut</b> cap = treasury_cap;
    <b>let</b> coins = coin::mint(&<b>mut</b> cap, amount, ctx);
    // 4. Create shared vault with the TreasuryCap locked inside
    <b>let</b> vault = <a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a>&lt;F&gt; {
        id: object::new(ctx),
        package_id: <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">ltc1::package_id</a>(token),
        treasury_cap: cap,
        total_claimed_snapshot: claimed_split,
        total_fractionalized: amount,
    };
    // 5. Emit Event
    // 5. Emit Event
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_vault_created">events::emit_vault_created</a>(
        object::id(&vault),
        <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">ltc1::package_id</a>(token),
        type_name::get&lt;F&gt;().into_string(),
        amount,
        ctx.sender(),
    );
    // 6. Share the vault so anyone can <a href="../nplex/fractional.md#(nplex=0x0)_fractional_redeem">redeem</a>
    <a href="../dependencies/iota/transfer.md#iota_transfer_share_object">iota::transfer::share_object</a>(vault);
    // 7. Send coins to the caller
    <a href="../dependencies/iota/transfer.md#iota_transfer_public_transfer">iota::transfer::public_transfer</a>(coins, ctx.sender());
}
</code></pre>



</details>

<a name="(nplex=0x0)_fractional_redeem"></a>

## Function `redeem`

Redeem: burn Coin<F> and receive a new LTC1Token with the corresponding balance.
The new token's claimed_revenue is set proportionally from the vault snapshot,
ensuring correct revenue accounting (no double-claims).

Anyone holding Coin<F> can call this (e.g., DEX buyers).


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_redeem">redeem</a>&lt;F, P&gt;(vault: &<b>mut</b> (nplex=0x0)::<a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">fractional::FractionalVault</a>&lt;F&gt;, coins: <a href="../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;F&gt;, package: &(nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Package">ltc1::LTC1Package</a>&lt;P&gt;, ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_redeem">redeem</a>&lt;F, P&gt;(
    vault: &<b>mut</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a>&lt;F&gt;,
    coins: Coin&lt;F&gt;,
    package: &LTC1Package&lt;P&gt;,
    ctx: &<b>mut</b> TxContext
) {
    <b>let</b> burn_amount = coin::value(&coins);
    <b>assert</b>!(burn_amount &gt; 0, <a href="../nplex/fractional.md#(nplex=0x0)_fractional_E_ZERO_AMOUNT">E_ZERO_AMOUNT</a>);
    // 1. Verify the vault belongs to this package
    <b>assert</b>!(vault.package_id == object::id(package), <a href="../nplex/fractional.md#(nplex=0x0)_fractional_E_PACKAGE_MISMATCH">E_PACKAGE_MISMATCH</a>);
    // 2. Burn the coins
    coin::burn(&<b>mut</b> vault.treasury_cap, coins);
    // 3. Calculate proportional claimed_revenue
    <b>let</b> claimed = <b>if</b> (vault.total_claimed_snapshot == 0) {
        0
    } <b>else</b> {
        (((vault.total_claimed_snapshot <b>as</b> u256) * (burn_amount <b>as</b> u256)) / (vault.total_fractionalized <b>as</b> u256) <b>as</b> u64)
    };
    // 4. Create a new LTC1Token with the redeemed balance
    <b>let</b> token = <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_create_token_from_fraction">ltc1::create_token_from_fraction</a>(
        vault.package_id,
        burn_amount,
        claimed,
        ctx
    );
    // 5. Transfer the new token to the caller
    <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_send_token_to">ltc1::send_token_to</a>(token, ctx.sender());
    // 5.5 Emit <a href="../nplex/fractional.md#(nplex=0x0)_fractional_redeem">redeem</a> event
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_fraction_redeemed">events::emit_fraction_redeemed</a>(
        object::id(vault),
        burn_amount,
        ctx.sender(),
    );
    // 6. Check <b>if</b> empty and emit event (but do NOT destroy automatically)
    <b>if</b> (coin::total_supply(&vault.treasury_cap) == 0) {
        <a href="../nplex/events.md#(nplex=0x0)_events_emit_vault_empty">events::emit_vault_empty</a>(
            object::id(vault),
            type_name::get&lt;F&gt;().into_string(),
        );
    };
}
</code></pre>



</details>

<a name="(nplex=0x0)_fractional_merge_back"></a>

## Function `merge_back`

Merge back: burn Coin<F> and add the balance back to an existing LTC1Token.
Useful for the original fractionalizer who still holds their token.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_merge_back">merge_back</a>&lt;F&gt;(token: &<b>mut</b> (nplex=0x0)::<a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_LTC1Token">ltc1::LTC1Token</a>, vault: &<b>mut</b> (nplex=0x0)::<a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">fractional::FractionalVault</a>&lt;F&gt;, coins: <a href="../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;F&gt;, _ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_merge_back">merge_back</a>&lt;F&gt;(
    token: &<b>mut</b> LTC1Token,
    vault: &<b>mut</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a>&lt;F&gt;,
    coins: Coin&lt;F&gt;,
    _ctx: &<b>mut</b> TxContext
) {
    <b>let</b> burn_amount = coin::value(&coins);
    <b>assert</b>!(burn_amount &gt; 0, <a href="../nplex/fractional.md#(nplex=0x0)_fractional_E_ZERO_AMOUNT">E_ZERO_AMOUNT</a>);
    // 1. Verify same package
    <b>assert</b>!(vault.package_id == <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_package_id">ltc1::package_id</a>(token), <a href="../nplex/fractional.md#(nplex=0x0)_fractional_E_PACKAGE_MISMATCH">E_PACKAGE_MISMATCH</a>);
    // 2. Burn the coins
    coin::burn(&<b>mut</b> vault.treasury_cap, coins);
    // 3. Calculate proportional claimed_revenue
    <b>let</b> claimed = <b>if</b> (vault.total_claimed_snapshot == 0) {
        0
    } <b>else</b> {
        (((vault.total_claimed_snapshot <b>as</b> u256) * (burn_amount <b>as</b> u256)) / (vault.total_fractionalized <b>as</b> u256) <b>as</b> u64)
    };
    // 4. Add back to the existing token
    <a href="../nplex/ltc1.md#(nplex=0x0)_ltc1_add_fraction_balance">ltc1::add_fraction_balance</a>(token, burn_amount, claimed);
    // 4.5 Emit merge event
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_fraction_merged_back">events::emit_fraction_merged_back</a>(
        object::id(vault),
        object::id(token),
        burn_amount,
    );
    // 5. Check <b>if</b> empty and emit event
    <b>if</b> (coin::total_supply(&vault.treasury_cap) == 0) {
        <a href="../nplex/events.md#(nplex=0x0)_events_emit_vault_empty">events::emit_vault_empty</a>(
            object::id(vault),
            type_name::get&lt;F&gt;().into_string(),
        );
    };
}
</code></pre>



</details>

<a name="(nplex=0x0)_fractional_destroy_empty_vault"></a>

## Function `destroy_empty_vault`

Manually destroy an empty vault and return the TreasuryCap.
Anyone can call this to clean up the state (permissionless).


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_destroy_empty_vault">destroy_empty_vault</a>&lt;F&gt;(vault: (nplex=0x0)::<a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">fractional::FractionalVault</a>&lt;F&gt;, _ctx: &<b>mut</b> <a href="../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_destroy_empty_vault">destroy_empty_vault</a>&lt;F&gt;(
    vault: <a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a>&lt;F&gt;,
    _ctx: &<b>mut</b> TxContext
) {
    <b>assert</b>!(coin::total_supply(&vault.treasury_cap) == 0, <a href="../nplex/fractional.md#(nplex=0x0)_fractional_E_ZERO_AMOUNT">E_ZERO_AMOUNT</a>); // Reusing error code <b>for</b> checking non-zero supply
    <b>let</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a> {
        id,
        package_id: _,
        treasury_cap,
        total_claimed_snapshot: _,
        total_fractionalized: _,
    } = vault;
    <a href="../nplex/events.md#(nplex=0x0)_events_emit_vault_destroyed">events::emit_vault_destroyed</a>(object::uid_to_inner(&id));
    object::delete(id);
    <a href="../dependencies/iota/transfer.md#iota_transfer_public_freeze_object">iota::transfer::public_freeze_object</a>(treasury_cap);
}
</code></pre>



</details>

<a name="(nplex=0x0)_fractional_vault_package_id"></a>

## Function `vault_package_id`

Returns the package ID of the fractionalized token.
Retrieves <code><a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a>.package_id</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_vault_package_id">vault_package_id</a>&lt;F&gt;(vault: &(nplex=0x0)::<a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">fractional::FractionalVault</a>&lt;F&gt;): <a href="../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_vault_package_id">vault_package_id</a>&lt;F&gt;(vault: &<a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a>&lt;F&gt;): ID {
    vault.package_id
}
</code></pre>



</details>

<a name="(nplex=0x0)_fractional_vault_total_supply"></a>

## Function `vault_total_supply`

Returns the total supply of the fractionalized token.
Calculates standard <code>coin::total_supply</code> using <code><a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a>.treasury_cap</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_vault_total_supply">vault_total_supply</a>&lt;F&gt;(vault: &(nplex=0x0)::<a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">fractional::FractionalVault</a>&lt;F&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_vault_total_supply">vault_total_supply</a>&lt;F&gt;(vault: &<a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a>&lt;F&gt;): u64 {
    coin::total_supply(&vault.treasury_cap)
}
</code></pre>



</details>

<a name="(nplex=0x0)_fractional_vault_total_fractionalized"></a>

## Function `vault_total_fractionalized`

Returns the total amount of coins that were fractionalized.
Retrieves <code><a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a>.total_fractionalized</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_vault_total_fractionalized">vault_total_fractionalized</a>&lt;F&gt;(vault: &(nplex=0x0)::<a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">fractional::FractionalVault</a>&lt;F&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../nplex/fractional.md#(nplex=0x0)_fractional_vault_total_fractionalized">vault_total_fractionalized</a>&lt;F&gt;(vault: &<a href="../nplex/fractional.md#(nplex=0x0)_fractional_FractionalVault">FractionalVault</a>&lt;F&gt;): u64 {
    vault.total_fractionalized
}
</code></pre>



</details>
