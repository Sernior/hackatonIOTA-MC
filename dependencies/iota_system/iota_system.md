
<a name="iota_system_iota_system"></a>

# Module `iota_system::iota_system`

IOTA System State Type Upgrade Guide
<code><a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a></code> is a thin wrapper around <code>IotaSystemStateV1</code> that provides a versioned interface.
The <code><a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a></code> object has a fixed ID 0x5, and the <code>IotaSystemStateV1</code> object is stored as a dynamic field.
There are a few different ways to upgrade the <code>IotaSystemStateV1</code> type:

The simplest and one that doesn't involve a real upgrade is to just add dynamic fields to the <code>extra_fields</code> field
of <code>IotaSystemStateV1</code> or any of its sub type. This is useful when we are in a rush, or making a small change,
or still experimenting a new field.

To properly upgrade the <code>IotaSystemStateV1</code> type, we need to ship a new framework that does the following:
1. Define a new <code><a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a></code>type (e.g. <code>IotaSystemStateV2</code>).
2. Define a data migration function that migrates the old (e.g. <code>IotaSystemStateV1</code>) to the new one (e.g. <code>IotaSystemStateV2</code>).
3. Replace all uses of <code>IotaSystemStateV1</code> with <code>IotaSystemStateV2</code> in both iota_system.move and iota_system_state_inner.move,
with the exception of the <code>iota_system_state_inner::create</code> function, which should always return the genesis type.
4. Inside <code><a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_inner_maybe_upgrade">load_inner_maybe_upgrade</a></code> function, check the current version in the wrapper, and if it's not the latest version,
call the data migration function to upgrade the inner object. Make sure to also update the version in the wrapper.
A detailed example can be found in iota/tests/framework_upgrades/mock_iota_systems/shallow_upgrade.
Along with the Move change, we also need to update the Rust code to support the new type. This includes:
1. Define a new <code><a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a></code> struct type that matches the new Move type, and implement the <code>IotaSystemStateTrait</code>.
2. Update the <code><a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a></code> struct to include the new version as a new enum variant.
3. Update the <code>get_iota_system_state</code> function to handle the new version.
To test that the upgrade will be successful, we need to modify <code>iota_system_state_production_upgrade_test</code> test in
protocol_version_tests and trigger a real upgrade using the new framework. We will need to keep this directory as old version,
put the new framework in a new directory, and run the test to exercise the upgrade.

To upgrade Validator type, besides everything above, we also need to:
1. Define a new Validator type (e.g. ValidatorV2).
2. Define a data migration function that migrates the old ValidatorV1 to the new one (i.e. ValidatorV2).
3. Replace all uses of ValidatorV1 with ValidatorV2 except the genesis creation function.
4. In validator_wrapper::upgrade_to_latest, check the current version in the wrapper, and if it's not the latest version,
call the data migration function to upgrade it.
In Rust, we also need to add a new case in <code>get_validator_from_table</code>.
Note that it is possible to upgrade IotaSystemStateV1 without upgrading ValidatorV1, but not the other way around.
And when we only upgrade IotaSystemStateV1, the version of ValidatorV1 in the wrapper will not be updated, and hence may become
inconsistent with the version of IotaSystemStateV1. This is fine as long as we don't use the ValidatorV1 version to determine
the IotaSystemStateV1 version, or vice versa.


-  [Struct `IotaSystemState`](#iota_system_iota_system_IotaSystemState)
-  [Constants](#@Constants_0)
-  [Function `create`](#iota_system_iota_system_create)
-  [Function `request_add_validator_candidate`](#iota_system_iota_system_request_add_validator_candidate)
-  [Function `request_remove_validator_candidate`](#iota_system_iota_system_request_remove_validator_candidate)
-  [Function `request_add_validator`](#iota_system_iota_system_request_add_validator)
-  [Function `request_remove_validator`](#iota_system_iota_system_request_remove_validator)
-  [Function `request_set_gas_price`](#iota_system_iota_system_request_set_gas_price)
-  [Function `set_candidate_validator_gas_price`](#iota_system_iota_system_set_candidate_validator_gas_price)
-  [Function `request_set_commission_rate`](#iota_system_iota_system_request_set_commission_rate)
-  [Function `set_candidate_validator_commission_rate`](#iota_system_iota_system_set_candidate_validator_commission_rate)
-  [Function `request_add_stake`](#iota_system_iota_system_request_add_stake)
-  [Function `request_add_stake_non_entry`](#iota_system_iota_system_request_add_stake_non_entry)
-  [Function `request_add_stake_mul_coin`](#iota_system_iota_system_request_add_stake_mul_coin)
-  [Function `request_withdraw_stake`](#iota_system_iota_system_request_withdraw_stake)
-  [Function `request_withdraw_stake_non_entry`](#iota_system_iota_system_request_withdraw_stake_non_entry)
-  [Function `report_validator`](#iota_system_iota_system_report_validator)
-  [Function `undo_report_validator`](#iota_system_iota_system_undo_report_validator)
-  [Function `rotate_operation_cap`](#iota_system_iota_system_rotate_operation_cap)
-  [Function `update_validator_name`](#iota_system_iota_system_update_validator_name)
-  [Function `update_validator_description`](#iota_system_iota_system_update_validator_description)
-  [Function `update_validator_image_url`](#iota_system_iota_system_update_validator_image_url)
-  [Function `update_validator_project_url`](#iota_system_iota_system_update_validator_project_url)
-  [Function `update_validator_next_epoch_network_address`](#iota_system_iota_system_update_validator_next_epoch_network_address)
-  [Function `update_candidate_validator_network_address`](#iota_system_iota_system_update_candidate_validator_network_address)
-  [Function `update_validator_next_epoch_p2p_address`](#iota_system_iota_system_update_validator_next_epoch_p2p_address)
-  [Function `update_candidate_validator_p2p_address`](#iota_system_iota_system_update_candidate_validator_p2p_address)
-  [Function `update_validator_next_epoch_primary_address`](#iota_system_iota_system_update_validator_next_epoch_primary_address)
-  [Function `update_candidate_validator_primary_address`](#iota_system_iota_system_update_candidate_validator_primary_address)
-  [Function `update_validator_next_epoch_authority_pubkey`](#iota_system_iota_system_update_validator_next_epoch_authority_pubkey)
-  [Function `update_candidate_validator_authority_pubkey`](#iota_system_iota_system_update_candidate_validator_authority_pubkey)
-  [Function `update_validator_next_epoch_protocol_pubkey`](#iota_system_iota_system_update_validator_next_epoch_protocol_pubkey)
-  [Function `update_candidate_validator_protocol_pubkey`](#iota_system_iota_system_update_candidate_validator_protocol_pubkey)
-  [Function `update_validator_next_epoch_network_pubkey`](#iota_system_iota_system_update_validator_next_epoch_network_pubkey)
-  [Function `update_candidate_validator_network_pubkey`](#iota_system_iota_system_update_candidate_validator_network_pubkey)
-  [Function `validator_address_by_pool_id`](#iota_system_iota_system_validator_address_by_pool_id)
-  [Function `pool_exchange_rates`](#iota_system_iota_system_pool_exchange_rates)
-  [Function `active_validator_addresses`](#iota_system_iota_system_active_validator_addresses)
-  [Function `committee_validator_addresses`](#iota_system_iota_system_committee_validator_addresses)
-  [Function `load_iota_system_admin_cap`](#iota_system_iota_system_load_iota_system_admin_cap)
-  [Function `advance_epoch`](#iota_system_iota_system_advance_epoch)
-  [Function `load_system_state`](#iota_system_iota_system_load_system_state)
-  [Function `load_system_state_mut`](#iota_system_iota_system_load_system_state_mut)
-  [Function `load_inner_maybe_upgrade`](#iota_system_iota_system_load_inner_maybe_upgrade)
-  [Function `validator_voting_powers`](#iota_system_iota_system_validator_voting_powers)
-  [Function `get_total_iota_supply`](#iota_system_iota_system_get_total_iota_supply)


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
<b>use</b> <a href="../../dependencies/iota/pay.md#iota_pay">iota::pay</a>;
<b>use</b> <a href="../../dependencies/iota/priority_queue.md#iota_priority_queue">iota::priority_queue</a>;
<b>use</b> <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap">iota::system_admin_cap</a>;
<b>use</b> <a href="../../dependencies/iota/table.md#iota_table">iota::table</a>;
<b>use</b> <a href="../../dependencies/iota/table_vec.md#iota_table_vec">iota::table_vec</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/iota/vec_set.md#iota_vec_set">iota::vec_set</a>;
<b>use</b> <a href="../../dependencies/iota/versioned.md#iota_versioned">iota::versioned</a>;
<b>use</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner">iota_system::iota_system_state_inner</a>;
<b>use</b> <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool">iota_system::staking_pool</a>;
<b>use</b> <a href="../../dependencies/iota_system/storage_fund.md#iota_system_storage_fund">iota_system::storage_fund</a>;
<b>use</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator">iota_system::validator</a>;
<b>use</b> <a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap">iota_system::validator_cap</a>;
<b>use</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set">iota_system::validator_set</a>;
<b>use</b> <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper">iota_system::validator_wrapper</a>;
<b>use</b> <a href="../../dependencies/iota_system/voting_power.md#iota_system_voting_power">iota_system::voting_power</a>;
<b>use</b> <a href="../../dependencies/std/address.md#std_address">std::address</a>;
<b>use</b> <a href="../../dependencies/std/ascii.md#std_ascii">std::ascii</a>;
<b>use</b> <a href="../../dependencies/std/bcs.md#std_bcs">std::bcs</a>;
<b>use</b> <a href="../../dependencies/std/option.md#std_option">std::option</a>;
<b>use</b> <a href="../../dependencies/std/string.md#std_string">std::string</a>;
<b>use</b> <a href="../../dependencies/std/type_name.md#std_type_name">std::type_name</a>;
<b>use</b> <a href="../../dependencies/std/u64.md#std_u64">std::u64</a>;
<b>use</b> <a href="../../dependencies/std/vector.md#std_vector">std::vector</a>;
</code></pre>



<a name="iota_system_iota_system_IotaSystemState"></a>

## Struct `IotaSystemState`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a> <b>has</b> key
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
<code>version: u64</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_system_iota_system_ENotSystemAddress"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_ENotSystemAddress">ENotSystemAddress</a>: u64 = 0;
</code></pre>



<a name="iota_system_iota_system_EWrongInnerVersion"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_EWrongInnerVersion">EWrongInnerVersion</a>: u64 = 1;
</code></pre>



<a name="iota_system_iota_system_create"></a>

## Function `create`

Create a new IotaSystemState object and make it shared.
This function will be called only once in genesis.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_create">create</a>(id: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>, iota_treasury_cap: <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>, validators: vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, storage_fund: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, protocol_version: u64, epoch_start_timestamp_ms: u64, parameters: <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemParametersV1">iota_system::iota_system_state_inner::SystemParametersV1</a>, iota_system_admin_cap: <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">iota::system_admin_cap::IotaSystemAdminCap</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_create">create</a>(
    id: UID,
    iota_treasury_cap: IotaTreasuryCap,
    validators: vector&lt;ValidatorV1&gt;,
    storage_fund: Balance&lt;IOTA&gt;,
    protocol_version: u64,
    epoch_start_timestamp_ms: u64,
    parameters: SystemParametersV1,
    iota_system_admin_cap: IotaSystemAdminCap,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> system_state = iota_system_state_inner::create(
        iota_treasury_cap,
        validators,
        storage_fund,
        protocol_version,
        epoch_start_timestamp_ms,
        parameters,
        iota_system_admin_cap,
        ctx,
    );
    <b>let</b> version = iota_system_state_inner::genesis_system_state_version();
    <b>let</b> <b>mut</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a> {
        id,
        version,
    };
    dynamic_field::add(&<b>mut</b> self.id, version, system_state);
    transfer::share_object(self);
}
</code></pre>



</details>

<a name="iota_system_iota_system_request_add_validator_candidate"></a>

## Function `request_add_validator_candidate`

Can be called by anyone who wishes to become a validator candidate and starts accruing delegated
stakes in their staking pool. Once they have at least <code>MIN_VALIDATOR_JOINING_STAKE</code> amount of stake they
can call <code><a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_validator">request_add_validator</a></code> to officially become an active validator at the next epoch.
Aborts if the caller is already a pending or active validator, or a validator candidate.
Note: <code>proof_of_possession</code> MUST be a valid signature using iota_address and authority_pubkey_bytes.
To produce a valid PoP, run [fn test_proof_of_possession].


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_validator_candidate">request_add_validator_candidate</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, authority_pubkey_bytes: vector&lt;u8&gt;, network_pubkey_bytes: vector&lt;u8&gt;, protocol_pubkey_bytes: vector&lt;u8&gt;, proof_of_possession: vector&lt;u8&gt;, name: vector&lt;u8&gt;, description: vector&lt;u8&gt;, image_url: vector&lt;u8&gt;, project_url: vector&lt;u8&gt;, net_address: vector&lt;u8&gt;, p2p_address: vector&lt;u8&gt;, primary_address: vector&lt;u8&gt;, gas_price: u64, commission_rate: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_validator_candidate">request_add_validator_candidate</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    authority_pubkey_bytes: vector&lt;u8&gt;,
    network_pubkey_bytes: vector&lt;u8&gt;,
    protocol_pubkey_bytes: vector&lt;u8&gt;,
    proof_of_possession: vector&lt;u8&gt;,
    name: vector&lt;u8&gt;,
    description: vector&lt;u8&gt;,
    image_url: vector&lt;u8&gt;,
    project_url: vector&lt;u8&gt;,
    net_address: vector&lt;u8&gt;,
    p2p_address: vector&lt;u8&gt;,
    primary_address: vector&lt;u8&gt;,
    gas_price: u64,
    commission_rate: u64,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_validator_candidate">request_add_validator_candidate</a>(
        authority_pubkey_bytes,
        network_pubkey_bytes,
        protocol_pubkey_bytes,
        proof_of_possession,
        name,
        description,
        image_url,
        project_url,
        net_address,
        p2p_address,
        primary_address,
        gas_price,
        commission_rate,
        ctx,
    )
}
</code></pre>



</details>

<a name="iota_system_iota_system_request_remove_validator_candidate"></a>

## Function `request_remove_validator_candidate`

Called by a validator candidate to remove themselves from the candidacy. After this call
their staking pool becomes deactivate.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_remove_validator_candidate">request_remove_validator_candidate</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_remove_validator_candidate">request_remove_validator_candidate</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_remove_validator_candidate">request_remove_validator_candidate</a>(ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_request_add_validator"></a>

## Function `request_add_validator`

Called by a validator candidate to add themselves to the active validator set beginning next epoch.
Aborts if the validator is a duplicate with one of the pending or active validators, or if the amount of
stake the validator has doesn't meet the min threshold, or if the number of new validators for the next
epoch has already reached the maximum.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_validator">request_add_validator</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_validator">request_add_validator</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>, ctx: &<b>mut</b> TxContext) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_validator">request_add_validator</a>(ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_request_remove_validator"></a>

## Function `request_remove_validator`

A validator can call this function to request a removal in the next epoch.
We use the sender of <code>ctx</code> to look up the validator
(i.e. sender must match the iota_address in the validator).
At the end of the epoch, the <code>validator</code> object will be returned to the iota_address
of the validator.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_remove_validator">request_remove_validator</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_remove_validator">request_remove_validator</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>, ctx: &<b>mut</b> TxContext) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_remove_validator">request_remove_validator</a>(ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_request_set_gas_price"></a>

## Function `request_set_gas_price`



<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_set_gas_price">request_set_gas_price</a>(_wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, _cap: &<a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap_UnverifiedValidatorOperationCap">iota_system::validator_cap::UnverifiedValidatorOperationCap</a>, _new_gas_price: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_set_gas_price">request_set_gas_price</a>(
    _wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    _cap: &UnverifiedValidatorOperationCap,
    _new_gas_price: u64,
) {}
</code></pre>



</details>

<a name="iota_system_iota_system_set_candidate_validator_gas_price"></a>

## Function `set_candidate_validator_gas_price`



<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_set_candidate_validator_gas_price">set_candidate_validator_gas_price</a>(_wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, _cap: &<a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap_UnverifiedValidatorOperationCap">iota_system::validator_cap::UnverifiedValidatorOperationCap</a>, _new_gas_price: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_set_candidate_validator_gas_price">set_candidate_validator_gas_price</a>(
    _wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    _cap: &UnverifiedValidatorOperationCap,
    _new_gas_price: u64,
) {}
</code></pre>



</details>

<a name="iota_system_iota_system_request_set_commission_rate"></a>

## Function `request_set_commission_rate`

A validator can call this entry function to set a new commission rate, updated at the end of
the epoch.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_set_commission_rate">request_set_commission_rate</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, new_commission_rate: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_set_commission_rate">request_set_commission_rate</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    new_commission_rate: u64,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_set_commission_rate">request_set_commission_rate</a>(new_commission_rate, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_set_candidate_validator_commission_rate"></a>

## Function `set_candidate_validator_commission_rate`

This entry function is used to set new commission rate for candidate validators


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_set_candidate_validator_commission_rate">set_candidate_validator_commission_rate</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, new_commission_rate: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_set_candidate_validator_commission_rate">set_candidate_validator_commission_rate</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    new_commission_rate: u64,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_set_candidate_validator_commission_rate">set_candidate_validator_commission_rate</a>(new_commission_rate, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_request_add_stake"></a>

## Function `request_add_stake`

Add stake to a validator's staking pool.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_stake">request_add_stake</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, stake: <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, validator_address: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_stake">request_add_stake</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    stake: Coin&lt;IOTA&gt;,
    validator_address: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> staked_iota = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_stake_non_entry">request_add_stake_non_entry</a>(wrapper, stake, validator_address, ctx);
    transfer::public_transfer(staked_iota, ctx.sender());
}
</code></pre>



</details>

<a name="iota_system_iota_system_request_add_stake_non_entry"></a>

## Function `request_add_stake_non_entry`

The non-entry version of <code><a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_stake">request_add_stake</a></code>, which returns the staked IOTA instead of transferring it to the sender.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_stake_non_entry">request_add_stake_non_entry</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, stake: <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, validator_address: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_stake_non_entry">request_add_stake_non_entry</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    stake: Coin&lt;IOTA&gt;,
    validator_address: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
): StakedIota {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_stake">request_add_stake</a>(stake, validator_address, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_request_add_stake_mul_coin"></a>

## Function `request_add_stake_mul_coin`

Add stake to a validator's staking pool using multiple coins.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_stake_mul_coin">request_add_stake_mul_coin</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, stakes: vector&lt;<a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;&gt;, stake_amount: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, validator_address: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_stake_mul_coin">request_add_stake_mul_coin</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    stakes: vector&lt;Coin&lt;IOTA&gt;&gt;,
    stake_amount: option::Option&lt;u64&gt;,
    validator_address: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    <b>let</b> staked_iota = self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_add_stake_mul_coin">request_add_stake_mul_coin</a>(stakes, stake_amount, validator_address, ctx);
    transfer::public_transfer(staked_iota, ctx.sender());
}
</code></pre>



</details>

<a name="iota_system_iota_system_request_withdraw_stake"></a>

## Function `request_withdraw_stake`

Withdraw stake from a validator's staking pool.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_withdraw_stake">request_withdraw_stake</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, staked_iota: <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_withdraw_stake">request_withdraw_stake</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    staked_iota: StakedIota,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> withdrawn_stake = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_withdraw_stake_non_entry">request_withdraw_stake_non_entry</a>(wrapper, staked_iota, ctx);
    transfer::public_transfer(withdrawn_stake.into_coin(ctx), ctx.sender());
}
</code></pre>



</details>

<a name="iota_system_iota_system_request_withdraw_stake_non_entry"></a>

## Function `request_withdraw_stake_non_entry`

Non-entry version of <code><a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_withdraw_stake">request_withdraw_stake</a></code> that returns the withdrawn IOTA instead of transferring it to the sender.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_withdraw_stake_non_entry">request_withdraw_stake_non_entry</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, staked_iota: <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_withdraw_stake_non_entry">request_withdraw_stake_non_entry</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    staked_iota: StakedIota,
    ctx: &<b>mut</b> TxContext,
): Balance&lt;IOTA&gt; {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_request_withdraw_stake">request_withdraw_stake</a>(staked_iota, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_report_validator"></a>

## Function `report_validator`

Report a validator as a bad or non-performant actor in the system.
Succeeds if all the following are satisfied:
1. both the reporter in <code>cap</code> and the input <code>reportee_addr</code> are committee validators.
2. reporter and reportee not the same address.
3. the cap object is still valid.
This function is idempotent.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_report_validator">report_validator</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, cap: &<a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap_UnverifiedValidatorOperationCap">iota_system::validator_cap::UnverifiedValidatorOperationCap</a>, reportee_addr: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_report_validator">report_validator</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    cap: &UnverifiedValidatorOperationCap,
    reportee_addr: <b>address</b>,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_report_validator">report_validator</a>(cap, reportee_addr)
}
</code></pre>



</details>

<a name="iota_system_iota_system_undo_report_validator"></a>

## Function `undo_report_validator`

Undo a <code><a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_report_validator">report_validator</a></code> action. Aborts if
1. the reportee is not a currently committee validator or
2. the sender has not previously reported the <code>reportee_addr</code>, or
3. the cap is not valid


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_undo_report_validator">undo_report_validator</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, cap: &<a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap_UnverifiedValidatorOperationCap">iota_system::validator_cap::UnverifiedValidatorOperationCap</a>, reportee_addr: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_undo_report_validator">undo_report_validator</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    cap: &UnverifiedValidatorOperationCap,
    reportee_addr: <b>address</b>,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_undo_report_validator">undo_report_validator</a>(cap, reportee_addr)
}
</code></pre>



</details>

<a name="iota_system_iota_system_rotate_operation_cap"></a>

## Function `rotate_operation_cap`

Create a new <code>UnverifiedValidatorOperationCap</code>, transfer it to the
validator and registers it. The original object is thus revoked.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_rotate_operation_cap">rotate_operation_cap</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_rotate_operation_cap">rotate_operation_cap</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>, ctx: &<b>mut</b> TxContext) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_rotate_operation_cap">rotate_operation_cap</a>(ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_validator_name"></a>

## Function `update_validator_name`

Update a validator's name.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_name">update_validator_name</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, name: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_name">update_validator_name</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    name: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_name">update_validator_name</a>(name, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_validator_description"></a>

## Function `update_validator_description`

Update a validator's description


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_description">update_validator_description</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, description: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_description">update_validator_description</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    description: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_description">update_validator_description</a>(description, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_validator_image_url"></a>

## Function `update_validator_image_url`

Update a validator's image url


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_image_url">update_validator_image_url</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, image_url: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_image_url">update_validator_image_url</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    image_url: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_image_url">update_validator_image_url</a>(image_url, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_validator_project_url"></a>

## Function `update_validator_project_url`

Update a validator's project url


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_project_url">update_validator_project_url</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, project_url: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_project_url">update_validator_project_url</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    project_url: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_project_url">update_validator_project_url</a>(project_url, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_validator_next_epoch_network_address"></a>

## Function `update_validator_next_epoch_network_address`

Update a validator's network address.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_network_address">update_validator_next_epoch_network_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, network_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_network_address">update_validator_next_epoch_network_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    network_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_network_address">update_validator_next_epoch_network_address</a>(network_address, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_candidate_validator_network_address"></a>

## Function `update_candidate_validator_network_address`

Update candidate validator's network address.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_network_address">update_candidate_validator_network_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, network_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_network_address">update_candidate_validator_network_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    network_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_network_address">update_candidate_validator_network_address</a>(network_address, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_validator_next_epoch_p2p_address"></a>

## Function `update_validator_next_epoch_p2p_address`

Update a validator's p2p address.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_p2p_address">update_validator_next_epoch_p2p_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, p2p_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_p2p_address">update_validator_next_epoch_p2p_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    p2p_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_p2p_address">update_validator_next_epoch_p2p_address</a>(p2p_address, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_candidate_validator_p2p_address"></a>

## Function `update_candidate_validator_p2p_address`

Update candidate validator's p2p address.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_p2p_address">update_candidate_validator_p2p_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, p2p_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_p2p_address">update_candidate_validator_p2p_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    p2p_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_p2p_address">update_candidate_validator_p2p_address</a>(p2p_address, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_validator_next_epoch_primary_address"></a>

## Function `update_validator_next_epoch_primary_address`

Update a validator's primary address.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_primary_address">update_validator_next_epoch_primary_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, primary_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_primary_address">update_validator_next_epoch_primary_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    primary_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_primary_address">update_validator_next_epoch_primary_address</a>(primary_address, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_candidate_validator_primary_address"></a>

## Function `update_candidate_validator_primary_address`

Update candidate validator's primary address.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_primary_address">update_candidate_validator_primary_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, primary_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_primary_address">update_candidate_validator_primary_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    primary_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_primary_address">update_candidate_validator_primary_address</a>(primary_address, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_validator_next_epoch_authority_pubkey"></a>

## Function `update_validator_next_epoch_authority_pubkey`

Update a validator's public key of authority key and proof of possession.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_authority_pubkey">update_validator_next_epoch_authority_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, authority_pubkey: vector&lt;u8&gt;, proof_of_possession: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_authority_pubkey">update_validator_next_epoch_authority_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    authority_pubkey: vector&lt;u8&gt;,
    proof_of_possession: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_authority_pubkey">update_validator_next_epoch_authority_pubkey</a>(authority_pubkey, proof_of_possession, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_candidate_validator_authority_pubkey"></a>

## Function `update_candidate_validator_authority_pubkey`

Update candidate validator's public key of authority key and proof of possession.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_authority_pubkey">update_candidate_validator_authority_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, authority_pubkey: vector&lt;u8&gt;, proof_of_possession: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_authority_pubkey">update_candidate_validator_authority_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    authority_pubkey: vector&lt;u8&gt;,
    proof_of_possession: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_authority_pubkey">update_candidate_validator_authority_pubkey</a>(authority_pubkey, proof_of_possession, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_validator_next_epoch_protocol_pubkey"></a>

## Function `update_validator_next_epoch_protocol_pubkey`

Update a validator's public key of protocol key.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_protocol_pubkey">update_validator_next_epoch_protocol_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, protocol_pubkey: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_protocol_pubkey">update_validator_next_epoch_protocol_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    protocol_pubkey: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_protocol_pubkey">update_validator_next_epoch_protocol_pubkey</a>(protocol_pubkey, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_candidate_validator_protocol_pubkey"></a>

## Function `update_candidate_validator_protocol_pubkey`

Update candidate validator's public key of protocol key.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_protocol_pubkey">update_candidate_validator_protocol_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, protocol_pubkey: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_protocol_pubkey">update_candidate_validator_protocol_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    protocol_pubkey: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_protocol_pubkey">update_candidate_validator_protocol_pubkey</a>(protocol_pubkey, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_validator_next_epoch_network_pubkey"></a>

## Function `update_validator_next_epoch_network_pubkey`

Update a validator's public key of network key.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_network_pubkey">update_validator_next_epoch_network_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, network_pubkey: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_network_pubkey">update_validator_next_epoch_network_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    network_pubkey: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_validator_next_epoch_network_pubkey">update_validator_next_epoch_network_pubkey</a>(network_pubkey, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_update_candidate_validator_network_pubkey"></a>

## Function `update_candidate_validator_network_pubkey`

Update candidate validator's public key of network key.


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_network_pubkey">update_candidate_validator_network_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, network_pubkey: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>entry</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_network_pubkey">update_candidate_validator_network_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    network_pubkey: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_update_candidate_validator_network_pubkey">update_candidate_validator_network_pubkey</a>(network_pubkey, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_validator_address_by_pool_id"></a>

## Function `validator_address_by_pool_id`

Getter of the validator's address by the pool ID.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_validator_address_by_pool_id">validator_address_by_pool_id</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, pool_id: &<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): <b>address</b>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_validator_address_by_pool_id">validator_address_by_pool_id</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>, pool_id: &ID): <b>address</b> {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_validator_address_by_pool_id">validator_address_by_pool_id</a>(pool_id)
}
</code></pre>



</details>

<a name="iota_system_iota_system_pool_exchange_rates"></a>

## Function `pool_exchange_rates`

Getter of the pool token exchange rate of a staking pool. Works for both active and inactive pools.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_pool_exchange_rates">pool_exchange_rates</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, pool_id: &<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): &<a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;u64, <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_PoolTokenExchangeRate">iota_system::staking_pool::PoolTokenExchangeRate</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_pool_exchange_rates">pool_exchange_rates</a>(
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    pool_id: &ID,
): &Table&lt;u64, PoolTokenExchangeRate&gt; {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_pool_exchange_rates">pool_exchange_rates</a>(pool_id)
}
</code></pre>



</details>

<a name="iota_system_iota_system_active_validator_addresses"></a>

## Function `active_validator_addresses`

Getter returning addresses of the currently active validators.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_active_validator_addresses">active_validator_addresses</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>): vector&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_active_validator_addresses">active_validator_addresses</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>): vector&lt;<b>address</b>&gt; {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state">load_system_state</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_active_validator_addresses">active_validator_addresses</a>()
}
</code></pre>



</details>

<a name="iota_system_iota_system_committee_validator_addresses"></a>

## Function `committee_validator_addresses`

Getter returning addresses of the current committee validators.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_committee_validator_addresses">committee_validator_addresses</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>): vector&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_committee_validator_addresses">committee_validator_addresses</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>): vector&lt;<b>address</b>&gt; {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state">load_system_state</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_committee_validator_addresses">committee_validator_addresses</a>()
}
</code></pre>



</details>

<a name="iota_system_iota_system_load_iota_system_admin_cap"></a>

## Function `load_iota_system_admin_cap`

Returns the IOTA system admin capability reference.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_iota_system_admin_cap">load_iota_system_admin_cap</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>): &<a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">iota::system_admin_cap::IotaSystemAdminCap</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_iota_system_admin_cap">load_iota_system_admin_cap</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>): &IotaSystemAdminCap {
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state">load_system_state</a>().iota_system_admin_cap()
}
</code></pre>



</details>

<a name="iota_system_iota_system_advance_epoch"></a>

## Function `advance_epoch`

This function should be called at the end of an epoch, and advances the system to the next epoch.
It does the following things:
1. Add storage charge to the storage fund.
2. Burn the storage rebates from the storage fund. These are already refunded to transaction sender's
gas coins.
3. Mint or burn IOTA tokens depending on whether the validator subsidy is greater
or smaller than the computation reward.
4. Distribute the rewards to the validators.
5. Burn any leftover rewards.
6. Update all validators.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_advance_epoch">advance_epoch</a>(validator_subsidy: u64, storage_charge: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, computation_charge: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, computation_charge_burned: u64, wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>, new_epoch: u64, next_protocol_version: u64, storage_rebate: u64, non_refundable_storage_fee: u64, reward_slashing_rate: u64, epoch_start_timestamp_ms: u64, max_committee_members_count: u64, eligible_active_validators: vector&lt;u64&gt;, scores: vector&lt;u64&gt;, adjust_rewards_by_score: bool, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_advance_epoch">advance_epoch</a>(
    validator_subsidy: u64,
    storage_charge: Balance&lt;IOTA&gt;,
    computation_charge: Balance&lt;IOTA&gt;,
    computation_charge_burned: u64,
    wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>,
    new_epoch: u64,
    next_protocol_version: u64,
    storage_rebate: u64,
    non_refundable_storage_fee: u64,
    reward_slashing_rate: u64, // how much rewards are slashed to punish a validator, in bps.
    epoch_start_timestamp_ms: u64, // Timestamp of the epoch start
    max_committee_members_count: u64,
    eligible_active_validators: vector&lt;u64&gt;,
    scores : vector&lt;u64&gt;,
    adjust_rewards_by_score: bool,
    ctx: &<b>mut</b> TxContext,
): Balance&lt;IOTA&gt; {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(wrapper);
    // ValidatorV1 will make a special system call with sender set <b>as</b> 0x0.
    <b>assert</b>!(ctx.sender() == @0x0, <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_ENotSystemAddress">ENotSystemAddress</a>);
    <b>let</b> storage_rebate = self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_advance_epoch">advance_epoch</a>(
        new_epoch,
        next_protocol_version,
        validator_subsidy,
        storage_charge,
        computation_charge,
        computation_charge_burned,
        storage_rebate,
        non_refundable_storage_fee,
        reward_slashing_rate,
        epoch_start_timestamp_ms,
        max_committee_members_count,
        eligible_active_validators,
        scores,
        adjust_rewards_by_score,
        ctx,
    );
    storage_rebate
}
</code></pre>



</details>

<a name="iota_system_iota_system_load_system_state"></a>

## Function `load_system_state`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state">load_system_state</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>): &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state">load_system_state</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>): &IotaSystemStateV2 {
    <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_inner_maybe_upgrade">load_inner_maybe_upgrade</a>(self)
}
</code></pre>



</details>

<a name="iota_system_iota_system_load_system_state_mut"></a>

## Function `load_system_state_mut`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>): &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state_mut">load_system_state_mut</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>): &<b>mut</b> IotaSystemStateV2 {
    <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_inner_maybe_upgrade">load_inner_maybe_upgrade</a>(self)
}
</code></pre>



</details>

<a name="iota_system_iota_system_load_inner_maybe_upgrade"></a>

## Function `load_inner_maybe_upgrade`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_inner_maybe_upgrade">load_inner_maybe_upgrade</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>): &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_inner_maybe_upgrade">load_inner_maybe_upgrade</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>): &<b>mut</b> IotaSystemStateV2 {
    <b>if</b> (self.version == 1) {
        <b>let</b> v1: IotaSystemStateV1 = dynamic_field::remove(
            &<b>mut</b> self.id,
            self.version,
        );
        <b>let</b> v2 = v1.v1_to_v2();
        self.version = 2;
        dynamic_field::add(&<b>mut</b> self.id, self.version, v2);
    };
    <b>let</b> inner: &<b>mut</b> IotaSystemStateV2 = dynamic_field::borrow_mut(
        &<b>mut</b> self.id,
        self.version,
    );
    <b>assert</b>!(inner.system_state_version() == self.version, <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_EWrongInnerVersion">EWrongInnerVersion</a>);
    inner
}
</code></pre>



</details>

<a name="iota_system_iota_system_validator_voting_powers"></a>

## Function `validator_voting_powers`

Returns the voting power of the active validators, values are voting power in the scale of 10000.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_validator_voting_powers">validator_voting_powers</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>): <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_validator_voting_powers">validator_voting_powers</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>): VecMap&lt;<b>address</b>, u64&gt; {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state">load_system_state</a>(wrapper);
    iota_system_state_inner::committee_validator_voting_powers(self)
}
</code></pre>



</details>

<a name="iota_system_iota_system_get_total_iota_supply"></a>

## Function `get_total_iota_supply`

Returns the total iota supply.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_get_total_iota_supply">get_total_iota_supply</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">iota_system::iota_system::IotaSystemState</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_get_total_iota_supply">get_total_iota_supply</a>(wrapper: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_IotaSystemState">IotaSystemState</a>): u64 {
    <b>let</b> self = <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_load_system_state">load_system_state</a>(wrapper);
    self.<a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system_get_total_iota_supply">get_total_iota_supply</a>()
}
</code></pre>



</details>
