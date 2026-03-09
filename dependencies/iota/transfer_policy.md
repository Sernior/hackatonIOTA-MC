
<a name="iota_transfer_policy"></a>

# Module `iota::transfer_policy`

Defines the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code> type and the logic to approve <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code>s.

- TransferPolicy - is a highly customizable primitive, which provides an
interface for the type owner to set custom transfer rules for every
deal performed in the <code>Kiosk</code> or a similar system that integrates with TP.

- Once a <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;</code> is created for and shared (or frozen), the
type <code>T</code> becomes tradable in <code>Kiosk</code>s. On every purchase operation, a
<code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code> is created and needs to be confirmed by the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>
hot potato or transaction will fail.

- Type owner (creator) can set any Rules as long as the ecosystem supports
them. All of the Rules need to be resolved within a single transaction (eg
pay royalty and pay fixed commission). Once required actions are performed,
the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code> can be "confirmed" via <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_confirm_request">confirm_request</a></code> call.

- <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code> aims to be the main interface for creators to control trades
of their types and collect profits if a fee is required on sales. Custom
policies can be removed at any moment, and the change will affect all instances
of the type at once.


-  [Struct `TransferRequest`](#iota_transfer_policy_TransferRequest)
-  [Struct `TransferPolicy`](#iota_transfer_policy_TransferPolicy)
-  [Struct `TransferPolicyCap`](#iota_transfer_policy_TransferPolicyCap)
-  [Struct `TransferPolicyCreated`](#iota_transfer_policy_TransferPolicyCreated)
-  [Struct `TransferPolicyDestroyed`](#iota_transfer_policy_TransferPolicyDestroyed)
-  [Struct `RuleKey`](#iota_transfer_policy_RuleKey)
-  [Constants](#@Constants_0)
-  [Function `new_request`](#iota_transfer_policy_new_request)
-  [Function `new`](#iota_transfer_policy_new)
-  [Function `default`](#iota_transfer_policy_default)
-  [Function `withdraw`](#iota_transfer_policy_withdraw)
-  [Function `destroy_and_withdraw`](#iota_transfer_policy_destroy_and_withdraw)
-  [Function `confirm_request`](#iota_transfer_policy_confirm_request)
-  [Function `add_rule`](#iota_transfer_policy_add_rule)
-  [Function `get_rule`](#iota_transfer_policy_get_rule)
-  [Function `add_to_balance`](#iota_transfer_policy_add_to_balance)
-  [Function `add_receipt`](#iota_transfer_policy_add_receipt)
-  [Function `has_rule`](#iota_transfer_policy_has_rule)
-  [Function `remove_rule`](#iota_transfer_policy_remove_rule)
-  [Function `uid`](#iota_transfer_policy_uid)
-  [Function `uid_mut_as_owner`](#iota_transfer_policy_uid_mut_as_owner)
-  [Function `rules`](#iota_transfer_policy_rules)
-  [Function `item`](#iota_transfer_policy_item)
-  [Function `paid`](#iota_transfer_policy_paid)
-  [Function `from`](#iota_transfer_policy_from)


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
<b>use</b> <a href="../../dependencies/iota/iota.md#iota_iota">iota::iota</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/package.md#iota_package">iota::package</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/iota/vec_set.md#iota_vec_set">iota::vec_set</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_transfer_policy_TransferRequest"></a>

## Struct `TransferRequest`

A "Hot Potato" forcing the buyer to get a transfer permission
from the item type (<code>T</code>) owner on purchase attempt.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a>&lt;<b>phantom</b> T&gt;
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_item">item</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 The ID of the transferred item. Although the <code>T</code> has no
 constraints, the main use case for this module is to work
 with Objects.
</dd>
<dt>
<code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_paid">paid</a>: u64</code>
</dt>
<dd>
 Amount of IOTA paid for the item. Can be used to
 calculate the fee / transfer policy enforcement.
</dd>
<dt>
<code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_from">from</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 The ID of the Kiosk / Safe the object is being sold from.
 Can be used by the TransferPolicy implementors.
</dd>
<dt>
<code>receipts: <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>&gt;</code>
</dt>
<dd>
 Collected Receipts. Used to verify that all of the rules
 were followed and <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code> can be confirmed.
</dd>
</dl>


</details>

<a name="iota_transfer_policy_TransferPolicy"></a>

## Struct `TransferPolicy`

A unique capability that allows the owner of the <code>T</code> to authorize
transfers. Can only be created with the <code>Publisher</code> object. Although
there's no limitation to how many policies can be created, for most
of the cases there's no need to create more than one since any of the
policies can be used to confirm the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;<b>phantom</b> T&gt; <b>has</b> key, store
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
<code>balance: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;</code>
</dt>
<dd>
 The Balance of the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code> which collects <code>IOTA</code>.
 By default, transfer policy does not collect anything , and it's
 a matter of an implementation of a specific rule - whether to add
 to balance and how much.
</dd>
<dt>
<code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_rules">rules</a>: <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>&gt;</code>
</dt>
<dd>
 Set of types of attached rules - used to verify <code>receipts</code> when
 a <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code> is received in <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_confirm_request">confirm_request</a></code> function.
 Additionally provides a way to look up currently attached Rules.
</dd>
</dl>


</details>

<a name="iota_transfer_policy_TransferPolicyCap"></a>

## Struct `TransferPolicyCap`

A Capability granting the owner permission to add/remove rules as well
as to <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_withdraw">withdraw</a></code> and <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_destroy_and_withdraw">destroy_and_withdraw</a></code> the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a>&lt;<b>phantom</b> T&gt; <b>has</b> key, store
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
<code>policy_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_transfer_policy_TransferPolicyCreated"></a>

## Struct `TransferPolicyCreated`

Event that is emitted when a publisher creates a new <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a></code>
making the discoverability and tracking the supported types easier.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCreated">TransferPolicyCreated</a>&lt;<b>phantom</b> T&gt; <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_transfer_policy_TransferPolicyDestroyed"></a>

## Struct `TransferPolicyDestroyed`

Event that is emitted when a publisher destroys a <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a></code>.
Allows for tracking supported policies.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyDestroyed">TransferPolicyDestroyed</a>&lt;<b>phantom</b> T&gt; <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_transfer_policy_RuleKey"></a>

## Struct `RuleKey`

Key to store "Rule" configuration for a specific <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_RuleKey">RuleKey</a>&lt;<b>phantom</b> T: drop&gt; <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_transfer_policy_EPolicyNotSatisfied"></a>

The number of receipts does not match the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code> requirement.


<pre><code><b>const</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_EPolicyNotSatisfied">EPolicyNotSatisfied</a>: u64 = 0;
</code></pre>



<a name="iota_transfer_policy_EIllegalRule"></a>

A completed rule is not set in the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>.


<pre><code><b>const</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_EIllegalRule">EIllegalRule</a>: u64 = 1;
</code></pre>



<a name="iota_transfer_policy_EUnknownRequirement"></a>

A Rule is not set.


<pre><code><b>const</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_EUnknownRequirement">EUnknownRequirement</a>: u64 = 2;
</code></pre>



<a name="iota_transfer_policy_ERuleAlreadySet"></a>

Attempting to create a Rule that is already set.


<pre><code><b>const</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_ERuleAlreadySet">ERuleAlreadySet</a>: u64 = 3;
</code></pre>



<a name="iota_transfer_policy_ENotOwner"></a>

Trying to <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_withdraw">withdraw</a></code> or <code>close_and_withdraw</code> with a wrong Cap.


<pre><code><b>const</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_ENotOwner">ENotOwner</a>: u64 = 4;
</code></pre>



<a name="iota_transfer_policy_ENotEnough"></a>

Trying to <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_withdraw">withdraw</a></code> more than there is.


<pre><code><b>const</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_ENotEnough">ENotEnough</a>: u64 = 5;
</code></pre>



<a name="iota_transfer_policy_new_request"></a>

## Function `new_request`

Construct a new <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code> hot potato which requires an
approving action from the creator to be destroyed / resolved. Once
created, it must be confirmed in the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_confirm_request">confirm_request</a></code> call otherwise
the transaction will fail.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_new_request">new_request</a>&lt;T&gt;(<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_item">item</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_paid">paid</a>: u64, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_from">from</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">iota::transfer_policy::TransferRequest</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_new_request">new_request</a>&lt;T&gt;(<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_item">item</a>: ID, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_paid">paid</a>: u64, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_from">from</a>: ID): <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a>&lt;T&gt; {
    <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a> { <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_item">item</a>, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_paid">paid</a>, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_from">from</a>, receipts: vec_set::empty() }
}
</code></pre>



</details>

<a name="iota_transfer_policy_new"></a>

## Function `new`

Register a type in the Kiosk system and receive a <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code> and
a <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a></code> for the type. The <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code> is required to
confirm kiosk deals for the <code>T</code>. If there's no <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>
available for use, the type can not be traded in kiosks.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_new">new</a>&lt;T&gt;(pub: &<a href="../../dependencies/iota/package.md#iota_package_Publisher">iota::package::Publisher</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">iota::transfer_policy::TransferPolicyCap</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_new">new</a>&lt;T&gt;(pub: &Publisher, ctx: &<b>mut</b> TxContext): (<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a>&lt;T&gt;) {
    <b>assert</b>!(package::from_package&lt;T&gt;(pub), 0);
    <b>let</b> id = object::new(ctx);
    <b>let</b> policy_id = id.to_inner();
    event::emit(<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCreated">TransferPolicyCreated</a>&lt;T&gt; { id: policy_id });
    (
        <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a> { id, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_rules">rules</a>: vec_set::empty(), balance: balance::zero() },
        <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a> { id: object::new(ctx), policy_id },
    )
}
</code></pre>



</details>

<a name="iota_transfer_policy_default"></a>

## Function `default`

Initialize the Transfer Policy in the default scenario: Create and share
the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>, transfer <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a></code> to the transaction
sender.


<pre><code><b>entry</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_default">default</a>&lt;T&gt;(pub: &<a href="../../dependencies/iota/package.md#iota_package_Publisher">iota::package::Publisher</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>entry</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_default">default</a>&lt;T&gt;(pub: &Publisher, ctx: &<b>mut</b> TxContext) {
    <b>let</b> (policy, cap) = <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_new">new</a>&lt;T&gt;(pub, ctx);
    <a href="../../dependencies/iota/transfer.md#iota_transfer_share_object">iota::transfer::share_object</a>(policy);
    <a href="../../dependencies/iota/transfer.md#iota_transfer_transfer">iota::transfer::transfer</a>(cap, ctx.sender());
}
</code></pre>



</details>

<a name="iota_transfer_policy_withdraw"></a>

## Function `withdraw`

Withdraw some amount of profits from the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>. If amount
is not specified, all profits are withdrawn.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_withdraw">withdraw</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">iota::transfer_policy::TransferPolicyCap</a>&lt;T&gt;, amount: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_withdraw">withdraw</a>&lt;T&gt;(
    self: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;,
    cap: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a>&lt;T&gt;,
    amount: Option&lt;u64&gt;,
    ctx: &<b>mut</b> TxContext,
): Coin&lt;IOTA&gt; {
    <b>assert</b>!(object::id(self) == cap.policy_id, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_ENotOwner">ENotOwner</a>);
    <b>let</b> amount = <b>if</b> (amount.is_some()) {
        <b>let</b> amt = amount.destroy_some();
        <b>assert</b>!(amt &lt;= self.balance.value(), <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_ENotEnough">ENotEnough</a>);
        amt
    } <b>else</b> {
        self.balance.value()
    };
    coin::take(&<b>mut</b> self.balance, amount, ctx)
}
</code></pre>



</details>

<a name="iota_transfer_policy_destroy_and_withdraw"></a>

## Function `destroy_and_withdraw`

Destroy a TransferPolicyCap.
Can be performed by any party as long as they own it.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_destroy_and_withdraw">destroy_and_withdraw</a>&lt;T&gt;(self: <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;, cap: <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">iota::transfer_policy::TransferPolicyCap</a>&lt;T&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_destroy_and_withdraw">destroy_and_withdraw</a>&lt;T&gt;(
    self: <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;,
    cap: <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a>&lt;T&gt;,
    ctx: &<b>mut</b> TxContext,
): Coin&lt;IOTA&gt; {
    <b>assert</b>!(object::id(&self) == cap.policy_id, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_ENotOwner">ENotOwner</a>);
    <b>let</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a> { id: cap_id, policy_id } = cap;
    <b>let</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a> { id, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_rules">rules</a>: _, balance } = self;
    id.delete();
    cap_id.delete();
    event::emit(<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyDestroyed">TransferPolicyDestroyed</a>&lt;T&gt; { id: policy_id });
    balance.into_coin(ctx)
}
</code></pre>



</details>

<a name="iota_transfer_policy_confirm_request"></a>

## Function `confirm_request`

Allow a <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code> for the type <code>T</code>. The call is protected
by the type constraint, as only the publisher of the <code>T</code> can get
<code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;</code>.

Note: unless there's a policy for <code>T</code> to allow transfers,
Kiosk trades will not be possible.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_confirm_request">confirm_request</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;, request: <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">iota::transfer_policy::TransferRequest</a>&lt;T&gt;): (<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, u64, <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_confirm_request">confirm_request</a>&lt;T&gt;(
    self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;,
    request: <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a>&lt;T&gt;,
): (ID, u64, ID) {
    <b>let</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a> { <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_item">item</a>, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_paid">paid</a>, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_from">from</a>, receipts } = request;
    <b>let</b> <b>mut</b> completed = receipts.into_keys();
    <b>let</b> <b>mut</b> total = completed.length();
    <b>assert</b>!(total == self.<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_rules">rules</a>.size(), <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_EPolicyNotSatisfied">EPolicyNotSatisfied</a>);
    <b>while</b> (total &gt; 0) {
        <b>let</b> rule_type = completed.pop_back();
        <b>assert</b>!(self.<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_rules">rules</a>.contains(&rule_type), <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_EIllegalRule">EIllegalRule</a>);
        total = total - 1;
    };
    (<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_item">item</a>, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_paid">paid</a>, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_from">from</a>)
}
</code></pre>



</details>

<a name="iota_transfer_policy_add_rule"></a>

## Function `add_rule`

Add a custom Rule to the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>. Once set, <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code> must
receive a confirmation of the rule executed so the hot potato can be unpacked.

- T: the type to which TransferPolicy<T> is applied.
- Rule: the witness type for the Custom rule
- Config: a custom configuration for the rule

Config requires <code>drop</code> to allow creators to remove any policy at any moment,
even if graceful unpacking has not been implemented in a "rule module".


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_add_rule">add_rule</a>&lt;T, Rule: drop, Config: drop, store&gt;(_: Rule, policy: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">iota::transfer_policy::TransferPolicyCap</a>&lt;T&gt;, cfg: Config)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_add_rule">add_rule</a>&lt;T, Rule: drop, Config: store + drop&gt;(
    _: Rule,
    policy: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;,
    cap: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a>&lt;T&gt;,
    cfg: Config,
) {
    <b>assert</b>!(object::id(policy) == cap.policy_id, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_ENotOwner">ENotOwner</a>);
    <b>assert</b>!(!<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_has_rule">has_rule</a>&lt;T, Rule&gt;(policy), <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_ERuleAlreadySet">ERuleAlreadySet</a>);
    df::add(&<b>mut</b> policy.id, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_RuleKey">RuleKey</a>&lt;Rule&gt; {}, cfg);
    policy.<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_rules">rules</a>.insert(type_name::get&lt;Rule&gt;())
}
</code></pre>



</details>

<a name="iota_transfer_policy_get_rule"></a>

## Function `get_rule`

Get the custom Config for the Rule (can be only one per "Rule" type).


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_get_rule">get_rule</a>&lt;T, Rule: drop, Config: drop, store&gt;(_: Rule, policy: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;): &Config
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_get_rule">get_rule</a>&lt;T, Rule: drop, Config: store + drop&gt;(
    _: Rule,
    policy: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;,
): &Config {
    df::borrow(&policy.id, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_RuleKey">RuleKey</a>&lt;Rule&gt; {})
}
</code></pre>



</details>

<a name="iota_transfer_policy_add_to_balance"></a>

## Function `add_to_balance`

Add some <code>IOTA</code> to the balance of a <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_add_to_balance">add_to_balance</a>&lt;T, Rule: drop&gt;(_: Rule, policy: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;, coin: <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_add_to_balance">add_to_balance</a>&lt;T, Rule: drop&gt;(
    _: Rule,
    policy: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;,
    coin: Coin&lt;IOTA&gt;,
) {
    <b>assert</b>!(<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_has_rule">has_rule</a>&lt;T, Rule&gt;(policy), <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_EUnknownRequirement">EUnknownRequirement</a>);
    coin::put(&<b>mut</b> policy.balance, coin)
}
</code></pre>



</details>

<a name="iota_transfer_policy_add_receipt"></a>

## Function `add_receipt`

Adds a <code>Receipt</code> to the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code>, unblocking the request and
confirming that the policy requirements are satisfied.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_add_receipt">add_receipt</a>&lt;T, Rule: drop&gt;(_: Rule, request: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">iota::transfer_policy::TransferRequest</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_add_receipt">add_receipt</a>&lt;T, Rule: drop&gt;(_: Rule, request: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a>&lt;T&gt;) {
    request.receipts.insert(type_name::get&lt;Rule&gt;())
}
</code></pre>



</details>

<a name="iota_transfer_policy_has_rule"></a>

## Function `has_rule`

Check whether a custom rule has been added to the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_has_rule">has_rule</a>&lt;T, Rule: drop&gt;(policy: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_has_rule">has_rule</a>&lt;T, Rule: drop&gt;(policy: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;): bool {
    df::exists_(&policy.id, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_RuleKey">RuleKey</a>&lt;Rule&gt; {})
}
</code></pre>



</details>

<a name="iota_transfer_policy_remove_rule"></a>

## Function `remove_rule`

Remove the Rule from the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_remove_rule">remove_rule</a>&lt;T, Rule: drop, Config: drop, store&gt;(policy: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">iota::transfer_policy::TransferPolicyCap</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_remove_rule">remove_rule</a>&lt;T, Rule: drop, Config: store + drop&gt;(
    policy: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;,
    cap: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a>&lt;T&gt;,
) {
    <b>assert</b>!(object::id(policy) == cap.policy_id, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_ENotOwner">ENotOwner</a>);
    <b>let</b> _: Config = df::remove(&<b>mut</b> policy.id, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_RuleKey">RuleKey</a>&lt;Rule&gt; {});
    policy.<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_rules">rules</a>.remove(&type_name::get&lt;Rule&gt;());
}
</code></pre>



</details>

<a name="iota_transfer_policy_uid"></a>

## Function `uid`

Allows reading custom attachments to the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code> if there are any.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_uid">uid</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;): &<a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_uid">uid</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;): &UID { &self.id }
</code></pre>



</details>

<a name="iota_transfer_policy_uid_mut_as_owner"></a>

## Function `uid_mut_as_owner`

Get a mutable reference to the <code>self.id</code> to enable custom attachments
to the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_uid_mut_as_owner">uid_mut_as_owner</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">iota::transfer_policy::TransferPolicyCap</a>&lt;T&gt;): &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_uid_mut_as_owner">uid_mut_as_owner</a>&lt;T&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;, cap: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicyCap">TransferPolicyCap</a>&lt;T&gt;): &<b>mut</b> UID {
    <b>assert</b>!(object::id(self) == cap.policy_id, <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_ENotOwner">ENotOwner</a>);
    &<b>mut</b> self.id
}
</code></pre>



</details>

<a name="iota_transfer_policy_rules"></a>

## Function `rules`

Read the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_rules">rules</a></code> field from the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_rules">rules</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">iota::transfer_policy::TransferPolicy</a>&lt;T&gt;): &<a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_rules">rules</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferPolicy">TransferPolicy</a>&lt;T&gt;): &VecSet&lt;TypeName&gt; {
    &self.<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_rules">rules</a>
}
</code></pre>



</details>

<a name="iota_transfer_policy_item"></a>

## Function `item`

Get the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_item">item</a></code> field of the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_item">item</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">iota::transfer_policy::TransferRequest</a>&lt;T&gt;): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_item">item</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a>&lt;T&gt;): ID { self.<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_item">item</a> }
</code></pre>



</details>

<a name="iota_transfer_policy_paid"></a>

## Function `paid`

Get the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_paid">paid</a></code> field of the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_paid">paid</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">iota::transfer_policy::TransferRequest</a>&lt;T&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_paid">paid</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a>&lt;T&gt;): u64 { self.<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_paid">paid</a> }
</code></pre>



</details>

<a name="iota_transfer_policy_from"></a>

## Function `from`

Get the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_from">from</a></code> field of the <code><a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_from">from</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">iota::transfer_policy::TransferRequest</a>&lt;T&gt;): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_from">from</a>&lt;T&gt;(self: &<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_TransferRequest">TransferRequest</a>&lt;T&gt;): ID { self.<a href="../../dependencies/iota/transfer_policy.md#iota_transfer_policy_from">from</a> }
</code></pre>



</details>
