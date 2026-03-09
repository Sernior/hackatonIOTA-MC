
<a name="iota_system_validator_set"></a>

# Module `iota_system::validator_set`



-  [Struct `ValidatorSetV1`](#iota_system_validator_set_ValidatorSetV1)
-  [Struct `ValidatorSetV2`](#iota_system_validator_set_ValidatorSetV2)
-  [Struct `ValidatorEpochInfoEventV1`](#iota_system_validator_set_ValidatorEpochInfoEventV1)
-  [Struct `ValidatorJoinEvent`](#iota_system_validator_set_ValidatorJoinEvent)
-  [Struct `ValidatorLeaveEvent`](#iota_system_validator_set_ValidatorLeaveEvent)
-  [Struct `CommitteeValidatorJoinEvent`](#iota_system_validator_set_CommitteeValidatorJoinEvent)
-  [Struct `CommitteeValidatorLeaveEvent`](#iota_system_validator_set_CommitteeValidatorLeaveEvent)
-  [Constants](#@Constants_0)
-  [Function `new_v1`](#iota_system_validator_set_new_v1)
-  [Function `v1_to_v2`](#iota_system_validator_set_v1_to_v2)
-  [Function `request_add_validator_candidate`](#iota_system_validator_set_request_add_validator_candidate)
-  [Function `request_remove_validator_candidate`](#iota_system_validator_set_request_remove_validator_candidate)
-  [Function `request_add_validator`](#iota_system_validator_set_request_add_validator)
-  [Function `assert_no_pending_or_active_duplicates`](#iota_system_validator_set_assert_no_pending_or_active_duplicates)
-  [Function `request_remove_validator`](#iota_system_validator_set_request_remove_validator)
-  [Function `request_add_stake`](#iota_system_validator_set_request_add_stake)
-  [Function `request_withdraw_stake`](#iota_system_validator_set_request_withdraw_stake)
-  [Function `request_set_commission_rate`](#iota_system_validator_set_request_set_commission_rate)
-  [Function `advance_epoch`](#iota_system_validator_set_advance_epoch)
-  [Function `update_and_process_low_stake_departures`](#iota_system_validator_set_update_and_process_low_stake_departures)
-  [Function `effectuate_staged_metadata`](#iota_system_validator_set_effectuate_staged_metadata)
-  [Function `derive_reference_gas_price`](#iota_system_validator_set_derive_reference_gas_price)
-  [Function `total_stake`](#iota_system_validator_set_total_stake)
-  [Function `validator_total_stake_amount`](#iota_system_validator_set_validator_total_stake_amount)
-  [Function `validator_stake_amount`](#iota_system_validator_set_validator_stake_amount)
-  [Function `validator_voting_power`](#iota_system_validator_set_validator_voting_power)
-  [Function `validator_staking_pool_id`](#iota_system_validator_set_validator_staking_pool_id)
-  [Function `staking_pool_mappings`](#iota_system_validator_set_staking_pool_mappings)
-  [Function `total_stake_inner`](#iota_system_validator_set_total_stake_inner)
-  [Function `validator_total_stake_amount_inner`](#iota_system_validator_set_validator_total_stake_amount_inner)
-  [Function `validator_stake_amount_inner`](#iota_system_validator_set_validator_stake_amount_inner)
-  [Function `validator_voting_power_inner`](#iota_system_validator_set_validator_voting_power_inner)
-  [Function `validator_staking_pool_id_inner`](#iota_system_validator_set_validator_staking_pool_id_inner)
-  [Function `staking_pool_mappings_inner`](#iota_system_validator_set_staking_pool_mappings_inner)
-  [Function `validator_address_by_pool_id_inner`](#iota_system_validator_set_validator_address_by_pool_id_inner)
-  [Function `pool_exchange_rates`](#iota_system_validator_set_pool_exchange_rates)
-  [Function `next_epoch_validator_count`](#iota_system_validator_set_next_epoch_validator_count)
-  [Function `is_active_validator_by_iota_address`](#iota_system_validator_set_is_active_validator_by_iota_address)
-  [Function `is_committee_validator_by_iota_address`](#iota_system_validator_set_is_committee_validator_by_iota_address)
-  [Function `is_duplicate_with_active_validator`](#iota_system_validator_set_is_duplicate_with_active_validator)
-  [Function `is_duplicate_validator`](#iota_system_validator_set_is_duplicate_validator)
-  [Function `count_duplicates_vec`](#iota_system_validator_set_count_duplicates_vec)
-  [Function `is_duplicate_with_pending_validator`](#iota_system_validator_set_is_duplicate_with_pending_validator)
-  [Function `count_duplicates_tablevec`](#iota_system_validator_set_count_duplicates_tablevec)
-  [Function `get_candidate_or_active_validator_mut`](#iota_system_validator_set_get_candidate_or_active_validator_mut)
-  [Function `find_validator`](#iota_system_validator_set_find_validator)
-  [Function `find_validator_from_table_vec`](#iota_system_validator_set_find_validator_from_table_vec)
-  [Function `get_validator_indices_set`](#iota_system_validator_set_get_validator_indices_set)
-  [Function `get_validator_mut`](#iota_system_validator_set_get_validator_mut)
-  [Function `get_active_or_pending_or_candidate_validator_mut`](#iota_system_validator_set_get_active_or_pending_or_candidate_validator_mut)
-  [Function `get_validator_mut_with_verified_cap`](#iota_system_validator_set_get_validator_mut_with_verified_cap)
-  [Function `get_validator_mut_with_ctx`](#iota_system_validator_set_get_validator_mut_with_ctx)
-  [Function `get_validator_mut_with_ctx_including_candidates`](#iota_system_validator_set_get_validator_mut_with_ctx_including_candidates)
-  [Function `get_validator_ref`](#iota_system_validator_set_get_validator_ref)
-  [Function `get_active_or_pending_or_candidate_validator_ref`](#iota_system_validator_set_get_active_or_pending_or_candidate_validator_ref)
-  [Function `get_active_validator_ref`](#iota_system_validator_set_get_active_validator_ref)
-  [Function `get_pending_validator_ref`](#iota_system_validator_set_get_pending_validator_ref)
-  [Function `get_active_validator_ref_inner`](#iota_system_validator_set_get_active_validator_ref_inner)
-  [Function `get_committee_validator_ref_inner`](#iota_system_validator_set_get_committee_validator_ref_inner)
-  [Function `get_pending_validator_ref_inner`](#iota_system_validator_set_get_pending_validator_ref_inner)
-  [Function `verify_cap`](#iota_system_validator_set_verify_cap)
-  [Function `process_pending_removals`](#iota_system_validator_set_process_pending_removals)
-  [Function `process_validator_departure`](#iota_system_validator_set_process_validator_departure)
-  [Function `clean_report_records_leaving_validator`](#iota_system_validator_set_clean_report_records_leaving_validator)
-  [Function `process_pending_validators`](#iota_system_validator_set_process_pending_validators)
-  [Function `sort_removal_list`](#iota_system_validator_set_sort_removal_list)
-  [Function `process_pending_stakes_and_withdraws`](#iota_system_validator_set_process_pending_stakes_and_withdraws)
-  [Function `calculate_total_active_stakes`](#iota_system_validator_set_calculate_total_active_stakes)
-  [Function `calculate_total_committee_stakes`](#iota_system_validator_set_calculate_total_committee_stakes)
-  [Function `validate_eligible_validators_voting_power`](#iota_system_validator_set_validate_eligible_validators_voting_power)
-  [Function `adjust_next_epoch_commission_rate`](#iota_system_validator_set_adjust_next_epoch_commission_rate)
-  [Function `compute_slashed_validators`](#iota_system_validator_set_compute_slashed_validators)
-  [Function `compute_unadjusted_reward_distribution`](#iota_system_validator_set_compute_unadjusted_reward_distribution)
-  [Function `compute_adjusted_reward_distribution`](#iota_system_validator_set_compute_adjusted_reward_distribution)
-  [Function `distribute_reward`](#iota_system_validator_set_distribute_reward)
-  [Function `emit_validator_epoch_events`](#iota_system_validator_set_emit_validator_epoch_events)
-  [Function `sum_voting_power_by_addresses`](#iota_system_validator_set_sum_voting_power_by_addresses)
-  [Function `sum_committee_voting_power_by_addresses`](#iota_system_validator_set_sum_committee_voting_power_by_addresses)
-  [Function `active_validators`](#iota_system_validator_set_active_validators)
-  [Function `is_validator_candidate`](#iota_system_validator_set_is_validator_candidate)
-  [Function `is_inactive_validator`](#iota_system_validator_set_is_inactive_validator)
-  [Function `active_validators_inner`](#iota_system_validator_set_active_validators_inner)
-  [Function `is_validator_candidate_inner`](#iota_system_validator_set_is_validator_candidate_inner)
-  [Function `is_inactive_validator_inner`](#iota_system_validator_set_is_inactive_validator_inner)
-  [Function `active_validator_addresses`](#iota_system_validator_set_active_validator_addresses)
-  [Function `committee_validator_addresses`](#iota_system_validator_set_committee_validator_addresses)
-  [Function `select_committee_members_from_eligible`](#iota_system_validator_set_select_committee_members_from_eligible)
-  [Function `process_new_committee`](#iota_system_validator_set_process_new_committee)


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
<b>use</b> <a href="../../dependencies/iota/priority_queue.md#iota_priority_queue">iota::priority_queue</a>;
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
<b>use</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator">iota_system::validator</a>;
<b>use</b> <a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap">iota_system::validator_cap</a>;
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



<a name="iota_system_validator_set_ValidatorSetV1"></a>

## Struct `ValidatorSetV1`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a>: u64</code>
</dt>
<dd>
 Total amount of stake from all active validators at the beginning of the epoch.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>: vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;</code>
</dt>
<dd>
 The current list of active validators.
</dd>
<dt>
<code>pending_active_validators: <a href="../../dependencies/iota/table_vec.md#iota_table_vec_TableVec">iota::table_vec::TableVec</a>&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;</code>
</dt>
<dd>
 List of new validator candidates added during the current epoch.
 They will be processed at the end of the epoch.
</dd>
<dt>
<code>pending_removals: vector&lt;u64&gt;</code>
</dt>
<dd>
 Removal requests from the validators. Each element is an index
 pointing to <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a></code>.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>: <a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, <b>address</b>&gt;</code>
</dt>
<dd>
 Mappings from staking pool's ID to the iota address of a validator.
</dd>
<dt>
<code>inactive_validators: <a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">iota_system::validator_wrapper::Validator</a>&gt;</code>
</dt>
<dd>
 Mapping from a staking pool ID to the inactive validator that has that pool as its staking pool.
 When a validator is deactivated the validator is removed from <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a></code> it
 is added to this table so that stakers can continue to withdraw their stake from it.
</dd>
<dt>
<code>validator_candidates: <a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<b>address</b>, <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">iota_system::validator_wrapper::Validator</a>&gt;</code>
</dt>
<dd>
 Table storing preactive/candidate validators, mapping their addresses to their <code>ValidatorV1 </code> structs.
 When an address calls <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_validator_candidate">request_add_validator_candidate</a></code>, they get added to this table and become a preactive
 validator.
 When the candidate has met the min stake requirement, they can call <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_validator">request_add_validator</a></code> to
 officially add them to the active validator set <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a></code> next epoch.
</dd>
<dt>
<code>at_risk_validators: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;</code>
</dt>
<dd>
 Table storing the number of epochs during which a validator's stake has been below the low stake threshold.
</dd>
<dt>
<code>extra_fields: <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a></code>
</dt>
<dd>
 Any extra fields that's not defined statically.
</dd>
</dl>


</details>

<a name="iota_system_validator_set_ValidatorSetV2"></a>

## Struct `ValidatorSetV2`

The second version of the struct storing information about validator set.
This version is an extension on the first one, that supports a new approach to committee selection,
where committee members taking part in consensus are selected from a set of <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a></code>
before an epoch begins. <code>committee_members</code> is a vector of indices of validators stored in <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a></code>,
that have been selected to take part in consensus during the current epoch.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a>: u64</code>
</dt>
<dd>
 Total amount of stake from all committee validators at the beginning of the epoch.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>: vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;</code>
</dt>
<dd>
 The current list of active validators.
</dd>
<dt>
<code>committee_members: vector&lt;u64&gt;</code>
</dt>
<dd>
 Subset of validators responsible for consensus. Each element is an index
 pointing to <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a></code>.
</dd>
<dt>
<code>pending_active_validators: <a href="../../dependencies/iota/table_vec.md#iota_table_vec_TableVec">iota::table_vec::TableVec</a>&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;</code>
</dt>
<dd>
 List of new validator candidates added during the current epoch.
 They will be processed at the end of the epoch.
</dd>
<dt>
<code>pending_removals: vector&lt;u64&gt;</code>
</dt>
<dd>
 Removal requests from the validators. Each element is an index
 pointing to <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a></code>.
</dd>
<dt>
<code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>: <a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, <b>address</b>&gt;</code>
</dt>
<dd>
 Mappings from staking pool's ID to the iota address of a validator.
</dd>
<dt>
<code>inactive_validators: <a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">iota_system::validator_wrapper::Validator</a>&gt;</code>
</dt>
<dd>
 Mapping from a staking pool ID to the inactive validator that has that pool as its staking pool.
 When a validator is deactivated the validator is removed from <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a></code> it
 is added to this table so that stakers can continue to withdraw their stake from it.
</dd>
<dt>
<code>validator_candidates: <a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<b>address</b>, <a href="../../dependencies/iota_system/validator_wrapper.md#iota_system_validator_wrapper_Validator">iota_system::validator_wrapper::Validator</a>&gt;</code>
</dt>
<dd>
 Table storing preactive/candidate validators, mapping their addresses to their <code>ValidatorV1 </code> structs.
 When an address calls <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_validator_candidate">request_add_validator_candidate</a></code>, they get added to this table and become a preactive
 validator.
 When the candidate has met the min stake requirement, they can call <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_validator">request_add_validator</a></code> to
 officially add them to the active validator set <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a></code> next epoch.
</dd>
<dt>
<code>at_risk_validators: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, u64&gt;</code>
</dt>
<dd>
 Table storing the number of epochs during which a validator's stake has been below the low stake threshold.
</dd>
<dt>
<code>extra_fields: <a href="../../dependencies/iota/bag.md#iota_bag_Bag">iota::bag::Bag</a></code>
</dt>
<dd>
 Any extra fields that's not defined statically.
</dd>
</dl>


</details>

<a name="iota_system_validator_set_ValidatorEpochInfoEventV1"></a>

## Struct `ValidatorEpochInfoEventV1`

Event containing staking and rewards related information of
each validator, emitted during epoch advancement.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorEpochInfoEventV1">ValidatorEpochInfoEventV1</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>epoch: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>validator_address: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>reference_gas_survey_quote: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>stake: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>voting_power: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>commission_rate: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>pool_staking_reward: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>pool_token_exchange_rate: <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_PoolTokenExchangeRate">iota_system::staking_pool::PoolTokenExchangeRate</a></code>
</dt>
<dd>
</dd>
<dt>
<code>tallying_rule_reporters: vector&lt;<b>address</b>&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>tallying_rule_global_score: u64</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_system_validator_set_ValidatorJoinEvent"></a>

## Struct `ValidatorJoinEvent`

Event emitted every time a new validator becomes active.
The epoch value corresponds to the first epoch this change takes place.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorJoinEvent">ValidatorJoinEvent</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>epoch: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>validator_address: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>staking_pool_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_system_validator_set_ValidatorLeaveEvent"></a>

## Struct `ValidatorLeaveEvent`

Event emitted every time a validator leaves the active validator set.
The epoch value corresponds to the first epoch this change takes place.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorLeaveEvent">ValidatorLeaveEvent</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>epoch: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>validator_address: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>staking_pool_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>is_voluntary: bool</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_system_validator_set_CommitteeValidatorJoinEvent"></a>

## Struct `CommitteeValidatorJoinEvent`

Event emitted every time a new validator becomes part of the committee.
The epoch value corresponds to the first epoch this change takes place.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_CommitteeValidatorJoinEvent">CommitteeValidatorJoinEvent</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>epoch: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>validator_address: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>staking_pool_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_system_validator_set_CommitteeValidatorLeaveEvent"></a>

## Struct `CommitteeValidatorLeaveEvent`

Event emitted every time a validator leaves the committee at the end of the epoch.
The epoch value corresponds to the first epoch this change takes place.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_CommitteeValidatorLeaveEvent">CommitteeValidatorLeaveEvent</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>epoch: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>validator_address: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>staking_pool_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_system_validator_set_COMMITTEE_VALIDATOR_ONLY"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_COMMITTEE_VALIDATOR_ONLY">COMMITTEE_VALIDATOR_ONLY</a>: u8 = 1;
</code></pre>



<a name="iota_system_validator_set_ACTIVE_OR_PENDING_VALIDATOR"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ACTIVE_OR_PENDING_VALIDATOR">ACTIVE_OR_PENDING_VALIDATOR</a>: u8 = 2;
</code></pre>



<a name="iota_system_validator_set_ANY_VALIDATOR"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ANY_VALIDATOR">ANY_VALIDATOR</a>: u8 = 3;
</code></pre>



<a name="iota_system_validator_set_BASIS_POINT_DENOMINATOR"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_BASIS_POINT_DENOMINATOR">BASIS_POINT_DENOMINATOR</a>: u128 = 10000;
</code></pre>



<a name="iota_system_validator_set_MAX_SCORE"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_MAX_SCORE">MAX_SCORE</a>: u128 = 65536;
</code></pre>



<a name="iota_system_validator_set_MIN_STAKING_THRESHOLD"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_MIN_STAKING_THRESHOLD">MIN_STAKING_THRESHOLD</a>: u64 = 1000000000;
</code></pre>



<a name="iota_system_validator_set_ENonValidatorInReportRecords"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENonValidatorInReportRecords">ENonValidatorInReportRecords</a>: u64 = 0;
</code></pre>



<a name="iota_system_validator_set_EInvalidStakeAdjustmentAmount"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidStakeAdjustmentAmount">EInvalidStakeAdjustmentAmount</a>: u64 = 1;
</code></pre>



<a name="iota_system_validator_set_EDuplicateValidator"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EDuplicateValidator">EDuplicateValidator</a>: u64 = 2;
</code></pre>



<a name="iota_system_validator_set_ENoPoolFound"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENoPoolFound">ENoPoolFound</a>: u64 = 3;
</code></pre>



<a name="iota_system_validator_set_ENotAValidator"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotAValidator">ENotAValidator</a>: u64 = 4;
</code></pre>



<a name="iota_system_validator_set_EMinJoiningStakeNotReached"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EMinJoiningStakeNotReached">EMinJoiningStakeNotReached</a>: u64 = 5;
</code></pre>



<a name="iota_system_validator_set_EAlreadyValidatorCandidate"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EAlreadyValidatorCandidate">EAlreadyValidatorCandidate</a>: u64 = 6;
</code></pre>



<a name="iota_system_validator_set_EValidatorNotCandidate"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EValidatorNotCandidate">EValidatorNotCandidate</a>: u64 = 7;
</code></pre>



<a name="iota_system_validator_set_ENotValidatorCandidate"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotValidatorCandidate">ENotValidatorCandidate</a>: u64 = 8;
</code></pre>



<a name="iota_system_validator_set_ENotActiveOrPendingValidator"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotActiveOrPendingValidator">ENotActiveOrPendingValidator</a>: u64 = 9;
</code></pre>



<a name="iota_system_validator_set_EStakingBelowThreshold"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EStakingBelowThreshold">EStakingBelowThreshold</a>: u64 = 10;
</code></pre>



<a name="iota_system_validator_set_EValidatorAlreadyRemoved"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EValidatorAlreadyRemoved">EValidatorAlreadyRemoved</a>: u64 = 11;
</code></pre>



<a name="iota_system_validator_set_ENotAPendingValidator"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotAPendingValidator">ENotAPendingValidator</a>: u64 = 12;
</code></pre>



<a name="iota_system_validator_set_EValidatorSetEmpty"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EValidatorSetEmpty">EValidatorSetEmpty</a>: u64 = 13;
</code></pre>



<a name="iota_system_validator_set_ENotACommitteeValidator"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotACommitteeValidator">ENotACommitteeValidator</a>: u64 = 14;
</code></pre>



<a name="iota_system_validator_set_EInvalidStakeAmount"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidStakeAmount">EInvalidStakeAmount</a>: u64 = 15;
</code></pre>



<a name="iota_system_validator_set_EInvalidEligibleValidatorIndex"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidEligibleValidatorIndex">EInvalidEligibleValidatorIndex</a>: u64 = 16;
</code></pre>



<a name="iota_system_validator_set_EInvalidRewardAdjustmentData"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidRewardAdjustmentData">EInvalidRewardAdjustmentData</a>: u64 = 17;
</code></pre>



<a name="iota_system_validator_set_EInvalidScoresData"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidScoresData">EInvalidScoresData</a>: u64 = 18;
</code></pre>



<a name="iota_system_validator_set_EIncompatibleVotingPowerDenominator"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EIncompatibleVotingPowerDenominator">EIncompatibleVotingPowerDenominator</a>: u64 = 19;
</code></pre>



<a name="iota_system_validator_set_EInvalidCap"></a>



<pre><code><b>const</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidCap">EInvalidCap</a>: u64 = 101;
</code></pre>



<a name="iota_system_validator_set_new_v1"></a>

## Function `new_v1`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_new_v1">new_v1</a>(init_active_validators: vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_new_v1">new_v1</a>(
    init_active_validators: vector&lt;ValidatorV1&gt;,
    ctx: &<b>mut</b> TxContext,
): <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a> {
    <b>let</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a> = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_calculate_total_active_stakes">calculate_total_active_stakes</a>(&init_active_validators);
    <b>let</b> <b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a> = table::new(ctx);
    <b>let</b> num_validators = init_active_validators.length();
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; num_validators) {
        <b>let</b> validator = &init_active_validators[i];
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>.add(staking_pool_id(validator), iota_address(validator));
        i = i + 1;
    };
    <b>let</b> <b>mut</b> validators = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a> {
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a>,
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>: init_active_validators,
        pending_active_validators: table_vec::empty(ctx),
        pending_removals: vector[],
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>,
        inactive_validators: table::new(ctx),
        validator_candidates: table::new(ctx),
        at_risk_validators: vec_map::empty(),
        extra_fields: bag::new(ctx),
    };
    <b>let</b> validators_num = validators.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.length();
    <b>let</b> committee_of_all_validators = vector::tabulate!(validators_num, |i| i);
    voting_power::set_voting_power(&committee_of_all_validators, &<b>mut</b> validators.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>);
    validators
}
</code></pre>



</details>

<a name="iota_system_validator_set_v1_to_v2"></a>

## Function `v1_to_v2`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_v1_to_v2">v1_to_v2</a>(self: <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>): <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_v1_to_v2">v1_to_v2</a>(self: <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>): <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a> {
    <b>let</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a> {
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a>,
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>,
        pending_active_validators,
        pending_removals,
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>,
        inactive_validators,
        validator_candidates,
        at_risk_validators,
        extra_fields,
    } = self;
    <b>let</b> committee_members = vector::tabulate!(<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.length(), |i| i);
    <b>let</b> validators = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a> {
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a>,
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>,
        committee_members,
        pending_active_validators,
        pending_removals,
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>,
        inactive_validators,
        validator_candidates,
        at_risk_validators,
        extra_fields,
    };
    validators
}
</code></pre>



</details>

<a name="iota_system_validator_set_request_add_validator_candidate"></a>

## Function `request_add_validator_candidate`

Called by <code>iota_system</code> to add a new validator candidate.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_validator_candidate">request_add_validator_candidate</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator: <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_validator_candidate">request_add_validator_candidate</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator: ValidatorV1,
    ctx: &<b>mut</b> TxContext,
) {
    // The next assertions are not critical <b>for</b> the protocol, but they are here to catch problematic configs earlier.
    <b>assert</b>!(
        !<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_duplicate_with_active_validator">is_duplicate_with_active_validator</a>(self, &validator)
                && !<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_duplicate_with_pending_validator">is_duplicate_with_pending_validator</a>(self, &validator),
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EDuplicateValidator">EDuplicateValidator</a>,
    );
    <b>let</b> validator_address = iota_address(&validator);
    <b>assert</b>!(!self.validator_candidates.contains(validator_address), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EAlreadyValidatorCandidate">EAlreadyValidatorCandidate</a>);
    <b>assert</b>!(validator.is_preactive(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EValidatorNotCandidate">EValidatorNotCandidate</a>);
    // Add validator to the candidates mapping and the pool id mappings so that users can start
    // staking with this candidate.
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>.add(staking_pool_id(&validator), validator_address);
    self
        .validator_candidates
        .add(
            iota_address(&validator),
            validator_wrapper::create_v1(validator, ctx),
        );
}
</code></pre>



</details>

<a name="iota_system_validator_set_request_remove_validator_candidate"></a>

## Function `request_remove_validator_candidate`

Called by <code>iota_system</code> to remove a validator candidate, and move them to <code>inactive_validators</code>.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_remove_validator_candidate">request_remove_validator_candidate</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_remove_validator_candidate">request_remove_validator_candidate</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> validator_address = ctx.sender();
    <b>assert</b>!(self.validator_candidates.contains(validator_address), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotValidatorCandidate">ENotValidatorCandidate</a>);
    <b>let</b> wrapper = self.validator_candidates.remove(validator_address);
    <b>let</b> <b>mut</b> validator = wrapper.destroy();
    <b>assert</b>!(validator.is_preactive(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EValidatorNotCandidate">EValidatorNotCandidate</a>);
    <b>let</b> staking_pool_id = staking_pool_id(&validator);
    // Remove the validator's staking pool from mappings.
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>.remove(staking_pool_id);
    // Deactivate the staking pool.
    validator.deactivate(ctx.epoch());
    // Add to the inactive tables.
    self
        .inactive_validators
        .add(
            staking_pool_id,
            validator_wrapper::create_v1(validator, ctx),
        );
}
</code></pre>



</details>

<a name="iota_system_validator_set_request_add_validator"></a>

## Function `request_add_validator`

Called by <code>iota_system</code> to add a new validator to <code>pending_active_validators</code>, which will be
processed at the end of epoch.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_validator">request_add_validator</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, min_joining_stake_amount: u64, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_validator">request_add_validator</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    min_joining_stake_amount: u64,
    ctx: &TxContext,
) {
    <b>let</b> validator_address = ctx.sender();
    <b>assert</b>!(self.validator_candidates.contains(validator_address), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotValidatorCandidate">ENotValidatorCandidate</a>);
    <b>let</b> wrapper = self.validator_candidates.remove(validator_address);
    <b>let</b> validator = wrapper.destroy();
    <b>assert</b>!(
        !<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_duplicate_with_active_validator">is_duplicate_with_active_validator</a>(self, &validator)
                && !<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_duplicate_with_pending_validator">is_duplicate_with_pending_validator</a>(self, &validator),
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EDuplicateValidator">EDuplicateValidator</a>,
    );
    <b>assert</b>!(validator.is_preactive(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EValidatorNotCandidate">EValidatorNotCandidate</a>);
    <b>assert</b>!(validator.total_stake_amount() == validator.next_epoch_stake(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidStakeAmount">EInvalidStakeAmount</a>);
    <b>assert</b>!(validator.total_stake_amount() &gt;= min_joining_stake_amount, <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EMinJoiningStakeNotReached">EMinJoiningStakeNotReached</a>);
    self.pending_active_validators.push_back(validator);
}
</code></pre>



</details>

<a name="iota_system_validator_set_assert_no_pending_or_active_duplicates"></a>

## Function `assert_no_pending_or_active_duplicates`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_assert_no_pending_or_active_duplicates">assert_no_pending_or_active_duplicates</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator: &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_assert_no_pending_or_active_duplicates">assert_no_pending_or_active_duplicates</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator: &ValidatorV1,
) {
    // Validator here must be active or pending, and thus must be identified <b>as</b> duplicate exactly once.
    <b>assert</b>!(
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_count_duplicates_vec">count_duplicates_vec</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator) +
                <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_count_duplicates_tablevec">count_duplicates_tablevec</a>(&self.pending_active_validators, validator) == 1,
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EDuplicateValidator">EDuplicateValidator</a>,
    );
}
</code></pre>



</details>

<a name="iota_system_validator_set_request_remove_validator"></a>

## Function `request_remove_validator`

Called by <code>iota_system</code>, to remove a validator.
The index of the validator is added to <code>pending_removals</code> and
will be processed at the end of epoch.
Only an active validator can request to be removed.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_remove_validator">request_remove_validator</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_remove_validator">request_remove_validator</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>, ctx: &TxContext) {
    <b>let</b> validator_address = ctx.sender();
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    <b>assert</b>!(validator_index_opt.is_some(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotAValidator">ENotAValidator</a>);
    <b>let</b> validator_index = validator_index_opt.extract();
    <b>assert</b>!(!self.pending_removals.contains(&validator_index), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EValidatorAlreadyRemoved">EValidatorAlreadyRemoved</a>);
    self.pending_removals.push_back(validator_index);
}
</code></pre>



</details>

<a name="iota_system_validator_set_request_add_stake"></a>

## Function `request_add_stake`

Called by <code>iota_system</code>, to add a new stake to the validator.
This request is added to the validator's staking pool's pending stake entries, processed at the end
of the epoch.
Aborts in case the staking amount is smaller than MIN_STAKING_THRESHOLD


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_stake">request_add_stake</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>, stake: <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_stake">request_add_stake</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
    stake: Balance&lt;IOTA&gt;,
    ctx: &<b>mut</b> TxContext,
): StakedIota {
    <b>let</b> iota_amount = stake.value();
    <b>assert</b>!(iota_amount &gt;= <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_MIN_STAKING_THRESHOLD">MIN_STAKING_THRESHOLD</a>, <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EStakingBelowThreshold">EStakingBelowThreshold</a>);
    <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_candidate_or_active_validator_mut">get_candidate_or_active_validator_mut</a>(self, validator_address);
    validator.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_stake">request_add_stake</a>(stake, ctx.sender(), ctx)
}
</code></pre>



</details>

<a name="iota_system_validator_set_request_withdraw_stake"></a>

## Function `request_withdraw_stake`

Called by <code>iota_system</code>, to withdraw some share of a stake from the validator. The share to withdraw
is denoted by <code>principal_withdraw_amount</code>. One of two things occurs in this function:
1. If the <code>staked_iota</code> is staked with an active validator, the request is added to the validator's
staking pool's pending stake withdraw entries, processed at the end of the epoch.
2. If the <code>staked_iota</code> was staked with a validator that is no longer active,
the stake and any rewards corresponding to it will be immediately processed.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_withdraw_stake">request_withdraw_stake</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, staked_iota: <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_StakedIota">iota_system::staking_pool::StakedIota</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_withdraw_stake">request_withdraw_stake</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    staked_iota: StakedIota,
    ctx: &TxContext,
): Balance&lt;IOTA&gt; {
    <b>let</b> staking_pool_id = pool_id(&staked_iota);
    <b>let</b> validator = <b>if</b> (self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>.contains(staking_pool_id)) {
        // This is an active validator.
        <b>let</b> validator_address = self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>[pool_id(&staked_iota)];
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_candidate_or_active_validator_mut">get_candidate_or_active_validator_mut</a>(self, validator_address)
    } <b>else</b> {
        // This is an inactive pool.
        <b>assert</b>!(self.inactive_validators.contains(staking_pool_id), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENoPoolFound">ENoPoolFound</a>);
        <b>let</b> wrapper = &<b>mut</b> self.inactive_validators[staking_pool_id];
        wrapper.load_validator_maybe_upgrade()
    };
    validator.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_withdraw_stake">request_withdraw_stake</a>(staked_iota, ctx)
}
</code></pre>



</details>

<a name="iota_system_validator_set_request_set_commission_rate"></a>

## Function `request_set_commission_rate`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_set_commission_rate">request_set_commission_rate</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, new_commission_rate: u64, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_set_commission_rate">request_set_commission_rate</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    new_commission_rate: u64,
    ctx: &TxContext,
) {
    <b>let</b> validator_address = ctx.sender();
    <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_mut">get_validator_mut</a>(&<b>mut</b> self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    validator.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_set_commission_rate">request_set_commission_rate</a>(new_commission_rate);
}
</code></pre>



</details>

<a name="iota_system_validator_set_advance_epoch"></a>

## Function `advance_epoch`

Update the validator set at the end of epoch.
It does the following things:
1. Distribute stake award.
2. Process pending stake deposits and withdraws for each validator (<code>adjust_stake</code>).
3. Process pending stake deposits, and withdraws.
4. Process pending validator application and withdraws.
5. At the end, we calculate the total stake for the new epoch.

IMPORTANT: With the new authority capability notification system, newly activated validators
cannot immediately join the committee. They must wait one epoch after activation to:
1. Notify their AuthorityCapabilities to the network
2. Show that they support the correct ProtocolVersion
This means validators activated in epoch N can only become committee members in epoch N+2.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_advance_epoch">advance_epoch</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, total_validator_rewards: &<b>mut</b> <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, validator_report_records: &<b>mut</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;&gt;, reward_slashing_rate: u64, low_stake_threshold: u64, very_low_stake_threshold: u64, low_stake_grace_period: u64, committee_size: u64, eligible_active_validators: vector&lt;u64&gt;, scores: vector&lt;u64&gt;, adjust_rewards_by_score: bool, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_advance_epoch">advance_epoch</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    total_validator_rewards: &<b>mut</b> Balance&lt;IOTA&gt;,
    validator_report_records: &<b>mut</b> VecMap&lt;<b>address</b>, VecSet&lt;<b>address</b>&gt;&gt;,
    reward_slashing_rate: u64,
    low_stake_threshold: u64,
    very_low_stake_threshold: u64,
    low_stake_grace_period: u64,
    committee_size: u64,
    eligible_active_validators: vector&lt;u64&gt;,
    scores: vector&lt;u64&gt;,
    adjust_rewards_by_score: bool,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> new_epoch = ctx.epoch() + 1;
    <b>let</b> total_voting_power = voting_power::total_voting_power();
    // Compute the reward distribution without taking into account the scores or reporting.
    <b>let</b> unadjusted_staking_reward_amounts = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_compute_unadjusted_reward_distribution">compute_unadjusted_reward_distribution</a>(
        &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>,
        &self.committee_members,
        total_voting_power,
        total_validator_rewards.value(),
    );
    // Use the tallying rule report records <b>for</b> the epoch to compute validators that will be
    // punished.
    <b>let</b> slashed_validators = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_compute_slashed_validators">compute_slashed_validators</a>(self, *validator_report_records);
    // Compute the adjusted amounts of stake each committee validator should get according to the tallying rule.
    // `<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_compute_adjusted_reward_distribution">compute_adjusted_reward_distribution</a>` must be called before `<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_distribute_reward">distribute_reward</a>` and `<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_adjust_next_epoch_commission_rate">adjust_next_epoch_commission_rate</a>` to
    // make sure we are using the current epoch's stake information to compute reward distribution.
    <b>let</b> adjusted_staking_reward_amounts = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_compute_adjusted_reward_distribution">compute_adjusted_reward_distribution</a>(
        &self.committee_members,
        unadjusted_staking_reward_amounts,
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_indices_set">get_validator_indices_set</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, &slashed_validators),
        reward_slashing_rate,
        scores,
        adjust_rewards_by_score,
    );
    // Distribute the rewards before adjusting stake so that we immediately start compounding
    // the rewards <b>for</b> validators and stakers.
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_distribute_reward">distribute_reward</a>(
        &<b>mut</b> self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>,
        &self.committee_members,
        &adjusted_staking_reward_amounts,
        total_validator_rewards,
        ctx,
    );
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_adjust_next_epoch_commission_rate">adjust_next_epoch_commission_rate</a>(&<b>mut</b> self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>);
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_pending_stakes_and_withdraws">process_pending_stakes_and_withdraws</a>(&<b>mut</b> self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, ctx);
    // Emit <a href="../../nplex/events.md#(nplex=0x0)_events">events</a> after we have processed all the rewards distribution and pending stakes.
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_emit_validator_epoch_events">emit_validator_epoch_events</a>(
        new_epoch,
        &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>,
        &self.committee_members,
        &adjusted_staking_reward_amounts,
        validator_report_records,
        &slashed_validators,
        scores,
    );
    // Collect committee validator addresses before modifying the `<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>`.
    // Getting this later would result in incorrect addresses, because `committee_members` values
    // would be pointing to incorrect validators in `<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>`.
    <b>let</b> prev_committee_validator_addresses = self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_committee_validator_addresses">committee_validator_addresses</a>();
    // Collect active validator addresses before modifying the `<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>`.
    // This is needed <b>for</b> proper eligible validator index mapping.
    <b>let</b> prev_active_validator_addresses = self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validator_addresses">active_validator_addresses</a>();
    // Validate eligible validators have sufficient voting power before processing pending validators
    <b>let</b> validated_eligible_validators = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validate_eligible_validators_voting_power">validate_eligible_validators_voting_power</a>(
        &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>,
        eligible_active_validators,
    );
    // Note that all their staged next epoch metadata will be effectuated below.
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_pending_validators">process_pending_validators</a>(self, new_epoch);
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_pending_removals">process_pending_removals</a>(
        self,
        prev_committee_validator_addresses,
        validator_report_records,
        ctx,
    );
    // kick low stake validators out.
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_update_and_process_low_stake_departures">update_and_process_low_stake_departures</a>(
        self,
        low_stake_threshold,
        very_low_stake_threshold,
        low_stake_grace_period,
        validator_report_records,
        prev_committee_validator_addresses,
        ctx,
    );
    // Fail advancing epoch <b>if</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a> set is empty.
    <b>assert</b>!(!self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.is_empty(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EValidatorSetEmpty">EValidatorSetEmpty</a>);
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_new_committee">process_new_committee</a>(
        committee_size,
        prev_committee_validator_addresses,
        prev_active_validator_addresses,
        validated_eligible_validators,
        ctx,
    );
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a> =
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_calculate_total_committee_stakes">calculate_total_committee_stakes</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, &self.committee_members);
    voting_power::set_voting_power(&self.committee_members, &<b>mut</b> self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>);
    // At this point, self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a> and the self.committee_members are updated <b>for</b> next epoch.
    // Now we process the staged validator metadata.
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_effectuate_staged_metadata">effectuate_staged_metadata</a>(self);
}
</code></pre>



</details>

<a name="iota_system_validator_set_update_and_process_low_stake_departures"></a>

## Function `update_and_process_low_stake_departures`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_update_and_process_low_stake_departures">update_and_process_low_stake_departures</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, low_stake_threshold: u64, very_low_stake_threshold: u64, low_stake_grace_period: u64, validator_report_records: &<b>mut</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;&gt;, committee_addresses: vector&lt;<b>address</b>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_update_and_process_low_stake_departures">update_and_process_low_stake_departures</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    low_stake_threshold: u64,
    very_low_stake_threshold: u64,
    low_stake_grace_period: u64,
    validator_report_records: &<b>mut</b> VecMap&lt;<b>address</b>, VecSet&lt;<b>address</b>&gt;&gt;,
    committee_addresses: vector&lt;<b>address</b>&gt;,
    ctx: &<b>mut</b> TxContext,
) {
    // Iterate through all the active validators, record their low stake status, and kick them out <b>if</b> the condition is met.
    <b>let</b> <b>mut</b> i = self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.length();
    <b>while</b> (i &gt; 0) {
        i = i - 1;
        <b>let</b> validator_ref = &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>[i];
        <b>let</b> validator_address = validator_ref.iota_address();
        <b>let</b> stake = validator_ref.total_stake_amount();
        <b>if</b> (stake &gt;= low_stake_threshold) {
            // The validator is safe. We remove their <b>entry</b> from the at_risk map <b>if</b> there exists one.
            <b>if</b> (self.at_risk_validators.contains(&validator_address)) {
                self.at_risk_validators.remove(&validator_address);
            }
        } <b>else</b> <b>if</b> (stake &gt;= very_low_stake_threshold) {
            // The stake is a bit below the threshold so we increment the <b>entry</b> of the validator in the map.
            <b>let</b> new_low_stake_period = <b>if</b> (self.at_risk_validators.contains(&validator_address)) {
                <b>let</b> num_epochs = &<b>mut</b> self.at_risk_validators[&validator_address];
                *num_epochs = *num_epochs + 1;
                *num_epochs
            } <b>else</b> {
                self.at_risk_validators.insert(validator_address, 1);
                1
            };
            // If the grace period <b>has</b> passed, the validator <b>has</b> to leave us.
            <b>if</b> (new_low_stake_period &gt; low_stake_grace_period) {
                <b>let</b> validator = self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.remove(i);
                <b>let</b> is_committee = committee_addresses.contains(&validator.iota_address());
                <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_validator_departure">process_validator_departure</a>(
                    self,
                    validator,
                    validator_report_records,
                    <b>false</b>,
                    /* the validator is kicked out involuntarily */
                    is_committee,
                    ctx,
                );
            }
        } <b>else</b> {
            // The validator's stake is lower than the very low threshold so we kick them out immediately.
            <b>let</b> validator = self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.remove(i);
            <b>let</b> is_committee = committee_addresses.contains(&validator.iota_address());
            <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_validator_departure">process_validator_departure</a>(
                self,
                validator,
                validator_report_records,
                <b>false</b>,
                /* the validator is kicked out involuntarily */
                is_committee,
                ctx,
            );
        }
    }
}
</code></pre>



</details>

<a name="iota_system_validator_set_effectuate_staged_metadata"></a>

## Function `effectuate_staged_metadata`

Effectutate pending next epoch metadata if they are staged.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_effectuate_staged_metadata">effectuate_staged_metadata</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_effectuate_staged_metadata">effectuate_staged_metadata</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>) {
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.do_mut!(|v| v.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_effectuate_staged_metadata">effectuate_staged_metadata</a>());
}
</code></pre>



</details>

<a name="iota_system_validator_set_derive_reference_gas_price"></a>

## Function `derive_reference_gas_price`

Called by <code>iota_system</code> to derive reference gas price for the new epoch for ValidatorSetV1.
Derive the reference gas price based on the gas price quote submitted by each validator.
The returned gas price should be greater than or equal to 2/3 of the validators submitted
gas price, weighted by stake.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_derive_reference_gas_price">derive_reference_gas_price</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_derive_reference_gas_price">derive_reference_gas_price</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>): u64 {
    <b>let</b> vs = &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>;
    <b>let</b> num_validators = vs.length();
    <b>let</b> <b>mut</b> entries = vector[];
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; num_validators) {
        <b>let</b> v = &vs[i];
        entries.push_back(
            pq::new_entry(v.gas_price(), v.voting_power()),
        );
        i = i + 1;
    };
    // Build a priority queue that will pop entries with gas price from the highest to the lowest.
    <b>let</b> <b>mut</b> pq = pq::new(entries);
    <b>let</b> <b>mut</b> sum = 0;
    <b>let</b> threshold = voting_power::total_voting_power() - voting_power::quorum_threshold();
    <b>let</b> <b>mut</b> result = 0;
    <b>while</b> (sum &lt; threshold) {
        <b>let</b> (gas_price, voting_power) = pq.pop_max();
        result = gas_price;
        sum = sum + voting_power;
    };
    result
}
</code></pre>



</details>

<a name="iota_system_validator_set_total_stake"></a>

## Function `total_stake`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>): u64 {
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a>
}
</code></pre>



</details>

<a name="iota_system_validator_set_validator_total_stake_amount"></a>

## Function `validator_total_stake_amount`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_total_stake_amount">validator_total_stake_amount</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>, validator_address: <b>address</b>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_total_stake_amount">validator_total_stake_amount</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>, validator_address: <b>address</b>): u64 {
    <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_ref">get_validator_ref</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    validator.total_stake_amount()
}
</code></pre>



</details>

<a name="iota_system_validator_set_validator_stake_amount"></a>

## Function `validator_stake_amount`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_stake_amount">validator_stake_amount</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>, validator_address: <b>address</b>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_stake_amount">validator_stake_amount</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>, validator_address: <b>address</b>): u64 {
    <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_ref">get_validator_ref</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    validator.stake_amount()
}
</code></pre>



</details>

<a name="iota_system_validator_set_validator_voting_power"></a>

## Function `validator_voting_power`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_voting_power">validator_voting_power</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>, validator_address: <b>address</b>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_voting_power">validator_voting_power</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>, validator_address: <b>address</b>): u64 {
    <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_ref">get_validator_ref</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    validator.voting_power()
}
</code></pre>



</details>

<a name="iota_system_validator_set_validator_staking_pool_id"></a>

## Function `validator_staking_pool_id`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_staking_pool_id">validator_staking_pool_id</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>, validator_address: <b>address</b>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_staking_pool_id">validator_staking_pool_id</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>, validator_address: <b>address</b>): ID {
    <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_ref">get_validator_ref</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    validator.staking_pool_id()
}
</code></pre>



</details>

<a name="iota_system_validator_set_staking_pool_mappings"></a>

## Function `staking_pool_mappings`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>): &<a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, <b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>): &Table&lt;ID, <b>address</b>&gt; {
    &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>
}
</code></pre>



</details>

<a name="iota_system_validator_set_total_stake_inner"></a>

## Function `total_stake_inner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake_inner">total_stake_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake_inner">total_stake_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>): u64 {
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a>
}
</code></pre>



</details>

<a name="iota_system_validator_set_validator_total_stake_amount_inner"></a>

## Function `validator_total_stake_amount_inner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_total_stake_amount_inner">validator_total_stake_amount_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_total_stake_amount_inner">validator_total_stake_amount_inner</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
): u64 {
    <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_ref">get_validator_ref</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    validator.total_stake_amount()
}
</code></pre>



</details>

<a name="iota_system_validator_set_validator_stake_amount_inner"></a>

## Function `validator_stake_amount_inner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_stake_amount_inner">validator_stake_amount_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_stake_amount_inner">validator_stake_amount_inner</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
): u64 {
    <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_ref">get_validator_ref</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    validator.stake_amount()
}
</code></pre>



</details>

<a name="iota_system_validator_set_validator_voting_power_inner"></a>

## Function `validator_voting_power_inner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_voting_power_inner">validator_voting_power_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_voting_power_inner">validator_voting_power_inner</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
): u64 {
    <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_ref">get_validator_ref</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    validator.voting_power()
}
</code></pre>



</details>

<a name="iota_system_validator_set_validator_staking_pool_id_inner"></a>

## Function `validator_staking_pool_id_inner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_staking_pool_id_inner">validator_staking_pool_id_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>): <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_staking_pool_id_inner">validator_staking_pool_id_inner</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
): ID {
    <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_ref">get_validator_ref</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    validator.staking_pool_id()
}
</code></pre>



</details>

<a name="iota_system_validator_set_staking_pool_mappings_inner"></a>

## Function `staking_pool_mappings_inner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings_inner">staking_pool_mappings_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>): &<a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>, <b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings_inner">staking_pool_mappings_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>): &Table&lt;ID, <b>address</b>&gt; {
    &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>
}
</code></pre>



</details>

<a name="iota_system_validator_set_validator_address_by_pool_id_inner"></a>

## Function `validator_address_by_pool_id_inner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_address_by_pool_id_inner">validator_address_by_pool_id_inner</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, pool_id: &<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): <b>address</b>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validator_address_by_pool_id_inner">validator_address_by_pool_id_inner</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    pool_id: &ID,
): <b>address</b> {
    // If the pool id is recorded in the mapping, then it must be either candidate or active.
    <b>if</b> (self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>.contains(*pool_id)) {
        self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>[*pool_id]
    } <b>else</b> {
        // otherwise it's inactive
        <b>let</b> wrapper = &<b>mut</b> self.inactive_validators[*pool_id];
        <b>let</b> validator = wrapper.load_validator_maybe_upgrade();
        validator.iota_address()
    }
}
</code></pre>



</details>

<a name="iota_system_validator_set_pool_exchange_rates"></a>

## Function `pool_exchange_rates`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_pool_exchange_rates">pool_exchange_rates</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, pool_id: &<a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): &<a href="../../dependencies/iota/table.md#iota_table_Table">iota::table::Table</a>&lt;u64, <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool_PoolTokenExchangeRate">iota_system::staking_pool::PoolTokenExchangeRate</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_pool_exchange_rates">pool_exchange_rates</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    pool_id: &ID,
): &Table&lt;u64, PoolTokenExchangeRate&gt; {
    <b>let</b> validator // If the pool id is recorded in the mapping, then it must be either candidate or active.
     = <b>if</b> (self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>.contains(*pool_id)) {
        <b>let</b> validator_address = self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>[*pool_id];
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_or_pending_or_candidate_validator_ref">get_active_or_pending_or_candidate_validator_ref</a>(self, validator_address, <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ANY_VALIDATOR">ANY_VALIDATOR</a>)
    } <b>else</b> {
        // otherwise it's inactive
        <b>let</b> wrapper = &<b>mut</b> self.inactive_validators[*pool_id];
        wrapper.load_validator_maybe_upgrade()
    };
    validator.get_staking_pool_ref().exchange_rates()
}
</code></pre>



</details>

<a name="iota_system_validator_set_next_epoch_validator_count"></a>

## Function `next_epoch_validator_count`

Get the total number of validators in the next epoch.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_next_epoch_validator_count">next_epoch_validator_count</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_next_epoch_validator_count">next_epoch_validator_count</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>): u64 {
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.length() - self.pending_removals.length() + self.pending_active_validators.length()
}
</code></pre>



</details>

<a name="iota_system_validator_set_is_active_validator_by_iota_address"></a>

## Function `is_active_validator_by_iota_address`

Returns true iff the address exists in active validators.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_active_validator_by_iota_address">is_active_validator_by_iota_address</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_active_validator_by_iota_address">is_active_validator_by_iota_address</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
): bool {
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address).is_some()
}
</code></pre>



</details>

<a name="iota_system_validator_set_is_committee_validator_by_iota_address"></a>

## Function `is_committee_validator_by_iota_address`

Returns true iff the address exists in committee validators.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_committee_validator_by_iota_address">is_committee_validator_by_iota_address</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_committee_validator_by_iota_address">is_committee_validator_by_iota_address</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
): bool {
    <b>let</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    // Validator is part of the committee <b>if</b> it belongs to the set of active validators
    // and it's index is part of the committee members set.
    validator_index_opt.is_some() && self.committee_members.contains(validator_index_opt.borrow())
}
</code></pre>



</details>

<a name="iota_system_validator_set_is_duplicate_with_active_validator"></a>

## Function `is_duplicate_with_active_validator`

Checks whether <code>new_validator</code> is duplicate with any currently active validators.
It differs from <code><a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_active_validator_by_iota_address">is_active_validator_by_iota_address</a></code> in that the former checks
only the iota address but this function looks at more metadata.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_duplicate_with_active_validator">is_duplicate_with_active_validator</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, new_validator: &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_duplicate_with_active_validator">is_duplicate_with_active_validator</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>, new_validator: &ValidatorV1): bool {
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_duplicate_validator">is_duplicate_validator</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, new_validator)
}
</code></pre>



</details>

<a name="iota_system_validator_set_is_duplicate_validator"></a>

## Function `is_duplicate_validator`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_duplicate_validator">is_duplicate_validator</a>(validators: &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, new_validator: &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_duplicate_validator">is_duplicate_validator</a>(
    validators: &vector&lt;ValidatorV1&gt;,
    new_validator: &ValidatorV1,
): bool {
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_count_duplicates_vec">count_duplicates_vec</a>(validators, new_validator) &gt; 0
}
</code></pre>



</details>

<a name="iota_system_validator_set_count_duplicates_vec"></a>

## Function `count_duplicates_vec`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_count_duplicates_vec">count_duplicates_vec</a>(validators: &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, validator: &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_count_duplicates_vec">count_duplicates_vec</a>(validators: &vector&lt;ValidatorV1&gt;, validator: &ValidatorV1): u64 {
    <b>let</b> <b>mut</b> result = 0;
    validators.do_ref!(|v| {
        <b>if</b> (v.is_duplicate(validator)) {
            result = result + 1;
        };
    });
    result
}
</code></pre>



</details>

<a name="iota_system_validator_set_is_duplicate_with_pending_validator"></a>

## Function `is_duplicate_with_pending_validator`

Checks whether <code>new_validator</code> is duplicate with any currently pending validators.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_duplicate_with_pending_validator">is_duplicate_with_pending_validator</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, new_validator: &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_duplicate_with_pending_validator">is_duplicate_with_pending_validator</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>, new_validator: &ValidatorV1): bool {
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_count_duplicates_tablevec">count_duplicates_tablevec</a>(&self.pending_active_validators, new_validator) &gt; 0
}
</code></pre>



</details>

<a name="iota_system_validator_set_count_duplicates_tablevec"></a>

## Function `count_duplicates_tablevec`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_count_duplicates_tablevec">count_duplicates_tablevec</a>(validators: &<a href="../../dependencies/iota/table_vec.md#iota_table_vec_TableVec">iota::table_vec::TableVec</a>&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, validator: &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_count_duplicates_tablevec">count_duplicates_tablevec</a>(validators: &TableVec&lt;ValidatorV1&gt;, validator: &ValidatorV1): u64 {
    <b>let</b> len = validators.length();
    <b>let</b> <b>mut</b> i = 0;
    <b>let</b> <b>mut</b> result = 0;
    <b>while</b> (i &lt; len) {
        <b>let</b> v = &validators[i];
        <b>if</b> (v.is_duplicate(validator)) {
            result = result + 1;
        };
        i = i + 1;
    };
    result
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_candidate_or_active_validator_mut"></a>

## Function `get_candidate_or_active_validator_mut`

Get mutable reference to either a candidate or an active validator by address.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_candidate_or_active_validator_mut">get_candidate_or_active_validator_mut</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>): &<b>mut</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_candidate_or_active_validator_mut">get_candidate_or_active_validator_mut</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
): &<b>mut</b> ValidatorV1 {
    <b>if</b> (self.validator_candidates.contains(validator_address)) {
        <b>let</b> wrapper = &<b>mut</b> self.validator_candidates[validator_address];
        <b>return</b> wrapper.load_validator_maybe_upgrade()
    };
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_mut">get_validator_mut</a>(&<b>mut</b> self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address)
}
</code></pre>



</details>

<a name="iota_system_validator_set_find_validator"></a>

## Function `find_validator`

Find validator by <code>validator_address</code>, in <code>validators</code>.
Returns (true, index) if the validator is found, and the index is its index in the list.
If not found, returns (false, 0).


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(validators: &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, validator_address: <b>address</b>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(validators: &vector&lt;ValidatorV1&gt;, validator_address: <b>address</b>): Option&lt;u64&gt; {
    validators.find_index!(|v| v.iota_address() == validator_address)
}
</code></pre>



</details>

<a name="iota_system_validator_set_find_validator_from_table_vec"></a>

## Function `find_validator_from_table_vec`

Find validator by <code>validator_address</code>, in <code>validators</code>.
Returns (true, index) if the validator is found, and the index is its index in the list.
If not found, returns (false, 0).


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator_from_table_vec">find_validator_from_table_vec</a>(validators: &<a href="../../dependencies/iota/table_vec.md#iota_table_vec_TableVec">iota::table_vec::TableVec</a>&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, validator_address: <b>address</b>): <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator_from_table_vec">find_validator_from_table_vec</a>(
    validators: &TableVec&lt;ValidatorV1&gt;,
    validator_address: <b>address</b>,
): Option&lt;u64&gt; {
    <b>let</b> length = validators.length();
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; length) {
        <b>let</b> v = &validators[i];
        <b>if</b> (v.iota_address() == validator_address) {
            <b>return</b> option::some(i)
        };
        i = i + 1;
    };
    option::none()
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_validator_indices_set"></a>

## Function `get_validator_indices_set`

Given a vector of validator addresses, return a set of all indices of the validators.
Aborts if any address isn't in the given validator set.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_indices_set">get_validator_indices_set</a>(validators: &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, validator_addresses: &vector&lt;<b>address</b>&gt;): <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;u64&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_indices_set">get_validator_indices_set</a>(
    validators: &vector&lt;ValidatorV1&gt;,
    validator_addresses: &vector&lt;<b>address</b>&gt;,
): VecSet&lt;u64&gt; {
    <b>let</b> <b>mut</b> res = vec_set::empty();
    validator_addresses.do_ref!(|addr| {
        <b>let</b> index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(validators, *addr);
        <b>assert</b>!(index_opt.is_some(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotAValidator">ENotAValidator</a>);
        res.insert(index_opt.destroy_some());
    });
    res
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_validator_mut"></a>

## Function `get_validator_mut`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_mut">get_validator_mut</a>(validators: &<b>mut</b> vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, validator_address: <b>address</b>): &<b>mut</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_mut">get_validator_mut</a>(
    validators: &<b>mut</b> vector&lt;ValidatorV1&gt;,
    validator_address: <b>address</b>,
): &<b>mut</b> ValidatorV1 {
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(validators, validator_address);
    <b>assert</b>!(validator_index_opt.is_some(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotAValidator">ENotAValidator</a>);
    <b>let</b> validator_index = validator_index_opt.extract();
    &<b>mut</b> validators[validator_index]
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_active_or_pending_or_candidate_validator_mut"></a>

## Function `get_active_or_pending_or_candidate_validator_mut`

Get mutable reference to an active or (if active does not exist) pending or (if pending and
active do not exist) or candidate validator by address.
Note: this function should be called carefully, only after verifying the transaction
sender has the ability to modify the <code>ValidatorV1</code>.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_or_pending_or_candidate_validator_mut">get_active_or_pending_or_candidate_validator_mut</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>, include_candidate: bool): &<b>mut</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_or_pending_or_candidate_validator_mut">get_active_or_pending_or_candidate_validator_mut</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
    include_candidate: bool,
): &<b>mut</b> ValidatorV1 {
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    <b>if</b> (validator_index_opt.is_some()) {
        <b>let</b> validator_index = validator_index_opt.extract();
        <b>return</b> &<b>mut</b> self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>[validator_index]
    };
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator_from_table_vec">find_validator_from_table_vec</a>(
        &self.pending_active_validators,
        validator_address,
    );
    // consider both pending validators and the candidate ones
    <b>if</b> (validator_index_opt.is_some()) {
        <b>let</b> validator_index = validator_index_opt.extract();
        <b>return</b> &<b>mut</b> self.pending_active_validators[validator_index]
    };
    <b>assert</b>!(include_candidate, <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotActiveOrPendingValidator">ENotActiveOrPendingValidator</a>);
    <b>let</b> wrapper = &<b>mut</b> self.validator_candidates[validator_address];
    wrapper.load_validator_maybe_upgrade()
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_validator_mut_with_verified_cap"></a>

## Function `get_validator_mut_with_verified_cap`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_mut_with_verified_cap">get_validator_mut_with_verified_cap</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, verified_cap: &<a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap_ValidatorOperationCap">iota_system::validator_cap::ValidatorOperationCap</a>, include_candidate: bool): &<b>mut</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_mut_with_verified_cap">get_validator_mut_with_verified_cap</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    verified_cap: &ValidatorOperationCap,
    include_candidate: bool,
): &<b>mut</b> ValidatorV1 {
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_or_pending_or_candidate_validator_mut">get_active_or_pending_or_candidate_validator_mut</a>(
        self,
        *verified_cap.verified_operation_cap_address(),
        include_candidate,
    )
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_validator_mut_with_ctx"></a>

## Function `get_validator_mut_with_ctx`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_mut_with_ctx">get_validator_mut_with_ctx</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): &<b>mut</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_mut_with_ctx">get_validator_mut_with_ctx</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    ctx: &TxContext,
): &<b>mut</b> ValidatorV1 {
    <b>let</b> validator_address = ctx.sender();
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_or_pending_or_candidate_validator_mut">get_active_or_pending_or_candidate_validator_mut</a>(self, validator_address, <b>false</b>)
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_validator_mut_with_ctx_including_candidates"></a>

## Function `get_validator_mut_with_ctx_including_candidates`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_mut_with_ctx_including_candidates">get_validator_mut_with_ctx_including_candidates</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): &<b>mut</b> <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_mut_with_ctx_including_candidates">get_validator_mut_with_ctx_including_candidates</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    ctx: &TxContext,
): &<b>mut</b> ValidatorV1 {
    <b>let</b> validator_address = ctx.sender();
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_or_pending_or_candidate_validator_mut">get_active_or_pending_or_candidate_validator_mut</a>(self, validator_address, <b>true</b>)
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_validator_ref"></a>

## Function `get_validator_ref`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_ref">get_validator_ref</a>(validators: &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, validator_address: <b>address</b>): &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_ref">get_validator_ref</a>(validators: &vector&lt;ValidatorV1&gt;, validator_address: <b>address</b>): &ValidatorV1 {
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(validators, validator_address);
    <b>assert</b>!(validator_index_opt.is_some(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotAValidator">ENotAValidator</a>);
    <b>let</b> validator_index = validator_index_opt.extract();
    &validators[validator_index]
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_active_or_pending_or_candidate_validator_ref"></a>

## Function `get_active_or_pending_or_candidate_validator_ref`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_or_pending_or_candidate_validator_ref">get_active_or_pending_or_candidate_validator_ref</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>, which_validator: u8): &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_or_pending_or_candidate_validator_ref">get_active_or_pending_or_candidate_validator_ref</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
    which_validator: u8,
): &ValidatorV1 {
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    <b>if</b> (validator_index_opt.is_some() || which_validator == <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_COMMITTEE_VALIDATOR_ONLY">COMMITTEE_VALIDATOR_ONLY</a>) {
        <b>let</b> validator_index = validator_index_opt.extract();
        <b>return</b> &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>[validator_index]
    };
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator_from_table_vec">find_validator_from_table_vec</a>(
        &self.pending_active_validators,
        validator_address,
    );
    <b>if</b> (validator_index_opt.is_some() || which_validator == <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ACTIVE_OR_PENDING_VALIDATOR">ACTIVE_OR_PENDING_VALIDATOR</a>) {
        <b>let</b> validator_index = validator_index_opt.extract();
        <b>return</b> &self.pending_active_validators[validator_index]
    };
    self.validator_candidates[validator_address].load_validator_maybe_upgrade()
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_active_validator_ref"></a>

## Function `get_active_validator_ref`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_validator_ref">get_active_validator_ref</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>, validator_address: <b>address</b>): &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_validator_ref">get_active_validator_ref</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>,
    validator_address: <b>address</b>,
): &ValidatorV1 {
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    <b>assert</b>!(validator_index_opt.is_some(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotAValidator">ENotAValidator</a>);
    <b>let</b> validator_index = validator_index_opt.extract();
    &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>[validator_index]
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_pending_validator_ref"></a>

## Function `get_pending_validator_ref`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_pending_validator_ref">get_pending_validator_ref</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>, validator_address: <b>address</b>): &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_pending_validator_ref">get_pending_validator_ref</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>,
    validator_address: <b>address</b>,
): &ValidatorV1 {
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator_from_table_vec">find_validator_from_table_vec</a>(
        &self.pending_active_validators,
        validator_address,
    );
    <b>assert</b>!(validator_index_opt.is_some(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotAPendingValidator">ENotAPendingValidator</a>);
    <b>let</b> validator_index = validator_index_opt.extract();
    &self.pending_active_validators[validator_index]
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_active_validator_ref_inner"></a>

## Function `get_active_validator_ref_inner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_validator_ref_inner">get_active_validator_ref_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>): &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_validator_ref_inner">get_active_validator_ref_inner</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
): &ValidatorV1 {
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    <b>assert</b>!(validator_index_opt.is_some(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotAValidator">ENotAValidator</a>);
    <b>let</b> validator_index = validator_index_opt.extract();
    &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>[validator_index]
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_committee_validator_ref_inner"></a>

## Function `get_committee_validator_ref_inner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_committee_validator_ref_inner">get_committee_validator_ref_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>): &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_committee_validator_ref_inner">get_committee_validator_ref_inner</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
): &ValidatorV1 {
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, validator_address);
    <b>assert</b>!(validator_index_opt.is_some(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotAValidator">ENotAValidator</a>);
    <b>assert</b>!(self.committee_members.contains(validator_index_opt.borrow()), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotACommitteeValidator">ENotACommitteeValidator</a>);
    <b>let</b> validator_index = validator_index_opt.extract();
    &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>[validator_index]
}
</code></pre>



</details>

<a name="iota_system_validator_set_get_pending_validator_ref_inner"></a>

## Function `get_pending_validator_ref_inner`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_pending_validator_ref_inner">get_pending_validator_ref_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_address: <b>address</b>): &<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_pending_validator_ref_inner">get_pending_validator_ref_inner</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    validator_address: <b>address</b>,
): &ValidatorV1 {
    <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator_from_table_vec">find_validator_from_table_vec</a>(
        &self.pending_active_validators,
        validator_address,
    );
    <b>assert</b>!(validator_index_opt.is_some(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENotAPendingValidator">ENotAPendingValidator</a>);
    <b>let</b> validator_index = validator_index_opt.extract();
    &self.pending_active_validators[validator_index]
}
</code></pre>



</details>

<a name="iota_system_validator_set_verify_cap"></a>

## Function `verify_cap`

Verify the capability is valid for a Validator.
If <code>which_validator == <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_COMMITTEE_VALIDATOR_ONLY">COMMITTEE_VALIDATOR_ONLY</a></code> is true, only verify the Cap for an committee validator.
Otherwise, verify the Cap for an either active or pending validator.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_verify_cap">verify_cap</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, cap: &<a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap_UnverifiedValidatorOperationCap">iota_system::validator_cap::UnverifiedValidatorOperationCap</a>, which_validator: u8): <a href="../../dependencies/iota_system/validator_cap.md#iota_system_validator_cap_ValidatorOperationCap">iota_system::validator_cap::ValidatorOperationCap</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_verify_cap">verify_cap</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    cap: &UnverifiedValidatorOperationCap,
    which_validator: u8,
): ValidatorOperationCap {
    <b>let</b> cap_address = *cap.unverified_operation_cap_address();
    <b>let</b> validator = <b>if</b> (which_validator == <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_COMMITTEE_VALIDATOR_ONLY">COMMITTEE_VALIDATOR_ONLY</a>)
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_committee_validator_ref_inner">get_committee_validator_ref_inner</a>(self, cap_address)
    <b>else</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_active_or_pending_or_candidate_validator_ref">get_active_or_pending_or_candidate_validator_ref</a>(self, cap_address, which_validator);
    <b>assert</b>!(validator.operation_cap_id() == &object::id(cap), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidCap">EInvalidCap</a>);
    validator_cap::new_from_unverified(cap)
}
</code></pre>



</details>

<a name="iota_system_validator_set_process_pending_removals"></a>

## Function `process_pending_removals`

Process the pending withdraw requests. For each pending request, the validator
is removed from <code>validators</code> and its staking pool is put into the <code>inactive_validators</code> table.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_pending_removals">process_pending_removals</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, committee_addresses: vector&lt;<b>address</b>&gt;, validator_report_records: &<b>mut</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_pending_removals">process_pending_removals</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    committee_addresses: vector&lt;<b>address</b>&gt;,
    validator_report_records: &<b>mut</b> VecMap&lt;<b>address</b>, VecSet&lt;<b>address</b>&gt;&gt;,
    ctx: &<b>mut</b> TxContext,
) {
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_sort_removal_list">sort_removal_list</a>(&<b>mut</b> self.pending_removals);
    <b>while</b> (!self.pending_removals.is_empty()) {
        <b>let</b> index = self.pending_removals.pop_back();
        <b>let</b> validator = self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.remove(index);
        <b>let</b> is_committee = committee_addresses.contains(&validator.iota_address());
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_validator_departure">process_validator_departure</a>(
            self,
            validator,
            validator_report_records,
            <b>true</b>,
            /* the validator removes itself voluntarily */
            is_committee,
            ctx,
        );
    }
}
</code></pre>



</details>

<a name="iota_system_validator_set_process_validator_departure"></a>

## Function `process_validator_departure`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_validator_departure">process_validator_departure</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator: <a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>, validator_report_records: &<b>mut</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;&gt;, is_voluntary: bool, is_committee: bool, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_validator_departure">process_validator_departure</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    <b>mut</b> validator: ValidatorV1,
    validator_report_records: &<b>mut</b> VecMap&lt;<b>address</b>, VecSet&lt;<b>address</b>&gt;&gt;,
    is_voluntary: bool,
    is_committee: bool,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> new_epoch = ctx.epoch() + 1;
    <b>let</b> validator_address = validator.iota_address();
    <b>let</b> validator_pool_id = staking_pool_id(&validator);
    // Remove the validator from our tables.
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_staking_pool_mappings">staking_pool_mappings</a>.remove(validator_pool_id);
    <b>if</b> (self.at_risk_validators.contains(&validator_address)) {
        self.at_risk_validators.remove(&validator_address);
    };
    <b>if</b> (is_committee) {
        self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a> = self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a> - validator.total_stake_amount();
        event::emit(<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_CommitteeValidatorLeaveEvent">CommitteeValidatorLeaveEvent</a> {
            epoch: new_epoch,
            validator_address,
            staking_pool_id: staking_pool_id(&validator),
        });
    };
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_clean_report_records_leaving_validator">clean_report_records_leaving_validator</a>(validator_report_records, validator_address);
    event::emit(<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorLeaveEvent">ValidatorLeaveEvent</a> {
        epoch: new_epoch,
        validator_address,
        staking_pool_id: staking_pool_id(&validator),
        is_voluntary,
    });
    // Deactivate the validator and its staking pool
    validator.deactivate(new_epoch);
    self
        .inactive_validators
        .add(
            validator_pool_id,
            validator_wrapper::create_v1(validator, ctx),
        );
}
</code></pre>



</details>

<a name="iota_system_validator_set_clean_report_records_leaving_validator"></a>

## Function `clean_report_records_leaving_validator`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_clean_report_records_leaving_validator">clean_report_records_leaving_validator</a>(validator_report_records: &<b>mut</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;&gt;, leaving_validator_addr: <b>address</b>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_clean_report_records_leaving_validator">clean_report_records_leaving_validator</a>(
    validator_report_records: &<b>mut</b> VecMap&lt;<b>address</b>, VecSet&lt;<b>address</b>&gt;&gt;,
    leaving_validator_addr: <b>address</b>,
) {
    // Remove the records about this validator
    <b>if</b> (validator_report_records.contains(&leaving_validator_addr)) {
        validator_report_records.remove(&leaving_validator_addr);
    };
    // Remove the reports submitted by this validator
    <b>let</b> reported_validators = validator_report_records.keys();
    <b>let</b> length = reported_validators.length();
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; length) {
        <b>let</b> reported_validator_addr = &reported_validators[i];
        <b>let</b> reporters = &<b>mut</b> validator_report_records[reported_validator_addr];
        <b>if</b> (reporters.contains(&leaving_validator_addr)) {
            reporters.remove(&leaving_validator_addr);
            <b>if</b> (reporters.is_empty()) {
                validator_report_records.remove(reported_validator_addr);
            };
        };
        i = i + 1;
    }
}
</code></pre>



</details>

<a name="iota_system_validator_set_process_pending_validators"></a>

## Function `process_pending_validators`

Process the pending new validators. They are activated and inserted into <code>validators</code>.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_pending_validators">process_pending_validators</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, new_epoch: u64)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_pending_validators">process_pending_validators</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>, new_epoch: u64) {
    <b>while</b> (!self.pending_active_validators.is_empty()) {
        <b>let</b> <b>mut</b> validator = self.pending_active_validators.pop_back();
        validator.activate(new_epoch);
        event::emit(<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorJoinEvent">ValidatorJoinEvent</a> {
            epoch: new_epoch,
            validator_address: validator.iota_address(),
            staking_pool_id: staking_pool_id(&validator),
        });
        self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.push_back(validator);
    }
}
</code></pre>



</details>

<a name="iota_system_validator_set_sort_removal_list"></a>

## Function `sort_removal_list`

Sort all the pending removal indexes.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_sort_removal_list">sort_removal_list</a>(withdraw_list: &<b>mut</b> vector&lt;u64&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_sort_removal_list">sort_removal_list</a>(withdraw_list: &<b>mut</b> vector&lt;u64&gt;) {
    <b>let</b> length = withdraw_list.length();
    <b>let</b> <b>mut</b> i = 1;
    <b>while</b> (i &lt; length) {
        <b>let</b> cur = withdraw_list[i];
        <b>let</b> <b>mut</b> j = i;
        <b>while</b> (j &gt; 0) {
            j = j - 1;
            <b>if</b> (withdraw_list[j] &gt; cur) {
                withdraw_list.swap(j, j + 1);
            } <b>else</b> {
                <b>break</b>
            };
        };
        i = i + 1;
    };
}
</code></pre>



</details>

<a name="iota_system_validator_set_process_pending_stakes_and_withdraws"></a>

## Function `process_pending_stakes_and_withdraws`

Process all active validators' pending stake deposits and withdraws.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_pending_stakes_and_withdraws">process_pending_stakes_and_withdraws</a>(validators: &<b>mut</b> vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_pending_stakes_and_withdraws">process_pending_stakes_and_withdraws</a>(validators: &<b>mut</b> vector&lt;ValidatorV1&gt;, ctx: &TxContext) {
    <b>let</b> length = validators.length();
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; length) {
        <b>let</b> validator = &<b>mut</b> validators[i];
        validator.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_pending_stakes_and_withdraws">process_pending_stakes_and_withdraws</a>(ctx);
        i = i + 1;
    }
}
</code></pre>



</details>

<a name="iota_system_validator_set_calculate_total_active_stakes"></a>

## Function `calculate_total_active_stakes`

Calculate the total active validator stake.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_calculate_total_active_stakes">calculate_total_active_stakes</a>(validators: &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_calculate_total_active_stakes">calculate_total_active_stakes</a>(validators: &vector&lt;ValidatorV1&gt;): u64 {
    <b>let</b> <b>mut</b> stake = 0;
    <b>let</b> length = validators.length();
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; length) {
        <b>let</b> v = &validators[i];
        stake = stake + v.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_total_stake">total_stake</a>();
        i = i + 1;
    };
    stake
}
</code></pre>



</details>

<a name="iota_system_validator_set_calculate_total_committee_stakes"></a>

## Function `calculate_total_committee_stakes`

Calculate the total committee validator stake.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_calculate_total_committee_stakes">calculate_total_committee_stakes</a>(validators: &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, committee_members: &vector&lt;u64&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_calculate_total_committee_stakes">calculate_total_committee_stakes</a>(
    validators: &vector&lt;ValidatorV1&gt;,
    committee_members: &vector&lt;u64&gt;,
): u64 {
    voting_power::total_committee_stake(validators, committee_members)
}
</code></pre>



</details>

<a name="iota_system_validator_set_validate_eligible_validators_voting_power"></a>

## Function `validate_eligible_validators_voting_power`

Validates that eligible validators have sufficient voting power (at least quorum threshold).
If they don't, returns indices of all validators as fallback.
This ensures the committee selection process has enough voting power to meet consensus requirements.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validate_eligible_validators_voting_power">validate_eligible_validators_voting_power</a>(<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>: &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, eligible_active_validators: vector&lt;u64&gt;): vector&lt;u64&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_validate_eligible_validators_voting_power">validate_eligible_validators_voting_power</a>(
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>: &vector&lt;ValidatorV1&gt;,
    eligible_active_validators: vector&lt;u64&gt;,
): vector&lt;u64&gt; {
    // If eligible_active_validators is empty, <b>use</b> all validators <b>as</b> fallback.
    // This can happen only <b>if</b> the protocol does not support selecting committee only from eligible validators or there is a bug in the caller.
    <b>if</b> (eligible_active_validators.is_empty()) {
        <b>return</b> vector::tabulate!(<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.length(), |i| i)
    };
    // Calculate total voting power of eligible validators
    <b>let</b> <b>mut</b> eligible_total_voting_power = 0;
    eligible_active_validators.do_ref!(|idx| {
        // Validate index bounds
        <b>assert</b>!(*idx &lt; <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.length(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidEligibleValidatorIndex">EInvalidEligibleValidatorIndex</a>);
        eligible_total_voting_power =
            eligible_total_voting_power + <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>[*idx].voting_power();
    });
    // If eligible validators don't have enough voting power, fallback to all validators.
    // This should never happen under normal circumstances, but we include this
    // safeguard to ensure the committee selection can always proceed in a safe manner.
    <b>if</b> (eligible_total_voting_power &lt; voting_power::quorum_threshold()) {
        vector::tabulate!(<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.length(), |i| i)
    } <b>else</b> {
        eligible_active_validators
    }
}
</code></pre>



</details>

<a name="iota_system_validator_set_adjust_next_epoch_commission_rate"></a>

## Function `adjust_next_epoch_commission_rate`

Process the pending stake changes for each validator.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_adjust_next_epoch_commission_rate">adjust_next_epoch_commission_rate</a>(validators: &<b>mut</b> vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_adjust_next_epoch_commission_rate">adjust_next_epoch_commission_rate</a>(validators: &<b>mut</b> vector&lt;ValidatorV1&gt;) {
    <b>let</b> length = validators.length();
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; length) {
        <b>let</b> validator = &<b>mut</b> validators[i];
        validator.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_adjust_next_epoch_commission_rate">adjust_next_epoch_commission_rate</a>();
        i = i + 1;
    }
}
</code></pre>



</details>

<a name="iota_system_validator_set_compute_slashed_validators"></a>

## Function `compute_slashed_validators`

Process the validator report records of the epoch and return the addresses of the
non-performant committee validators according to the input threshold.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_compute_slashed_validators">compute_slashed_validators</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, validator_report_records: <a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;&gt;): vector&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_compute_slashed_validators">compute_slashed_validators</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    <b>mut</b> validator_report_records: VecMap&lt;<b>address</b>, VecSet&lt;<b>address</b>&gt;&gt;,
): vector&lt;<b>address</b>&gt; {
    <b>let</b> <b>mut</b> slashed_validators = vector[];
    <b>while</b> (!validator_report_records.is_empty()) {
        <b>let</b> (validator_address, reporters) = validator_report_records.pop();
        <b>assert</b>!(
            <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_committee_validator_by_iota_address">is_committee_validator_by_iota_address</a>(self, validator_address),
            <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ENonValidatorInReportRecords">ENonValidatorInReportRecords</a>,
        );
        // Sum up the voting power of validators that have reported this validator and check <b>if</b> it <b>has</b>
        // passed the slashing threshold.
        <b>let</b> reporter_votes = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_sum_committee_voting_power_by_addresses">sum_committee_voting_power_by_addresses</a>(self, &reporters.into_keys());
        <b>if</b> (reporter_votes &gt;= voting_power::quorum_threshold()) {
            slashed_validators.push_back(validator_address);
        }
    };
    slashed_validators
}
</code></pre>



</details>

<a name="iota_system_validator_set_compute_unadjusted_reward_distribution"></a>

## Function `compute_unadjusted_reward_distribution`

Given the current list of committee validators, the total stake and total reward,
calculate the amount of reward each validator should get, without taking into
account the tallying rule results.
Returns the unadjusted amounts of staking reward for each validator.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_compute_unadjusted_reward_distribution">compute_unadjusted_reward_distribution</a>(<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>: &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, committee_members: &vector&lt;u64&gt;, total_voting_power: u64, total_staking_reward: u64): vector&lt;u64&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_compute_unadjusted_reward_distribution">compute_unadjusted_reward_distribution</a>(
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>: &vector&lt;ValidatorV1&gt;,
    committee_members: &vector&lt;u64&gt;,
    total_voting_power: u64,
    total_staking_reward: u64,
): vector&lt;u64&gt; {
    <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.take_map_ref!(committee_members, |validator| {
        // Integer divisions will truncate the results. Because of this, we expect that at the end
        // there will be some reward remaining in `total_staking_reward`.
        // Use u128 to avoid multiplication overflow.
        <b>let</b> voting_power: u128 = validator.voting_power() <b>as</b> u128;
        <b>let</b> reward_amount =
            voting_power * (total_staking_reward <b>as</b> u128) / (total_voting_power <b>as</b> u128);
        reward_amount <b>as</b> u64
    })
}
</code></pre>



</details>

<a name="iota_system_validator_set_compute_adjusted_reward_distribution"></a>

## Function `compute_adjusted_reward_distribution`

Use the reward adjustment info to compute the adjusted rewards each validator should get.
Returns the staking rewards each validator gets.
The staking rewards are shared with the stakers.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_compute_adjusted_reward_distribution">compute_adjusted_reward_distribution</a>(committee_members: &vector&lt;u64&gt;, unadjusted_staking_reward_amounts: vector&lt;u64&gt;, slashed_validator_indices_set: <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;u64&gt;, reward_slashing_rate: u64, scores: vector&lt;u64&gt;, adjust_rewards_by_score: bool): vector&lt;u64&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_compute_adjusted_reward_distribution">compute_adjusted_reward_distribution</a>(
    committee_members: &vector&lt;u64&gt;,
    unadjusted_staking_reward_amounts: vector&lt;u64&gt;,
    slashed_validator_indices_set: VecSet&lt;u64&gt;,
    reward_slashing_rate: u64,
    scores: vector&lt;u64&gt;,
    adjust_rewards_by_score: bool,
): vector&lt;u64&gt; {
    <b>let</b> <b>mut</b> adjusted_staking_reward_amounts = vector[];
    // Loop through each validator and adjust rewards <b>as</b> necessary
    <b>let</b> length = committee_members.length();
    <b>assert</b>!(length == unadjusted_staking_reward_amounts.length(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidRewardAdjustmentData">EInvalidRewardAdjustmentData</a>);
    <b>assert</b>!(unadjusted_staking_reward_amounts.length() == scores.length(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidScoresData">EInvalidScoresData</a>);
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; length) {
        <b>let</b> unadjusted_staking_reward_amount = unadjusted_staking_reward_amounts[i];
        // Calculate staking reward amount adjusted <b>for</b> the validator's score
        <b>let</b> score_adjusted_staking_reward_amount = <b>if</b> (adjust_rewards_by_score) {
            scores[i] <b>as</b> u128 * (unadjusted_staking_reward_amount <b>as</b> u128) / <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_MAX_SCORE">MAX_SCORE</a>
        } <b>else</b> {
            unadjusted_staking_reward_amount <b>as</b> u128
        };
        // Check <b>if</b> the validator is slashed
        <b>let</b> adjusted_staking_reward_amount = <b>if</b> (
            slashed_validator_indices_set.contains(&committee_members[i])
        ) {
            // Use the slashing rate to compute the amount of staking rewards slashed from this punished validator.
            // Use u128 to avoid multiplication overflow.
            <b>let</b> staking_reward_adjustment_u128 =
                (score_adjusted_staking_reward_amount * (reward_slashing_rate <b>as</b> u128)) / <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_BASIS_POINT_DENOMINATOR">BASIS_POINT_DENOMINATOR</a>;
            score_adjusted_staking_reward_amount - staking_reward_adjustment_u128
        } <b>else</b> {
            // Otherwise, unadjusted staking reward amount is assigned to the unslashed validators
            score_adjusted_staking_reward_amount
        };
        adjusted_staking_reward_amounts.push_back(adjusted_staking_reward_amount <b>as</b> u64);
        // Move to the next validator
        i = i + 1;
    };
    // The sum of the adjusted staking rewards may not be equal to the total staking reward,
    // because of integer division truncation and the slashing of the rewards <b>for</b> the slashed validators.
    adjusted_staking_reward_amounts
}
</code></pre>



</details>

<a name="iota_system_validator_set_distribute_reward"></a>

## Function `distribute_reward`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_distribute_reward">distribute_reward</a>(validators: &<b>mut</b> vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, committee_members: &vector&lt;u64&gt;, adjusted_staking_reward_amounts: &vector&lt;u64&gt;, staking_rewards: &<b>mut</b> <a href="../../dependencies/iota/balance.md#iota_balance_Balance">iota::balance::Balance</a>&lt;<a href="../../dependencies/iota/iota.md#iota_iota_IOTA">iota::iota::IOTA</a>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_distribute_reward">distribute_reward</a>(
    validators: &<b>mut</b> vector&lt;ValidatorV1&gt;,
    committee_members: &vector&lt;u64&gt;,
    adjusted_staking_reward_amounts: &vector&lt;u64&gt;,
    staking_rewards: &<b>mut</b> Balance&lt;IOTA&gt;,
    ctx: &<b>mut</b> TxContext,
) {
    // non-empty committee_members implies non-empty validators, but not vice versa
    <b>assert</b>!(!committee_members.is_empty(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EValidatorSetEmpty">EValidatorSetEmpty</a>);
    // For IIP-8 we will be calculating an effective commission rate <b>for</b> each validator.
    // This assumes that both the commission rate and voting power are represented in basis points
    // with a common denominator.
    <b>assert</b>!(
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_BASIS_POINT_DENOMINATOR">BASIS_POINT_DENOMINATOR</a> == voting_power::total_voting_power() <b>as</b> u128,
        <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EIncompatibleVotingPowerDenominator">EIncompatibleVotingPowerDenominator</a>,
    );
    validators.take_do_with_ix_mut!(committee_members, |i, _, validator| {
        <b>let</b> staking_reward_amount = adjusted_staking_reward_amounts[i];
        <b>let</b> <b>mut</b> staker_reward = staking_rewards.split(staking_reward_amount);
        // Enforce the effective minimum commission <b>for</b> the epoch according to IIP-8.
        <b>let</b> effective_commission_rate = validator.commission_rate().max(validator.voting_power());
        // Validator takes a cut of the rewards <b>as</b> commission.
        <b>let</b> validator_commission_amount =
            (staking_reward_amount <b>as</b> u128) * (effective_commission_rate <b>as</b> u128) / <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_BASIS_POINT_DENOMINATOR">BASIS_POINT_DENOMINATOR</a>;
        // The validator reward = commission.
        <b>let</b> validator_reward = staker_reward.split(validator_commission_amount <b>as</b> u64);
        // Add rewards to the validator. Don't try and distribute rewards though <b>if</b> the payout is zero.
        <b>if</b> (validator_reward.value() &gt; 0) {
            <b>let</b> validator_address = validator.iota_address();
            <b>let</b> rewards_stake = validator.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_request_add_stake">request_add_stake</a>(
                validator_reward,
                validator_address,
                ctx,
            );
            transfer::public_transfer(rewards_stake, validator_address);
        } <b>else</b> {
            validator_reward.destroy_zero();
        };
        // Add rewards to stake staking pool to auto compound <b>for</b> stakers.
        validator.deposit_stake_rewards(staker_reward);
    });
}
</code></pre>



</details>

<a name="iota_system_validator_set_emit_validator_epoch_events"></a>

## Function `emit_validator_epoch_events`

Emit events containing information of each committee validator for the epoch,
including stakes, rewards, performance, etc.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_emit_validator_epoch_events">emit_validator_epoch_events</a>(new_epoch: u64, vs: &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, committee_members: &vector&lt;u64&gt;, pool_staking_reward_amounts: &vector&lt;u64&gt;, report_records: &<a href="../../dependencies/iota/vec_map.md#iota_vec_map_VecMap">iota::vec_map::VecMap</a>&lt;<b>address</b>, <a href="../../dependencies/iota/vec_set.md#iota_vec_set_VecSet">iota::vec_set::VecSet</a>&lt;<b>address</b>&gt;&gt;, slashed_validators: &vector&lt;<b>address</b>&gt;, scores: vector&lt;u64&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_emit_validator_epoch_events">emit_validator_epoch_events</a>(
    new_epoch: u64,
    vs: &vector&lt;ValidatorV1&gt;,
    committee_members: &vector&lt;u64&gt;,
    pool_staking_reward_amounts: &vector&lt;u64&gt;,
    report_records: &VecMap&lt;<b>address</b>, VecSet&lt;<b>address</b>&gt;&gt;,
    slashed_validators: &vector&lt;<b>address</b>&gt;,
    scores: vector&lt;u64&gt;,
) {
    <b>assert</b>!(committee_members.length() == pool_staking_reward_amounts.length());
    <b>let</b> <b>mut</b> i = 0;
    vs.do_ref!(|v| {
        <b>let</b> validator_address = v.iota_address();
        <b>let</b> tallying_rule_reporters = <b>if</b> (report_records.contains(&validator_address)) {
            report_records[&validator_address].into_keys()
        } <b>else</b> {
            vector[]
        };
        <b>let</b> committee_member_index = committee_members.find_index!(|c| c == i);
        <b>let</b> tallying_rule_global_score = <b>if</b> (
            slashed_validators.contains(&validator_address) || committee_member_index.is_none()
        ) 0 <b>else</b> scores[*committee_member_index.borrow()];
        <b>let</b> pool_staking_reward = <b>if</b> (committee_member_index.is_some()) {
            // prepare event <b>for</b> a committee validator
            pool_staking_reward_amounts[*committee_member_index.borrow()]
        } <b>else</b> {
            // prepare event <b>for</b> an active non-committee validator
            0
        };
        event::emit(<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorEpochInfoEventV1">ValidatorEpochInfoEventV1</a> {
            epoch: new_epoch,
            validator_address,
            reference_gas_survey_quote: v.gas_price(),
            stake: v.total_stake_amount(),
            voting_power: v.voting_power(),
            commission_rate: v.commission_rate(),
            pool_staking_reward,
            pool_token_exchange_rate: v.pool_token_exchange_rate_at_epoch(new_epoch),
            tallying_rule_reporters,
            tallying_rule_global_score,
        });
        i = i + 1;
    });
}
</code></pre>



</details>

<a name="iota_system_validator_set_sum_voting_power_by_addresses"></a>

## Function `sum_voting_power_by_addresses`

Sum up the total stake of a given list of validator addresses.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_sum_voting_power_by_addresses">sum_voting_power_by_addresses</a>(vs: &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, addresses: &vector&lt;<b>address</b>&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_sum_voting_power_by_addresses">sum_voting_power_by_addresses</a>(
    vs: &vector&lt;ValidatorV1&gt;,
    addresses: &vector&lt;<b>address</b>&gt;,
): u64 {
    <b>let</b> <b>mut</b> sum = 0;
    <b>let</b> <b>mut</b> i = 0;
    <b>let</b> length = addresses.length();
    <b>while</b> (i &lt; length) {
        <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_validator_ref">get_validator_ref</a>(vs, addresses[i]);
        sum = sum + validator.voting_power();
        i = i + 1;
    };
    sum
}
</code></pre>



</details>

<a name="iota_system_validator_set_sum_committee_voting_power_by_addresses"></a>

## Function `sum_committee_voting_power_by_addresses`

Sum up the total stake of a given list of committee validator addresses.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_sum_committee_voting_power_by_addresses">sum_committee_voting_power_by_addresses</a>(vs: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, addresses: &vector&lt;<b>address</b>&gt;): u64
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_sum_committee_voting_power_by_addresses">sum_committee_voting_power_by_addresses</a>(
    vs: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    addresses: &vector&lt;<b>address</b>&gt;,
): u64 {
    <b>let</b> <b>mut</b> sum = 0;
    addresses.do_ref!(|addr| {
        <b>let</b> validator = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_get_committee_validator_ref_inner">get_committee_validator_ref_inner</a>(vs, *addr);
        sum = sum + validator.voting_power();
    });
    sum
}
</code></pre>



</details>

<a name="iota_system_validator_set_active_validators"></a>

## Function `active_validators`

Return the active validators in <code>self</code>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>): &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>): &vector&lt;ValidatorV1&gt; {
    &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>
}
</code></pre>



</details>

<a name="iota_system_validator_set_is_validator_candidate"></a>

## Function `is_validator_candidate`

Returns true if the <code>addr</code> is a validator candidate.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_validator_candidate">is_validator_candidate</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>, addr: <b>address</b>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_validator_candidate">is_validator_candidate</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>, addr: <b>address</b>): bool {
    self.validator_candidates.contains(addr)
}
</code></pre>



</details>

<a name="iota_system_validator_set_is_inactive_validator"></a>

## Function `is_inactive_validator`

Returns true if the staking pool identified by <code>staking_pool_id</code> is of an inactive validator.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_inactive_validator">is_inactive_validator</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">iota_system::validator_set::ValidatorSetV1</a>, staking_pool_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_inactive_validator">is_inactive_validator</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV1">ValidatorSetV1</a>, staking_pool_id: ID): bool {
    self.inactive_validators.contains(staking_pool_id)
}
</code></pre>



</details>

<a name="iota_system_validator_set_active_validators_inner"></a>

## Function `active_validators_inner`

Return the active validators in <code>self</code>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators_inner">active_validators_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>): &vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators_inner">active_validators_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>): &vector&lt;ValidatorV1&gt; {
    &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>
}
</code></pre>



</details>

<a name="iota_system_validator_set_is_validator_candidate_inner"></a>

## Function `is_validator_candidate_inner`

Returns true if the <code>addr</code> is a validator candidate.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_validator_candidate_inner">is_validator_candidate_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, addr: <b>address</b>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_validator_candidate_inner">is_validator_candidate_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>, addr: <b>address</b>): bool {
    self.validator_candidates.contains(addr)
}
</code></pre>



</details>

<a name="iota_system_validator_set_is_inactive_validator_inner"></a>

## Function `is_inactive_validator_inner`

Returns true if the staking pool identified by <code>staking_pool_id</code> is of an inactive validator.


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_inactive_validator_inner">is_inactive_validator_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, staking_pool_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a>): bool
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_is_inactive_validator_inner">is_inactive_validator_inner</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>, staking_pool_id: ID): bool {
    self.inactive_validators.contains(staking_pool_id)
}
</code></pre>



</details>

<a name="iota_system_validator_set_active_validator_addresses"></a>

## Function `active_validator_addresses`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validator_addresses">active_validator_addresses</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>): vector&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validator_addresses">active_validator_addresses</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>): vector&lt;<b>address</b>&gt; {
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.map_ref!(|v| v.iota_address())
}
</code></pre>



</details>

<a name="iota_system_validator_set_committee_validator_addresses"></a>

## Function `committee_validator_addresses`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_committee_validator_addresses">committee_validator_addresses</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>): vector&lt;<b>address</b>&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_committee_validator_addresses">committee_validator_addresses</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>): vector&lt;<b>address</b>&gt; {
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.take_map_ref!(&self.committee_members, |v| v.iota_address())
}
</code></pre>



</details>

<a name="iota_system_validator_set_select_committee_members_from_eligible"></a>

## Function `select_committee_members_from_eligible`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_select_committee_members_from_eligible">select_committee_members_from_eligible</a>(self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, n: u64, eligible_indices: vector&lt;u64&gt;): vector&lt;u64&gt;
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_select_committee_members_from_eligible">select_committee_members_from_eligible</a>(
    self: &<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    n: u64,
    eligible_indices: vector&lt;u64&gt;,
): vector&lt;u64&gt; {
    // Use take_top_n on eligible indices, comparing the validators they point to
    <b>let</b> selected_positions = eligible_indices.take_top_n!(n, |idx1, idx2| {
        self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>[*idx1].smaller_than(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>[*idx2])
    });
    // Convert positions in eligible_indices to actual <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a> indices
    selected_positions.map_ref!(|pos| eligible_indices[*pos])
}
</code></pre>



</details>

<a name="iota_system_validator_set_process_new_committee"></a>

## Function `process_new_committee`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_new_committee">process_new_committee</a>(self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">iota_system::validator_set::ValidatorSetV2</a>, committee_size: u64, prev_committee_addresses: vector&lt;<b>address</b>&gt;, prev_active_validator_addresses: vector&lt;<b>address</b>&gt;, eligible_active_validators: vector&lt;u64&gt;, ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_process_new_committee">process_new_committee</a>(
    self: &<b>mut</b> <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_ValidatorSetV2">ValidatorSetV2</a>,
    committee_size: u64,
    prev_committee_addresses: vector&lt;<b>address</b>&gt;,
    prev_active_validator_addresses: vector&lt;<b>address</b>&gt;,
    eligible_active_validators: vector&lt;u64&gt;,
    ctx: &TxContext,
) {
    // Convert eligible validator indices into current <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a> indices, independent of the changes in <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.
    <b>let</b> <b>mut</b> current_eligible_indices = vector[];
    eligible_active_validators.do_ref!(|idx| {
        // Validate that the index is within bounds of prev_active_validator_addresses
        <b>assert</b>!(*idx &lt; prev_active_validator_addresses.length(), <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_EInvalidEligibleValidatorIndex">EInvalidEligibleValidatorIndex</a>);
        // Get <b>address</b> from prev_active_validator_addresses using the old index
        <b>let</b> addr = prev_active_validator_addresses[*idx];
        // Find the corresponding index in current <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>
        <b>let</b> <b>mut</b> validator_index_opt = <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, addr);
        <b>if</b> (validator_index_opt.is_some()) {
            <b>let</b> current_index = validator_index_opt.extract();
            // Only add <b>if</b> not already present (handle duplicates by ignoring them)
            <b>if</b> (!current_eligible_indices.contains(&current_index)) {
                current_eligible_indices.push_back(current_index);
            };
        };
    });
    self.committee_members =
        self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_select_committee_members_from_eligible">select_committee_members_from_eligible</a>(committee_size, current_eligible_indices);
    <b>let</b> new_epoch = ctx.epoch() + 1;
    self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>.take_do_ref!(&self.committee_members, |validator| {
        <b>let</b> validator_address = validator.iota_address();
        // Emit join committee event only <b>if</b> the validator wasn't part of the old committee.
        <b>if</b> (!prev_committee_addresses.contains(&validator_address)) {
            event::emit(<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_CommitteeValidatorJoinEvent">CommitteeValidatorJoinEvent</a> {
                epoch: new_epoch,
                validator_address: validator_address,
                staking_pool_id: staking_pool_id(validator),
            });
        };
    });
    // Emit leave committee <a href="../../nplex/events.md#(nplex=0x0)_events">events</a>.
    <b>let</b> new_committee_addresses = self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_committee_validator_addresses">committee_validator_addresses</a>();
    prev_committee_addresses.do_ref!(|validator_address| {
        // Emit leave committee event only <b>if</b> validator is not part of the new committee AND is still an active validator.
        <b>if</b> (!new_committee_addresses.contains(validator_address)) {
            <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a>(&self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>, *validator_address).do!(|validator_index| {
                // SAFETY: <a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_find_validator">find_validator</a> returns a valid index within self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>
                <b>let</b> validator = &self.<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_active_validators">active_validators</a>[validator_index];
                // If it's not part of active validators anymore, it means that the leave committee event <b>has</b> been emitted before.
                event::emit(<a href="../../dependencies/iota_system/validator_set.md#iota_system_validator_set_CommitteeValidatorLeaveEvent">CommitteeValidatorLeaveEvent</a> {
                    epoch: new_epoch,
                    validator_address: *validator_address,
                    staking_pool_id: staking_pool_id(validator),
                });
            });
        };
    });
}
</code></pre>



</details>
