# Minting PURSE NFT(s)

When it comes to minting NFTs from a 404 token, most 404 tokens that have been deployed would behave in the following way: if an address’s balance reaches the required amount of tokens required to represent 1 NFT, an NFT will be minted to the address automatically. No separate transaction from the address is required to mint an NFT. This is, however, not the case for PURSE.

<figure><img src="../.gitbook/assets/purse404minting.png" alt=""><figcaption></figcaption></figure>

In PURSE, the minting of a PURSE NFT must be a transaction that an address voluntarily executes. That is, even if an address successfully accumulates enough PURSE tokens, they must still execute the `mintERC721` function successfully in the PURSE contract in order to mint their PURSE NFT(s). The number of NFTs mintable at once would depend on an address’s Inactive Balance (IB), and whether they have enough **Ether** **(ETH)** to pay for the total minting cost for each mintable NFT. The contract only accepts the **exact** amount of ETH required for the mint transaction; any amount that is not exact will result in a failure to mint the PURSE NFT(s).

$$
\small PURSE \ required \ from \ IB \ = \ no. \ of \ NFTs \ to \ mint \  * \  ERC20 \ equivalent \ amount \ for \ 1 \ NFT
$$

$$
\small payable \ amount \ in \ ETH \ = \ mintingCost \ per \ NFT \  * \  no. \ of \ NFTs \ to \ mint
$$

The rationale behind this design is to give users the flexibility to participate in different token types. Because of how the underlying ERC20 contract is preserved in PURSE, even if users choose not to mint any PURSE NFTs, PURSE would still function exactly as before - like any other ERC20 token. And if users decide to mint PURSE NFT(s), they can participate in new avenues for trading and asset management.

### Example

### Scenario 4: Minting an NFT

Remember how Alice transferred a total of 1,000,000 PURSE to Bob ([Scenario 2](accounting-of-balances.md#scenario-2-after-transfer-as-erc20)) a while back?&#x20;

Assuming Bob didn’t do anything after Alice transferred all that PURSE to him, Bob’s Total Balance (**TB**) will be 1,000,000 PURSE, where Inactive Balance (**IB**) = 1,000,000 PURSE and Active Balance (**AB**) = 0 PURSE. Bob will be able to transact with 1,000,000 PURSE ERC20, but he will not have any PURSE NFT in his address. Note that all regular transfers called by the `transfer` function will just be a regular ERC20 transfer, and this only affects values in the **IB**. This will be elaborated in the [Transferring PURSE](transferring-purse.md) section.

For Bob to obtain a PURSE NFT, he would have to execute `mintERC721` in the PURSE contract; and he would also need to have an appropriate amount of PURSE in his **IB** and supply the exact `mintingCost`, which is in **Ether (ETH)**, as part of the transaction. Thus for Bob to successfully mint 1 PURSE NFT, he needs to have at least 1,000,000 PURSE in his **IB**, and he also has to provide exactly:$$1 \ * \ mintingCost$$ of ETH, together with the transaction.&#x20;

After minting, Bob’s balance of PURSE would be: **IB** = 0 PURSE, **AB** = 1,000,000 PURSE, and **TB** = 1,000,000 PURSE; Bob will also have 1 PURSE NFT in his address.

Notice that in this scenario, Bob's **TB** of PURSE started at 1,000,000 PURSE and ended unchanged at 1,000,000 PURSE. Like in [Scenario 1](accounting-of-balances.md#scenario-1-before-and-after-minting), minting a PURSE NFT does not deduct PURSE from the Total Balance**;** instead, the amount of PURSE required to mint the PURSE NFT is just moved from the Inactive Balance to the Active Balance, and it is still accounted for in the Total Balance.
