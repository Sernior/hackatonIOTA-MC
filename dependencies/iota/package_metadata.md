
<a name="iota_package_metadata"></a>

# Module `iota::package_metadata`

Package metadata management module
An IOTA package can have associated metadata that provides,
on-chain, additional information about the package.


-  [Struct `PackageMetadataKey`](#iota_package_metadata_PackageMetadataKey)
-  [Struct `PackageMetadataV1`](#iota_package_metadata_PackageMetadataV1)
-  [Struct `ModuleMetadataV1`](#iota_package_metadata_ModuleMetadataV1)
-  [Struct `AuthenticatorMetadataV1`](#iota_package_metadata_AuthenticatorMetadataV1)
-  [Constants](#@Constants_0)
-  [Function `storage_id`](#iota_package_metadata_storage_id)
-  [Function `runtime_id`](#iota_package_metadata_runtime_id)
-  [Function `package_version`](#iota_package_metadata_package_version)
-  [Function `try_get_modules_metadata_v1`](#iota_package_metadata_try_get_modules_metadata_v1)
-  [Function `modules_metadata_v1`](#iota_package_metadata_modules_metadata_v1)
-  [Function `try_get_authenticator_metadata_v1`](#iota_package_metadata_try_get_authenticator_metadata_v1)
-  [Function `authenticator_metadata_v1`](#iota_package_metadata_authenticator_metadata_v1)
-  [Function `account_type`](#iota_package_metadata_account_type)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
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



<a name="iota_package_metadata_PackageMetadataKey"></a>

## Struct `PackageMetadataKey`

Key type for deriving the package metadata object address


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataKey">PackageMetadataKey</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="iota_package_metadata_PackageMetadataV1"></a>

## Struct `PackageMetadataV1`

Represents the metadata of a Move package. This includes information
such as the storage ID, runtime ID, version, and metadata for the
functions contained within the package.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">PackageMetadataV1</a> <b>has</b> key
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
<code><a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_storage_id">storage_id</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 Storage ID of the package represented by this metadata
 The object id of the runtime package metadata object is derived from
 this value.
</dd>
<dt>
<code><a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_runtime_id">runtime_id</a>: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
 Runtime ID of the package represented by this metadata. Runtime ID is
 the Storage ID of the first version of a package.
</dd>
<dt>
<code><a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_package_version">package_version</a>: u64</code>
</dt>
<dd>
 Version of the package represented by this metadata
</dd>
<dt>
<code>modules_metadata: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>, <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_ModuleMetadataV1">iota::package_metadata::ModuleMetadataV1</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_package_metadata_ModuleMetadataV1"></a>

## Struct `ModuleMetadataV1`

Represents metadata associated with a module in the package.
V1 includes only the authenticator functions information.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_ModuleMetadataV1">ModuleMetadataV1</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>authenticator_metadata: vector&lt;<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_AuthenticatorMetadataV1">iota::package_metadata::AuthenticatorMetadataV1</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_package_metadata_AuthenticatorMetadataV1"></a>

## Struct `AuthenticatorMetadataV1`

Represents metadata for an authenticator within the package.
It includes the name of the authenticate function and the TypeName
of the first parameter (i.e., the account object type).


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_AuthenticatorMetadataV1">AuthenticatorMetadataV1</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>function_name: <a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_account_type">account_type</a>: <a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_package_metadata_EModuleMetadataNotFound"></a>



<pre><code>#[error]
<b>const</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_EModuleMetadataNotFound">EModuleMetadataNotFound</a>: vector&lt;u8&gt; = b"The requested <b>module</b> metadata was not found in the package metadata.";
</code></pre>



<a name="iota_package_metadata_EAuthenticatorMetadataNotFound"></a>



<pre><code>#[error]
<b>const</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_EAuthenticatorMetadataNotFound">EAuthenticatorMetadataNotFound</a>: vector&lt;u8&gt; = b"The requested authenticator metadata was not found in the <b>module</b> metadata.";
</code></pre>



<a name="iota_package_metadata_storage_id"></a>

## Function `storage_id`

Return the storage ID of the package represented by this metadata


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_storage_id">storage_id</a>(metadata: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">iota::package_metadata::PackageMetadataV1</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_storage_id">storage_id</a>(metadata: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">PackageMetadataV1</a>): ID {
    metadata.<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_storage_id">storage_id</a>
}
</code></pre>



</details>

<a name="iota_package_metadata_runtime_id"></a>

## Function `runtime_id`

Return the runtime ID of the package represented by this metadata


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_runtime_id">runtime_id</a>(metadata: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">iota::package_metadata::PackageMetadataV1</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_runtime_id">runtime_id</a>(metadata: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">PackageMetadataV1</a>): ID {
    metadata.<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_runtime_id">runtime_id</a>
}
</code></pre>



</details>

<a name="iota_package_metadata_package_version"></a>

## Function `package_version`

Return the version of the package represented by this metadata


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_package_version">package_version</a>(metadata: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">iota::package_metadata::PackageMetadataV1</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_package_version">package_version</a>(metadata: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">PackageMetadataV1</a>): u64 {
    metadata.<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_package_version">package_version</a>
}
</code></pre>



</details>

<a name="iota_package_metadata_try_get_modules_metadata_v1"></a>

## Function `try_get_modules_metadata_v1`

Safely get the module metadata list of the package represented by this metadata


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_try_get_modules_metadata_v1">try_get_modules_metadata_v1</a>(self: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">iota::package_metadata::PackageMetadataV1</a>, module_name: &<a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_ModuleMetadataV1">iota::package_metadata::ModuleMetadataV1</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_try_get_modules_metadata_v1">try_get_modules_metadata_v1</a>(
    self: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">PackageMetadataV1</a>,
    module_name: &ascii::String,
): Option&lt;<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_ModuleMetadataV1">ModuleMetadataV1</a>&gt; {
    self.modules_metadata.try_get(module_name)
}
</code></pre>



</details>

<a name="iota_package_metadata_modules_metadata_v1"></a>

## Function `modules_metadata_v1`

Borrow the module metadata list of the package represented by this metadata.
Aborts if the module is not found.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_modules_metadata_v1">modules_metadata_v1</a>(self: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">iota::package_metadata::PackageMetadataV1</a>, module_name: &<a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>): &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_ModuleMetadataV1">iota::package_metadata::ModuleMetadataV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_modules_metadata_v1">modules_metadata_v1</a>(
    self: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_PackageMetadataV1">PackageMetadataV1</a>,
    module_name: &ascii::String,
): &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_ModuleMetadataV1">ModuleMetadataV1</a> {
    <b>assert</b>!(self.modules_metadata.contains(module_name), <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_EModuleMetadataNotFound">EModuleMetadataNotFound</a>);
    self.modules_metadata.get(module_name)
}
</code></pre>



</details>

<a name="iota_package_metadata_try_get_authenticator_metadata_v1"></a>

## Function `try_get_authenticator_metadata_v1`

Safely get the <code><a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_AuthenticatorMetadataV1">AuthenticatorMetadataV1</a></code> associated with the specified
<code>function_name</code> within the module metadata.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_try_get_authenticator_metadata_v1">try_get_authenticator_metadata_v1</a>(self: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_ModuleMetadataV1">iota::package_metadata::ModuleMetadataV1</a>, function_name: &<a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_AuthenticatorMetadataV1">iota::package_metadata::AuthenticatorMetadataV1</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_try_get_authenticator_metadata_v1">try_get_authenticator_metadata_v1</a>(
    self: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_ModuleMetadataV1">ModuleMetadataV1</a>,
    function_name: &ascii::String,
): Option&lt;<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_AuthenticatorMetadataV1">AuthenticatorMetadataV1</a>&gt; {
    self.authenticator_metadata.find_index!(|m| m.function_name == *function_name).and!(|index| {
        option::some(self.authenticator_metadata[index])
    })
}
</code></pre>



</details>

<a name="iota_package_metadata_authenticator_metadata_v1"></a>

## Function `authenticator_metadata_v1`

Borrow the <code><a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_AuthenticatorMetadataV1">AuthenticatorMetadataV1</a></code> associated with the specified
<code>function_name</code>.
Aborts if the authenticator metadata is not found for that function.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_authenticator_metadata_v1">authenticator_metadata_v1</a>(self: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_ModuleMetadataV1">iota::package_metadata::ModuleMetadataV1</a>, function_name: &<a href="../../dependencies/std/ascii.md#std_ascii_String">std::ascii::String</a>): &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_AuthenticatorMetadataV1">iota::package_metadata::AuthenticatorMetadataV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_authenticator_metadata_v1">authenticator_metadata_v1</a>(
    self: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_ModuleMetadataV1">ModuleMetadataV1</a>,
    function_name: &ascii::String,
): &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_AuthenticatorMetadataV1">AuthenticatorMetadataV1</a> {
    <b>let</b> <b>mut</b> index = self.authenticator_metadata.find_index!(|m| m.function_name == *function_name);
    <b>assert</b>!(index.is_some(), <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_EAuthenticatorMetadataNotFound">EAuthenticatorMetadataNotFound</a>);
    &self.authenticator_metadata[index.extract()]
}
</code></pre>



</details>

<a name="iota_package_metadata_account_type"></a>

## Function `account_type`

Return the account type of the authenticator represented by this metadata


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_account_type">account_type</a>(self: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_AuthenticatorMetadataV1">iota::package_metadata::AuthenticatorMetadataV1</a>): <a href="../../dependencies/std/type_name.md#std_type_name_TypeName">std::type_name::TypeName</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_account_type">account_type</a>(self: &<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_AuthenticatorMetadataV1">AuthenticatorMetadataV1</a>): TypeName {
    self.<a href="../../dependencies/iota/package_metadata.md#iota_package_metadata_account_type">account_type</a>
}
</code></pre>



</details>
