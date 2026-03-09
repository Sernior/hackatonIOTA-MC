
<a name="(iota_identity=0x0)_upgrade_proposal"></a>

# Module `(iota_identity=0x0)::upgrade_proposal`



-  [Struct `Upgrade`](#(iota_identity=0x0)_upgrade_proposal_Upgrade)
-  [Function `new`](#(iota_identity=0x0)_upgrade_proposal_new)


<pre><code></code></pre>



<a name="(iota_identity=0x0)_upgrade_proposal_Upgrade"></a>

## Struct `Upgrade`

Proposal's action used to upgrade an <code>Identity</code> to the package's current version.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/upgrade.md#(iota_identity=0x0)_upgrade_proposal_Upgrade">Upgrade</a> <b>has</b> <b>copy</b>, drop, store
</code></pre>



<details>
<summary>Fields</summary>


<dl>
</dl>


</details>

<a name="(iota_identity=0x0)_upgrade_proposal_new"></a>

## Function `new`

Creates a new <code><a href="../../dependencies/nplex/upgrade.md#(iota_identity=0x0)_upgrade_proposal_Upgrade">Upgrade</a></code> action.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/upgrade.md#(iota_identity=0x0)_upgrade_proposal_new">new</a>(): (iota_identity=0x0)::upgrade_proposal::Upgrade
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/upgrade.md#(iota_identity=0x0)_upgrade_proposal_new">new</a>(): <a href="../../dependencies/nplex/upgrade.md#(iota_identity=0x0)_upgrade_proposal_Upgrade">Upgrade</a> {
    <a href="../../dependencies/nplex/upgrade.md#(iota_identity=0x0)_upgrade_proposal_Upgrade">Upgrade</a> {}
}
</code></pre>



</details>
