
<a name="iota_account"></a>

# Module `iota::account`



-  [Struct `ImmutableAccountCreated`](#iota_account_ImmutableAccountCreated)
-  [Struct `MutableAccountCreated`](#iota_account_MutableAccountCreated)
-  [Struct `AuthenticatorFunctionRefV1Rotated`](#iota_account_AuthenticatorFunctionRefV1Rotated)
-  [Struct `AuthenticatorFunctionRefV1Key`](#iota_account_AuthenticatorFunctionRefV1Key)
-  [Constants](#@Constants_0)
-  [Function `create_account_v1`](#iota_account_create_account_v1)
-  [Function `create_immutable_account_v1`](#iota_account_create_immutable_account_v1)
-  [Function `rotate_auth_function_ref_v1`](#iota_account_rotate_auth_function_ref_v1)
-  [Function `borrow_auth_function_ref_v1`](#iota_account_borrow_auth_function_ref_v1)
-  [Function `has_auth_function_ref_v1`](#iota_account_has_auth_function_ref_v1)
-  [Function `auth_function_ref_v1_key`](#iota_account_auth_function_ref_v1_key)
-  [Function `attach_auth_function_ref_v1`](#iota_account_attach_auth_function_ref_v1)
-  [Function `borrow_account_uid_mut`](#iota_account_borrow_account_uid_mut)
-  [Function `create_account_v1_impl`](#iota_account_create_account_v1_impl)
-  [Function `create_immutable_account_v1_impl`](#iota_account_create_immutable_account_v1_impl)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function">iota::authenticator_function</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata">iota::package_metadata</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_account_ImmutableAccountCreated"></a>

## Struct `ImmutableAccountCreated`

Event: emitted when a new immutable account has been created.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/account.md#iota_account_ImmutableAccountCreated">ImmutableAccountCreated</a>&lt;<b>phantom</b> Account: key&gt; <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>account_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>authenticator: <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_account_MutableAccountCreated"></a>

## Struct `MutableAccountCreated`

Event: emitted when a new mutable account has been created.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/account.md#iota_account_MutableAccountCreated">MutableAccountCreated</a>&lt;<b>phantom</b> Account: key&gt; <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>account_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>authenticator: <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_account_AuthenticatorFunctionRefV1Rotated"></a>

## Struct `AuthenticatorFunctionRefV1Rotated`

Event: emitted when an account authenticator has been rotated.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Rotated">AuthenticatorFunctionRefV1Rotated</a>&lt;<b>phantom</b> Account: key&gt; <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>account_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>from: <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>to: <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_account_AuthenticatorFunctionRefV1Key"></a>

## Struct `AuthenticatorFunctionRefV1Key`

Dynamic field key, where the system will look for a potential
authenticate function.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Key">AuthenticatorFunctionRefV1Key</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_account_EAuthenticatorFunctionRefV1AlreadyAttached"></a>



<pre><code>#[error]
<b>const</b> <a href="../../dependencies/iota/account.md#iota_account_EAuthenticatorFunctionRefV1AlreadyAttached">EAuthenticatorFunctionRefV1AlreadyAttached</a>: vector&lt;u8&gt; = b"An `AuthenticatorFunctionRefV1` instance is already attached to the account.";
</code></pre>



<a name="iota_account_EAuthenticatorFunctionRefV1NotAttached"></a>



<pre><code>#[error]
<b>const</b> <a href="../../dependencies/iota/account.md#iota_account_EAuthenticatorFunctionRefV1NotAttached">EAuthenticatorFunctionRefV1NotAttached</a>: vector&lt;u8&gt; = b"'AuthenticatorFunctionRefV1' is not attached to the account.";
</code></pre>



<a name="iota_account_create_account_v1"></a>

## Function `create_account_v1`

Create an account as a mutable shared object with the provided <code>authenticator</code>.
The <code>authenticator</code> instance will be added to the account as a dynamic field specified by the <code><a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Key">AuthenticatorFunctionRefV1Key</a></code> name.
This function has custom rules performed by the IOTA Move bytecode verifier that ensures
that <code>Account</code> is an object defined in the module where <code><a href="../../dependencies/iota/account.md#iota_account_create_account_v1">create_account_v1</a></code> is invoked.
Emits an <code><a href="../../dependencies/iota/account.md#iota_account_MutableAccountCreated">MutableAccountCreated</a></code> event upon success.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_create_account_v1">create_account_v1</a>&lt;Account: key&gt;(account: Account, authenticator: <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_create_account_v1">create_account_v1</a>&lt;Account: key&gt;(
    <b>mut</b> account: Account,
    authenticator: AuthenticatorFunctionRefV1&lt;Account&gt;,
) {
    <b>let</b> event = <a href="../../dependencies/iota/account.md#iota_account_MutableAccountCreated">MutableAccountCreated</a> {
        account_id: *object::borrow_id(&account),
        authenticator,
    };
    <a href="../../dependencies/iota/account.md#iota_account_attach_auth_function_ref_v1">attach_auth_function_ref_v1</a>(&<b>mut</b> account, authenticator);
    <a href="../../dependencies/iota/account.md#iota_account_create_account_v1_impl">create_account_v1_impl</a>(account);
    event::emit(event);
}
</code></pre>



</details>

<a name="iota_account_create_immutable_account_v1"></a>

## Function `create_immutable_account_v1`

Create an account as an immutable object with the provided <code>authenticator</code>.
The <code>authenticator</code> instance will be added to the account as a dynamic field specified by the <code><a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Key">AuthenticatorFunctionRefV1Key</a></code> name.
This function has custom rules performed by the IOTA Move bytecode verifier that ensures
that <code>Account</code> is an object defined in the module where <code><a href="../../dependencies/iota/account.md#iota_account_create_immutable_account_v1">create_immutable_account_v1</a></code> is invoked.
Emits an <code><a href="../../dependencies/iota/account.md#iota_account_ImmutableAccountCreated">ImmutableAccountCreated</a></code> event upon success.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_create_immutable_account_v1">create_immutable_account_v1</a>&lt;Account: key&gt;(account: Account, authenticator: <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_create_immutable_account_v1">create_immutable_account_v1</a>&lt;Account: key&gt;(
    <b>mut</b> account: Account,
    authenticator: AuthenticatorFunctionRefV1&lt;Account&gt;,
) {
    <b>let</b> event = <a href="../../dependencies/iota/account.md#iota_account_ImmutableAccountCreated">ImmutableAccountCreated</a> {
        account_id: *object::borrow_id(&account),
        authenticator,
    };
    <a href="../../dependencies/iota/account.md#iota_account_attach_auth_function_ref_v1">attach_auth_function_ref_v1</a>(&<b>mut</b> account, authenticator);
    <a href="../../dependencies/iota/account.md#iota_account_create_immutable_account_v1_impl">create_immutable_account_v1_impl</a>(account);
    event::emit(event);
}
</code></pre>



</details>

<a name="iota_account_rotate_auth_function_ref_v1"></a>

## Function `rotate_auth_function_ref_v1`

Rotate the account-related authenticator.
The <code>authenticator</code> instance will replace the account dynamic field specified by the <code><a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Key">AuthenticatorFunctionRefV1Key</a></code> name.
This function has custom rules performed by the IOTA Move bytecode verifier that ensures
that <code>Account</code> is an object defined in the module where <code><a href="../../dependencies/iota/account.md#iota_account_rotate_auth_function_ref_v1">rotate_auth_function_ref_v1</a></code> is invoked.
Emits an <code><a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Rotated">AuthenticatorFunctionRefV1Rotated</a></code> event upon success.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_rotate_auth_function_ref_v1">rotate_auth_function_ref_v1</a>&lt;Account: key&gt;(account: &<b>mut</b> Account, authenticator: <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;): <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_rotate_auth_function_ref_v1">rotate_auth_function_ref_v1</a>&lt;Account: key&gt;(
    account: &<b>mut</b> Account,
    authenticator: AuthenticatorFunctionRefV1&lt;Account&gt;,
): AuthenticatorFunctionRefV1&lt;Account&gt; {
    <b>let</b> account_id = <a href="../../dependencies/iota/account.md#iota_account_borrow_account_uid_mut">borrow_account_uid_mut</a>(account);
    <b>assert</b>!(<a href="../../dependencies/iota/account.md#iota_account_has_auth_function_ref_v1">has_auth_function_ref_v1</a>(account_id), <a href="../../dependencies/iota/account.md#iota_account_EAuthenticatorFunctionRefV1NotAttached">EAuthenticatorFunctionRefV1NotAttached</a>);
    <b>let</b> name = <a href="../../dependencies/iota/account.md#iota_account_auth_function_ref_v1_key">auth_function_ref_v1_key</a>();
    <b>let</b> prev = dynamic_field::remove(account_id, name);
    <b>let</b> event = <a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Rotated">AuthenticatorFunctionRefV1Rotated</a> {
        account_id: *account_id.as_inner(),
        from: prev,
        to: authenticator,
    };
    dynamic_field::add(account_id, name, authenticator);
    event::emit(event);
    prev
}
</code></pre>



</details>

<a name="iota_account_borrow_auth_function_ref_v1"></a>

## Function `borrow_auth_function_ref_v1`

Borrow the account-related authenticator.
The dynamic field specified by the <code><a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Key">AuthenticatorFunctionRefV1Key</a></code> name will be returned.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_borrow_auth_function_ref_v1">borrow_auth_function_ref_v1</a>&lt;Account: key&gt;(account_id: &<a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>): &<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_borrow_auth_function_ref_v1">borrow_auth_function_ref_v1</a>&lt;Account: key&gt;(
    account_id: &UID,
): &AuthenticatorFunctionRefV1&lt;Account&gt; {
    <b>assert</b>!(<a href="../../dependencies/iota/account.md#iota_account_has_auth_function_ref_v1">has_auth_function_ref_v1</a>(account_id), <a href="../../dependencies/iota/account.md#iota_account_EAuthenticatorFunctionRefV1NotAttached">EAuthenticatorFunctionRefV1NotAttached</a>);
    dynamic_field::borrow(account_id, <a href="../../dependencies/iota/account.md#iota_account_auth_function_ref_v1_key">auth_function_ref_v1_key</a>())
}
</code></pre>



</details>

<a name="iota_account_has_auth_function_ref_v1"></a>

## Function `has_auth_function_ref_v1`

Check if an authenticator is attached. If a dynamic field with the <code><a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Key">AuthenticatorFunctionRefV1Key</a></code> name exists.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_has_auth_function_ref_v1">has_auth_function_ref_v1</a>(account_id: &<a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_has_auth_function_ref_v1">has_auth_function_ref_v1</a>(account_id: &UID): bool {
    dynamic_field::exists_(account_id, <a href="../../dependencies/iota/account.md#iota_account_auth_function_ref_v1_key">auth_function_ref_v1_key</a>())
}
</code></pre>



</details>

<a name="iota_account_auth_function_ref_v1_key"></a>

## Function `auth_function_ref_v1_key`



<pre><code><b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_auth_function_ref_v1_key">auth_function_ref_v1_key</a>(): <a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Key">iota::account::AuthenticatorFunctionRefV1Key</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_auth_function_ref_v1_key">auth_function_ref_v1_key</a>(): <a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Key">AuthenticatorFunctionRefV1Key</a> {
    <a href="../../dependencies/iota/account.md#iota_account_AuthenticatorFunctionRefV1Key">AuthenticatorFunctionRefV1Key</a> {}
}
</code></pre>



</details>

<a name="iota_account_attach_auth_function_ref_v1"></a>

## Function `attach_auth_function_ref_v1`

Add <code>authenticator</code> as a dynamic field to <code>account</code>.

IMPORTANT: This function is allowed to be called only by the functions that the IOTA Move bytecode verifier
prevents from being invoked outside the module where <code>Account</code> is declared.


<pre><code><b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_attach_auth_function_ref_v1">attach_auth_function_ref_v1</a>&lt;Account: key&gt;(account: &<b>mut</b> Account, authenticator: <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_attach_auth_function_ref_v1">attach_auth_function_ref_v1</a>&lt;Account: key&gt;(
    account: &<b>mut</b> Account,
    authenticator: AuthenticatorFunctionRefV1&lt;Account&gt;,
) {
    <b>let</b> account_id = <a href="../../dependencies/iota/account.md#iota_account_borrow_account_uid_mut">borrow_account_uid_mut</a>(account);
    <b>assert</b>!(!<a href="../../dependencies/iota/account.md#iota_account_has_auth_function_ref_v1">has_auth_function_ref_v1</a>(account_id), <a href="../../dependencies/iota/account.md#iota_account_EAuthenticatorFunctionRefV1AlreadyAttached">EAuthenticatorFunctionRefV1AlreadyAttached</a>);
    dynamic_field::add(account_id, <a href="../../dependencies/iota/account.md#iota_account_auth_function_ref_v1_key">auth_function_ref_v1_key</a>(), authenticator);
}
</code></pre>



</details>

<a name="iota_account_borrow_account_uid_mut"></a>

## Function `borrow_account_uid_mut`

Borrow the account <code>UID</code> mutably.

IMPORTANT: This function is allowed to be called only by the functions that the IOTA Move bytecode verifier
prevents from being invoked outside the module where <code>Account</code> is declared.


<pre><code><b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_borrow_account_uid_mut">borrow_account_uid_mut</a>&lt;Account: key&gt;(account: &<b>mut</b> Account): &<b>mut</b> <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>native</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_borrow_account_uid_mut">borrow_account_uid_mut</a>&lt;Account: key&gt;(account: &<b>mut</b> Account): &<b>mut</b> UID;
</code></pre>



</details>

<a name="iota_account_create_account_v1_impl"></a>

## Function `create_account_v1_impl`

Turn <code>account</code> into a mutable shared object.

IMPORTANT: This function is allowed to be called only by the functions that the IOTA Move bytecode verifier
prevents from being invoked outside the module where <code>Account</code> is declared.


<pre><code><b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_create_account_v1_impl">create_account_v1_impl</a>&lt;Account: key&gt;(account: Account)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>native</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_create_account_v1_impl">create_account_v1_impl</a>&lt;Account: key&gt;(account: Account);
</code></pre>



</details>

<a name="iota_account_create_immutable_account_v1_impl"></a>

## Function `create_immutable_account_v1_impl`

Turn <code>account</code> into an immutable object.

IMPORTANT: This function is allowed to be called only by the functions that the IOTA Move bytecode verifier
prevents from being invoked outside the module where <code>Account</code> is declared.


<pre><code><b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_create_immutable_account_v1_impl">create_immutable_account_v1_impl</a>&lt;Account: key&gt;(account: Account)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>native</b> <b>fun</b> <a href="../../dependencies/iota/account.md#iota_account_create_immutable_account_v1_impl">create_immutable_account_v1_impl</a>&lt;Account: key&gt;(account: Account);
</code></pre>



</details>
