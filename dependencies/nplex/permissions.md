
<a name="(iota_identity=0x0)_permissions"></a>

# Module `(iota_identity=0x0)::permissions`



-  [Constants](#@Constants_0)
-  [Function `can_create_proposal`](#(iota_identity=0x0)_permissions_can_create_proposal)
-  [Function `can_approve_proposal`](#(iota_identity=0x0)_permissions_can_approve_proposal)
-  [Function `can_execute_proposal`](#(iota_identity=0x0)_permissions_can_execute_proposal)
-  [Function `can_delete_proposal`](#(iota_identity=0x0)_permissions_can_delete_proposal)
-  [Function `can_remove_approval`](#(iota_identity=0x0)_permissions_can_remove_approval)
-  [Function `all`](#(iota_identity=0x0)_permissions_all)
-  [Function `not`](#(iota_identity=0x0)_permissions_not)


<pre><code></code></pre>



<a name="@Constants_0"></a>

## Constants


<a name="(iota_identity=0x0)_permissions_CAN_CREATE_PROPOSAL"></a>

Permission that enables a controller's delegate to create proposals.


<pre><code><b>const</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_CAN_CREATE_PROPOSAL">CAN_CREATE_PROPOSAL</a>: u32 = 1;
</code></pre>



<a name="(iota_identity=0x0)_permissions_CAN_APPROVE_PROPOSAL"></a>

Permission that enables a controller's delegate to approve proposals.


<pre><code><b>const</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_CAN_APPROVE_PROPOSAL">CAN_APPROVE_PROPOSAL</a>: u32 = 2;
</code></pre>



<a name="(iota_identity=0x0)_permissions_CAN_EXECUTE_PROPOSAL"></a>

Permission that enables a controller's delegate to execute proposals.


<pre><code><b>const</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_CAN_EXECUTE_PROPOSAL">CAN_EXECUTE_PROPOSAL</a>: u32 = 4;
</code></pre>



<a name="(iota_identity=0x0)_permissions_CAN_DELETE_PROPOSAL"></a>

Permission that enables a controller's delegate to delete proposals.


<pre><code><b>const</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_CAN_DELETE_PROPOSAL">CAN_DELETE_PROPOSAL</a>: u32 = 8;
</code></pre>



<a name="(iota_identity=0x0)_permissions_CAN_REMOVE_APPROVAL"></a>

Permission that enables a controller's delegate to remove a proposal's approval.


<pre><code><b>const</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_CAN_REMOVE_APPROVAL">CAN_REMOVE_APPROVAL</a>: u32 = 16;
</code></pre>



<a name="(iota_identity=0x0)_permissions_ALL_PERMISSIONS"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_ALL_PERMISSIONS">ALL_PERMISSIONS</a>: u32 = 4294967295;
</code></pre>



<a name="(iota_identity=0x0)_permissions_can_create_proposal"></a>

## Function `can_create_proposal`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_can_create_proposal">can_create_proposal</a>(): u32
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_can_create_proposal">can_create_proposal</a>(): u32 { <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_CAN_CREATE_PROPOSAL">CAN_CREATE_PROPOSAL</a> }
</code></pre>



</details>

<a name="(iota_identity=0x0)_permissions_can_approve_proposal"></a>

## Function `can_approve_proposal`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_can_approve_proposal">can_approve_proposal</a>(): u32
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_can_approve_proposal">can_approve_proposal</a>(): u32 { <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_CAN_APPROVE_PROPOSAL">CAN_APPROVE_PROPOSAL</a> }
</code></pre>



</details>

<a name="(iota_identity=0x0)_permissions_can_execute_proposal"></a>

## Function `can_execute_proposal`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_can_execute_proposal">can_execute_proposal</a>(): u32
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_can_execute_proposal">can_execute_proposal</a>(): u32 { <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_CAN_EXECUTE_PROPOSAL">CAN_EXECUTE_PROPOSAL</a> }
</code></pre>



</details>

<a name="(iota_identity=0x0)_permissions_can_delete_proposal"></a>

## Function `can_delete_proposal`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_can_delete_proposal">can_delete_proposal</a>(): u32
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_can_delete_proposal">can_delete_proposal</a>(): u32 { <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_CAN_DELETE_PROPOSAL">CAN_DELETE_PROPOSAL</a> }
</code></pre>



</details>

<a name="(iota_identity=0x0)_permissions_can_remove_approval"></a>

## Function `can_remove_approval`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_can_remove_approval">can_remove_approval</a>(): u32
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_can_remove_approval">can_remove_approval</a>(): u32 { <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_CAN_REMOVE_APPROVAL">CAN_REMOVE_APPROVAL</a> }
</code></pre>



</details>

<a name="(iota_identity=0x0)_permissions_all"></a>

## Function `all`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_all">all</a>(): u32
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_all">all</a>(): u32 { <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_ALL_PERMISSIONS">ALL_PERMISSIONS</a> }
</code></pre>



</details>

<a name="(iota_identity=0x0)_permissions_not"></a>

## Function `not`

Negate a permission


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_not">not</a>(permission: u32): u32
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_not">not</a>(permission: u32): u32 {
    permission ^ <a href="../../dependencies/nplex/permissions.md#(iota_identity=0x0)_permissions_all">all</a>()
}
</code></pre>



</details>
