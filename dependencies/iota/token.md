
<a name="iota_token"></a>

# Module `iota::token`

The Token module which implements a Closed Loop Token with a configurable
policy. The policy is defined by a set of rules that must be satisfied for
an action to be performed on the token.

The module is designed to be used with a <code>TreasuryCap</code> to allow for minting
and burning of the <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code>s. And can act as a replacement / extension or a
companion to existing open-loop (<code>Coin</code>) systems.

```
Module:      iota::balance       iota::coin             iota::token
Main type:   Balance<T>         Coin<T>               Token<T>
Capability:  Supply<T>  <---->  TreasuryCap<T> <----> TreasuryCap<T>
Abilities:   store              key + store           key
```

The Token system allows for fine-grained control over the actions performed
on the token. And hence it is highly suitable for applications that require
control over the currency which a simple open-loop system can't provide.


-  [Struct `Token`](#iota_token_Token)
-  [Struct `TokenPolicyCap`](#iota_token_TokenPolicyCap)
-  [Struct `TokenPolicy`](#iota_token_TokenPolicy)
-  [Struct `ActionRequest`](#iota_token_ActionRequest)
-  [Struct `RuleKey`](#iota_token_RuleKey)
-  [Struct `TokenPolicyCreated`](#iota_token_TokenPolicyCreated)
-  [Constants](#@Constants_0)
-  [Function `new_policy`](#iota_token_new_policy)
-  [Function `share_policy`](#iota_token_share_policy)
-  [Function `transfer`](#iota_token_transfer)
-  [Function `spend`](#iota_token_spend)
-  [Function `to_coin`](#iota_token_to_coin)
-  [Function `from_coin`](#iota_token_from_coin)
-  [Function `join`](#iota_token_join)
-  [Function `split`](#iota_token_split)
-  [Function `zero`](#iota_token_zero)
-  [Function `destroy_zero`](#iota_token_destroy_zero)
-  [Function `keep`](#iota_token_keep)
-  [Function `new_request`](#iota_token_new_request)
-  [Function `confirm_request`](#iota_token_confirm_request)
-  [Function `confirm_request_mut`](#iota_token_confirm_request_mut)
-  [Function `confirm_with_policy_cap`](#iota_token_confirm_with_policy_cap)
-  [Function `confirm_with_treasury_cap`](#iota_token_confirm_with_treasury_cap)
-  [Function `add_approval`](#iota_token_add_approval)
-  [Function `add_rule_config`](#iota_token_add_rule_config)
-  [Function `rule_config`](#iota_token_rule_config)
-  [Function `rule_config_mut`](#iota_token_rule_config_mut)
-  [Function `remove_rule_config`](#iota_token_remove_rule_config)
-  [Function `has_rule_config`](#iota_token_has_rule_config)
-  [Function `has_rule_config_with_type`](#iota_token_has_rule_config_with_type)
-  [Function `allow`](#iota_token_allow)
-  [Function `disallow`](#iota_token_disallow)
-  [Function `add_rule_for_action`](#iota_token_add_rule_for_action)
-  [Function `remove_rule_for_action`](#iota_token_remove_rule_for_action)
-  [Function `mint`](#iota_token_mint)
-  [Function `burn`](#iota_token_burn)
-  [Function `flush`](#iota_token_flush)
-  [Function `is_allowed`](#iota_token_is_allowed)
-  [Function `rules`](#iota_token_rules)
-  [Function `spent_balance`](#iota_token_spent_balance)
-  [Function `value`](#iota_token_value)
-  [Function `transfer_action`](#iota_token_transfer_action)
-  [Function `spend_action`](#iota_token_spend_action)
-  [Function `to_coin_action`](#iota_token_to_coin_action)
-  [Function `from_coin_action`](#iota_token_from_coin_action)
-  [Function `action`](#iota_token_action)
-  [Function `amount`](#iota_token_amount)
-  [Function `sender`](#iota_token_sender)
-  [Function `recipient`](#iota_token_recipient)
-  [Function `approvals`](#iota_token_approvals)
-  [Function `spent`](#iota_token_spent)
-  [Function `key`](#iota_token_key)


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
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/iota/vec_set.md#iota_vec_set">iota::vec_set</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_token_Token"></a>

## Struct `Token`

A single <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code> with <code>Balance</code> inside. Can only be owned by an address,
and actions performed on it must be confirmed in a matching <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;<b>phantom</b> T&gt; <b>has</b> <a href="../../dependencies/iota/token.md#iota_token_key">key</a>
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
<code>balance: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;</code>
</dt>
<dd>
 The Balance of the <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code>.
</dd>
</dl>


</details>

<a name="iota_token_TokenPolicyCap"></a>

## Struct `TokenPolicyCap`

A Capability that manages a single <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> specified in the <code><b>for</b></code>
field. Created together with <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> in the <code>new</code> function.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a>&lt;<b>phantom</b> T&gt; <b>has</b> <a href="../../dependencies/iota/token.md#iota_token_key">key</a>, store
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
<code><b>for</b>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_token_TokenPolicy"></a>

## Struct `TokenPolicy`

<code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> represents a set of rules that define what actions can be
performed on a <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code> and which <code>Rules</code> must be satisfied for the
action to succeed.

- For the sake of availability, <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> is a <code><a href="../../dependencies/iota/token.md#iota_token_key">key</a></code>-only object.
- Each <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> is managed by a matching <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code>.
- For an action to become available, there needs to be a record in the
<code><a href="../../dependencies/iota/token.md#iota_token_rules">rules</a></code> VecMap. To allow an action to be performed freely, there's an
<code><a href="../../dependencies/iota/token.md#iota_token_allow">allow</a></code> function that can be called by the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code> owner.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;<b>phantom</b> T&gt; <b>has</b> <a href="../../dependencies/iota/token.md#iota_token_key">key</a>
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
<code><a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;</code>
</dt>
<dd>
 The balance that is effectively spent by the user on the "spend"
 action. However, actual decrease of the supply can only be done by
 the <code>TreasuryCap</code> owner when <code><a href="../../dependencies/iota/token.md#iota_token_flush">flush</a></code> is called.
 This balance is effectively spent and cannot be accessed by anyone
 but the <code>TreasuryCap</code> owner.
</dd>
<dt>
<code><a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>&gt;&gt;</code>
</dt>
<dd>
 The set of rules that define what actions can be performed on the
 token. For each "action" there's a set of Rules that must be
 satisfied for the <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code> to be confirmed.
</dd>
</dl>


</details>

<a name="iota_token_ActionRequest"></a>

## Struct `ActionRequest`

A request to perform an "Action" on a token. Stores the information
about the action to be performed and must be consumed by the <code><a href="../../dependencies/iota/token.md#iota_token_confirm_request">confirm_request</a></code>
or <code><a href="../../dependencies/iota/token.md#iota_token_confirm_request_mut">confirm_request_mut</a></code> functions when the Rules are satisfied.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;<b>phantom</b> T&gt;
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>name: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a></code>
</dt>
<dd>
 Name of the Action to look up in the Policy. Name can be one of the
 default actions: <code><a href="../../dependencies/iota/token.md#iota_token_transfer">transfer</a></code>, <code><a href="../../dependencies/iota/token.md#iota_token_spend">spend</a></code>, <code><a href="../../dependencies/iota/token.md#iota_token_to_coin">to_coin</a></code>, <code><a href="../../dependencies/iota/token.md#iota_token_from_coin">from_coin</a></code> or a
 custom action.
</dd>
<dt>
<code><a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>: u64</code>
</dt>
<dd>
 Amount is present in all of the txs
</dd>
<dt>
<code><a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>: <b>address</b></code>
</dt>
<dd>
 Sender is a permanent field always
</dd>
<dt>
<code><a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;</code>
</dt>
<dd>
 Recipient is only available in <code><a href="../../dependencies/iota/token.md#iota_token_transfer">transfer</a></code> action.
</dd>
<dt>
<code><a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;&gt;</code>
</dt>
<dd>
 The balance to be "spent" in the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>, only available
 in the <code><a href="../../dependencies/iota/token.md#iota_token_spend">spend</a></code> action.
</dd>
<dt>
<code><a href="../../dependencies/iota/token.md#iota_token_approvals">approvals</a>: <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>&gt;</code>
</dt>
<dd>
 Collected approvals (stamps) from completed <code>Rules</code>. They're matched
 against <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a></code> to determine if the request can be
 confirmed.
</dd>
</dl>


</details>

<a name="iota_token_RuleKey"></a>

## Struct `RuleKey`

Dynamic field key for the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> to store the <code>Config</code> for a
specific action <code>Rule</code>. There can be only one configuration per
<code>Rule</code> per <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/token.md#iota_token_RuleKey">RuleKey</a>&lt;<b>phantom</b> T&gt; <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>is_protected: bool</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_token_TokenPolicyCreated"></a>

## Struct `TokenPolicyCreated`

An event emitted when a <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> is created and shared. Because
<code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> can only be shared (and potentially frozen in the future),
we emit this event in the <code><a href="../../dependencies/iota/token.md#iota_token_share_policy">share_policy</a></code> function and mark it as mutable.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCreated">TokenPolicyCreated</a>&lt;<b>phantom</b> T&gt; <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 ID of the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> that was created.
</dd>
<dt>
<code>is_mutable: bool</code>
</dt>
<dd>
 Whether the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> is "shared" (mutable) or "frozen"
 (immutable) - TBD.
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_token_EUnknownAction"></a>

The action is not allowed (defined) in the policy.


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_EUnknownAction">EUnknownAction</a>: u64 = 0;
</code></pre>



<a name="iota_token_ENotApproved"></a>

The rule was not approved.


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_ENotApproved">ENotApproved</a>: u64 = 1;
</code></pre>



<a name="iota_token_ENotAuthorized"></a>

Trying to perform an admin action with a wrong cap.


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_ENotAuthorized">ENotAuthorized</a>: u64 = 2;
</code></pre>



<a name="iota_token_EBalanceTooLow"></a>

The balance is too low to perform the action.


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_EBalanceTooLow">EBalanceTooLow</a>: u64 = 3;
</code></pre>



<a name="iota_token_ENotZero"></a>

The balance is not zero.


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_ENotZero">ENotZero</a>: u64 = 4;
</code></pre>



<a name="iota_token_ECantConsumeBalance"></a>

The balance is not zero when trying to confirm with <code>TransferPolicyCap</code>.


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_ECantConsumeBalance">ECantConsumeBalance</a>: u64 = 5;
</code></pre>



<a name="iota_token_ENoConfig"></a>

Rule is trying to access a missing config (with type).


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_ENoConfig">ENoConfig</a>: u64 = 6;
</code></pre>



<a name="iota_token_EUseImmutableConfirm"></a>

Using <code><a href="../../dependencies/iota/token.md#iota_token_confirm_request_mut">confirm_request_mut</a></code> without <code><a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a></code>. Immutable version
of the function must be used instead.


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_EUseImmutableConfirm">EUseImmutableConfirm</a>: u64 = 7;
</code></pre>



<a name="iota_token_SPEND"></a>

A Tag for the <code><a href="../../dependencies/iota/token.md#iota_token_spend">spend</a></code> action.


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_SPEND">SPEND</a>: vector&lt;u8&gt; = vector[115, 112, 101, 110, 100];
</code></pre>



<a name="iota_token_TRANSFER"></a>

A Tag for the <code><a href="../../dependencies/iota/token.md#iota_token_transfer">transfer</a></code> action.


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_TRANSFER">TRANSFER</a>: vector&lt;u8&gt; = vector[116, 114, 97, 110, 115, 102, 101, 114];
</code></pre>



<a name="iota_token_TO_COIN"></a>

A Tag for the <code><a href="../../dependencies/iota/token.md#iota_token_to_coin">to_coin</a></code> action.


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_TO_COIN">TO_COIN</a>: vector&lt;u8&gt; = vector[116, 111, 95, 99, 111, 105, 110];
</code></pre>



<a name="iota_token_FROM_COIN"></a>

A Tag for the <code><a href="../../dependencies/iota/token.md#iota_token_from_coin">from_coin</a></code> action.


<pre><code><b>const</b> <a href="../../dependencies/iota/token.md#iota_token_FROM_COIN">FROM_COIN</a>: vector&lt;u8&gt; = vector[102, 114, 111, 109, 95, 99, 111, 105, 110];
</code></pre>



<a name="iota_token_new_policy"></a>

## Function `new_policy`

Create a new <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> and a matching <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code>.
The <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> must then be shared using the <code><a href="../../dependencies/iota/token.md#iota_token_share_policy">share_policy</a></code> method.

<code>TreasuryCap</code> guarantees full ownership over the currency, and is unique,
hence it is safe to use it for authorization.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_new_policy">new_policy</a>&lt;T&gt;(_treasury_cap: &<a href="../../dependencies/iota/coin.md#iota_coin_TreasuryCap">iota::coin::TreasuryCap</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">iota::token::TokenPolicyCap</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_new_policy">new_policy</a>&lt;T&gt;(
    _treasury_cap: &TreasuryCap&lt;T&gt;,
    ctx: &<b>mut</b> TxContext,
): (<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a>&lt;T&gt;) {
    <b>let</b> policy = <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a> {
        id: object::new(ctx),
        <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>: balance::zero(),
        <a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>: vec_map::empty(),
    };
    <b>let</b> cap = <a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a> {
        id: object::new(ctx),
        `<b>for</b>`: object::id(&policy),
    };
    (policy, cap)
}
</code></pre>



</details>

<a name="iota_token_share_policy"></a>

## Function `share_policy`

Share the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>. Due to <code><a href="../../dependencies/iota/token.md#iota_token_key">key</a></code>-only restriction, it must be
shared after initialization.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_share_policy">share_policy</a>&lt;T&gt;(policy: <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_share_policy">share_policy</a>&lt;T&gt;(policy: <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;) {
    event::emit(<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCreated">TokenPolicyCreated</a>&lt;T&gt; {
        id: object::id(&policy),
        is_mutable: <b>true</b>,
    });
    transfer::share_object(policy)
}
</code></pre>



</details>

<a name="iota_token_transfer"></a>

## Function `transfer`

Transfer a <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code> to a <code><a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a></code>. Creates an <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code> for the
"transfer" action. The <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code> contains the <code><a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a></code> field
to be used in verification.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_transfer">transfer</a>&lt;T&gt;(t: <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_transfer">transfer</a>&lt;T&gt;(t: <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>: <b>address</b>, ctx: &<b>mut</b> TxContext): <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt; {
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a> = t.balance.<a href="../../dependencies/iota/token.md#iota_token_value">value</a>();
    transfer::transfer(t, <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>);
    <a href="../../dependencies/iota/token.md#iota_token_new_request">new_request</a>(
        <a href="../../dependencies/iota/token.md#iota_token_transfer_action">transfer_action</a>(),
        <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>,
        option::some(<a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>),
        option::none(),
        ctx,
    )
}
</code></pre>



</details>

<a name="iota_token_spend"></a>

## Function `spend`

Spend a <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code> by unwrapping it and storing the <code>Balance</code> in the
<code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code> for the "spend" action. The <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code> contains
the <code><a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a></code> field to be used in verification.

Spend action requires <code><a href="../../dependencies/iota/token.md#iota_token_confirm_request_mut">confirm_request_mut</a></code> to be called to confirm the
request and join the spent balance with the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_spend">spend</a>&lt;T&gt;(t: <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_spend">spend</a>&lt;T&gt;(t: <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt;, ctx: &<b>mut</b> TxContext): <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt; {
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a> { id, balance } = t;
    id.delete();
    <a href="../../dependencies/iota/token.md#iota_token_new_request">new_request</a>(
        <a href="../../dependencies/iota/token.md#iota_token_spend_action">spend_action</a>(),
        balance.<a href="../../dependencies/iota/token.md#iota_token_value">value</a>(),
        option::none(),
        option::some(balance),
        ctx,
    )
}
</code></pre>



</details>

<a name="iota_token_to_coin"></a>

## Function `to_coin`

Convert <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code> into an open <code>Coin</code>. Creates an <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code> for the
"to_coin" action.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_to_coin">to_coin</a>&lt;T&gt;(t: <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_to_coin">to_coin</a>&lt;T&gt;(t: <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt;, ctx: &<b>mut</b> TxContext): (Coin&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;) {
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a> { id, balance } = t;
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a> = balance.<a href="../../dependencies/iota/token.md#iota_token_value">value</a>();
    id.delete();
    (
        balance.into_coin(ctx),
        <a href="../../dependencies/iota/token.md#iota_token_new_request">new_request</a>(
            <a href="../../dependencies/iota/token.md#iota_token_to_coin_action">to_coin_action</a>(),
            <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>,
            option::none(),
            option::none(),
            ctx,
        ),
    )
}
</code></pre>



</details>

<a name="iota_token_from_coin"></a>

## Function `from_coin`

Convert an open <code>Coin</code> into a <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code>. Creates an <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code> for
the "from_coin" action.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_from_coin">from_coin</a>&lt;T&gt;(coin: <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_from_coin">from_coin</a>&lt;T&gt;(coin: Coin&lt;T&gt;, ctx: &<b>mut</b> TxContext): (<a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;) {
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a> = coin.<a href="../../dependencies/iota/token.md#iota_token_value">value</a>();
    <b>let</b> token = <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a> {
        id: object::new(ctx),
        balance: coin.into_balance(),
    };
    (
        token,
        <a href="../../dependencies/iota/token.md#iota_token_new_request">new_request</a>(
            <a href="../../dependencies/iota/token.md#iota_token_from_coin_action">from_coin_action</a>(),
            <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>,
            option::none(),
            option::none(),
            ctx,
        ),
    )
}
</code></pre>



</details>

<a name="iota_token_join"></a>

## Function `join`

Join two <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code>s into one, always available.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_join">join</a>&lt;T&gt;(token: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;, another: <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_join">join</a>&lt;T&gt;(token: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt;, another: <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt;) {
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a> { id, balance } = another;
    token.balance.<a href="../../dependencies/iota/token.md#iota_token_join">join</a>(balance);
    id.delete();
}
</code></pre>



</details>

<a name="iota_token_split"></a>

## Function `split`

Split a <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code> with <code><a href="../../dependencies/iota/token.md#iota_token_amount">amount</a></code>.
Aborts if the <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>.balance</code> is lower than <code><a href="../../dependencies/iota/token.md#iota_token_amount">amount</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_split">split</a>&lt;T&gt;(token: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_split">split</a>&lt;T&gt;(token: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>: u64, ctx: &<b>mut</b> TxContext): <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt; {
    <b>assert</b>!(token.balance.<a href="../../dependencies/iota/token.md#iota_token_value">value</a>() &gt;= <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>, <a href="../../dependencies/iota/token.md#iota_token_EBalanceTooLow">EBalanceTooLow</a>);
    <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a> {
        id: object::new(ctx),
        balance: token.balance.<a href="../../dependencies/iota/token.md#iota_token_split">split</a>(<a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>),
    }
}
</code></pre>



</details>

<a name="iota_token_zero"></a>

## Function `zero`

Create a zero <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_zero">zero</a>&lt;T&gt;(ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_zero">zero</a>&lt;T&gt;(ctx: &<b>mut</b> TxContext): <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt; {
    <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a> {
        id: object::new(ctx),
        balance: balance::zero(),
    }
}
</code></pre>



</details>

<a name="iota_token_destroy_zero"></a>

## Function `destroy_zero`

Destroy an empty <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code>, fails if the balance is non-zero.
Aborts if the <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>.balance</code> is not zero.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_destroy_zero">destroy_zero</a>&lt;T&gt;(token: <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_destroy_zero">destroy_zero</a>&lt;T&gt;(token: <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt;) {
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a> { id, balance } = token;
    <b>assert</b>!(balance.<a href="../../dependencies/iota/token.md#iota_token_value">value</a>() == 0, <a href="../../dependencies/iota/token.md#iota_token_ENotZero">ENotZero</a>);
    balance.<a href="../../dependencies/iota/token.md#iota_token_destroy_zero">destroy_zero</a>();
    id.delete();
}
</code></pre>



</details>

<a name="iota_token_keep"></a>

## Function `keep`

Transfer the <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code> to the transaction sender.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_keep">keep</a>&lt;T&gt;(token: <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_keep">keep</a>&lt;T&gt;(token: <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt;, ctx: &<b>mut</b> TxContext) {
    transfer::transfer(token, ctx.<a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>())
}
</code></pre>



</details>

<a name="iota_token_new_request"></a>

## Function `new_request`

Create a new <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code>.
Publicly available method to allow for custom actions.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_new_request">new_request</a>&lt;T&gt;(name: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>: u64, <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;, <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;T&gt;&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_new_request">new_request</a>&lt;T&gt;(
    name: String,
    <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>: u64,
    <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>: Option&lt;<b>address</b>&gt;,
    <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>: Option&lt;Balance&lt;T&gt;&gt;,
    ctx: &TxContext,
): <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt; {
    <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a> {
        name,
        <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>,
        <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>,
        <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>,
        <a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>: ctx.<a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>(),
        <a href="../../dependencies/iota/token.md#iota_token_approvals">approvals</a>: vec_set::empty(),
    }
}
</code></pre>



</details>

<a name="iota_token_confirm_request"></a>

## Function `confirm_request`

Confirm the request against the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> and return the parameters
of the request: (Name, Amount, Sender, Recipient).

Cannot be used for <code><a href="../../dependencies/iota/token.md#iota_token_spend">spend</a></code> and similar actions that deliver <code><a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a></code>
to the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>. For those actions use <code><a href="../../dependencies/iota/token.md#iota_token_confirm_request_mut">confirm_request_mut</a></code>.

Aborts if:
- the action is not allowed (missing record in <code><a href="../../dependencies/iota/token.md#iota_token_rules">rules</a></code>)
- action contains <code><a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a></code> (use <code><a href="../../dependencies/iota/token.md#iota_token_confirm_request_mut">confirm_request_mut</a></code>)
- the <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code> does not meet the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> rules for the action


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_confirm_request">confirm_request</a>&lt;T&gt;(policy: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, request: <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;, _ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, u64, <b>address</b>, <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_confirm_request">confirm_request</a>&lt;T&gt;(
    policy: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;,
    request: <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;,
    _ctx: &<b>mut</b> TxContext,
): (String, u64, <b>address</b>, Option&lt;<b>address</b>&gt;) {
    <b>assert</b>!(request.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.is_none(), <a href="../../dependencies/iota/token.md#iota_token_ECantConsumeBalance">ECantConsumeBalance</a>);
    <b>assert</b>!(policy.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>.contains(&request.name), <a href="../../dependencies/iota/token.md#iota_token_EUnknownAction">EUnknownAction</a>);
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a> {
        name,
        <a href="../../dependencies/iota/token.md#iota_token_approvals">approvals</a>,
        <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>,
        <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>,
        <a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>,
        <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>,
    } = request;
    <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.destroy_none();
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_rules">rules</a> = &(*policy.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>.get(&name)).into_keys();
    <b>let</b> rules_len = <a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>.length();
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; rules_len) {
        <b>let</b> rule = &<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>[i];
        <b>assert</b>!(<a href="../../dependencies/iota/token.md#iota_token_approvals">approvals</a>.contains(rule), <a href="../../dependencies/iota/token.md#iota_token_ENotApproved">ENotApproved</a>);
        i = i + 1;
    };
    (name, <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>, <a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>, <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>)
}
</code></pre>



</details>

<a name="iota_token_confirm_request_mut"></a>

## Function `confirm_request_mut`

Confirm the request against the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> and return the parameters
of the request: (Name, Amount, Sender, Recipient).

Unlike <code><a href="../../dependencies/iota/token.md#iota_token_confirm_request">confirm_request</a></code> this function requires mutable access to the
<code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> and must be used on <code><a href="../../dependencies/iota/token.md#iota_token_spend">spend</a></code> action. After dealing with the
spent balance it calls <code><a href="../../dependencies/iota/token.md#iota_token_confirm_request">confirm_request</a></code> internally.

See <code><a href="../../dependencies/iota/token.md#iota_token_confirm_request">confirm_request</a></code> for the list of abort conditions.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_confirm_request_mut">confirm_request_mut</a>&lt;T&gt;(policy: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, request: <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, u64, <b>address</b>, <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_confirm_request_mut">confirm_request_mut</a>&lt;T&gt;(
    policy: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;,
    <b>mut</b> request: <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;,
    ctx: &<b>mut</b> TxContext,
): (String, u64, <b>address</b>, Option&lt;<b>address</b>&gt;) {
    <b>assert</b>!(policy.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>.contains(&request.name), <a href="../../dependencies/iota/token.md#iota_token_EUnknownAction">EUnknownAction</a>);
    <b>assert</b>!(request.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.is_some(), <a href="../../dependencies/iota/token.md#iota_token_EUseImmutableConfirm">EUseImmutableConfirm</a>);
    policy.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.<a href="../../dependencies/iota/token.md#iota_token_join">join</a>(request.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.extract());
    <a href="../../dependencies/iota/token.md#iota_token_confirm_request">confirm_request</a>(policy, request, ctx)
}
</code></pre>



</details>

<a name="iota_token_confirm_with_policy_cap"></a>

## Function `confirm_with_policy_cap`

Confirm an <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code> as the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code> owner. This function
allows <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> owner to perform Capability-gated actions ignoring
the ruleset specified in the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.

Aborts if request contains <code><a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a></code> due to inability of the
<code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code> to decrease supply. For scenarios like this a
<code>TreasuryCap</code> is required (see <code><a href="../../dependencies/iota/token.md#iota_token_confirm_with_treasury_cap">confirm_with_treasury_cap</a></code>).


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_confirm_with_policy_cap">confirm_with_policy_cap</a>&lt;T&gt;(_policy_cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">iota::token::TokenPolicyCap</a>&lt;T&gt;, request: <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;, _ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, u64, <b>address</b>, <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_confirm_with_policy_cap">confirm_with_policy_cap</a>&lt;T&gt;(
    _policy_cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a>&lt;T&gt;,
    request: <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;,
    _ctx: &<b>mut</b> TxContext,
): (String, u64, <b>address</b>, Option&lt;<b>address</b>&gt;) {
    <b>assert</b>!(request.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.is_none(), <a href="../../dependencies/iota/token.md#iota_token_ECantConsumeBalance">ECantConsumeBalance</a>);
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a> {
        name,
        <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>,
        <a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>,
        <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>,
        <a href="../../dependencies/iota/token.md#iota_token_approvals">approvals</a>: _,
        <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>,
    } = request;
    <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.destroy_none();
    (name, <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>, <a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>, <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>)
}
</code></pre>



</details>

<a name="iota_token_confirm_with_treasury_cap"></a>

## Function `confirm_with_treasury_cap`

Confirm an <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code> as the <code>TreasuryCap</code> owner. This function
allows <code>TreasuryCap</code> owner to perform Capability-gated actions ignoring
the ruleset specified in the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.

Unlike <code><a href="../../dependencies/iota/token.md#iota_token_confirm_with_policy_cap">confirm_with_policy_cap</a></code> this function allows <code><a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a></code>
to be consumed, decreasing the <code>total_supply</code> of the <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_confirm_with_treasury_cap">confirm_with_treasury_cap</a>&lt;T&gt;(treasury_cap: &<b>mut</b> <a href="../../dependencies/iota/coin.md#iota_coin_TreasuryCap">iota::coin::TreasuryCap</a>&lt;T&gt;, request: <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;, _ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, u64, <b>address</b>, <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_confirm_with_treasury_cap">confirm_with_treasury_cap</a>&lt;T&gt;(
    treasury_cap: &<b>mut</b> TreasuryCap&lt;T&gt;,
    request: <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;,
    _ctx: &<b>mut</b> TxContext,
): (String, u64, <b>address</b>, Option&lt;<b>address</b>&gt;) {
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a> {
        name,
        <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>,
        <a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>,
        <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>,
        <a href="../../dependencies/iota/token.md#iota_token_approvals">approvals</a>: _,
        <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>,
    } = request;
    <b>if</b> (<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.is_some()) {
        treasury_cap.supply_mut().decrease_supply(<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.destroy_some());
    } <b>else</b> {
        <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.destroy_none();
    };
    (name, <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>, <a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>, <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>)
}
</code></pre>



</details>

<a name="iota_token_add_approval"></a>

## Function `add_approval`

Add an "approval" to the <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code> by providing a Witness.
Intended to be used by Rules to add their own approvals, however, can
be used to add arbitrary approvals to the request (not only the ones
required by the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>).


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_add_approval">add_approval</a>&lt;T, W: drop&gt;(_t: W, request: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;, _ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_add_approval">add_approval</a>&lt;T, W: drop&gt;(_t: W, request: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;, _ctx: &<b>mut</b> TxContext) {
    request.<a href="../../dependencies/iota/token.md#iota_token_approvals">approvals</a>.insert(type_name::get&lt;W&gt;())
}
</code></pre>



</details>

<a name="iota_token_add_rule_config"></a>

## Function `add_rule_config`

Add a <code>Config</code> for a <code>Rule</code> in the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>. Rule configuration is
independent from the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a></code> and needs to be managed by the
Rule itself. Configuration is stored per <code>Rule</code> and not per <code>Rule</code> per
<code>Action</code> to allow reuse in different actions.

- Rule witness guarantees that the <code>Config</code> is approved by the Rule.
- <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code> guarantees that the <code>Config</code> setup is initiated by
the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> owner.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_add_rule_config">add_rule_config</a>&lt;T, Rule: drop, Config: store&gt;(_rule: Rule, self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">iota::token::TokenPolicyCap</a>&lt;T&gt;, config: Config, _ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_add_rule_config">add_rule_config</a>&lt;T, Rule: drop, Config: store&gt;(
    _rule: Rule,
    self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;,
    cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a>&lt;T&gt;,
    config: Config,
    _ctx: &<b>mut</b> TxContext,
) {
    <b>assert</b>!(object::id(self) == cap.`<b>for</b>`, <a href="../../dependencies/iota/token.md#iota_token_ENotAuthorized">ENotAuthorized</a>);
    df::add(&<b>mut</b> self.id, <a href="../../dependencies/iota/token.md#iota_token_key">key</a>&lt;Rule&gt;(), config)
}
</code></pre>



</details>

<a name="iota_token_rule_config"></a>

## Function `rule_config`

Get a <code>Config</code> for a <code>Rule</code> in the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>. Requires <code>Rule</code>
witness, hence can only be read by the <code>Rule</code> itself. This requirement
guarantees safety of the stored <code>Config</code> and allows for simpler dynamic
field management inside the Rule Config (custom type keys are not needed
for access gating).

Aborts if the Config is not present.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_rule_config">rule_config</a>&lt;T, Rule: drop, Config: store&gt;(_rule: Rule, self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;): &Config
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_rule_config">rule_config</a>&lt;T, Rule: drop, Config: store&gt;(_rule: Rule, self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;): &Config {
    <b>assert</b>!(<a href="../../dependencies/iota/token.md#iota_token_has_rule_config_with_type">has_rule_config_with_type</a>&lt;T, Rule, Config&gt;(self), <a href="../../dependencies/iota/token.md#iota_token_ENoConfig">ENoConfig</a>);
    df::borrow(&self.id, <a href="../../dependencies/iota/token.md#iota_token_key">key</a>&lt;Rule&gt;())
}
</code></pre>



</details>

<a name="iota_token_rule_config_mut"></a>

## Function `rule_config_mut`

Get mutable access to the <code>Config</code> for a <code>Rule</code> in the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.
Requires <code>Rule</code> witness, hence can only be read by the <code>Rule</code> itself,
as well as <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code> to guarantee that the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> owner
is the one who initiated the <code>Config</code> modification.

Aborts if:
- the Config is not present
- <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code> is not matching the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_rule_config_mut">rule_config_mut</a>&lt;T, Rule: drop, Config: store&gt;(_rule: Rule, self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">iota::token::TokenPolicyCap</a>&lt;T&gt;): &<b>mut</b> Config
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_rule_config_mut">rule_config_mut</a>&lt;T, Rule: drop, Config: store&gt;(
    _rule: Rule,
    self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;,
    cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a>&lt;T&gt;,
): &<b>mut</b> Config {
    <b>assert</b>!(<a href="../../dependencies/iota/token.md#iota_token_has_rule_config_with_type">has_rule_config_with_type</a>&lt;T, Rule, Config&gt;(self), <a href="../../dependencies/iota/token.md#iota_token_ENoConfig">ENoConfig</a>);
    <b>assert</b>!(object::id(self) == cap.`<b>for</b>`, <a href="../../dependencies/iota/token.md#iota_token_ENotAuthorized">ENotAuthorized</a>);
    df::borrow_mut(&<b>mut</b> self.id, <a href="../../dependencies/iota/token.md#iota_token_key">key</a>&lt;Rule&gt;())
}
</code></pre>



</details>

<a name="iota_token_remove_rule_config"></a>

## Function `remove_rule_config`

Remove a <code>Config</code> for a <code>Rule</code> in the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.
Unlike the <code><a href="../../dependencies/iota/token.md#iota_token_add_rule_config">add_rule_config</a></code>, this function does not require a <code>Rule</code>
witness, hence can be performed by the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> owner on their own.

Rules need to make sure that the <code>Config</code> is present when performing
verification of the <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code>.

Aborts if:
- the Config is not present
- <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code> is not matching the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_remove_rule_config">remove_rule_config</a>&lt;T, Rule, Config: store&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">iota::token::TokenPolicyCap</a>&lt;T&gt;, _ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): Config
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_remove_rule_config">remove_rule_config</a>&lt;T, Rule, Config: store&gt;(
    self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;,
    cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a>&lt;T&gt;,
    _ctx: &<b>mut</b> TxContext,
): Config {
    <b>assert</b>!(<a href="../../dependencies/iota/token.md#iota_token_has_rule_config_with_type">has_rule_config_with_type</a>&lt;T, Rule, Config&gt;(self), <a href="../../dependencies/iota/token.md#iota_token_ENoConfig">ENoConfig</a>);
    <b>assert</b>!(object::id(self) == cap.`<b>for</b>`, <a href="../../dependencies/iota/token.md#iota_token_ENotAuthorized">ENotAuthorized</a>);
    df::remove(&<b>mut</b> self.id, <a href="../../dependencies/iota/token.md#iota_token_key">key</a>&lt;Rule&gt;())
}
</code></pre>



</details>

<a name="iota_token_has_rule_config"></a>

## Function `has_rule_config`

Check if a config for a <code>Rule</code> is set in the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> without
checking the type of the <code>Config</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_has_rule_config">has_rule_config</a>&lt;T, Rule&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_has_rule_config">has_rule_config</a>&lt;T, Rule&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;): bool {
    df::exists_&lt;<a href="../../dependencies/iota/token.md#iota_token_RuleKey">RuleKey</a>&lt;Rule&gt;&gt;(&self.id, <a href="../../dependencies/iota/token.md#iota_token_key">key</a>&lt;Rule&gt;())
}
</code></pre>



</details>

<a name="iota_token_has_rule_config_with_type"></a>

## Function `has_rule_config_with_type`

Check if a <code>Config</code> for a <code>Rule</code> is set in the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code> and that
it matches the type provided.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_has_rule_config_with_type">has_rule_config_with_type</a>&lt;T, Rule, Config: store&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_has_rule_config_with_type">has_rule_config_with_type</a>&lt;T, Rule, Config: store&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;): bool {
    df::exists_with_type&lt;<a href="../../dependencies/iota/token.md#iota_token_RuleKey">RuleKey</a>&lt;Rule&gt;, Config&gt;(&self.id, <a href="../../dependencies/iota/token.md#iota_token_key">key</a>&lt;Rule&gt;())
}
</code></pre>



</details>

<a name="iota_token_allow"></a>

## Function `allow`

Allows an <code><a href="../../dependencies/iota/token.md#iota_token_action">action</a></code> to be performed on the <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code> freely by adding an
empty set of <code>Rules</code> for the <code><a href="../../dependencies/iota/token.md#iota_token_action">action</a></code>.

Aborts if the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code> is not matching the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_allow">allow</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">iota::token::TokenPolicyCap</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, _ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_allow">allow</a>&lt;T&gt;(
    self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;,
    cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a>&lt;T&gt;,
    <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: String,
    _ctx: &<b>mut</b> TxContext,
) {
    <b>assert</b>!(object::id(self) == cap.`<b>for</b>`, <a href="../../dependencies/iota/token.md#iota_token_ENotAuthorized">ENotAuthorized</a>);
    self.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>.insert(<a href="../../dependencies/iota/token.md#iota_token_action">action</a>, vec_set::empty());
}
</code></pre>



</details>

<a name="iota_token_disallow"></a>

## Function `disallow`

Completely disallows an <code><a href="../../dependencies/iota/token.md#iota_token_action">action</a></code> on the <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code> by removing the record
from the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a></code>.

Aborts if the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code> is not matching the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_disallow">disallow</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">iota::token::TokenPolicyCap</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, _ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_disallow">disallow</a>&lt;T&gt;(
    self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;,
    cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a>&lt;T&gt;,
    <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: String,
    _ctx: &<b>mut</b> TxContext,
) {
    <b>assert</b>!(object::id(self) == cap.`<b>for</b>`, <a href="../../dependencies/iota/token.md#iota_token_ENotAuthorized">ENotAuthorized</a>);
    self.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>.remove(&<a href="../../dependencies/iota/token.md#iota_token_action">action</a>);
}
</code></pre>



</details>

<a name="iota_token_add_rule_for_action"></a>

## Function `add_rule_for_action`

Adds a Rule for an action with <code>name</code> in the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.

Aborts if the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code> is not matching the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_add_rule_for_action">add_rule_for_action</a>&lt;T, Rule: drop&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">iota::token::TokenPolicyCap</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_add_rule_for_action">add_rule_for_action</a>&lt;T, Rule: drop&gt;(
    self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;,
    cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a>&lt;T&gt;,
    <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: String,
    ctx: &<b>mut</b> TxContext,
) {
    <b>assert</b>!(object::id(self) == cap.`<b>for</b>`, <a href="../../dependencies/iota/token.md#iota_token_ENotAuthorized">ENotAuthorized</a>);
    <b>if</b> (!self.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>.contains(&<a href="../../dependencies/iota/token.md#iota_token_action">action</a>)) {
        <a href="../../dependencies/iota/token.md#iota_token_allow">allow</a>(self, cap, <a href="../../dependencies/iota/token.md#iota_token_action">action</a>, ctx);
    };
    self.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>.get_mut(&<a href="../../dependencies/iota/token.md#iota_token_action">action</a>).insert(type_name::get&lt;Rule&gt;())
}
</code></pre>



</details>

<a name="iota_token_remove_rule_for_action"></a>

## Function `remove_rule_for_action`

Removes a rule for an action with <code>name</code> in the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>. Returns
the config object to be handled by the sender (or a Rule itself).

Aborts if the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a></code> is not matching the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_remove_rule_for_action">remove_rule_for_action</a>&lt;T, Rule: drop&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">iota::token::TokenPolicyCap</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, _ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_remove_rule_for_action">remove_rule_for_action</a>&lt;T, Rule: drop&gt;(
    self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;,
    cap: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicyCap">TokenPolicyCap</a>&lt;T&gt;,
    <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: String,
    _ctx: &<b>mut</b> TxContext,
) {
    <b>assert</b>!(object::id(self) == cap.`<b>for</b>`, <a href="../../dependencies/iota/token.md#iota_token_ENotAuthorized">ENotAuthorized</a>);
    self.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>.get_mut(&<a href="../../dependencies/iota/token.md#iota_token_action">action</a>).remove(&type_name::get&lt;Rule&gt;())
}
</code></pre>



</details>

<a name="iota_token_mint"></a>

## Function `mint`

Mint a <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code> with a given <code><a href="../../dependencies/iota/token.md#iota_token_amount">amount</a></code> using the <code>TreasuryCap</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_mint">mint</a>&lt;T&gt;(cap: &<b>mut</b> <a href="../../dependencies/iota/coin.md#iota_coin_TreasuryCap">iota::coin::TreasuryCap</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_mint">mint</a>&lt;T&gt;(cap: &<b>mut</b> TreasuryCap&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>: u64, ctx: &<b>mut</b> TxContext): <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt; {
    <b>let</b> balance = cap.supply_mut().increase_supply(<a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>);
    <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a> { id: object::new(ctx), balance }
}
</code></pre>



</details>

<a name="iota_token_burn"></a>

## Function `burn`

Burn a <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code> using the <code>TreasuryCap</code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_burn">burn</a>&lt;T&gt;(cap: &<b>mut</b> <a href="../../dependencies/iota/coin.md#iota_coin_TreasuryCap">iota::coin::TreasuryCap</a>&lt;T&gt;, token: <a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_burn">burn</a>&lt;T&gt;(cap: &<b>mut</b> TreasuryCap&lt;T&gt;, token: <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt;) {
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_Token">Token</a> { id, balance } = token;
    cap.supply_mut().decrease_supply(balance);
    id.delete();
}
</code></pre>



</details>

<a name="iota_token_flush"></a>

## Function `flush`

Flush the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a></code> into the <code>TreasuryCap</code>. This
action is only available to the <code>TreasuryCap</code> owner.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_flush">flush</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, cap: &<b>mut</b> <a href="../../dependencies/iota/coin.md#iota_coin_TreasuryCap">iota::coin::TreasuryCap</a>&lt;T&gt;, _ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_flush">flush</a>&lt;T&gt;(
    self: &<b>mut</b> <a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;,
    cap: &<b>mut</b> TreasuryCap&lt;T&gt;,
    _ctx: &<b>mut</b> TxContext,
): u64 {
    <b>let</b> <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a> = self.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.<a href="../../dependencies/iota/token.md#iota_token_value">value</a>();
    <b>let</b> balance = self.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.<a href="../../dependencies/iota/token.md#iota_token_split">split</a>(<a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>);
    cap.supply_mut().decrease_supply(balance)
}
</code></pre>



</details>

<a name="iota_token_is_allowed"></a>

## Function `is_allowed`

Check whether an action is present in the rules VecMap.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_is_allowed">is_allowed</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: &<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_is_allowed">is_allowed</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: &String): bool {
    self.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>.contains(<a href="../../dependencies/iota/token.md#iota_token_action">action</a>)
}
</code></pre>



</details>

<a name="iota_token_rules"></a>

## Function `rules`

Returns the rules required for a specific action.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: &<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>): <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;, <a href="../../dependencies/iota/token.md#iota_token_action">action</a>: &String): VecSet&lt;TypeName&gt; {
    *self.<a href="../../dependencies/iota/token.md#iota_token_rules">rules</a>.get(<a href="../../dependencies/iota/token.md#iota_token_action">action</a>)
}
</code></pre>



</details>

<a name="iota_token_spent_balance"></a>

## Function `spent_balance`

Returns the <code><a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a></code> of the <code><a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">iota::token::TokenPolicy</a>&lt;T&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_TokenPolicy">TokenPolicy</a>&lt;T&gt;): u64 {
    self.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.<a href="../../dependencies/iota/token.md#iota_token_value">value</a>()
}
</code></pre>



</details>

<a name="iota_token_value"></a>

## Function `value`

Returns the <code>balance</code> of the <code><a href="../../dependencies/iota/token.md#iota_token_Token">Token</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_value">value</a>&lt;T&gt;(t: &<a href="../../dependencies/iota/token.md#iota_token_Token">iota::token::Token</a>&lt;T&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_value">value</a>&lt;T&gt;(t: &<a href="../../dependencies/iota/token.md#iota_token_Token">Token</a>&lt;T&gt;): u64 {
    t.balance.<a href="../../dependencies/iota/token.md#iota_token_value">value</a>()
}
</code></pre>



</details>

<a name="iota_token_transfer_action"></a>

## Function `transfer_action`

Name of the Transfer action.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_transfer_action">transfer_action</a>(): <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_transfer_action">transfer_action</a>(): String {
    <b>let</b> transfer_str = <a href="../../dependencies/iota/token.md#iota_token_TRANSFER">TRANSFER</a>;
    transfer_str.to_string()
}
</code></pre>



</details>

<a name="iota_token_spend_action"></a>

## Function `spend_action`

Name of the <code>Spend</code> action.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_spend_action">spend_action</a>(): <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_spend_action">spend_action</a>(): String {
    <b>let</b> spend_str = <a href="../../dependencies/iota/token.md#iota_token_SPEND">SPEND</a>;
    spend_str.to_string()
}
</code></pre>



</details>

<a name="iota_token_to_coin_action"></a>

## Function `to_coin_action`

Name of the <code>ToCoin</code> action.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_to_coin_action">to_coin_action</a>(): <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_to_coin_action">to_coin_action</a>(): String {
    <b>let</b> to_coin_str = <a href="../../dependencies/iota/token.md#iota_token_TO_COIN">TO_COIN</a>;
    to_coin_str.to_string()
}
</code></pre>



</details>

<a name="iota_token_from_coin_action"></a>

## Function `from_coin_action`

Name of the <code>FromCoin</code> action.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_from_coin_action">from_coin_action</a>(): <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_from_coin_action">from_coin_action</a>(): String {
    <b>let</b> from_coin_str = <a href="../../dependencies/iota/token.md#iota_token_FROM_COIN">FROM_COIN</a>;
    from_coin_str.to_string()
}
</code></pre>



</details>

<a name="iota_token_action"></a>

## Function `action`

The Action in the <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_action">action</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;): <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_action">action</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;): String { self.name }
</code></pre>



</details>

<a name="iota_token_amount"></a>

## Function `amount`

Amount of the <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_amount">amount</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;): u64 { self.<a href="../../dependencies/iota/token.md#iota_token_amount">amount</a> }
</code></pre>



</details>

<a name="iota_token_sender"></a>

## Function `sender`

Sender of the <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;): <b>address</b>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_sender">sender</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;): <b>address</b> { self.<a href="../../dependencies/iota/token.md#iota_token_sender">sender</a> }
</code></pre>



</details>

<a name="iota_token_recipient"></a>

## Function `recipient`

Recipient of the <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;): Option&lt;<b>address</b>&gt; {
    self.<a href="../../dependencies/iota/token.md#iota_token_recipient">recipient</a>
}
</code></pre>



</details>

<a name="iota_token_approvals"></a>

## Function `approvals`

Approvals of the <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_approvals">approvals</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;): <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_approvals">approvals</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;): VecSet&lt;TypeName&gt; {
    self.<a href="../../dependencies/iota/token.md#iota_token_approvals">approvals</a>
}
</code></pre>



</details>

<a name="iota_token_spent"></a>

## Function `spent`

Burned balance of the <code><a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_spent">spent</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">iota::token::ActionRequest</a>&lt;T&gt;): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_spent">spent</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/token.md#iota_token_ActionRequest">ActionRequest</a>&lt;T&gt;): Option&lt;u64&gt; {
    <b>if</b> (self.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.is_some()) {
        option::some(self.<a href="../../dependencies/iota/token.md#iota_token_spent_balance">spent_balance</a>.borrow().<a href="../../dependencies/iota/token.md#iota_token_value">value</a>())
    } <b>else</b> {
        option::none()
    }
}
</code></pre>



</details>

<a name="iota_token_key"></a>

## Function `key`

Create a new <code><a href="../../dependencies/iota/token.md#iota_token_RuleKey">RuleKey</a></code> for a <code>Rule</code>. The <code>is_protected</code> field is kept
for potential future use, if Rules were to have a freely modifiable
storage as addition / replacement for the <code>Config</code> system.

The goal of <code>is_protected</code> is to potentially allow Rules store a mutable
version of their configuration and mutate state on user action.


<pre><code><b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_key">key</a>&lt;Rule&gt;(): <a href="../../dependencies/iota/token.md#iota_token_RuleKey">iota::token::RuleKey</a>&lt;Rule&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/token.md#iota_token_key">key</a>&lt;Rule&gt;(): <a href="../../dependencies/iota/token.md#iota_token_RuleKey">RuleKey</a>&lt;Rule&gt; { <a href="../../dependencies/iota/token.md#iota_token_RuleKey">RuleKey</a> { is_protected: <b>true</b> } }
</code></pre>



</details>
