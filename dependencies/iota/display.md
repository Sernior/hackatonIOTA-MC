
<a name="iota_display"></a>

# Module `iota::display`

Defines a Display struct which defines the way an Object
should be displayed. The intention is to keep data as independent
from its display as possible, protecting the development process
and keeping it separate from the ecosystem agreements.

Each of the fields of the Display object should allow for pattern
substitution and filling-in the pieces using the data from the object T.

More entry functions might be added in the future depending on the use cases.


-  [Struct `Display`](#iota_display_Display)
-  [Struct `DisplayCreated`](#iota_display_DisplayCreated)
-  [Struct `VersionUpdated`](#iota_display_VersionUpdated)
-  [Constants](#@Constants_0)
-  [Function `new`](#iota_display_new)
-  [Function `new_with_fields`](#iota_display_new_with_fields)
-  [Function `create_and_keep`](#iota_display_create_and_keep)
-  [Function `update_version`](#iota_display_update_version)
-  [Function `add`](#iota_display_add)
-  [Function `add_multiple`](#iota_display_add_multiple)
-  [Function `edit`](#iota_display_edit)
-  [Function `remove`](#iota_display_remove)
-  [Function `is_authorized`](#iota_display_is_authorized)
-  [Function `version`](#iota_display_version)
-  [Function `fields`](#iota_display_fields)
-  [Function `create_internal`](#iota_display_create_internal)
-  [Function `add_internal`](#iota_display_add_internal)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/package.md#iota_package">iota::package</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_display_Display"></a>

## Struct `Display`

The Display<T> object. Defines the way a T instance should be
displayed. Display object can only be created and modified with
a PublisherCap, making sure that the rules are set by the owner
of the type.

Each of the display properties should support patterns outside
of the system, making it simpler to customize Display based
on the property values of an Object.
```
// Example of a display object
Display<0x107A::nft::Nft> {
fields:
<name, "IOTEST Nft">
<link, "https://iotestnft.com/nft/{ id }">
<image, "https://api.iotestnft.com/nft/{ id }/svg">
<description, "One of many Iotest Nfts">
}
```

Uses only String type due to external-facing nature of the object,
the property names have a priority over their types.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;<b>phantom</b> T: key&gt; <b>has</b> key, store
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
<code><a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
 Contains fields for display. Currently supported
 fields are: name, link, image and description.
</dd>
<dt>
<code><a href="../../dependencies/iota/display.md#iota_display_version">version</a>: u16</code>
</dt>
<dd>
 Version that can only be updated manually by the Publisher.
</dd>
</dl>


</details>

<a name="iota_display_DisplayCreated"></a>

## Struct `DisplayCreated`

Event: emitted when a new Display object has been created for type T.
Type signature of the event corresponds to the type while id serves for
the discovery.

Since IOTA RPC supports querying events by type, finding a Display for the T
would be as simple as looking for the first event with <code><a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt;</code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/display.md#iota_display_DisplayCreated">DisplayCreated</a>&lt;<b>phantom</b> T: key&gt; <b>has</b> <b>copy</b>, drop
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

<a name="iota_display_VersionUpdated"></a>

## Struct `VersionUpdated`

Version of Display got updated -


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/display.md#iota_display_VersionUpdated">VersionUpdated</a>&lt;<b>phantom</b> T: key&gt; <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/display.md#iota_display_version">version</a>: u16</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_display_ENotOwner"></a>

For when T does not belong to the package <code>Publisher</code>.


<pre><code><b>const</b> <a href="../../dependencies/iota/display.md#iota_display_ENotOwner">ENotOwner</a>: u64 = 0;
</code></pre>



<a name="iota_display_EVecLengthMismatch"></a>

For when vectors passed into one of the multiple insert functions
don't match in their lengths.


<pre><code><b>const</b> <a href="../../dependencies/iota/display.md#iota_display_EVecLengthMismatch">EVecLengthMismatch</a>: u64 = 1;
</code></pre>



<a name="iota_display_new"></a>

## Function `new`

Create an empty Display object. It can either be shared empty or filled
with data right away via cheaper <code>set_owned</code> method.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_new">new</a>&lt;T: key&gt;(pub: &<a href="../../dependencies/iota/package.md#iota_package_Publisher">iota::package::Publisher</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/display.md#iota_display_Display">iota::display::Display</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_new">new</a>&lt;T: key&gt;(pub: &Publisher, ctx: &<b>mut</b> TxContext): <a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt; {
    <b>assert</b>!(<a href="../../dependencies/iota/display.md#iota_display_is_authorized">is_authorized</a>&lt;T&gt;(pub), <a href="../../dependencies/iota/display.md#iota_display_ENotOwner">ENotOwner</a>);
    <a href="../../dependencies/iota/display.md#iota_display_create_internal">create_internal</a>(ctx)
}
</code></pre>



</details>

<a name="iota_display_new_with_fields"></a>

## Function `new_with_fields`

Create a new Display<T> object with a set of fields.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_new_with_fields">new_with_fields</a>&lt;T: key&gt;(pub: &<a href="../../dependencies/iota/package.md#iota_package_Publisher">iota::package::Publisher</a>, <a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>: vector&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, values: vector&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/display.md#iota_display_Display">iota::display::Display</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_new_with_fields">new_with_fields</a>&lt;T: key&gt;(
    pub: &Publisher,
    <a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>: vector&lt;String&gt;,
    values: vector&lt;String&gt;,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt; {
    <b>let</b> len = <a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>.length();
    <b>assert</b>!(len == values.length(), <a href="../../dependencies/iota/display.md#iota_display_EVecLengthMismatch">EVecLengthMismatch</a>);
    <b>let</b> <b>mut</b> i = 0;
    <b>let</b> <b>mut</b> display = <a href="../../dependencies/iota/display.md#iota_display_new">new</a>&lt;T&gt;(pub, ctx);
    <b>while</b> (i &lt; len) {
        display.<a href="../../dependencies/iota/display.md#iota_display_add_internal">add_internal</a>(<a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>[i], values[i]);
        i = i + 1;
    };
    display
}
</code></pre>



</details>

<a name="iota_display_create_and_keep"></a>

## Function `create_and_keep`

Create a new empty Display<T> object and keep it.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_create_and_keep">create_and_keep</a>&lt;T: key&gt;(pub: &<a href="../../dependencies/iota/package.md#iota_package_Publisher">iota::package::Publisher</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_create_and_keep">create_and_keep</a>&lt;T: key&gt;(pub: &Publisher, ctx: &<b>mut</b> TxContext) {
    transfer::public_transfer(<a href="../../dependencies/iota/display.md#iota_display_new">new</a>&lt;T&gt;(pub, ctx), ctx.sender())
}
</code></pre>



</details>

<a name="iota_display_update_version"></a>

## Function `update_version`

Manually bump the version and emit an event with the updated version's contents.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_update_version">update_version</a>&lt;T: key&gt;(display: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">iota::display::Display</a>&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_update_version">update_version</a>&lt;T: key&gt;(display: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt;) {
    display.<a href="../../dependencies/iota/display.md#iota_display_version">version</a> = display.<a href="../../dependencies/iota/display.md#iota_display_version">version</a> + 1;
    event::emit(<a href="../../dependencies/iota/display.md#iota_display_VersionUpdated">VersionUpdated</a>&lt;T&gt; {
        <a href="../../dependencies/iota/display.md#iota_display_version">version</a>: display.<a href="../../dependencies/iota/display.md#iota_display_version">version</a>,
        <a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>: *&display.<a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>,
        id: display.id.to_inner(),
    })
}
</code></pre>



</details>

<a name="iota_display_add"></a>

## Function `add`

Sets a custom <code>name</code> field with the <code>value</code>.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_add">add</a>&lt;T: key&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">iota::display::Display</a>&lt;T&gt;, name: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, value: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_add">add</a>&lt;T: key&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt;, name: String, value: String) {
    self.<a href="../../dependencies/iota/display.md#iota_display_add_internal">add_internal</a>(name, value)
}
</code></pre>



</details>

<a name="iota_display_add_multiple"></a>

## Function `add_multiple`

Sets multiple <code><a href="../../dependencies/iota/display.md#iota_display_fields">fields</a></code> with <code>values</code>.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_add_multiple">add_multiple</a>&lt;T: key&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">iota::display::Display</a>&lt;T&gt;, <a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>: vector&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, values: vector&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_add_multiple">add_multiple</a>&lt;T: key&gt;(
    self: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt;,
    <a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>: vector&lt;String&gt;,
    values: vector&lt;String&gt;,
) {
    <b>let</b> len = <a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>.length();
    <b>assert</b>!(len == values.length(), <a href="../../dependencies/iota/display.md#iota_display_EVecLengthMismatch">EVecLengthMismatch</a>);
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; len) {
        self.<a href="../../dependencies/iota/display.md#iota_display_add_internal">add_internal</a>(<a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>[i], values[i]);
        i = i + 1;
    };
}
</code></pre>



</details>

<a name="iota_display_edit"></a>

## Function `edit`

Change the value of the field.
TODO (long run): version changes;


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_edit">edit</a>&lt;T: key&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">iota::display::Display</a>&lt;T&gt;, name: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, value: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_edit">edit</a>&lt;T: key&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt;, name: String, value: String) {
    <b>let</b> (_, _) = self.<a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>.<a href="../../dependencies/iota/display.md#iota_display_remove">remove</a>(&name);
    self.<a href="../../dependencies/iota/display.md#iota_display_add_internal">add_internal</a>(name, value)
}
</code></pre>



</details>

<a name="iota_display_remove"></a>

## Function `remove`

Remove the key from the Display.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_remove">remove</a>&lt;T: key&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">iota::display::Display</a>&lt;T&gt;, name: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_remove">remove</a>&lt;T: key&gt;(self: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt;, name: String) {
    self.<a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>.<a href="../../dependencies/iota/display.md#iota_display_remove">remove</a>(&name);
}
</code></pre>



</details>

<a name="iota_display_is_authorized"></a>

## Function `is_authorized`

Authorization check; can be performed externally to implement protection rules for Display.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_is_authorized">is_authorized</a>&lt;T: key&gt;(pub: &<a href="../../dependencies/iota/package.md#iota_package_Publisher">iota::package::Publisher</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_is_authorized">is_authorized</a>&lt;T: key&gt;(pub: &Publisher): bool {
    pub.from_package&lt;T&gt;()
}
</code></pre>



</details>

<a name="iota_display_version"></a>

## Function `version`

Read the <code><a href="../../dependencies/iota/display.md#iota_display_version">version</a></code> field.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_version">version</a>&lt;T: key&gt;(d: &<a href="../../dependencies/iota/display.md#iota_display_Display">iota::display::Display</a>&lt;T&gt;): u16
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_version">version</a>&lt;T: key&gt;(d: &<a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt;): u16 {
    d.<a href="../../dependencies/iota/display.md#iota_display_version">version</a>
}
</code></pre>



</details>

<a name="iota_display_fields"></a>

## Function `fields`

Read the <code><a href="../../dependencies/iota/display.md#iota_display_fields">fields</a></code> field.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>&lt;T: key&gt;(d: &<a href="../../dependencies/iota/display.md#iota_display_Display">iota::display::Display</a>&lt;T&gt;): &<a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>&lt;T: key&gt;(d: &<a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt;): &VecMap&lt;String, String&gt; {
    &d.<a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>
}
</code></pre>



</details>

<a name="iota_display_create_internal"></a>

## Function `create_internal`

Internal function to create a new <code><a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt;</code>.


<pre><code><b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_create_internal">create_internal</a>&lt;T: key&gt;(ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/display.md#iota_display_Display">iota::display::Display</a>&lt;T&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_create_internal">create_internal</a>&lt;T: key&gt;(ctx: &<b>mut</b> TxContext): <a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt; {
    <b>let</b> uid = object::new(ctx);
    event::emit(<a href="../../dependencies/iota/display.md#iota_display_DisplayCreated">DisplayCreated</a>&lt;T&gt; {
        id: uid.to_inner(),
    });
    <a href="../../dependencies/iota/display.md#iota_display_Display">Display</a> {
        id: uid,
        <a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>: vec_map::empty(),
        <a href="../../dependencies/iota/display.md#iota_display_version">version</a>: 0,
    }
}
</code></pre>



</details>

<a name="iota_display_add_internal"></a>

## Function `add_internal`

Private method for inserting fields without security checks.


<pre><code><b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_add_internal">add_internal</a>&lt;T: key&gt;(display: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">iota::display::Display</a>&lt;T&gt;, name: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>, value: <a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/display.md#iota_display_add_internal">add_internal</a>&lt;T: key&gt;(display: &<b>mut</b> <a href="../../dependencies/iota/display.md#iota_display_Display">Display</a>&lt;T&gt;, name: String, value: String) {
    display.<a href="../../dependencies/iota/display.md#iota_display_fields">fields</a>.insert(name, value)
}
</code></pre>



</details>
