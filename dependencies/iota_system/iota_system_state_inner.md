
<a name="iota_system_iota_system_state_inner"></a>

# Module `iota_system::iota_system_state_inner`



-  [Struct `SystemParametersV1`](#iota_system_iota_system_state_inner_SystemParametersV1)
-  [Struct `IotaSystemStateV1`](#iota_system_iota_system_state_inner_IotaSystemStateV1)
-  [Struct `IotaSystemStateV2`](#iota_system_iota_system_state_inner_IotaSystemStateV2)
-  [Struct `SystemEpochInfoEventV1`](#iota_system_iota_system_state_inner_SystemEpochInfoEventV1)
-  [Struct `SystemEpochInfoEventV2`](#iota_system_iota_system_state_inner_SystemEpochInfoEventV2)
-  [Constants](#@Constants_0)
-  [Function `create`](#iota_system_iota_system_state_inner_create)
-  [Function `create_system_parameters`](#iota_system_iota_system_state_inner_create_system_parameters)
-  [Function `v1_to_v2`](#iota_system_iota_system_state_inner_v1_to_v2)
-  [Function `request_add_validator_candidate`](#iota_system_iota_system_state_inner_request_add_validator_candidate)
-  [Function `request_remove_validator_candidate`](#iota_system_iota_system_state_inner_request_remove_validator_candidate)
-  [Function `request_add_validator`](#iota_system_iota_system_state_inner_request_add_validator)
-  [Function `request_remove_validator`](#iota_system_iota_system_state_inner_request_remove_validator)
-  [Function `request_set_commission_rate`](#iota_system_iota_system_state_inner_request_set_commission_rate)
-  [Function `set_candidate_validator_commission_rate`](#iota_system_iota_system_state_inner_set_candidate_validator_commission_rate)
-  [Function `request_add_stake`](#iota_system_iota_system_state_inner_request_add_stake)
-  [Function `request_add_stake_mul_coin`](#iota_system_iota_system_state_inner_request_add_stake_mul_coin)
-  [Function `request_withdraw_stake`](#iota_system_iota_system_state_inner_request_withdraw_stake)
-  [Function `report_validator`](#iota_system_iota_system_state_inner_report_validator)
-  [Function `undo_report_validator`](#iota_system_iota_system_state_inner_undo_report_validator)
-  [Function `report_validator_impl`](#iota_system_iota_system_state_inner_report_validator_impl)
-  [Function `undo_report_validator_impl`](#iota_system_iota_system_state_inner_undo_report_validator_impl)
-  [Function `rotate_operation_cap`](#iota_system_iota_system_state_inner_rotate_operation_cap)
-  [Function `update_validator_name`](#iota_system_iota_system_state_inner_update_validator_name)
-  [Function `update_validator_description`](#iota_system_iota_system_state_inner_update_validator_description)
-  [Function `update_validator_image_url`](#iota_system_iota_system_state_inner_update_validator_image_url)
-  [Function `update_validator_project_url`](#iota_system_iota_system_state_inner_update_validator_project_url)
-  [Function `update_validator_next_epoch_network_address`](#iota_system_iota_system_state_inner_update_validator_next_epoch_network_address)
-  [Function `update_candidate_validator_network_address`](#iota_system_iota_system_state_inner_update_candidate_validator_network_address)
-  [Function `update_validator_next_epoch_p2p_address`](#iota_system_iota_system_state_inner_update_validator_next_epoch_p2p_address)
-  [Function `update_candidate_validator_p2p_address`](#iota_system_iota_system_state_inner_update_candidate_validator_p2p_address)
-  [Function `update_validator_next_epoch_primary_address`](#iota_system_iota_system_state_inner_update_validator_next_epoch_primary_address)
-  [Function `update_candidate_validator_primary_address`](#iota_system_iota_system_state_inner_update_candidate_validator_primary_address)
-  [Function `update_validator_next_epoch_authority_pubkey`](#iota_system_iota_system_state_inner_update_validator_next_epoch_authority_pubkey)
-  [Function `update_candidate_validator_authority_pubkey`](#iota_system_iota_system_state_inner_update_candidate_validator_authority_pubkey)
-  [Function `update_validator_next_epoch_protocol_pubkey`](#iota_system_iota_system_state_inner_update_validator_next_epoch_protocol_pubkey)
-  [Function `update_candidate_validator_protocol_pubkey`](#iota_system_iota_system_state_inner_update_candidate_validator_protocol_pubkey)
-  [Function `update_validator_next_epoch_network_pubkey`](#iota_system_iota_system_state_inner_update_validator_next_epoch_network_pubkey)
-  [Function `update_candidate_validator_network_pubkey`](#iota_system_iota_system_state_inner_update_candidate_validator_network_pubkey)
-  [Function `advance_epoch`](#iota_system_iota_system_state_inner_advance_epoch)
-  [Function `match_computation_charge_burned_to_validator_subsidy`](#iota_system_iota_system_state_inner_match_computation_charge_burned_to_validator_subsidy)
-  [Function `epoch`](#iota_system_iota_system_state_inner_epoch)
-  [Function `protocol_version`](#iota_system_iota_system_state_inner_protocol_version)
-  [Function `system_state_version`](#iota_system_iota_system_state_inner_system_state_version)
-  [Function `iota_system_admin_cap`](#iota_system_iota_system_state_inner_iota_system_admin_cap)
-  [Function `genesis_system_state_version`](#iota_system_iota_system_state_inner_genesis_system_state_version)
-  [Function `epoch_start_timestamp_ms`](#iota_system_iota_system_state_inner_epoch_start_timestamp_ms)
-  [Function `validator_stake_amount`](#iota_system_iota_system_state_inner_validator_stake_amount)
-  [Function `committee_validator_voting_powers`](#iota_system_iota_system_state_inner_committee_validator_voting_powers)
-  [Function `validator_staking_pool_id`](#iota_system_iota_system_state_inner_validator_staking_pool_id)
-  [Function `validator_staking_pool_mappings`](#iota_system_iota_system_state_inner_validator_staking_pool_mappings)
-  [Function `get_total_iota_supply`](#iota_system_iota_system_state_inner_get_total_iota_supply)
-  [Function `get_reporters_of`](#iota_system_iota_system_state_inner_get_reporters_of)
-  [Function `get_storage_fund_total_balance`](#iota_system_iota_system_state_inner_get_storage_fund_total_balance)
-  [Function `get_storage_fund_object_rebates`](#iota_system_iota_system_state_inner_get_storage_fund_object_rebates)
-  [Function `validator_address_by_pool_id`](#iota_system_iota_system_state_inner_validator_address_by_pool_id)
-  [Function `pool_exchange_rates`](#iota_system_iota_system_state_inner_pool_exchange_rates)
-  [Function `active_validator_addresses`](#iota_system_iota_system_state_inner_active_validator_addresses)
-  [Function `committee_validator_addresses`](#iota_system_iota_system_state_inner_committee_validator_addresses)
-  [Function `extract_coin_balance`](#iota_system_iota_system_state_inner_extract_coin_balance)


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



<a name="iota_system_iota_system_state_inner_SystemParametersV1"></a>

## Struct `SystemParametersV1`

A list of system config parameters.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemParametersV1">SystemParametersV1</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>epoch_duration_ms: u64</code>
</dt>
<dd>
 The duration of an epoch, in milliseconds.
</dd>
<dt>
<code>min_validator_count: u64</code>
</dt>
<dd>
 Minimum number of active validators at any moment.
</dd>
<dt>
<code>max_validator_count: u64</code>
</dt>
<dd>
 Maximum number of active validators at any moment.
 We do not allow the number of validators in any epoch to go above this.
</dd>
<dt>
<code>min_validator_joining_stake: u64</code>
</dt>
<dd>
 Lower-bound on the amount of stake required to become a validator.
</dd>
<dt>
<code>validator_low_stake_threshold: u64</code>
</dt>
<dd>
 Validators with stake amount below <code>validator_low_stake_threshold</code> are considered to
 have low stake and will be escorted out of the validator set after being below this
 threshold for more than <code>validator_low_stake_grace_period</code> number of epochs.
</dd>
<dt>
<code>validator_very_low_stake_threshold: u64</code>
</dt>
<dd>
 Validators with stake below <code>validator_very_low_stake_threshold</code> will be removed
 immediately at epoch change, no grace period.
</dd>
<dt>
<code>validator_low_stake_grace_period: u64</code>
</dt>
<dd>
 A validator can have stake below <code>validator_low_stake_threshold</code>
 for this many epochs before being kicked out.
</dd>
<dt>
<code>extra_fields: <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a></code>
</dt>
<dd>
 Any extra fields that's not defined statically.
</dd>
</dl>


</details>

<a name="iota_system_iota_system_state_inner_IotaSystemStateV1"></a>

## Struct `IotaSystemStateV1`

The top-level object containing all information of the IOTA system.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV1">IotaSystemStateV1</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>: u64</code>
</dt>
<dd>
 The current epoch ID, starting from 0.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>: u64</code>
</dt>
<dd>
 The current protocol version, starting from 1.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_system_state_version">system_state_version</a>: u64</code>
</dt>
<dd>
 The current version of the system state data structure type.
 This is always the same as IotaSystemState.version. Keeping a copy here so that
 we know what version it is by inspecting IotaSystemStateV1 as well.
</dd>
<dt>
<code>iota_treasury_cap: <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a></code>
</dt>
<dd>
 The IOTA's TreasuryCap.
</dd>
<dt>
<code>validators: <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a></code>
</dt>
<dd>
 Contains all information about the validators.
</dd>
<dt>
<code>storage_fund: <a href="../../dependencies/iota_system/storage_fund.md#iota_system_storage_fund_StorageFundV1">iota_system::storage_fund::StorageFundV1</a></code>
</dt>
<dd>
 The storage fund.
</dd>
<dt>
<code>parameters: <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemParametersV1">iota_system::iota_system_state_inner::SystemParametersV1</a></code>
</dt>
<dd>
 A list of system config parameters.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_iota_system_admin_cap">iota_system_admin_cap</a>: <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">iota::system_admin_cap::IotaSystemAdminCap</a></code>
</dt>
<dd>
 A capability allows to perform privileged IOTA system operations.
</dd>
<dt>
<code>reference_gas_price: u64</code>
</dt>
<dd>
 The reference gas price for the current epoch.
</dd>
<dt>
<code>validator_report_records: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;&gt;</code>
</dt>
<dd>
 A map storing the records of validator reporting each other.
 There is an entry in the map for each validator that has been reported
 at least once. The entry VecSet contains all the validators that reported
 them. If a validator has never been reported they don't have an entry in this map.
 This map persists across epoch: a peer continues being in a reported state until the
 reporter doesn't explicitly remove their report.
 Note that in case we want to support validator address change in future,
 the reports should be based on validator ids
</dd>
<dt>
<code>safe_mode: bool</code>
</dt>
<dd>
 Whether the system is running in a downgraded safe mode due to a non-recoverable bug.
 This is set whenever we failed to execute advance_epoch, and ended up executing advance_epoch_safe_mode.
 It can be reset once we are able to successfully execute advance_epoch.
 The rest of the fields starting with <code>safe_mode_</code> are accmulated during safe mode
 when advance_epoch_safe_mode is executed. They will eventually be processed once we
 are out of safe mode.
</dd>
<dt>
<code>safe_mode_storage_charges: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>safe_mode_computation_rewards: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>safe_mode_storage_rebates: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>safe_mode_non_refundable_storage_fee: u64</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>: u64</code>
</dt>
<dd>
 Unix timestamp of the current epoch start
</dd>
<dt>
<code>extra_fields: <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a></code>
</dt>
<dd>
 Any extra fields that's not defined statically.
</dd>
</dl>


</details>

<a name="iota_system_iota_system_state_inner_IotaSystemStateV2"></a>

## Struct `IotaSystemStateV2`

The top-level object containing all information of the Iota system.
An additional field <code>safe_mode_computation_charges_burned</code> is added over IotaSystemStateV1 to allow
for burning of base fees in safe mode when protocol_defined_base_fee is enabled in the protocol config.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>: u64</code>
</dt>
<dd>
 The current epoch ID, starting from 0.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>: u64</code>
</dt>
<dd>
 The current protocol version, starting from 1.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_system_state_version">system_state_version</a>: u64</code>
</dt>
<dd>
 The current version of the system state data structure type.
 This is always the same as IotaSystemState.version. Keeping a copy here so that
 we know what version it is by inspecting IotaSystemStateV2 as well.
</dd>
<dt>
<code>iota_treasury_cap: <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a></code>
</dt>
<dd>
 The IOTA's TreasuryCap.
</dd>
<dt>
<code>validators: <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a></code>
</dt>
<dd>
 Contains all information about the validators.
</dd>
<dt>
<code>storage_fund: <a href="../../dependencies/iota_system/storage_fund.md#iota_system_storage_fund_StorageFundV1">iota_system::storage_fund::StorageFundV1</a></code>
</dt>
<dd>
 The storage fund.
</dd>
<dt>
<code>parameters: <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemParametersV1">iota_system::iota_system_state_inner::SystemParametersV1</a></code>
</dt>
<dd>
 A list of system config parameters.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_iota_system_admin_cap">iota_system_admin_cap</a>: <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">iota::system_admin_cap::IotaSystemAdminCap</a></code>
</dt>
<dd>
 A capability allows to perform privileged IOTA system operations.
</dd>
<dt>
<code>reference_gas_price: u64</code>
</dt>
<dd>
 The reference gas price for the current epoch.
</dd>
<dt>
<code>validator_report_records: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;&gt;</code>
</dt>
<dd>
 A map storing the records of validator reporting each other.
 There is an entry in the map for each validator that has been reported
 at least once. The entry VecSet contains all the validators that reported
 them. If a validator has never been reported they don't have an entry in this map.
 This map persists across epoch: a peer continues being in a reported state until the
 reporter doesn't explicitly remove their report.
 Note that in case we want to support validator address change in future,
 the reports should be based on validator ids
</dd>
<dt>
<code>safe_mode: bool</code>
</dt>
<dd>
 Whether the system is running in a downgraded safe mode due to a non-recoverable bug.
 This is set whenever we failed to execute advance_epoch, and ended up executing advance_epoch_safe_mode.
 It can be reset once we are able to successfully execute advance_epoch.
 The rest of the fields starting with <code>safe_mode_</code> are accmulated during safe mode
 when advance_epoch_safe_mode is executed. They will eventually be processed once we
 are out of safe mode.
</dd>
<dt>
<code>safe_mode_storage_charges: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>safe_mode_computation_charges: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>safe_mode_computation_charges_burned: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>safe_mode_storage_rebates: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>safe_mode_non_refundable_storage_fee: u64</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>: u64</code>
</dt>
<dd>
 Unix timestamp of the current epoch start
</dd>
<dt>
<code>extra_fields: <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a></code>
</dt>
<dd>
 Any extra fields that's not defined statically.
</dd>
</dl>


</details>

<a name="iota_system_iota_system_state_inner_SystemEpochInfoEventV1"></a>

## Struct `SystemEpochInfoEventV1`

The first version of the event containing system-level epoch information,
emitted during the epoch advancement transaction.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemEpochInfoEventV1">SystemEpochInfoEventV1</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>: u64</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>reference_gas_price: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>total_stake: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>storage_charge: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>storage_rebate: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>storage_fund_balance: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>total_gas_fees: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>total_stake_rewards_distributed: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>burnt_tokens_amount: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>minted_tokens_amount: u64</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_system_iota_system_state_inner_SystemEpochInfoEventV2"></a>

## Struct `SystemEpochInfoEventV2`

The second version of the event containing system-level epoch information,
emitted during the epoch advancement transaction.
This version includes the tips_amount field to show how much of the total gas fees were paid to
validators (tips) rather than burned.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemEpochInfoEventV2">SystemEpochInfoEventV2</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>: u64</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>total_stake: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>storage_charge: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>storage_rebate: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>storage_fund_balance: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>total_gas_fees: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>total_stake_rewards_distributed: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>burnt_tokens_amount: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>minted_tokens_amount: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>tips_amount: u64</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_system_iota_system_state_inner_COMMITTEE_VALIDATOR_ONLY"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_COMMITTEE_VALIDATOR_ONLY">COMMITTEE_VALIDATOR_ONLY</a>: u8 = 1;
</code></pre>



<a name="iota_system_iota_system_state_inner_ACTIVE_OR_PENDING_VALIDATOR"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ACTIVE_OR_PENDING_VALIDATOR">ACTIVE_OR_PENDING_VALIDATOR</a>: u8 = 2;
</code></pre>



<a name="iota_system_iota_system_state_inner_ANY_VALIDATOR"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ANY_VALIDATOR">ANY_VALIDATOR</a>: u8 = 3;
</code></pre>



<a name="iota_system_iota_system_state_inner_SYSTEM_STATE_VERSION_V1"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SYSTEM_STATE_VERSION_V1">SYSTEM_STATE_VERSION_V1</a>: u64 = 1;
</code></pre>



<a name="iota_system_iota_system_state_inner_ENotCommitteeValidator"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ENotCommitteeValidator">ENotCommitteeValidator</a>: u64 = 0;
</code></pre>



<a name="iota_system_iota_system_state_inner_ELimitExceeded"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ELimitExceeded">ELimitExceeded</a>: u64 = 1;
</code></pre>



<a name="iota_system_iota_system_state_inner_ENotSystemAddress"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ENotSystemAddress">ENotSystemAddress</a>: u64 = 2;
</code></pre>



<a name="iota_system_iota_system_state_inner_ECannotReportOneself"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ECannotReportOneself">ECannotReportOneself</a>: u64 = 3;
</code></pre>



<a name="iota_system_iota_system_state_inner_EReportRecordNotFound"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_EReportRecordNotFound">EReportRecordNotFound</a>: u64 = 4;
</code></pre>



<a name="iota_system_iota_system_state_inner_EBpsTooLarge"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_EBpsTooLarge">EBpsTooLarge</a>: u64 = 5;
</code></pre>



<a name="iota_system_iota_system_state_inner_ESafeModeGasNotProcessed"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ESafeModeGasNotProcessed">ESafeModeGasNotProcessed</a>: u64 = 7;
</code></pre>



<a name="iota_system_iota_system_state_inner_EAdvancedToWrongEpoch"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_EAdvancedToWrongEpoch">EAdvancedToWrongEpoch</a>: u64 = 8;
</code></pre>



<a name="iota_system_iota_system_state_inner_BASIS_POINT_DENOMINATOR"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_BASIS_POINT_DENOMINATOR">BASIS_POINT_DENOMINATOR</a>: u128 = 10000;
</code></pre>



<a name="iota_system_iota_system_state_inner_create"></a>

## Function `create`

Create a new IotaSystemState object and make it shared.
This function will be called only once in genesis.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_create">create</a>(iota_treasury_cap: <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>, validators: vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, initial_storage_fund: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>: u64, <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>: u64, parameters: <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemParametersV1">iota_system::iota_system_state_inner::SystemParametersV1</a>, <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_iota_system_admin_cap">iota_system_admin_cap</a>: <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">iota::system_admin_cap::IotaSystemAdminCap</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV1">iota_system::iota_system_state_inner::IotaSystemStateV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_create">create</a>(
    iota_treasury_cap: IotaTreasuryCap,
    validators: vector&lt;ValidatorV1&gt;,
    initial_storage_fund: Balance&lt;IOTA&gt;,
    <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>: u64,
    <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>: u64,
    parameters: <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemParametersV1">SystemParametersV1</a>,
    <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_iota_system_admin_cap">iota_system_admin_cap</a>: IotaSystemAdminCap,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV1">IotaSystemStateV1</a> {
    <b>let</b> validators = validator_set::new_v1(validators, ctx);
    <b>let</b> reference_gas_price = validators.derive_reference_gas_price();
    // This type is fixed <b>as</b> it's created at genesis. It should not be updated during type upgrade.
    <b>let</b> system_state = <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV1">IotaSystemStateV1</a> {
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>: 0,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_system_state_version">system_state_version</a>: <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_genesis_system_state_version">genesis_system_state_version</a>(),
        iota_treasury_cap,
        validators,
        storage_fund: storage_fund::new(initial_storage_fund),
        parameters,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_iota_system_admin_cap">iota_system_admin_cap</a>,
        reference_gas_price,
        validator_report_records: vec_map::empty(),
        safe_mode: <b>false</b>,
        safe_mode_storage_charges: balance::zero(),
        safe_mode_computation_rewards: balance::zero(),
        safe_mode_storage_rebates: 0,
        safe_mode_non_refundable_storage_fee: 0,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>,
        extra_fields: bag::new(ctx),
    };
    system_state
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_create_system_parameters"></a>

## Function `create_system_parameters`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_create_system_parameters">create_system_parameters</a>(epoch_duration_ms: u64, max_validator_count: u64, min_validator_joining_stake: u64, validator_low_stake_threshold: u64, validator_very_low_stake_threshold: u64, validator_low_stake_grace_period: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemParametersV1">iota_system::iota_system_state_inner::SystemParametersV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_create_system_parameters">create_system_parameters</a>(
    epoch_duration_ms: u64,
    // ValidatorV1 committee parameters
    max_validator_count: u64,
    min_validator_joining_stake: u64,
    validator_low_stake_threshold: u64,
    validator_very_low_stake_threshold: u64,
    validator_low_stake_grace_period: u64,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemParametersV1">SystemParametersV1</a> {
    <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemParametersV1">SystemParametersV1</a> {
        epoch_duration_ms,
        min_validator_count: 4,
        max_validator_count,
        min_validator_joining_stake,
        validator_low_stake_threshold,
        validator_very_low_stake_threshold,
        validator_low_stake_grace_period,
        extra_fields: bag::new(ctx),
    }
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_v1_to_v2"></a>

## Function `v1_to_v2`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_v1_to_v2">v1_to_v2</a>(self: <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV1">iota_system::iota_system_state_inner::IotaSystemStateV1</a>): <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_v1_to_v2">v1_to_v2</a>(self: <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV1">IotaSystemStateV1</a>): <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a> {
    <b>let</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV1">IotaSystemStateV1</a> {
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_system_state_version">system_state_version</a>: _,
        iota_treasury_cap,
        validators,
        storage_fund,
        parameters,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_iota_system_admin_cap">iota_system_admin_cap</a>,
        reference_gas_price,
        validator_report_records,
        safe_mode,
        safe_mode_storage_charges,
        safe_mode_computation_rewards,
        safe_mode_storage_rebates,
        safe_mode_non_refundable_storage_fee,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>,
        extra_fields,
    } = self;
    // all computation charges are burned in protocol v1.
    <b>let</b> safe_mode_computation_charges_burned = safe_mode_computation_rewards.value();
    <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a> {
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_system_state_version">system_state_version</a>: 2,
        iota_treasury_cap,
        validators: validators.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_v1_to_v2">v1_to_v2</a>(),
        storage_fund,
        parameters,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_iota_system_admin_cap">iota_system_admin_cap</a>,
        reference_gas_price,
        validator_report_records,
        safe_mode,
        safe_mode_storage_charges,
        safe_mode_computation_charges: safe_mode_computation_rewards,
        safe_mode_computation_charges_burned,
        safe_mode_storage_rebates,
        safe_mode_non_refundable_storage_fee,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>,
        extra_fields,
    }
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_request_add_validator_candidate"></a>

## Function `request_add_validator_candidate`

Can be called by anyone who wishes to become a validator candidate and starts accruing delegated
stakes in their staking pool. Once they have at least <code>MIN_VALIDATOR_JOINING_STAKE</code> amount of stake they
can call <code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_validator">request_add_validator</a></code> to officially become an active validator at the next epoch.
Aborts if the caller is already a pending or active validator, or a validator candidate.
Note: <code>proof_of_possession</code> MUST be a valid signature using iota_address and authority_pubkey_bytes.
To produce a valid PoP, run [fn test_proof_of_possession].


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_validator_candidate">request_add_validator_candidate</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, authority_pubkey_bytes: vector&lt;u8&gt;, network_pubkey_bytes: vector&lt;u8&gt;, protocol_pubkey_bytes: vector&lt;u8&gt;, proof_of_possession: vector&lt;u8&gt;, name: vector&lt;u8&gt;, description: vector&lt;u8&gt;, image_url: vector&lt;u8&gt;, project_url: vector&lt;u8&gt;, net_address: vector&lt;u8&gt;, p2p_address: vector&lt;u8&gt;, primary_address: vector&lt;u8&gt;, gas_price: u64, commission_rate: u64, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_validator_candidate">request_add_validator_candidate</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
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
    <b>let</b> validator = validator::new(
        ctx.sender(),
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
    );
    self.validators.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_validator_candidate">request_add_validator_candidate</a>(validator, ctx);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_request_remove_validator_candidate"></a>

## Function `request_remove_validator_candidate`

Called by a validator candidate to remove themselves from the candidacy. After this call
their staking pool becomes deactivate.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_remove_validator_candidate">request_remove_validator_candidate</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_remove_validator_candidate">request_remove_validator_candidate</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    ctx: &<b>mut</b> TxContext,
) {
    self.validators.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_remove_validator_candidate">request_remove_validator_candidate</a>(ctx);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_request_add_validator"></a>

## Function `request_add_validator`

Called by a validator candidate to add themselves to the active validator set beginning next epoch.
Aborts if the validator is a duplicate with one of the pending or active validators, or if the amount of
stake the validator has doesn't meet the min threshold, or if the number of new validators for the next
epoch has already reached the maximum.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_validator">request_add_validator</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_validator">request_add_validator</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>, ctx: &TxContext) {
    <b>assert</b>!(
        self.validators.next_epoch_validator_count() &lt; self.parameters.max_validator_count,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ELimitExceeded">ELimitExceeded</a>,
    );
    self.validators.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_validator">request_add_validator</a>(self.parameters.min_validator_joining_stake, ctx);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_request_remove_validator"></a>

## Function `request_remove_validator`

A validator can call this function to request a removal in the next epoch.
We use the sender of <code>ctx</code> to look up the validator
(i.e. sender must match the iota_address in the validator).
At the end of the epoch, the <code>validator</code> object will be returned to the iota_address
of the validator.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_remove_validator">request_remove_validator</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_remove_validator">request_remove_validator</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>, ctx: &TxContext) {
    // Only check min validator condition <b>if</b> the current number of validators satisfy the constraint.
    // This is so that <b>if</b> we somehow already are in a state where we have less than min validators, it no longer matters
    // and is ok to stay so. This is useful <b>for</b> a test setup.
    <b>if</b> (self.validators.active_validators_inner().length() &gt;= self.parameters.min_validator_count) {
        <b>assert</b>!(
            self.validators.next_epoch_validator_count() &gt; self.parameters.min_validator_count,
            <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ELimitExceeded">ELimitExceeded</a>,
        );
    };
    self.validators.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_remove_validator">request_remove_validator</a>(ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_request_set_commission_rate"></a>

## Function `request_set_commission_rate`

A validator can call this function to set a new commission rate, updated at the end of
the epoch.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_set_commission_rate">request_set_commission_rate</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, new_commission_rate: u64, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_set_commission_rate">request_set_commission_rate</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    new_commission_rate: u64,
    ctx: &TxContext,
) {
    self
        .validators
        .<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_set_commission_rate">request_set_commission_rate</a>(
            new_commission_rate,
            ctx,
        )
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_set_candidate_validator_commission_rate"></a>

## Function `set_candidate_validator_commission_rate`

This function is used to set new commission rate for candidate validators


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_set_candidate_validator_commission_rate">set_candidate_validator_commission_rate</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, new_commission_rate: u64, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_set_candidate_validator_commission_rate">set_candidate_validator_commission_rate</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    new_commission_rate: u64,
    ctx: &TxContext,
) {
    <b>let</b> candidate = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    candidate.set_candidate_commission_rate(new_commission_rate)
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_request_add_stake"></a>

## Function `request_add_stake`

Add stake to a validator's staking pool.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_stake">request_add_stake</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, stake: <a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, validator_address: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_stake">request_add_stake</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    stake: Coin&lt;IOTA&gt;,
    validator_address: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
): StakedIota {
    self
        .validators
        .<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_stake">request_add_stake</a>(
            validator_address,
            stake.into_balance(),
            ctx,
        )
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_request_add_stake_mul_coin"></a>

## Function `request_add_stake_mul_coin`

Add stake to a validator's staking pool using multiple coins.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_stake_mul_coin">request_add_stake_mul_coin</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, stakes: vector&lt;<a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;&gt;, stake_amount: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, validator_address: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_stake_mul_coin">request_add_stake_mul_coin</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    stakes: vector&lt;Coin&lt;IOTA&gt;&gt;,
    stake_amount: option::Option&lt;u64&gt;,
    validator_address: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
): StakedIota {
    <b>let</b> balance = <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_extract_coin_balance">extract_coin_balance</a>(stakes, stake_amount, ctx);
    self.validators.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_add_stake">request_add_stake</a>(validator_address, balance, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_request_withdraw_stake"></a>

## Function `request_withdraw_stake`

Withdraw some portion of a stake from a validator's staking pool.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_withdraw_stake">request_withdraw_stake</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, staked_iota: <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_withdraw_stake">request_withdraw_stake</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    staked_iota: StakedIota,
    ctx: &TxContext,
): Balance&lt;IOTA&gt; {
    self.validators.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_request_withdraw_stake">request_withdraw_stake</a>(staked_iota, ctx)
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_report_validator"></a>

## Function `report_validator`

Report a validator as a bad or non-performant actor in the system.
Succeeds if all the following are satisfied:
1. both the reporter in <code>cap</code> and the input <code>reportee_addr</code> are committee validators.
2. reporter and reportee not the same address.
3. the cap object is still valid.
This function is idempotent.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_report_validator">report_validator</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, cap: &<a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap_UnverifiedValidatorOperationCap">iota_system::validator_cap::UnverifiedValidatorOperationCap</a>, reportee_addr: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_report_validator">report_validator</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    cap: &UnverifiedValidatorOperationCap,
    reportee_addr: <b>address</b>,
) {
    // Reportee needs to be a committee validator
    <b>assert</b>!(
        self.validators.is_committee_validator_by_iota_address(reportee_addr),
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ENotCommitteeValidator">ENotCommitteeValidator</a>,
    );
    // Verify the represented reporter <b>address</b> is a committee validator, and the capability is still valid.
    <b>let</b> verified_cap = self.validators.verify_cap(cap, <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_COMMITTEE_VALIDATOR_ONLY">COMMITTEE_VALIDATOR_ONLY</a>);
    <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_report_validator_impl">report_validator_impl</a>(verified_cap, reportee_addr, &<b>mut</b> self.validator_report_records);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_undo_report_validator"></a>

## Function `undo_report_validator`

Undo a <code><a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_report_validator">report_validator</a></code> action. Aborts if
1. the reportee is not a currently committee validator or
2. the sender has not previously reported the <code>reportee_addr</code>, or
3. the cap is not valid


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_undo_report_validator">undo_report_validator</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, cap: &<a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap_UnverifiedValidatorOperationCap">iota_system::validator_cap::UnverifiedValidatorOperationCap</a>, reportee_addr: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_undo_report_validator">undo_report_validator</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    cap: &UnverifiedValidatorOperationCap,
    reportee_addr: <b>address</b>,
) {
    <b>let</b> verified_cap = self.validators.verify_cap(cap, <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_COMMITTEE_VALIDATOR_ONLY">COMMITTEE_VALIDATOR_ONLY</a>);
    <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_undo_report_validator_impl">undo_report_validator_impl</a>(verified_cap, reportee_addr, &<b>mut</b> self.validator_report_records);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_report_validator_impl"></a>

## Function `report_validator_impl`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_report_validator_impl">report_validator_impl</a>(verified_cap: <a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap_ValidatorOperationCap">iota_system::validator_cap::ValidatorOperationCap</a>, reportee_addr: <b>address</b>, validator_report_records: &<b>mut</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_report_validator_impl">report_validator_impl</a>(
    verified_cap: ValidatorOperationCap,
    reportee_addr: <b>address</b>,
    validator_report_records: &<b>mut</b> VecMap&lt;<b>address</b>, VecSet&lt;<b>address</b>&gt;&gt;,
) {
    <b>let</b> reporter_address = *verified_cap.verified_operation_cap_address();
    <b>assert</b>!(reporter_address != reportee_addr, <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ECannotReportOneself">ECannotReportOneself</a>);
    <b>if</b> (!validator_report_records.contains(&reportee_addr)) {
        validator_report_records.insert(reportee_addr, vec_set::singleton(reporter_address));
    } <b>else</b> {
        <b>let</b> reporters = validator_report_records.get_mut(&reportee_addr);
        <b>if</b> (!reporters.contains(&reporter_address)) {
            reporters.insert(reporter_address);
        }
    }
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_undo_report_validator_impl"></a>

## Function `undo_report_validator_impl`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_undo_report_validator_impl">undo_report_validator_impl</a>(verified_cap: <a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap_ValidatorOperationCap">iota_system::validator_cap::ValidatorOperationCap</a>, reportee_addr: <b>address</b>, validator_report_records: &<b>mut</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_undo_report_validator_impl">undo_report_validator_impl</a>(
    verified_cap: ValidatorOperationCap,
    reportee_addr: <b>address</b>,
    validator_report_records: &<b>mut</b> VecMap&lt;<b>address</b>, VecSet&lt;<b>address</b>&gt;&gt;,
) {
    <b>assert</b>!(validator_report_records.contains(&reportee_addr), <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_EReportRecordNotFound">EReportRecordNotFound</a>);
    <b>let</b> reporters = validator_report_records.get_mut(&reportee_addr);
    <b>let</b> reporter_addr = *verified_cap.verified_operation_cap_address();
    <b>assert</b>!(reporters.contains(&reporter_addr), <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_EReportRecordNotFound">EReportRecordNotFound</a>);
    reporters.remove(&reporter_addr);
    <b>if</b> (reporters.is_empty()) {
        validator_report_records.remove(&reportee_addr);
    }
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_rotate_operation_cap"></a>

## Function `rotate_operation_cap`

Create a new <code>UnverifiedValidatorOperationCap</code>, transfer it to the
validator and registers it. The original object is thus revoked.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_rotate_operation_cap">rotate_operation_cap</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_rotate_operation_cap">rotate_operation_cap</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>, ctx: &<b>mut</b> TxContext) {
    <b>let</b> validator = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    validator.new_unverified_validator_operation_cap_and_transfer(ctx);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_validator_name"></a>

## Function `update_validator_name`

Update a validator's name.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_name">update_validator_name</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, name: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_name">update_validator_name</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    name: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> validator = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    validator.update_name(name);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_validator_description"></a>

## Function `update_validator_description`

Update a validator's description


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_description">update_validator_description</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, description: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_description">update_validator_description</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    description: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> validator = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    validator.update_description(description);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_validator_image_url"></a>

## Function `update_validator_image_url`

Update a validator's image url


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_image_url">update_validator_image_url</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, image_url: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_image_url">update_validator_image_url</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    image_url: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> validator = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    validator.update_image_url(image_url);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_validator_project_url"></a>

## Function `update_validator_project_url`

Update a validator's project url


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_project_url">update_validator_project_url</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, project_url: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_project_url">update_validator_project_url</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    project_url: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> validator = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    validator.update_project_url(project_url);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_validator_next_epoch_network_address"></a>

## Function `update_validator_next_epoch_network_address`

Update a validator's network address.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_network_address">update_validator_next_epoch_network_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, network_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_network_address">update_validator_next_epoch_network_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    network_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> validator = self.validators.get_validator_mut_with_ctx(ctx);
    validator.update_next_epoch_network_address(network_address);
    <b>let</b> validator: &ValidatorV1 = validator; // Force immutability <b>for</b> the following call
    self.validators.assert_no_pending_or_active_duplicates(validator);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_candidate_validator_network_address"></a>

## Function `update_candidate_validator_network_address`

Update candidate validator's network address.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_network_address">update_candidate_validator_network_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, network_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_network_address">update_candidate_validator_network_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    network_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> candidate = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    candidate.update_candidate_network_address(network_address);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_validator_next_epoch_p2p_address"></a>

## Function `update_validator_next_epoch_p2p_address`

Update a validator's p2p address.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_p2p_address">update_validator_next_epoch_p2p_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, p2p_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_p2p_address">update_validator_next_epoch_p2p_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    p2p_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> validator = self.validators.get_validator_mut_with_ctx(ctx);
    validator.update_next_epoch_p2p_address(p2p_address);
    <b>let</b> validator: &ValidatorV1 = validator; // Force immutability <b>for</b> the following call
    self.validators.assert_no_pending_or_active_duplicates(validator);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_candidate_validator_p2p_address"></a>

## Function `update_candidate_validator_p2p_address`

Update candidate validator's p2p address.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_p2p_address">update_candidate_validator_p2p_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, p2p_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_p2p_address">update_candidate_validator_p2p_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    p2p_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> candidate = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    candidate.update_candidate_p2p_address(p2p_address);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_validator_next_epoch_primary_address"></a>

## Function `update_validator_next_epoch_primary_address`

Update a validator's primary address.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_primary_address">update_validator_next_epoch_primary_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, primary_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_primary_address">update_validator_next_epoch_primary_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    primary_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> validator = self.validators.get_validator_mut_with_ctx(ctx);
    validator.update_next_epoch_primary_address(primary_address);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_candidate_validator_primary_address"></a>

## Function `update_candidate_validator_primary_address`

Update candidate validator's primary address.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_primary_address">update_candidate_validator_primary_address</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, primary_address: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_primary_address">update_candidate_validator_primary_address</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    primary_address: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> candidate = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    candidate.update_candidate_primary_address(primary_address);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_validator_next_epoch_authority_pubkey"></a>

## Function `update_validator_next_epoch_authority_pubkey`

Update a validator's public key of authority key and proof of possession.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_authority_pubkey">update_validator_next_epoch_authority_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, authority_pubkey: vector&lt;u8&gt;, proof_of_possession: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_authority_pubkey">update_validator_next_epoch_authority_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    authority_pubkey: vector&lt;u8&gt;,
    proof_of_possession: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> validator = self.validators.get_validator_mut_with_ctx(ctx);
    validator.update_next_epoch_authority_pubkey(authority_pubkey, proof_of_possession);
    <b>let</b> validator: &ValidatorV1 = validator; // Force immutability <b>for</b> the following call
    self.validators.assert_no_pending_or_active_duplicates(validator);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_candidate_validator_authority_pubkey"></a>

## Function `update_candidate_validator_authority_pubkey`

Update candidate validator's public key of authority key and proof of possession.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_authority_pubkey">update_candidate_validator_authority_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, authority_pubkey: vector&lt;u8&gt;, proof_of_possession: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_authority_pubkey">update_candidate_validator_authority_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    authority_pubkey: vector&lt;u8&gt;,
    proof_of_possession: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> candidate = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    candidate.update_candidate_authority_pubkey(authority_pubkey, proof_of_possession);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_validator_next_epoch_protocol_pubkey"></a>

## Function `update_validator_next_epoch_protocol_pubkey`

Update a validator's public key of protocol key.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_protocol_pubkey">update_validator_next_epoch_protocol_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, protocol_pubkey: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_protocol_pubkey">update_validator_next_epoch_protocol_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    protocol_pubkey: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> validator = self.validators.get_validator_mut_with_ctx(ctx);
    validator.update_next_epoch_protocol_pubkey(protocol_pubkey);
    <b>let</b> validator: &ValidatorV1 = validator; // Force immutability <b>for</b> the following call
    self.validators.assert_no_pending_or_active_duplicates(validator);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_candidate_validator_protocol_pubkey"></a>

## Function `update_candidate_validator_protocol_pubkey`

Update candidate validator's public key of protocol key.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_protocol_pubkey">update_candidate_validator_protocol_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, protocol_pubkey: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_protocol_pubkey">update_candidate_validator_protocol_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    protocol_pubkey: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> candidate = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    candidate.update_candidate_protocol_pubkey(protocol_pubkey);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_validator_next_epoch_network_pubkey"></a>

## Function `update_validator_next_epoch_network_pubkey`

Update a validator's public key of network key.
The change will only take effects starting from the next epoch.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_network_pubkey">update_validator_next_epoch_network_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, network_pubkey: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_validator_next_epoch_network_pubkey">update_validator_next_epoch_network_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    network_pubkey: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> validator = self.validators.get_validator_mut_with_ctx(ctx);
    validator.update_next_epoch_network_pubkey(network_pubkey);
    <b>let</b> validator: &ValidatorV1 = validator; // Force immutability <b>for</b> the following call
    self.validators.assert_no_pending_or_active_duplicates(validator);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_update_candidate_validator_network_pubkey"></a>

## Function `update_candidate_validator_network_pubkey`

Update candidate validator's public key of network key.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_network_pubkey">update_candidate_validator_network_pubkey</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, network_pubkey: vector&lt;u8&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_update_candidate_validator_network_pubkey">update_candidate_validator_network_pubkey</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    network_pubkey: vector&lt;u8&gt;,
    ctx: &TxContext,
) {
    <b>let</b> candidate = self.validators.get_validator_mut_with_ctx_including_candidates(ctx);
    candidate.update_candidate_network_pubkey(network_pubkey);
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_advance_epoch"></a>

## Function `advance_epoch`

This function should be called at the end of an epoch, and advances the system to the next epoch.
It does the following things:
1. Add storage charge to the storage fund.
2. Burn the storage rebates from the storage fund. These are already refunded to transaction sender's
gas coins.
3. Mint or burn IOTA tokens depending on whether the validator subsidy is greater
or smaller than the burned component of the computation charges.
4. Distribute the rewards to the validators.
5. Burn any leftover rewards.
6. Update all validators.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_advance_epoch">advance_epoch</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, new_epoch: u64, next_protocol_version: u64, validator_subsidy: u64, storage_charge: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, computation_charge: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, computation_charge_burned: u64, storage_rebate_amount: u64, non_refundable_storage_fee_amount: u64, reward_slashing_rate: u64, <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>: u64, max_committee_members_count: u64, eligible_active_validators: vector&lt;u64&gt;, scores: vector&lt;u64&gt;, adjust_rewards_by_score: bool, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_advance_epoch">advance_epoch</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    new_epoch: u64,
    next_protocol_version: u64,
    validator_subsidy: u64,
    <b>mut</b> storage_charge: Balance&lt;IOTA&gt;,
    <b>mut</b> computation_charge: Balance&lt;IOTA&gt;,
    <b>mut</b> computation_charge_burned: u64,
    <b>mut</b> storage_rebate_amount: u64,
    <b>mut</b> non_refundable_storage_fee_amount: u64,
    reward_slashing_rate: u64, // how much rewards are slashed to punish a validator, in bps.
    <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>: u64, // Timestamp of the <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a> start
    max_committee_members_count: u64,
    eligible_active_validators: vector&lt;u64&gt;,
    scores: vector&lt;u64&gt;,
    adjust_rewards_by_score: bool,
    ctx: &<b>mut</b> TxContext,
): Balance&lt;IOTA&gt; {
    self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a> = <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>;
    <b>let</b> bps_denominator_u64 = <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_BASIS_POINT_DENOMINATOR">BASIS_POINT_DENOMINATOR</a> <b>as</b> u64;
    // Rates can't be higher than 100%.
    <b>assert</b>!(reward_slashing_rate &lt;= bps_denominator_u64, <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_EBpsTooLarge">EBpsTooLarge</a>);
    // Accumulate the gas summary during safe_mode before processing any rewards:
    <b>let</b> safe_mode_storage_charges = self.safe_mode_storage_charges.withdraw_all();
    storage_charge.join(safe_mode_storage_charges);
    <b>let</b> safe_mode_computation_charges = self.safe_mode_computation_charges.withdraw_all();
    computation_charge.join(safe_mode_computation_charges);
    computation_charge_burned =
        computation_charge_burned + self.safe_mode_computation_charges_burned;
    storage_rebate_amount = storage_rebate_amount + self.safe_mode_storage_rebates;
    self.safe_mode_storage_rebates = 0;
    non_refundable_storage_fee_amount =
        non_refundable_storage_fee_amount + self.safe_mode_non_refundable_storage_fee;
    self.safe_mode_non_refundable_storage_fee = 0;
    <b>let</b> storage_charge_value = storage_charge.value();
    <b>let</b> total_gas_fees = computation_charge.value();
    <b>let</b> tips_amount = total_gas_fees - computation_charge_burned;
    // Mints or burns tokens depending on the computation charge burned and the minted subsidy.
    // Since not all rewards are distributed in case of slashed validators,
    // tokens might be minted here and burnt in the same <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a> change.
    <b>let</b> (
        <b>mut</b> total_validator_rewards,
        minted_tokens_amount,
        <b>mut</b> burnt_tokens_amount,
    ) = <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_match_computation_charge_burned_to_validator_subsidy">match_computation_charge_burned_to_validator_subsidy</a>(
        validator_subsidy,
        computation_charge,
        computation_charge_burned,
        &<b>mut</b> self.iota_treasury_cap,
        ctx,
    );
    self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a> = self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a> + 1;
    // Sanity check to make sure we are advancing to the right <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>.
    <b>assert</b>!(new_epoch == self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>, <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_EAdvancedToWrongEpoch">EAdvancedToWrongEpoch</a>);
    <b>let</b> total_validator_rewards_amount_before_distribution = total_validator_rewards.value();
    self
        .validators
        .<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_advance_epoch">advance_epoch</a>(
            &<b>mut</b> total_validator_rewards,
            &<b>mut</b> self.validator_report_records,
            reward_slashing_rate,
            self.parameters.validator_low_stake_threshold,
            self.parameters.validator_very_low_stake_threshold,
            self.parameters.validator_low_stake_grace_period,
            max_committee_members_count,
            eligible_active_validators,
            scores,
            adjust_rewards_by_score,
            ctx,
        );
    <b>let</b> new_total_stake = self.validators.total_stake_inner();
    <b>let</b> remaining_validator_rewards_amount_after_distribution = total_validator_rewards.value();
    <b>let</b> total_stake_rewards_distributed =
        total_validator_rewards_amount_before_distribution - remaining_validator_rewards_amount_after_distribution;
    self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a> = next_protocol_version;
    // Because of precision issues with integer divisions, we expect that there will be some
    // remaining balance in `total_validator_rewards`.
    <b>let</b> leftover_staking_rewards = total_validator_rewards;
    // Burn any remaining leftover rewards.
    burnt_tokens_amount = burnt_tokens_amount + leftover_staking_rewards.value();
    self.iota_treasury_cap.burn_balance(leftover_staking_rewards, ctx);
    <b>let</b> refunded_storage_rebate = self
        .storage_fund
        .<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_advance_epoch">advance_epoch</a>(
            storage_charge,
            storage_rebate_amount,
            non_refundable_storage_fee_amount,
        );
    event::emit(<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SystemEpochInfoEventV2">SystemEpochInfoEventV2</a> {
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>: self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>: self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>,
        total_stake: new_total_stake,
        storage_charge: storage_charge_value,
        storage_rebate: storage_rebate_amount,
        storage_fund_balance: self.storage_fund.total_balance(),
        total_gas_fees,
        total_stake_rewards_distributed,
        burnt_tokens_amount,
        minted_tokens_amount,
        tips_amount,
    });
    self.safe_mode = <b>false</b>;
    // Double check that the gas from safe mode <b>has</b> been processed.
    <b>assert</b>!(
        self.safe_mode_storage_rebates == 0
            && self.safe_mode_storage_charges.value() == 0
            && self.safe_mode_computation_charges.value() == 0,
        <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_ESafeModeGasNotProcessed">ESafeModeGasNotProcessed</a>,
    );
    // Return the storage rebate split from storage fund that's already refunded to the transaction senders.
    // This will be burnt at the last step of <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a> change programmable transaction.
    refunded_storage_rebate
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_match_computation_charge_burned_to_validator_subsidy"></a>

## Function `match_computation_charge_burned_to_validator_subsidy`

Mint or burn IOTA tokens depending on the given subsidy per validator
and the amount of computation fees burned in this epoch.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_match_computation_charge_burned_to_validator_subsidy">match_computation_charge_burned_to_validator_subsidy</a>(validator_subsidy: u64, computation_charges: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, computation_charge_burned: u64, iota_treasury_cap: &<b>mut</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): (<a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, u64, u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_match_computation_charge_burned_to_validator_subsidy">match_computation_charge_burned_to_validator_subsidy</a>(
    validator_subsidy: u64,
    <b>mut</b> computation_charges: Balance&lt;IOTA&gt;,
    computation_charge_burned: u64,
    iota_treasury_cap: &<b>mut</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>,
    ctx: &TxContext,
): (Balance&lt;IOTA&gt;, u64, u64) {
    <b>let</b> burnt_tokens_amount = computation_charge_burned;
    <b>let</b> minted_tokens_amount = validator_subsidy;
    <b>if</b> (burnt_tokens_amount &lt; minted_tokens_amount) {
        <b>let</b> actual_amount_to_mint = minted_tokens_amount - burnt_tokens_amount;
        <b>let</b> balance_to_mint = iota_treasury_cap.mint_balance(actual_amount_to_mint, ctx);
        // total validator reward
        // = computation_charge + (minted_balance)
        // = computation_charge + (validator_subsidy - computation_charge_burned)
        // = validator_subsidy + (computation_charge - computation_charge_burned)
        // = validator_subsidy + (tips)
        computation_charges.join(balance_to_mint);
    } <b>else</b> <b>if</b> (burnt_tokens_amount &gt; minted_tokens_amount) {
        <b>let</b> actual_amount_to_burn = burnt_tokens_amount - minted_tokens_amount;
        // total validator reward
        // = computation_charge - (amount_to_burn)
        // = computation_charge - (computation_charge_burned - validator_subsidy)
        // = validator_subsidy + (computation_charge - computation_charge_burned)
        // = validator_subsidy + (tips)
        <b>let</b> balance_to_burn = computation_charges.split(actual_amount_to_burn);
        iota_treasury_cap.burn_balance(balance_to_burn, ctx);
    };
    (computation_charges, minted_tokens_amount, burnt_tokens_amount)
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_epoch"></a>

## Function `epoch`

Return the current epoch number. Useful for applications that need a coarse-grained concept of time,
since epochs are ever-increasing and epoch changes are intended to happen every 24 hours.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>): u64 {
    self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch">epoch</a>
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_protocol_version"></a>

## Function `protocol_version`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>): u64 {
    self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_protocol_version">protocol_version</a>
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_system_state_version"></a>

## Function `system_state_version`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_system_state_version">system_state_version</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_system_state_version">system_state_version</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>): u64 {
    self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_system_state_version">system_state_version</a>
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_iota_system_admin_cap"></a>

## Function `iota_system_admin_cap`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_iota_system_admin_cap">iota_system_admin_cap</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): &<a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">iota::system_admin_cap::IotaSystemAdminCap</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_iota_system_admin_cap">iota_system_admin_cap</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>): &IotaSystemAdminCap {
    &self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_iota_system_admin_cap">iota_system_admin_cap</a>
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_genesis_system_state_version"></a>

## Function `genesis_system_state_version`

This function always return the genesis system state version, which is used to create the system state in genesis.
It should never change for a given network.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_genesis_system_state_version">genesis_system_state_version</a>(): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_genesis_system_state_version">genesis_system_state_version</a>(): u64 {
    <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_SYSTEM_STATE_VERSION_V1">SYSTEM_STATE_VERSION_V1</a>
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_epoch_start_timestamp_ms"></a>

## Function `epoch_start_timestamp_ms`

Returns unix timestamp of the start of current epoch


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>): u64 {
    self.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_epoch_start_timestamp_ms">epoch_start_timestamp_ms</a>
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_validator_stake_amount"></a>

## Function `validator_stake_amount`

Returns the total amount staked with <code>validator_addr</code>.
Aborts if <code>validator_addr</code> is not an active validator.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_validator_stake_amount">validator_stake_amount</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, validator_addr: <b>address</b>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_validator_stake_amount">validator_stake_amount</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>, validator_addr: <b>address</b>): u64 {
    self.validators.validator_total_stake_amount_inner(validator_addr)
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_committee_validator_voting_powers"></a>

## Function `committee_validator_voting_powers`

Returns the voting power for <code>validator_addr</code>.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_committee_validator_voting_powers">committee_validator_voting_powers</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_committee_validator_voting_powers">committee_validator_voting_powers</a>(
    self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
): VecMap&lt;<b>address</b>, u64&gt; {
    <b>let</b> <b>mut</b> committee_validators = <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_committee_validator_addresses">committee_validator_addresses</a>(self);
    <b>let</b> <b>mut</b> voting_powers = vec_map::empty();
    <b>while</b> (!vector::is_empty(&committee_validators)) {
        <b>let</b> validator = vector::pop_back(&<b>mut</b> committee_validators);
        <b>let</b> voting_power = self.validators.validator_voting_power_inner(validator);
        vec_map::insert(&<b>mut</b> voting_powers, validator, voting_power);
    };
    voting_powers
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_validator_staking_pool_id"></a>

## Function `validator_staking_pool_id`

Returns the staking pool id of a given validator.
Aborts if <code>validator_addr</code> is not an active validator.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_validator_staking_pool_id">validator_staking_pool_id</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, validator_addr: <b>address</b>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_validator_staking_pool_id">validator_staking_pool_id</a>(
    self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    validator_addr: <b>address</b>,
): ID { self.validators.validator_staking_pool_id_inner(validator_addr) }
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_validator_staking_pool_mappings"></a>

## Function `validator_staking_pool_mappings`

Returns reference to the staking pool mappings that map pool ids to active validator addresses


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_validator_staking_pool_mappings">validator_staking_pool_mappings</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): &<a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, <b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_validator_staking_pool_mappings">validator_staking_pool_mappings</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>): &Table&lt;ID, <b>address</b>&gt; {
    self.validators.staking_pool_mappings_inner()
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_get_total_iota_supply"></a>

## Function `get_total_iota_supply`

Returns the total iota supply.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_get_total_iota_supply">get_total_iota_supply</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_get_total_iota_supply">get_total_iota_supply</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>): u64 {
    self.iota_treasury_cap.total_supply()
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_get_reporters_of"></a>

## Function `get_reporters_of`

Returns all the validators who are currently reporting <code>addr</code>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_get_reporters_of">get_reporters_of</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, addr: <b>address</b>): <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_get_reporters_of">get_reporters_of</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>, addr: <b>address</b>): VecSet&lt;<b>address</b>&gt; {
    <b>if</b> (self.validator_report_records.contains(&addr)) {
        self.validator_report_records[&addr]
    } <b>else</b> {
        vec_set::empty()
    }
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_get_storage_fund_total_balance"></a>

## Function `get_storage_fund_total_balance`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_get_storage_fund_total_balance">get_storage_fund_total_balance</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_get_storage_fund_total_balance">get_storage_fund_total_balance</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>): u64 {
    self.storage_fund.total_balance()
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_get_storage_fund_object_rebates"></a>

## Function `get_storage_fund_object_rebates`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_get_storage_fund_object_rebates">get_storage_fund_object_rebates</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_get_storage_fund_object_rebates">get_storage_fund_object_rebates</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>): u64 {
    self.storage_fund.total_object_storage_rebates()
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_validator_address_by_pool_id"></a>

## Function `validator_address_by_pool_id`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_validator_address_by_pool_id">validator_address_by_pool_id</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, pool_id: &<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): <b>address</b>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_validator_address_by_pool_id">validator_address_by_pool_id</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    pool_id: &ID,
): <b>address</b> {
    self.validators.validator_address_by_pool_id_inner(pool_id)
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_pool_exchange_rates"></a>

## Function `pool_exchange_rates`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_pool_exchange_rates">pool_exchange_rates</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>, pool_id: &<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): &<a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;u64, <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_PoolTokenExchangeRate">iota_system::staking_pool::PoolTokenExchangeRate</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_pool_exchange_rates">pool_exchange_rates</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>,
    pool_id: &ID,
): &Table&lt;u64, PoolTokenExchangeRate&gt; {
    <b>let</b> validators = &<b>mut</b> self.validators;
    validators.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_pool_exchange_rates">pool_exchange_rates</a>(pool_id)
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_active_validator_addresses"></a>

## Function `active_validator_addresses`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_active_validator_addresses">active_validator_addresses</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): vector&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_active_validator_addresses">active_validator_addresses</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>): vector&lt;<b>address</b>&gt; {
    <b>let</b> validator_set = &self.validators;
    validator_set.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_active_validator_addresses">active_validator_addresses</a>()
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_committee_validator_addresses"></a>

## Function `committee_validator_addresses`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_committee_validator_addresses">committee_validator_addresses</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">iota_system::iota_system_state_inner::IotaSystemStateV2</a>): vector&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_committee_validator_addresses">committee_validator_addresses</a>(self: &<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_IotaSystemStateV2">IotaSystemStateV2</a>): vector&lt;<b>address</b>&gt; {
    <b>let</b> validator_set = &self.validators;
    validator_set.<a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_committee_validator_addresses">committee_validator_addresses</a>()
}
</code></pre>



</details>

<a name="iota_system_iota_system_state_inner_extract_coin_balance"></a>

## Function `extract_coin_balance`

Extract required Balance from vector of Coin<IOTA>, transfer the remainder back to sender.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_extract_coin_balance">extract_coin_balance</a>(coins: vector&lt;<a href="../../dependencies/iota/coin.md#iota_coin_Coin">iota::coin::Coin</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;&gt;, amount: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner_extract_coin_balance">extract_coin_balance</a>(
    <b>mut</b> coins: vector&lt;Coin&lt;IOTA&gt;&gt;,
    amount: option::Option&lt;u64&gt;,
    ctx: &<b>mut</b> TxContext,
): Balance&lt;IOTA&gt; {
    <b>let</b> <b>mut</b> merged_coin = coins.pop_back();
    merged_coin.join_vec(coins);
    <b>let</b> <b>mut</b> total_balance = merged_coin.into_balance();
    // <b>return</b> the full amount <b>if</b> amount is not specified
    <b>if</b> (amount.is_some()) {
        <b>let</b> amount = amount.destroy_some();
        <b>let</b> balance = total_balance.split(amount);
        // transfer back the remainder <b>if</b> non zero.
        <b>if</b> (total_balance.value() &gt; 0) {
            transfer::public_transfer(total_balance.into_coin(ctx), ctx.sender());
        } <b>else</b> {
            total_balance.destroy_zero();
        };
        balance
    } <b>else</b> {
        total_balance
    }
}
</code></pre>



</details>
