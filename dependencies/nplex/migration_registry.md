
<a name="(iota_identity=0x0)_migration_registry"></a>

# Module `(iota_identity=0x0)::migration_registry`



-  [Struct `MIGRATION_REGISTRY`](#(iota_identity=0x0)_migration_registry_MIGRATION_REGISTRY)
-  [Struct `MigrationRegistryCreated`](#(iota_identity=0x0)_migration_registry_MigrationRegistryCreated)
-  [Struct `MigrationRegistry`](#(iota_identity=0x0)_migration_registry_MigrationRegistry)
-  [Constants](#@Constants_0)
-  [Function `init`](#(iota_identity=0x0)_migration_registry_init)
-  [Function `exists`](#(iota_identity=0x0)_migration_registry_exists)
-  [Function `lookup`](#(iota_identity=0x0)_migration_registry_lookup)
-  [Function `add`](#(iota_identity=0x0)_migration_registry_add)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="(iota_identity=0x0)_migration_registry_MIGRATION_REGISTRY"></a>

## Struct `MIGRATION_REGISTRY`

One time witness needed to construct a singleton <code><a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MigrationRegistry">MigrationRegistry</a></code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MIGRATION_REGISTRY">MIGRATION_REGISTRY</a> <b>has</b> drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="(iota_identity=0x0)_migration_registry_MigrationRegistryCreated"></a>

## Struct `MigrationRegistryCreated`

Event type that is fired upon creation of a <code><a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MigrationRegistry">MigrationRegistry</a></code>.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MigrationRegistryCreated">MigrationRegistryCreated</a> <b>has</b> <b>copy</b>, drop
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
<code>beacon: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_migration_registry_MigrationRegistry"></a>

## Struct `MigrationRegistry`

Object that tracks migrated alias outputs to their corresponding object IDs.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MigrationRegistry">MigrationRegistry</a> <b>has</b> key
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>id: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(iota_identity=0x0)_migration_registry_BEACON_BYTES"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_BEACON_BYTES">BEACON_BYTES</a>: vector&lt;u8&gt; = vector[105, 100, 101, 110, 116, 105, 116, 121, 46, 114, 115, 95, 112, 107, 103];
</code></pre>



<a name="(iota_identity=0x0)_migration_registry_init"></a>

## Function `init`

Creates a singleton instance of <code><a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MigrationRegistry">MigrationRegistry</a></code> when publishing this package.


<pre><code><b>fun</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_init">init</a>(_otw: (iota_identity=0x0)::migration_registry::MIGRATION_REGISTRY, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_init">init</a>(_otw: <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MIGRATION_REGISTRY">MIGRATION_REGISTRY</a>, ctx: &<b>mut</b> TxContext) {
    <b>let</b> id = object::new(ctx);
    <b>let</b> registry_id = id.to_inner();
    <b>let</b> <a href="../../nplex/registry.md#(nplex=0x0)_registry">registry</a> = <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MigrationRegistry">MigrationRegistry</a> {
        id,
    };
    share_object(<a href="../../nplex/registry.md#(nplex=0x0)_registry">registry</a>);
    // Signal the creation of a migration <a href="../../nplex/registry.md#(nplex=0x0)_registry">registry</a>.
    event::emit(<a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MigrationRegistryCreated">MigrationRegistryCreated</a> { id: registry_id, beacon: <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_BEACON_BYTES">BEACON_BYTES</a> });
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_migration_registry_exists"></a>

## Function `exists`

Checks whether the given alias ID exists in the migration registry.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_exists">exists</a>(self: &(iota_identity=0x0)::migration_registry::MigrationRegistry, alias_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_exists">exists</a>(self: &<a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MigrationRegistry">MigrationRegistry</a>, alias_id: ID): bool {
    field::exists_(&self.id, alias_id)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_migration_registry_lookup"></a>

## Function `lookup`

Lookup an alias ID into the migration registry.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_lookup">lookup</a>(self: &(iota_identity=0x0)::migration_registry::MigrationRegistry, alias_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_lookup">lookup</a>(self: &<a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MigrationRegistry">MigrationRegistry</a>, alias_id: ID): ID {
    *field::borrow&lt;ID, ID&gt;(&self.id, alias_id)
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_migration_registry_add"></a>

## Function `add`

Adds a new Alias ID -> Object ID binding to the regitry.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_add">add</a>(self: &<b>mut</b> (iota_identity=0x0)::migration_registry::MigrationRegistry, alias_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, identity_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_add">add</a>(self: &<b>mut</b> <a href="../../dependencies/nplex/migration_registry.md#(iota_identity=0x0)_migration_registry_MigrationRegistry">MigrationRegistry</a>, alias_id: ID, identity_id: ID) {
    field::add(&<b>mut</b> self.id, alias_id, identity_id);
}
</code></pre>



</details>
