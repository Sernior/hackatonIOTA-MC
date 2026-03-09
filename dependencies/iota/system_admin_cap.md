
<a name="iota_system_admin_cap"></a>

# Module `iota::system_admin_cap`

A system admin capability implementation.


-  [Struct `IotaSystemAdminCap`](#iota_system_admin_cap_IotaSystemAdminCap)
-  [Constants](#@Constants_0)
-  [Function `new_system_admin_cap`](#iota_system_admin_cap_new_system_admin_cap)


<pre><code><b>use</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context">iota::tx_context</a>;
</code></pre>



<a name="iota_system_admin_cap_IotaSystemAdminCap"></a>

## Struct `IotaSystemAdminCap`

<code><a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">IotaSystemAdminCap</a></code> allows to perform privileged IOTA system operations.
For example, packing and unpacking <code>TimeLock</code>s during staking, etc.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">IotaSystemAdminCap</a> <b>has</b> store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="iota_system_admin_cap_ENotCalledAtGenesis"></a>

The <code>new</code> function was called at a non-genesis epoch.


<pre><code><b>const</b> <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_ENotCalledAtGenesis">ENotCalledAtGenesis</a>: u64 = 0;
</code></pre>



<a name="iota_system_admin_cap_ENotSystemAddress"></a>

Sender is not @0x0 the system address.


<pre><code><b>const</b> <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_ENotSystemAddress">ENotSystemAddress</a>: u64 = 1;
</code></pre>



<a name="iota_system_admin_cap_new_system_admin_cap"></a>

## Function `new_system_admin_cap`

Create a <code><a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">IotaSystemAdminCap</a></code>.
This should be called only once during genesis creation.


<pre><code><b>fun</b> <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_new_system_admin_cap">new_system_admin_cap</a>(ctx: &<a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>): <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">iota::system_admin_cap::IotaSystemAdminCap</a>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>fun</b> <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_new_system_admin_cap">new_system_admin_cap</a>(ctx: &TxContext): <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">IotaSystemAdminCap</a> {
    <b>assert</b>!(ctx.sender() == @0x0, <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_ENotSystemAddress">ENotSystemAddress</a>);
    <b>assert</b>!(ctx.epoch() == 0, <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_ENotCalledAtGenesis">ENotCalledAtGenesis</a>);
    <a href="../../dependencies/iota/system_admin_cap.md#iota_system_admin_cap_IotaSystemAdminCap">IotaSystemAdminCap</a> {}
}
</code></pre>



</details>
