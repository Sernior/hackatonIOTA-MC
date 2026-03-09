
<a name="(iota_identity=0x0)_asset"></a>

# Module `(iota_identity=0x0)::asset`



-  [Struct `AssetTransferCreated`](#(iota_identity=0x0)_asset_AssetTransferCreated)
-  [Struct `AssetTransferConcluded`](#(iota_identity=0x0)_asset_AssetTransferConcluded)
-  [Struct `AuthenticatedAsset`](#(iota_identity=0x0)_asset_AuthenticatedAsset)
-  [Struct `TransferProposal`](#(iota_identity=0x0)_asset_TransferProposal)
-  [Struct `SenderCap`](#(iota_identity=0x0)_asset_SenderCap)
-  [Struct `RecipientCap`](#(iota_identity=0x0)_asset_RecipientCap)
-  [Constants](#@Constants_0)
-  [Function `new`](#(iota_identity=0x0)_asset_new)
-  [Function `new_with_config`](#(iota_identity=0x0)_asset_new_with_config)
-  [Function `origin`](#(iota_identity=0x0)_asset_origin)
-  [Function `borrow`](#(iota_identity=0x0)_asset_borrow)
-  [Function `borrow_mut`](#(iota_identity=0x0)_asset_borrow_mut)
-  [Function `set_content`](#(iota_identity=0x0)_asset_set_content)
-  [Function `delete`](#(iota_identity=0x0)_asset_delete)
-  [Function `new_with_address`](#(iota_identity=0x0)_asset_new_with_address)
-  [Function `transfer`](#(iota_identity=0x0)_asset_transfer)
-  [Function `accept`](#(iota_identity=0x0)_asset_accept)
-  [Function `conclude_or_cancel`](#(iota_identity=0x0)_asset_conclude_or_cancel)
-  [Function `delete_sender_cap`](#(iota_identity=0x0)_asset_delete_sender_cap)
-  [Function `delete_recipient_cap`](#(iota_identity=0x0)_asset_delete_recipient_cap)
-  [Function `delete_transfer`](#(iota_identity=0x0)_asset_delete_transfer)


<pre><code><b>use</b> <a href="../../dependencies/iota/address.md#iota_address">iota::address</a>;
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



<a name="(iota_identity=0x0)_asset_AssetTransferCreated"></a>

## Struct `AssetTransferCreated`

Event emitted when the owner of an <code><a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a></code>
proposes its transfer to a new address.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AssetTransferCreated">AssetTransferCreated</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>asset: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>proposal: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>sender: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>recipient: <b>address</b></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_asset_AssetTransferConcluded"></a>

## Struct `AssetTransferConcluded`

Event emitted when an active transfer is concluded,
either canceled or completed.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AssetTransferConcluded">AssetTransferConcluded</a> <b>has</b> <b>copy</b>, drop
</code></pre>



<details>
<summary>Fields</summary>


<dl>
<dt>
<code>asset: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>proposal: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>sender: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>recipient: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>concluded: bool</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_asset_AuthenticatedAsset"></a>

## Struct `AuthenticatedAsset`

Structures that couples some data <code>T</code> with well known
ownership and origin, along configurable abilities e.g.
transferability, mutability and deletability.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a>&lt;T: store&gt; <b>has</b> key
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
<code>inner: T</code>
</dt>
<dd>
</dd>
<dt>
<code><a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_origin">origin</a>: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>owner: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>mutable: bool</code>
</dt>
<dd>
</dd>
<dt>
<code>transferable: bool</code>
</dt>
<dd>
</dd>
<dt>
<code>deletable: bool</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_asset_TransferProposal"></a>

## Struct `TransferProposal`

Structure that encodes the logic required to transfer an <code><a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a></code>
from one address to another. The transfer can be refused by the recipient.


<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_TransferProposal">TransferProposal</a> <b>has</b> key
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
<code>asset_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>sender_address: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>sender_cap_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>recipient_address: <b>address</b></code>
</dt>
<dd>
</dd>
<dt>
<code>recipient_cap_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
<dt>
<code>done: bool</code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_asset_SenderCap"></a>

## Struct `SenderCap`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_SenderCap">SenderCap</a> <b>has</b> key
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
<code>transfer_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="(iota_identity=0x0)_asset_RecipientCap"></a>

## Struct `RecipientCap`



<pre><code><b>public</b> <b>struct</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_RecipientCap">RecipientCap</a> <b>has</b> key
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
<code>transfer_id: <a href="../../dependencies/iota/object.md#iota_object_ID">iota::object::ID</a></code>
</dt>
<dd>
</dd>
</dl>


</details>

<a name="@Constants_0"></a>

## Constants


<a name="(iota_identity=0x0)_asset_EImmutable"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_EImmutable">EImmutable</a>: u64 = 0;
</code></pre>



<a name="(iota_identity=0x0)_asset_ENonTransferable"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_ENonTransferable">ENonTransferable</a>: u64 = 1;
</code></pre>



<a name="(iota_identity=0x0)_asset_ENonDeletable"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_ENonDeletable">ENonDeletable</a>: u64 = 2;
</code></pre>



<a name="(iota_identity=0x0)_asset_EInvalidRecipient"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_EInvalidRecipient">EInvalidRecipient</a>: u64 = 3;
</code></pre>



<a name="(iota_identity=0x0)_asset_EInvalidSender"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_EInvalidSender">EInvalidSender</a>: u64 = 4;
</code></pre>



<a name="(iota_identity=0x0)_asset_EInvalidAsset"></a>



<pre><code><b>const</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_EInvalidAsset">EInvalidAsset</a>: u64 = 5;
</code></pre>



<a name="(iota_identity=0x0)_asset_new"></a>

## Function `new`

Creates a new <code><a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a></code> with default configuration: immutable, non-transferable, non-deletable;
and sends it to the tx's sender.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_new">new</a>&lt;T: store&gt;(inner: T, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_new">new</a>&lt;T: store&gt;(inner: T, ctx: &<b>mut</b> TxContext) {
    <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_new_with_address">new_with_address</a>(inner, ctx.sender(), <b>false</b>, <b>false</b>, <b>false</b>, ctx);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_new_with_config"></a>

## Function `new_with_config`

Creates a new <code><a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a></code> with configurable properties and sends it to the tx's sender.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_new_with_config">new_with_config</a>&lt;T: store&gt;(inner: T, mutable: bool, transferable: bool, deletable: bool, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_new_with_config">new_with_config</a>&lt;T: store&gt;(
    inner: T,
    mutable: bool,
    transferable: bool,
    deletable: bool,
    ctx: &<b>mut</b> TxContext,
) {
    <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_new_with_address">new_with_address</a>(inner, ctx.sender(), mutable, transferable, deletable, ctx);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_origin"></a>

## Function `origin`

Returns the address that created this <code><a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a></code>.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_origin">origin</a>&lt;T: store&gt;(self: &(iota_identity=0x0)::asset::AuthenticatedAsset&lt;T&gt;): <b>address</b>
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_origin">origin</a>&lt;T: store&gt;(self: &<a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a>&lt;T&gt;): <b>address</b> {
    self.<a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_origin">origin</a>
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_borrow"></a>

## Function `borrow`

Immutably borrow the content of an <code><a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a></code>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_borrow">borrow</a>&lt;T: store&gt;(self: &(iota_identity=0x0)::asset::AuthenticatedAsset&lt;T&gt;): &T
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_borrow">borrow</a>&lt;T: store&gt;(self: &<a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a>&lt;T&gt;): &T {
    &self.inner
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_borrow_mut"></a>

## Function `borrow_mut`

Mutably borrow the content of an <code><a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a></code>.
This operation will fail if <code><a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a></code> is configured as non-mutable.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_borrow_mut">borrow_mut</a>&lt;T: store&gt;(self: &<b>mut</b> (iota_identity=0x0)::asset::AuthenticatedAsset&lt;T&gt;): &<b>mut</b> T
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_borrow_mut">borrow_mut</a>&lt;T: store&gt;(self: &<b>mut</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a>&lt;T&gt;): &<b>mut</b> T {
    <b>assert</b>!(self.mutable, <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_EImmutable">EImmutable</a>);
    &<b>mut</b> self.inner
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_set_content"></a>

## Function `set_content`

Updates the value of the stored content. Fails if this <code><a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a></code> is immutable.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_set_content">set_content</a>&lt;T: drop, store&gt;(self: &<b>mut</b> (iota_identity=0x0)::asset::AuthenticatedAsset&lt;T&gt;, new_content: T)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_set_content">set_content</a>&lt;T: store + drop&gt;(self: &<b>mut</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a>&lt;T&gt;, new_content: T) {
    <b>assert</b>!(self.mutable, <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_EImmutable">EImmutable</a>);
    self.inner = new_content;
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_delete"></a>

## Function `delete`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_delete">delete</a>&lt;T: drop, store&gt;(self: (iota_identity=0x0)::asset::AuthenticatedAsset&lt;T&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_delete">delete</a>&lt;T: store + drop&gt;(self: <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a>&lt;T&gt;) {
    <b>assert</b>!(self.deletable, <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_ENonDeletable">ENonDeletable</a>);
    <b>let</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a> {
        id,
        inner: _,
        <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_origin">origin</a>: _,
        owner: _,
        mutable: _,
        transferable: _,
        deletable: _,
    } = self;
    object::delete(id);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_new_with_address"></a>

## Function `new_with_address`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_new_with_address">new_with_address</a>&lt;T: store&gt;(inner: T, addr: <b>address</b>, mutable: bool, transferable: bool, deletable: bool, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_new_with_address">new_with_address</a>&lt;T: store&gt;(
    inner: T,
    addr: <b>address</b>,
    mutable: bool,
    transferable: bool,
    deletable: bool,
    ctx: &<b>mut</b> TxContext,
) {
    <b>let</b> asset = <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a> {
        id: object::new(ctx),
        inner,
        <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_origin">origin</a>: addr,
        owner: addr,
        mutable,
        transferable,
        deletable,
    };
    transfer::transfer(asset, addr);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_transfer"></a>

## Function `transfer`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_transfer">transfer</a>&lt;T: store&gt;(asset: (iota_identity=0x0)::asset::AuthenticatedAsset&lt;T&gt;, recipient: <b>address</b>, ctx: &<b>mut</b> <a href="../../dependencies/iota/tx_context.md#iota_tx_context_TxContext">iota::tx_context::TxContext</a>)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_transfer">transfer</a>&lt;T: store&gt;(
    asset: <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a>&lt;T&gt;,
    recipient: <b>address</b>,
    ctx: &<b>mut</b> TxContext,
) {
    <b>assert</b>!(asset.transferable, <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_ENonTransferable">ENonTransferable</a>);
    <b>let</b> proposal_id = object::new(ctx);
    <b>let</b> sender_cap = <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_SenderCap">SenderCap</a> {
        id: object::new(ctx),
        transfer_id: proposal_id.to_inner(),
    };
    <b>let</b> recipient_cap = <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_RecipientCap">RecipientCap</a> {
        id: object::new(ctx),
        transfer_id: proposal_id.to_inner(),
    };
    <b>let</b> proposal = <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_TransferProposal">TransferProposal</a> {
        id: proposal_id,
        asset_id: object::id(&asset),
        sender_cap_id: object::id(&sender_cap),
        sender_address: asset.owner,
        recipient_cap_id: object::id(&recipient_cap),
        recipient_address: recipient,
        done: <b>false</b>,
    };
    <a href="../../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AssetTransferCreated">AssetTransferCreated</a> {
        proposal: object::id(&proposal),
        asset: object::id(&asset),
        sender: asset.owner,
        recipient,
    });
    transfer::transfer(sender_cap, asset.owner);
    transfer::transfer(recipient_cap, recipient);
    transfer::transfer(asset, proposal.id.to_address());
    transfer::share_object(proposal);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_accept"></a>

## Function `accept`

Accept the transfer of the asset.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_accept">accept</a>&lt;T: store&gt;(self: &<b>mut</b> (iota_identity=0x0)::asset::TransferProposal, cap: (iota_identity=0x0)::asset::RecipientCap, asset: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;(iota_identity=0x0)::asset::AuthenticatedAsset&lt;T&gt;&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_accept">accept</a>&lt;T: store&gt;(
    self: &<b>mut</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_TransferProposal">TransferProposal</a>,
    cap: <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_RecipientCap">RecipientCap</a>,
    asset: transfer::Receiving&lt;<a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a>&lt;T&gt;&gt;,
) {
    <b>assert</b>!(self.recipient_cap_id == object::id(&cap), <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_EInvalidRecipient">EInvalidRecipient</a>);
    <b>let</b> <b>mut</b> asset = transfer::receive(&<b>mut</b> self.id, asset);
    <b>assert</b>!(self.asset_id == object::id(&asset), <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_EInvalidAsset">EInvalidAsset</a>);
    asset.owner = self.recipient_address;
    transfer::transfer(asset, self.recipient_address);
    cap.<a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_delete">delete</a>();
    self.done = <b>true</b>;
    <a href="../../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AssetTransferConcluded">AssetTransferConcluded</a> {
        proposal: self.id.to_inner(),
        asset: self.asset_id,
        sender: self.sender_address,
        recipient: self.recipient_address,
        concluded: <b>true</b>,
    })
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_conclude_or_cancel"></a>

## Function `conclude_or_cancel`

The sender of the asset consumes the <code><a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_TransferProposal">TransferProposal</a></code> to either
cancel it or to conclude it.


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_conclude_or_cancel">conclude_or_cancel</a>&lt;T: store&gt;(proposal: (iota_identity=0x0)::asset::TransferProposal, cap: (iota_identity=0x0)::asset::SenderCap, asset: <a href="../../dependencies/iota/transfer.md#iota_transfer_Receiving">iota::transfer::Receiving</a>&lt;(iota_identity=0x0)::asset::AuthenticatedAsset&lt;T&gt;&gt;)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_conclude_or_cancel">conclude_or_cancel</a>&lt;T: store&gt;(
    <b>mut</b> proposal: <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_TransferProposal">TransferProposal</a>,
    cap: <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_SenderCap">SenderCap</a>,
    asset: transfer::Receiving&lt;<a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AuthenticatedAsset">AuthenticatedAsset</a>&lt;T&gt;&gt;,
) {
    <b>assert</b>!(proposal.sender_cap_id == object::id(&cap), <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_EInvalidSender">EInvalidSender</a>);
    <b>if</b> (!proposal.done) {
        <b>let</b> asset = transfer::receive(&<b>mut</b> proposal.id, asset);
        <b>assert</b>!(proposal.asset_id == object::id(&asset), <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_EInvalidAsset">EInvalidAsset</a>);
        transfer::transfer(asset, proposal.sender_address);
        <a href="../../dependencies/iota/event.md#iota_event_emit">iota::event::emit</a>(<a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_AssetTransferConcluded">AssetTransferConcluded</a> {
            proposal: proposal.id.to_inner(),
            asset: proposal.asset_id,
            sender: proposal.sender_address,
            recipient: proposal.recipient_address,
            concluded: <b>false</b>,
        })
    };
    <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_delete_transfer">delete_transfer</a>(proposal);
    <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_delete_sender_cap">delete_sender_cap</a>(cap);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_delete_sender_cap"></a>

## Function `delete_sender_cap`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_delete_sender_cap">delete_sender_cap</a>(cap: (iota_identity=0x0)::asset::SenderCap)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_delete_sender_cap">delete_sender_cap</a>(cap: <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_SenderCap">SenderCap</a>) {
    <b>let</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_SenderCap">SenderCap</a> {
        id,
        ..,
    } = cap;
    object::delete(id);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_delete_recipient_cap"></a>

## Function `delete_recipient_cap`



<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_delete_recipient_cap">delete_recipient_cap</a>(cap: (iota_identity=0x0)::asset::RecipientCap)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b> <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_delete_recipient_cap">delete_recipient_cap</a>(cap: <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_RecipientCap">RecipientCap</a>) {
    <b>let</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_RecipientCap">RecipientCap</a> {
        id,
        ..,
    } = cap;
    object::delete(id);
}
</code></pre>



</details>

<a name="(iota_identity=0x0)_asset_delete_transfer"></a>

## Function `delete_transfer`



<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_delete_transfer">delete_transfer</a>(self: (iota_identity=0x0)::asset::TransferProposal)
</code></pre>



<details>
<summary>Implementation</summary>


<pre><code><b>public</b>(package) <b>fun</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_delete_transfer">delete_transfer</a>(self: <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_TransferProposal">TransferProposal</a>) {
    <b>let</b> <a href="../../dependencies/nplex/asset.md#(iota_identity=0x0)_asset_TransferProposal">TransferProposal</a> {
        id,
        asset_id: _,
        sender_cap_id: _,
        recipient_cap_id: _,
        sender_address: _,
        recipient_address: _,
        done: _,
    } = self;
    object::delete(id);
}
</code></pre>



</details>
