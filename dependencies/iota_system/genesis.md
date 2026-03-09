
<a name="iota_system_genesis"></a>

# Module `iota_system::genesis`



-  [Struct `GenesisValidatorMetadata`](#iota_system_genesis_GenesisValidatorMetadata)
-  [Struct `GenesisChainParameters`](#iota_system_genesis_GenesisChainParameters)
-  [Struct `TokenDistributionSchedule`](#iota_system_genesis_TokenDistributionSchedule)
-  [Struct `TokenAllocation`](#iota_system_genesis_TokenAllocation)
-  [Constants](#@Constants_0)
-  [Function `create`](#iota_system_genesis_create)
-  [Function `allocate_tokens`](#iota_system_genesis_allocate_tokens)
-  [Function `activate_validators`](#iota_system_genesis_activate_validators)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
<b>use</b> <a href="../../dependencies/iota/bag.md#iota_bag">iota::bag</a>;
<b>use</b> <a href="../../dependencies/iota/balance.md#iota_balance">iota::balance</a>;
<b>use</b> <a href="../../dependencies/iota/clock.md#iota_clock">iota::clock</a>;
<b>use</b> <a href="../../dependencies/iota/coin.md#iota_coin">iota::coin</a>;
<b>use</b> <a href="../../dependencies/iota/config.md#iota_config">iota::config</a>;
<b>use</b> <a href="../../dependencies/iota/deny_list.md#iota_deny_list">iota::deny_list</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_field.md#iota_dynamic_field">iota::dynamic_field</a>;
<b>use</b> <a href="../../dependencies/iota/dynamic_object_field.md#iota_dynamic_object_field">iota::dynamic_object_field</a>;
<b>use</b> <a href="../../dependencies/iota/event.md#iota_event">iota::event</a>;
<b>use</b> <a href="../../dependencies/iota/hex.md#iota_hex">iota::hex</a>;
<b>use</b> <a href="../../dependencies/iota/iota.md#iota_iota">iota::iota</a>;
<b>use</b> <a href="../../dependencies/iota/labeler.md#iota_labeler">iota::labeler</a>;
<b>use</b> <a href="../../dependencies/iota/object.md#iota_object">iota::object</a>;
<b>use</b> <a href="../../dependencies/iota/pay.md#iota_pay">iota::pay</a>;
<b>use</b> <a href="../../dependencies/iota/priority_queue.md#iota_priority_queue">iota::priority_queue</a>;
<b>use</b> <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap">iota::system_admin_cap</a>;
<b>use</b> <a href="../../dependencies/iota/table.md#iota_table">iota::table</a>;
<b>use</b> <a href="../../dependencies/iota/table_vec.md#iota_table_vec">iota::table_vec</a>;
<b>use</b> <a href="../../dependencies/iota/timelock.md#iota_timelock">iota::timelock</a>;
<b>use</b> <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>;
<b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
<b>use</b> <a href="../../dependencies/iota/types.md#iota_types">iota::types</a>;
<b>use</b> <a href="../../dependencies/iota/url.md#iota_url">iota::url</a>;
<b>use</b> <a href="../../dependencies/iota/vec_map.md#iota_vec_map">iota::vec_map</a>;
<b>use</b> <a href="../../dependencies/iota/vec_set.md#iota_vec_set">iota::vec_set</a>;
<b>use</b> <a href="../../dependencies/iota/versioned.md#iota_versioned">iota::versioned</a>;
<b>use</b> <a href="../../dependencies/iota_system/iota_system.md#iota_system_iota_system">iota_system::iota_system</a>;
<b>use</b> <a href="../../dependencies/iota_system/iota_system_state_inner.md#iota_system_iota_system_state_inner">iota_system::iota_system_state_inner</a>;
<b>use</b> <a href="../../dependencies/iota_system/staking_pool.md#iota_system_staking_pool">iota_system::staking_pool</a>;
<b>use</b> <a href="../../dependencies/iota_system/storage_fund.md#iota_system_storage_fund">iota_system::storage_fund</a>;
<b>use</b> <a href="../../dependencies/iota_system/timelocked_staking.md#iota_system_timelocked_staking">iota_system::timelocked_staking</a>;
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



<a name="iota_system_genesis_GenesisValidatorMetadata"></a>

## Struct `GenesisValidatorMetadata`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_GenesisValidatorMetadata">GenesisValidatorMetadata</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>name: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>description: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>image_url: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>project_url: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>iota_address: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>gas_price: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>commission_rate: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>authority_public_key: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>proof_of_possession: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>network_public_key: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>protocol_public_key: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>network_address: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>p2p_address: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
<dt>
<code>primary_address: vector&lt;u8&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_system_genesis_GenesisChainParameters"></a>

## Struct `GenesisChainParameters`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_GenesisChainParameters">GenesisChainParameters</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>protocol_version: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>chain_start_timestamp_ms: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>epoch_duration_ms: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>max_validator_count: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>min_validator_joining_stake: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>validator_low_stake_threshold: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>validator_very_low_stake_threshold: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>validator_low_stake_grace_period: u64</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_system_genesis_TokenDistributionSchedule"></a>

## Struct `TokenDistributionSchedule`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_TokenDistributionSchedule">TokenDistributionSchedule</a>
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>pre_minted_supply: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>allocations: vector&lt;<a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_TokenAllocation">iota_system::genesis::TokenAllocation</a>&gt;</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="iota_system_genesis_TokenAllocation"></a>

## Struct `TokenAllocation`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_TokenAllocation">TokenAllocation</a>
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>recipient_address: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>amount_nanos: u64</code>
</dt>
<dd>
</dd>
<dt>
<code>staked_with_validator: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<b>address</b>&gt;</code>
</dt>
<dd>
 Indicates if this allocation should be staked at genesis and with which validator
</dd>
<dt>
<code>staked_with_timelock_expiration: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;u64&gt;</code>
</dt>
<dd>
 Indicates if this allocation should be staked with timelock at genesis
 and contains its timelock_expiration
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_system_genesis_ENotCalledAtGenesis"></a>

The <code><a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_create">create</a></code> function was called at a non-genesis epoch.


<pre><code><b>const</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_ENotCalledAtGenesis">ENotCalledAtGenesis</a>: u64 = 0;
</code></pre>



<a name="iota_system_genesis_EDuplicateValidator"></a>

The <code><a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_create">create</a></code> function was called with duplicate validators.


<pre><code><b>const</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_EDuplicateValidator">EDuplicateValidator</a>: u64 = 1;
</code></pre>



<a name="iota_system_genesis_EWrongPreMintedSupply"></a>

The <code><a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_create">create</a></code> function was called with wrong pre-minted supply.


<pre><code><b>const</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_EWrongPreMintedSupply">EWrongPreMintedSupply</a>: u64 = 2;
</code></pre>



<a name="iota_system_genesis_create"></a>

## Function `create`

This function will be explicitly called once at genesis.
It will create a singleton IotaSystemState object, which contains
all the information we need in the system.


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_create">create</a>(iota_system_state_id: <a href="../../dependencies/iota/object.md#iota_object_UID">iota::object::UID</a>, iota_treasury_cap: <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>, genesis_chain_parameters: <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_GenesisChainParameters">iota_system::genesis::GenesisChainParameters</a>, genesis_validators: vector&lt;<a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_GenesisValidatorMetadata">iota_system::genesis::GenesisValidatorMetadata</a>&gt;, token_distribution_schedule: <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_TokenDistributionSchedule">iota_system::genesis::TokenDistributionSchedule</a>, timelock_genesis_label: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, iota_system_admin_cap: <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">iota::system_admin_cap::IotaSystemAdminCap</a>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_create">create</a>(
    iota_system_state_id: UID,
    <b>mut</b> iota_treasury_cap: IotaTreasuryCap,
    genesis_chain_parameters: <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_GenesisChainParameters">GenesisChainParameters</a>,
    genesis_validators: vector&lt;<a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_GenesisValidatorMetadata">GenesisValidatorMetadata</a>&gt;,
    token_distribution_schedule: <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_TokenDistributionSchedule">TokenDistributionSchedule</a>,
    timelock_genesis_label: Option&lt;String&gt;,
    iota_system_admin_cap: IotaSystemAdminCap,
    ctx: &<b>mut</b> TxContext,
) {
    // Ensure this is only called at genesis
    <b>assert</b>!(ctx.epoch() == 0, <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_ENotCalledAtGenesis">ENotCalledAtGenesis</a>);
    <b>let</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_TokenDistributionSchedule">TokenDistributionSchedule</a> {
        pre_minted_supply,
        allocations,
    } = token_distribution_schedule;
    <b>assert</b>!(iota_treasury_cap.total_supply() == pre_minted_supply, <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_EWrongPreMintedSupply">EWrongPreMintedSupply</a>);
    <b>let</b> storage_fund = balance::zero();
    // Create all the `ValidatorV1` structs
    <b>let</b> <b>mut</b> validators = vector[];
    <b>let</b> count = genesis_validators.length();
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; count) {
        <b>let</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_GenesisValidatorMetadata">GenesisValidatorMetadata</a> {
            name,
            description,
            image_url,
            project_url,
            iota_address,
            gas_price,
            commission_rate,
            authority_public_key,
            proof_of_possession,
            network_public_key,
            protocol_public_key,
            network_address,
            p2p_address,
            primary_address,
        } = genesis_validators[i];
        <b>let</b> validator = validator::new(
            iota_address,
            authority_public_key,
            network_public_key,
            protocol_public_key,
            proof_of_possession,
            name,
            description,
            image_url,
            project_url,
            network_address,
            p2p_address,
            primary_address,
            gas_price,
            commission_rate,
            ctx,
        );
        // Ensure that each validator is unique
        <b>assert</b>!(
            !validator_set::is_duplicate_validator(&validators, &validator),
            <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_EDuplicateValidator">EDuplicateValidator</a>,
        );
        validators.push_back(validator);
        i = i + 1;
    };
    // Allocate tokens and staking operations
    <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_allocate_tokens">allocate_tokens</a>(
        &<b>mut</b> iota_treasury_cap,
        allocations,
        &<b>mut</b> validators,
        timelock_genesis_label,
        ctx,
    );
    // Activate all validators
    <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_activate_validators">activate_validators</a>(&<b>mut</b> validators);
    <b>let</b> system_parameters = iota_system_state_inner::create_system_parameters(
        genesis_chain_parameters.epoch_duration_ms,
        // ValidatorV1 committee parameters
        genesis_chain_parameters.max_validator_count,
        genesis_chain_parameters.min_validator_joining_stake,
        genesis_chain_parameters.validator_low_stake_threshold,
        genesis_chain_parameters.validator_very_low_stake_threshold,
        genesis_chain_parameters.validator_low_stake_grace_period,
        ctx,
    );
    iota_system::create(
        iota_system_state_id,
        iota_treasury_cap,
        validators,
        storage_fund,
        genesis_chain_parameters.protocol_version,
        genesis_chain_parameters.chain_start_timestamp_ms,
        system_parameters,
        iota_system_admin_cap,
        ctx,
    );
}
</code></pre>



</details>

<a name="iota_system_genesis_allocate_tokens"></a>

## Function `allocate_tokens`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_allocate_tokens">allocate_tokens</a>(iota_treasury_cap: &<b>mut</b> <a href="../../dependencies/iota/iota.md#iota_iota_IotaTreasuryCap">iota::iota::IotaTreasuryCap</a>, allocations: vector&lt;<a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_TokenAllocation">iota_system::genesis::TokenAllocation</a>&gt;, validators: &<b>mut</b> vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;, timelock_genesis_label: <a href="../../dependencies/std/option.md#std_option_Option">std::option::Option</a>&lt;<a href="../../dependencies/std/string.md#std_string_String">std::string::String</a>&gt;, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_allocate_tokens">allocate_tokens</a>(
    iota_treasury_cap: &<b>mut</b> IotaTreasuryCap,
    <b>mut</b> allocations: vector&lt;<a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_TokenAllocation">TokenAllocation</a>&gt;,
    validators: &<b>mut</b> vector&lt;ValidatorV1&gt;,
    timelock_genesis_label: Option&lt;String&gt;,
    ctx: &<b>mut</b> TxContext,
) { <b>while</b> (!allocations.is_empty()) {
        <b>let</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_TokenAllocation">TokenAllocation</a> {
            recipient_address,
            amount_nanos,
            staked_with_validator,
            staked_with_timelock_expiration,
        } = allocations.pop_back();
        <b>let</b> allocation_balance = iota_treasury_cap.mint_balance(amount_nanos, ctx);
        <b>if</b> (staked_with_validator.is_some()) {
            <b>let</b> validator_address = staked_with_validator.destroy_some();
            <b>let</b> validator = validator_set::get_validator_mut(
                validators,
                validator_address,
            );
            <b>if</b> (staked_with_timelock_expiration.is_some()) {
                <b>let</b> timelock_expiration = staked_with_timelock_expiration.destroy_some();
                timelocked_staking::request_add_stake_at_genesis(
                    validator,
                    allocation_balance,
                    recipient_address,
                    timelock_expiration,
                    timelock_genesis_label,
                    ctx,
                );
            } <b>else</b> {
                validator.request_add_stake_at_genesis(
                    allocation_balance,
                    recipient_address,
                    ctx,
                );
            }
        } <b>else</b> {
            <a href="../../dependencies/iota/transfer.md#iota_transfer">iota::transfer</a>(
                allocation_balance.into_coin(ctx),
                recipient_address,
            );
        };
    }; allocations.destroy_empty(); }
</code></pre>



</details>

<a name="iota_system_genesis_activate_validators"></a>

## Function `activate_validators`



<pre><code><b>fun</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_activate_validators">activate_validators</a>(validators: &<b>mut</b> vector&lt;<a href="../../dependencies/iota_system/validator.md#iota_system_validator_ValidatorV1">iota_system::validator::ValidatorV1</a>&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota_system/genesis.md#iota_system_genesis_activate_validators">activate_validators</a>(validators: &<b>mut</b> vector&lt;ValidatorV1&gt;) {
    // Activate all genesis validators
    <b>let</b> count = validators.length();
    <b>let</b> <b>mut</b> i = 0;
    <b>while</b> (i &lt; count) {
        <b>let</b> validator = &<b>mut</b> validators[i];
        validator.activate(0);
        i = i + 1;
    };
}
</code></pre>



</details>
