
<a name="iota_authenticator_function"></a>

# Module `iota::authenticator_function`



-  [Struct `AuthenticatorFunctionRefV1`](#iota_authenticator_function_AuthenticatorFunctionRefV1)
-  [Constants](#@Constants_0)
-  [Function `create_auth_function_ref_v1`](#iota_authenticator_function_create_auth_function_ref_v1)
-  [Function `package`](#iota_authenticator_function_package)
-  [Function `module_name`](#iota_authenticator_function_module_name)
-  [Function `function_name`](#iota_authenticator_function_function_name)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
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



<a name="iota_authenticator_function_AuthenticatorFunctionRefV1"></a>

## Struct `AuthenticatorFunctionRefV1`

Represents a validated authenticate function.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">AuthenticatorFunctionRefV1</a>&lt;<b>phantom</b> Account: key&gt; <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_package">package</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_module_name">module_name</a>: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_function_name">function_name</a>: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_authenticator_function_EAuthenticatorFunctionRefV1NotCompatibleWithAccount"></a>



<pre><code>#[error]
<b>const</b> <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_EAuthenticatorFunctionRefV1NotCompatibleWithAccount">EAuthenticatorFunctionRefV1NotCompatibleWithAccount</a>: vector&lt;u8&gt; = b"The provided `<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">AuthenticatorFunctionRefV1</a>` is not compatible with the account type.";
</code></pre>



<a name="iota_authenticator_function_create_auth_function_ref_v1"></a>

## Function `create_auth_function_ref_v1`

Create an "AuthenticatorFunctionRefV1" using an <code>authenticate</code> function defined outside of this version of the package

The referred <code><a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_package">package</a></code>, <code><a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_module_name">module_name</a></code>, <code><a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_function_name">function_name</a></code> can refer to any valid <code>authenticate</code> function,
regardless of package dependencies or versions.
For example package A has two versions V1 and V2. V2 of package A may refer to an <code>authenticate</code>
function defined in V1. Or it can refer to any package B with an appropriate <code>authenticate</code> function
even if package A does not have a dependency on package B.
In fact package A may have a dependency on package B version 1, but can still refer to an <code>authenticate</code>
function defined in package B version 2.
Referring to an <code>authenticate</code> function with <code><a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_create_auth_function_ref_v1">create_auth_function_ref_v1</a></code> is a strictly runtime dependency and
it does not collide with any compile time restrictions.

This function cannot be used in <code><b>move</b> unit tests</code> as there is no mechanism to refer to the package being tested.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_create_auth_function_ref_v1">create_auth_function_ref_v1</a>&lt;Account: key&gt;(package_metadata: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">iota::package_metadata::PackageMetadataV1</a>, <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_module_name">module_name</a>: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>, <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_function_name">function_name</a>: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>): <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_create_auth_function_ref_v1">create_auth_function_ref_v1</a>&lt;Account: key&gt;(
    package_metadata: &PackageMetadataV1,
    <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_module_name">module_name</a>: ascii::String,
    <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_function_name">function_name</a>: ascii::String,
): <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">AuthenticatorFunctionRefV1</a>&lt;Account&gt; {
    <b>let</b> authenticator_metadata = package_metadata
        .modules_metadata_v1(
            &<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_module_name">module_name</a>,
        )
        .authenticator_metadata_v1(&<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_function_name">function_name</a>);
    <b>assert</b>!(
        type_name::get&lt;Account&gt;() == authenticator_metadata.account_type(),
        <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_EAuthenticatorFunctionRefV1NotCompatibleWithAccount">EAuthenticatorFunctionRefV1NotCompatibleWithAccount</a>,
    );
    <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">AuthenticatorFunctionRefV1</a> {
        <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_package">package</a>: package_metadata.storage_id(),
        <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_module_name">module_name</a>,
        <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_function_name">function_name</a>,
    }
}
</code></pre>



</details>

<a name="iota_authenticator_function_package"></a>

## Function `package`

Return the storage ID of the package represented by <code><a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">AuthenticatorFunctionRefV1</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_package">package</a>&lt;Account: key&gt;(self: &<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_package">package</a>&lt;Account: key&gt;(self: &<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">AuthenticatorFunctionRefV1</a>&lt;Account&gt;): ID {
    self.<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_package">package</a>
}
</code></pre>



</details>

<a name="iota_authenticator_function_module_name"></a>

## Function `module_name`

Return the name of the module represented by <code><a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">AuthenticatorFunctionRefV1</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_module_name">module_name</a>&lt;Account: key&gt;(self: &<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;): &<a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_module_name">module_name</a>&lt;Account: key&gt;(self: &<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">AuthenticatorFunctionRefV1</a>&lt;Account&gt;): &ascii::String {
    &self.<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_module_name">module_name</a>
}
</code></pre>



</details>

<a name="iota_authenticator_function_function_name"></a>

## Function `function_name`

Return the name of the function represented by <code><a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">AuthenticatorFunctionRefV1</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_function_name">function_name</a>&lt;Account: key&gt;(self: &<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">iota::authenticator_function::AuthenticatorFunctionRefV1</a>&lt;Account&gt;): &<a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_function_name">function_name</a>&lt;Account: key&gt;(self: &<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_AuthenticatorFunctionRefV1">AuthenticatorFunctionRefV1</a>&lt;Account&gt;): &ascii::String {
    &self.<a href="../../dependencies/iota/authenticator_function.md#iota_authenticator_function_function_name">function_name</a>
}
</code></pre>



</details>
