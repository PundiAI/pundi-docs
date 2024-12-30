# Transferring PURSE

The upgraded PURSE contract has a number of functions to transfer PURSE as ERC20 or ERC721.

PURSE transfers that are ERC20 related remain mostly the same prior to the upgrade, however there are some important updates. Some of the updates concerning PURSE transfers are: `transferFrom` is now a function that can be used for both ERC20 and ERC721, depending on the value that is passed as the `valueOrId_` argument; and `erc20TransferFrom` and `erc721TransferFrom` are functions added as wrappers to emulate what a pure `transferFrom` would behave in standard ERC20 and ERC721 tokens. A detailed breakdown for each transfer related function is provided below.

During PURSE ERC20 transfers, the contract will first try to use up all the PURSE in an address’s Inactive Balance. Once the Inactive Balance is depleted, the contract will start to use the PURSE in the address’s Active Balance - which represents the PURSE NFTs owned by the address. However, this will result in NFTs being removed from the address to offset the deficit in the Inactive Balance; and each removal of an NFT would result in an increment of 1,000,000 PURSE in the Inactive Balance, but a reduction of 1,000,000 PURSE in the Active Balance. (See [Scenario 3](accounting-of-balances.md#scenario-3-after-transfer-as-erc20-which-results-in-nft-deduction) as an example)

When a PURSE NFT is successfully transferred from one address to another - regardless of whether the recipient is an Externally Owned Account (EOA) or a smart contract, the ownership of the NFT is transferred to the recipient, and the Active Balances of both the sender and the recipient are updated accordingly. Since 1 PURSE NFT is represented by 1,000,000 PURSE ERC20, the sender’s Active Balance will be deducted by this amount while the recipient’s Active Balance will be increased by the same amount; and the Inactive Balance for both parties will remain unchanged since this is an ERC721 transfer.

When a PURSE NFT is transferred, the transfer is technically moving 1,000,000 PURSE from the sender to the recipient; but instead of the change in balance being accounted for in the Inactive Balance, it is accounted for in the Active Balance. Since the Total Balance is the sum of the Inactive Balance and Active Balance, this change will also be reflected in the current Total Balance of PURSE for both the sender and the recipient.

### Example

### Scenario 5: Transferring PURSE NFT

With 1,000,000 PURSE in his balance, Bob decides to mint a PURSE NFT. After minting, Bob’s Total Balance (**TB**) of PURSE is still 1,000,000 PURSE, but the breakdown of his total balance will now be: Inactive Balance (**IB**) = 0 PURSE and Active Balance (**AB**) = 1,000,000 PURSE.

Bob determines that he wants to return Alice the PURSE she sent him, but he only has one PURSE NFT in his address which represents all the PURSE in his current balance. Bob transfers the PURSE NFT to Alice, and now his balance of PURSE is completely zero. On the other hand, Alice’s balance has now increased by 1,000,000 PURSE, and she has one PURSE NFT in her address.

Recall at the end of [Scenario 3](accounting-of-balances.md#scenario-3-after-transfer-as-erc20-which-results-in-nft-deduction), Alice’s total balance was 900,000 PURSE, where **IB** = 900,000 and **AB** = 0, and she didn't have a PURSE NFT. Now after receiving Bob’s PURSE NFT, Alice’s **TB** is now 1,900,000 PURSE, where **IB** = 900,000 PURSE and **AB** = 1,000,000 PURSE, and she has one PURSE NFT.\\

### ERC20 Transfers

The following are functions that can be used to transfer PURSE as an ERC20 token:

1. `transfer`

```solidity
function transfer(address to_, uint256 value_) public virtual override returns (bool)
```

* Pure ERC20 `transfer`.
* `value_` is strictly treated as ERC20 amounts, even if the amount is a valid ERC721 token id. Assumes the operator is attempting to transfer as ERC20.
* Updates the Inactive Balance of both the `msg.sender` and `to_`.
* Returns a `boolean` value indicating operation success.

2. `transferFrom`

{% code overflow="wrap" %}
```solidity
function transferFrom(address from_, address to_, uint256 valueOrId_) public virtual override returns (bool)
```
{% endcode %}

* Function for mixed transfers using either `erc20TransferFrom` or `erc721TransferFrom`, depending on `valueOrId_`.
* The function assumes that the operator is attempting to transfer as ERC721 if `valueOrId_` is a valid ERC721 token id.
* If `valueOrId_` is not a valid ERC721 token id, it transfers as ERC20.
* Returns a `boolean` value indicating operation success.

3. `erc20TransferFrom`

{% code overflow="wrap" %}
```solidity
function erc20TransferFrom(address from_, address to_, uint256 value_) public virtual returns (bool)
```
{% endcode %}

* Function for ERC20 `transferFrom`.
* Moves `value_` amount of PURSE from `from_` to `to_` using the allowance mechanism. Updates only the Inactive Balance of both `from_` and `to_`.
* `value_` is deducted from the operator’s allowance.
* Updates the Inactive Balance of both `from_` and `to_`.
* Returns a `boolean` value indicating operation success.

### ERC721 Transfers

The following are functions that can be used to transfer PURSE as an ERC721 token:

1. `transferFrom`

{% code overflow="wrap" %}
```solidity
function transferFrom(address from_, address to_, uint256 valueOrId_) public virtual override returns (bool)
```
{% endcode %}

* Function for mixed transfers using either `erc20TransferFrom` or `erc721TransferFrom`, depending on `valueOrId_`.
* The function assumes that the operator is attempting to transfer as ERC721 if `valueOrId_` is a valid ERC721 token id.
* If `valueOrId_` is not a valid ERC721 token id, it transfers as ERC20.
* Returns a `boolean` value indicating operation success.
* **Use of `safeTransferFrom` is preferred and highly recommended over `transferFrom` for ERC721 transfers.**

2. `erc721TransferFrom`

{% code overflow="wrap" %}
```solidity
function erc721TransferFrom(address from_, address to_, uint256 id_) public virtual
```
{% endcode %}

* Function for ERC721 \`transferFrom\`.
* Transfers \`id\_\` from \`from\_\` to \`to\_\`.
* Both \`from\_\` and \`to\_\` cannot be the zero address.
* \`id\_\` must be owned by \`from\_\`
* If the operator is not \`from\_\`, the operator must be approved to move the token by either \`approve\` or \`setApprovalForAll\`.
* Updates both Inactive Balance and Active Balance of both \`from\_\` and \`to\_\`.
* **IMPORTANT: The operator is responsible for confirming that the recipient (`to_`) is capable of receiving ERC721 tokens or else they may be permanently lost. Recommend to use `safeTransferFrom` but the operator must understand that this adds an external call to the recipient which may create a reentrancy vulnerability.**

3. `safeTransferFrom`

{% code overflow="wrap" %}
```solidity
function safeTransferFrom(address from_, address to_, uint256 id_) public virtual
```
{% endcode %}

* Safely transfers `id_` token from `from_` to `to_`, checking first that contract recipients are aware of the ERC721 protocol and returns the magic value to the PURSE contract. This prevents tokens from being locked permanently.
* Same as `erc721TransferFrom`.
* **If `to_` is a smart contract, it must implement `IERC721Receiver.onERC721Received`, which is called upon a safe transfer.**

4. `safeTransferFrom` (with additional `bytes`)

{% code overflow="wrap" %}
```solidity
function safeTransferFrom(address from_, address to_, uint256 id_, bytes memory data_) public virtual
```
{% endcode %}

* Overloaded function of `safeTransferFrom`.
* Takes an additional bytes argument: `data_`.

### Transfer Guide

The following table provides recommendations for the different transfer functions to execute based on the circumstances of the transfer.

<table><thead><tr><th width="257">Scenario</th><th>Recommended Function</th></tr></thead><tbody><tr><td>Send PURSE as ERC20</td><td><ul><li>transfer(address,uint256)</li><li>transferFrom(address,address,uint256)</li></ul></td></tr><tr><td>Send PURSE as ERC721</td><td><ul><li>safeTransferFrom(address,address,uint256)</li></ul></td></tr><tr><td>Send PURSE as ERC721, with additional data</td><td><ul><li>safeTransferFrom(address,address,uint256,bytes)</li></ul></td></tr><tr><td>Send PURSE as ERC721, without recipient check</td><td><ul><li>transferFrom(address,address,uint256)</li></ul></td></tr></tbody></table>
