
<a name="stardust_address_unlock_condition"></a>

# Module `stardust::address_unlock_condition`



-  [Function `unlock_alias_address_owned_basic`](#stardust_address_unlock_condition_unlock_alias_address_owned_basic)
-  [Function `unlock_alias_address_owned_nft`](#stardust_address_unlock_condition_unlock_alias_address_owned_nft)
-  [Function `unlock_alias_address_owned_alias`](#stardust_address_unlock_condition_unlock_alias_address_owned_alias)
-  [Function `unlock_alias_address_owned_coinmanager_treasury`](#stardust_address_unlock_condition_unlock_alias_address_owned_coinmanager_treasury)
-  [Function `unlock_nft_address_owned_basic`](#stardust_address_unlock_condition_unlock_nft_address_owned_basic)
-  [Function `unlock_nft_address_owned_nft`](#stardust_address_unlock_condition_unlock_nft_address_owned_nft)
-  [Function `unlock_nft_address_owned_alias`](#stardust_address_unlock_condition_unlock_nft_address_owned_alias)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../../dependencies/iota/coin.md#iota_coin">iota::coin</a>;
<b>use</b> <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager">iota::coin_manager</a>;
<b>use</b> <a href="../../dependencies/iota/config.md#iota_config">iota::config</a>;
<b>use</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list">iota::deny_list</a>;
<b>use</b> <a href="../../dependencies/iota/display.md#iota_display">iota::display</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/package.md#iota_package">iota::package</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/stardust/alias.md#stardust_alias">stardust::alias</a>;
<b>use</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output">stardust::alias_output</a>;
<b>use</b> <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output">stardust::basic_output</a>;
<b>use</b> <a href="../../dependencies/stardust/expiration_unlock_condition.md#stardust_expiration_unlock_condition">stardust::expiration_unlock_condition</a>;
<b>use</b> <a href="../../dependencies/stardust/irc27.md#stardust_irc27">stardust::irc27</a>;
<b>use</b> <a href="../../dependencies/stardust/nft.md#stardust_nft">stardust::nft</a>;
<b>use</b> <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output">stardust::nft_output</a>;
<b>use</b> <a href="../../dependencies/stardust/storage_deposit_return_unlock_condition.md#stardust_storage_deposit_return_unlock_condition">stardust::storage_deposit_return_unlock_condition</a>;
<b>use</b> <a href="../../dependencies/stardust/timelock_unlock_condition.md#stardust_timelock_unlock_condition">stardust::timelock_unlock_condition</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/fixed_point32.md#std_fixed_point32">std::fixed_point32</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="stardust_address_unlock_condition_unlock_alias_address_owned_basic"></a>

## Function `unlock_alias_address_owned_basic`

Unlock a <code>BasicOutput</code> locked to the alias address.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_alias_address_owned_basic">unlock_alias_address_owned_basic</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>, output_to_unlock: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;<a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">stardust::basic_output::BasicOutput</a>&lt;T&gt;&gt;): <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">stardust::basic_output::BasicOutput</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_alias_address_owned_basic">unlock_alias_address_owned_basic</a>&lt;T&gt;(
    self: &<b>mut</b> Alias,
    output_to_unlock: Receiving&lt;BasicOutput&lt;T&gt;&gt;,
): BasicOutput&lt;T&gt; {
    basic_output::receive(self.id(), output_to_unlock)
}
</code></pre>



</details>

<a name="stardust_address_unlock_condition_unlock_alias_address_owned_nft"></a>

## Function `unlock_alias_address_owned_nft`

Unlock an <code>NftOutput</code> locked to the alias address.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_alias_address_owned_nft">unlock_alias_address_owned_nft</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>, output_to_unlock: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;<a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">stardust::nft_output::NftOutput</a>&lt;T&gt;&gt;): <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">stardust::nft_output::NftOutput</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_alias_address_owned_nft">unlock_alias_address_owned_nft</a>&lt;T&gt;(
    self: &<b>mut</b> Alias,
    output_to_unlock: Receiving&lt;NftOutput&lt;T&gt;&gt;,
): NftOutput&lt;T&gt; {
    nft_output::receive(self.id(), output_to_unlock)
}
</code></pre>



</details>

<a name="stardust_address_unlock_condition_unlock_alias_address_owned_alias"></a>

## Function `unlock_alias_address_owned_alias`

Unlock an <code>AliasOutput</code> locked to the alias address.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_alias_address_owned_alias">unlock_alias_address_owned_alias</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>, output_to_unlock: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;<a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">stardust::alias_output::AliasOutput</a>&lt;T&gt;&gt;): <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">stardust::alias_output::AliasOutput</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_alias_address_owned_alias">unlock_alias_address_owned_alias</a>&lt;T&gt;(
    self: &<b>mut</b> Alias,
    output_to_unlock: Receiving&lt;AliasOutput&lt;T&gt;&gt;,
): AliasOutput&lt;T&gt; {
    alias_output::receive(self.id(), output_to_unlock)
}
</code></pre>



</details>

<a name="stardust_address_unlock_condition_unlock_alias_address_owned_coinmanager_treasury"></a>

## Function `unlock_alias_address_owned_coinmanager_treasury`

Unlock a <code>CoinManagerTreasuryCap</code> locked to the alias address.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_alias_address_owned_coinmanager_treasury">unlock_alias_address_owned_coinmanager_treasury</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>, treasury_to_unlock: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;<a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">iota::coin_manager::CoinManagerTreasuryCap</a>&lt;T&gt;&gt;): <a href="../../dependencies/iota/coin_manager.md#iota_coin_manager_CoinManagerTreasuryCap">iota::coin_manager::CoinManagerTreasuryCap</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_alias_address_owned_coinmanager_treasury">unlock_alias_address_owned_coinmanager_treasury</a>&lt;T&gt;(
    self: &<b>mut</b> Alias,
    treasury_to_unlock: Receiving&lt;CoinManagerTreasuryCap&lt;T&gt;&gt;,
): CoinManagerTreasuryCap&lt;T&gt; {
    transfer::public_receive(self.id(), treasury_to_unlock)
}
</code></pre>



</details>

<a name="stardust_address_unlock_condition_unlock_nft_address_owned_basic"></a>

## Function `unlock_nft_address_owned_basic`

Unlock a <code>BasicOutput</code> locked to the <code>Nft</code> address.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_nft_address_owned_basic">unlock_nft_address_owned_basic</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>, output_to_unlock: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;<a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">stardust::basic_output::BasicOutput</a>&lt;T&gt;&gt;): <a href="../../dependencies/stardust/basic_output.md#stardust_basic_output_BasicOutput">stardust::basic_output::BasicOutput</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_nft_address_owned_basic">unlock_nft_address_owned_basic</a>&lt;T&gt;(
    self: &<b>mut</b> Nft,
    output_to_unlock: Receiving&lt;BasicOutput&lt;T&gt;&gt;,
): BasicOutput&lt;T&gt; {
    basic_output::receive(self.id(), output_to_unlock)
}
</code></pre>



</details>

<a name="stardust_address_unlock_condition_unlock_nft_address_owned_nft"></a>

## Function `unlock_nft_address_owned_nft`

Unlock an <code>NftOutput</code> locked to the <code>Nft</code> address.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_nft_address_owned_nft">unlock_nft_address_owned_nft</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>, output_to_unlock: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;<a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">stardust::nft_output::NftOutput</a>&lt;T&gt;&gt;): <a href="../../dependencies/stardust/nft_output.md#stardust_nft_output_NftOutput">stardust::nft_output::NftOutput</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_nft_address_owned_nft">unlock_nft_address_owned_nft</a>&lt;T&gt;(
    self: &<b>mut</b> Nft,
    output_to_unlock: Receiving&lt;NftOutput&lt;T&gt;&gt;,
): NftOutput&lt;T&gt; {
    nft_output::receive(self.id(), output_to_unlock)
}
</code></pre>



</details>

<a name="stardust_address_unlock_condition_unlock_nft_address_owned_alias"></a>

## Function `unlock_nft_address_owned_alias`

Unlock an <code>AliasOutput</code> locked to the <code>Nft</code> address.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_nft_address_owned_alias">unlock_nft_address_owned_alias</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/stardust/nft.md#stardust_nft_Nft">stardust::nft::Nft</a>, output_to_unlock: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;<a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">stardust::alias_output::AliasOutput</a>&lt;T&gt;&gt;): <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">stardust::alias_output::AliasOutput</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/stardust/address_unlock_condition.md#stardust_address_unlock_condition_unlock_nft_address_owned_alias">unlock_nft_address_owned_alias</a>&lt;T&gt;(
    self: &<b>mut</b> Nft,
    output_to_unlock: Receiving&lt;AliasOutput&lt;T&gt;&gt;,
): AliasOutput&lt;T&gt; {
    alias_output::receive(self.id(), output_to_unlock)
}
</code></pre>



</details>
