
<a name="(iota_identity=0x0)_migration"></a>

# Module `(iota_identity=0x0)::migration`



-  [Constants](#@Constants_0)
-  [Function `migrate_alias`](#(iota_identity=0x0)_migration_migrate_alias)
-  [Function `migrate_alias_output`](#(iota_identity=0x0)_migration_migrate_alias_output)


<pre><code><b>use</b> (iota_identity=0x0)::access_sub_entity_proposal;
<b>use</b> (iota_identity=0x0)::borrow_proposal;
<b>use</b> (iota_identity=0x0)::config_proposal;
<b>use</b> (iota_identity=0x0)::controller;
<b>use</b> (iota_identity=0x0)::controller_proposal;
<b>use</b> (iota_identity=0x0)::delete_proposal;
<b>use</b> (iota_identity=0x0)::identity;
<b>use</b> (iota_identity=0x0)::migration_registry;
<b>use</b> (iota_identity=0x0)::multicontroller;
<b>use</b> (iota_identity=0x0)::permissions;
<b>use</b> (iota_identity=0x0)::transfer_proposal;
<b>use</b> (iota_identity=0x0)::update_value_proposal;
<b>use</b> (iota_identity=0x0)::upgrade_proposal;
<b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../../dependencies/iota/borrow.md#iota_borrow">iota::borrow</a>;
<b>use</b> <a href="../../dependencies/iota/clock.md#iota_clock">iota::clock</a>;
<b>use</b> <a href="../../dependencies/iota/coin.md#iota_coin">iota::coin</a>;
<b>use</b> <a href="../../dependencies/iota/config.md#iota_config">iota::config</a>;
<b>use</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list">iota::deny_list</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/iota.md#iota_iota">iota::iota</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/object_bag.md#iota_object_bag">iota::object_bag</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/iota/vec_set.md#iota_vec_set">iota::vec_set</a>;
<b>use</b> <a href="../../dependencies/stardust/alias.md#stardust_alias">stardust::alias</a>;
<b>use</b> <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output">stardust::alias_output</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="@Constants_0"></a>

## Constants


<a name="(iota_identity=0x0)_migration_ENotADidOutput"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/migration.md#(iota_identity=0x0)_migration_ENotADidOutput">ENotADidOutput</a>: u64 = 1;
</code></pre>



<a name="(iota_identity=0x0)_migration_migrate_alias"></a>

## Function `migrate_alias`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/migration.md#(iota_identity=0x0)_migration_migrate_alias">migrate_alias</a>(alias: <a href="../../dependencies/stardust/alias.md#stardust_alias_Alias">stardust::alias::Alias</a>, migration_registry: &<b>mut</b> (iota_identity=0x0)::migration_registry::MigrationRegistry, creation_timestamp: u64, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <b>address</b>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/migration.md#(iota_identity=0x0)_migration_migrate_alias">migrate_alias</a>(
    alias: Alias,
    migration_registry: &<b>mut</b> MigrationRegistry,
    creation_timestamp: u64,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
): <b>address</b> {
    // Extract needed data from `alias`.
    <b>let</b> alias_id = object::id(&alias);
    <b>let</b> <b>mut</b> state_metadata = *alias.state_metadata();
    // `alias` is not needed anymore, destroy it.
    alias.destroy();
    // Check <b>if</b> `state_metadata` contains a DID document.
    <b>assert</b>!(
        state_metadata.is_some() && identity::is_did_output(state_metadata.borrow()),
        <a href="../../dependencies/nplex/migration.md#(iota_identity=0x0)_migration_ENotADidOutput">ENotADidOutput</a>,
    );
    <b>let</b> identity_id = identity::new_with_migration_data(
        option::some(state_metadata.extract()),
        creation_timestamp,
        alias_id,
        clock,
        ctx,
    );
    // Add a migration record.
    migration_registry.add(alias_id, identity_id);
    identity_id.to_address()
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_migration_migrate_alias_output"></a>

## Function `migrate_alias_output`

Creates a new <code>Identity</code> from an Iota 1.0 legacy <code>AliasOutput</code> containing a DID Document.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/migration.md#(iota_identity=0x0)_migration_migrate_alias_output">migrate_alias_output</a>(alias_output: <a href="../../dependencies/stardust/alias_output.md#stardust_alias_output_AliasOutput">stardust::alias_output::AliasOutput</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, migration_registry: &<b>mut</b> (iota_identity=0x0)::migration_registry::MigrationRegistry, creation_timestamp: u64, clock: &<a href="../../dependencies/iota/clock.md#iota_clock_Clock">iota::clock::Clock</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/migration.md#(iota_identity=0x0)_migration_migrate_alias_output">migrate_alias_output</a>(
    alias_output: AliasOutput&lt;IOTA&gt;,
    migration_registry: &<b>mut</b> MigrationRegistry,
    creation_timestamp: u64,
    clock: &Clock,
    ctx: &<b>mut</b> TxContext,
) {
    // Extract required data from output.
    <b>let</b> (iota, native_tokens, alias_data) = alias_output.extract_assets();
    <b>let</b> identity_addr = <a href="../../dependencies/nplex/migration.md#(iota_identity=0x0)_migration_migrate_alias">migrate_alias</a>(
        alias_data,
        migration_registry,
        creation_timestamp,
        clock,
        ctx,
    );
    <b>let</b> coin = coin::from_balance(iota, ctx);
    transfer::public_transfer(coin, identity_addr);
    transfer::public_transfer(native_tokens, identity_addr);
}
</code></pre>



</details>
