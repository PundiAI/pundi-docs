# Accounting of Balances

PURSE now accounts for 2 types of balances:

* Inactive Balance: Refers to the amount of PURSE (ERC20) that an address has
* Active Balance: Refers to the ERC20 value of PURSE (ERC721) that an address has
* Total Balance: Refers to the sum of Inactive Balance and Active Balance of an address
  * This also refers to how much PURSE an address still has.

<figure><img src="../.gitbook/assets/purse404Balances.png" alt=""><figcaption></figcaption></figure>

An address’s total balance of PURSE at any given point in time would be the sum of its Inactive Balance and Active Balance; and this would also be how much PURSE an address can still transact with. On a granular level, the Inactive Balance of an address accounts for the PURSE tokens that have not been used for minting any PURSE NFTs, and the Active Balance of an address accounts for the ERC20 value of the total number of NFTs an address currently holds.

The accounting of an address’s Inactive Balance and Active Balance of PURSE follows the general guidelines:

1. ERC20 related transfers update the Inactive Balance.
2. ERC721 related transfers update the Active Balance.
3. The Total Balance, which is the sum of the Inactive Balance and Active Balance, represents the total amount of PURSE an address can use.
4. When the Inactive Balance is insufficient to cover an ERC20 related transfer, funds in the Active Balance will be moved to the Inactive Balance to cover the deficit. (NFT(s) will be removed).
5. The Active Balance can only be multiples of 1,000,000; and 1,000,000 PURSE in the Active Balance represents 1 NFT.

### Examples

Currently 1 PURSE NFT requires 1,000,000 PURSE ERC20 tokens for minting. In other words, 1 PURSE NFT is equivalent to 1,000,000 PURSE ERC20. The following scenarios will describe how PURSE conducts its accounting of balances in different circumstances.

### Scenario 1: Before & After Minting

If Alice currently has 5,000,000 PURSE ERC20 tokens and she has not minted any PURSE NFTs, her Inactive balance (**IB**) will be 5,000,000 PURSE, Active balance (**AB**) will be 0 PURSE, and Total Balance (**TB**) will be 5,000,000 PURSE.&#x20;

Now, Alice decides to mint 1 PURSE NFT, and this will require 1,000,000 PURSE ERC20. After minting 1 PURSE NFT, Alice’s balance will now be: **IB** = 4,000,000 PURSE, **AB** = 1,000,000 PURSE, and **TB** = 5,000,000 PURSE. And if we check her balance of NFTs through the contract’s `erc721BalanceOf`  function, it will return 1.

Even though Alice technically “spent” 1,000,000 PURSE ERC20 to mint 1 PURSE NFT, that amount is just deducted from her Inactive Balance and added to her Active Balance. Recall that the Active Balance of an address represents the total ERC20 value of all ERC721 tokens an address is holding; and this explains why Alice’s **AB** is 1,000,000 even though `erc721BalanceOf` of her address returns 1. After minting 1 PURSE NFT, Alice did not technically lose 1,000,000 PURSE from her Total Balance, the contract just moved that amount to a different storage slot for accounting.&#x20;

At the end of minting a PURSE NFT, Alice’s Total Balance will still remain at 5,000,000 PURSE since **TB** = **IB** + **AB**. If we check her total balance of PURSE through the contract’s `balanceOf` function, it will return 5,000,000 PURSE.

### **Scenario 2: After Transfer, as ERC20**

In PURSE, an address is responsible for ensuring that it always has sufficient balance to represent the NFT(s) it owns, otherwise, NFT(s) will be removed from the address. In Alice’s example, this means that if she wanted to hold onto her single PURSE NFT, she must ensure that her **IB** is sufficient to cover any PURSE related transactions.

Since Alice has a total of 5,000,000 PURSE, she decides that it’d be good to generate some returns from having so much PURSE; and so Alice deposits 3,000,000 PURSE into Purse Staking. As Alice is depositing PURSE as ERC20 tokens, this amount is deducted from her Inactive Balance, and her Active Balance remains unchanged. Alice’s **TB** will now be 2,000,000 PURSE; and if we break her address’s Total Balance down, it will be: **IB** = 1,000,000 PURSE, and **AB** = 1,000,000 PURSE. At this point, Alice still has her PURSE NFT with her address since she did not do anything with it; and she can still transact with 2,000,000 PURSE.

Bob, who is Alice’s best friend, wants to try depositing PURSE into Purse Staking but he does not have any PURSE. Alice, who is feeling more than generous, decides to transfer 500,000 PURSE ERC20 to Bob so that he can also earn a little extra on the side. After transferring PURSE to Bob, Alice’s **TB** will be 1,500,000 PURSE; and specifically: **IB** = 500,000 PURSE, **AB** = 1,000,000 PURSE, and Alice still has her PURSE NFT in her address.&#x20;

Next, Alice decides that she wants to transfer another 500,000 PURSE ERC20 to Bob just for the sake of it. After the second transfer to Bob, Alice’s **TB** will be 1,000,000 PURSE; and in more detail: **IB** = 0 PURSE, **AB** = 1,000,000 PURSE, and her single PURSE NFT remains in her address.&#x20;

During these two transfers to Bob, Alice did not lose her PURSE NFT because her Inactive Balance was sufficient to cover both ERC20 transfers. Despite Alice’s Inactive Balance reaching 0, Alice still successfully keeps her PURSE NFT because her Active Balance was untouched. In addition, since her Total Balance is 1,000,000 PURSE (**TB** = **IB** + **AB**), Alice can still transact with 1,000,000 PURSE.

### Scenario 3: After Transfer, as ERC20, which Results in NFT Deduction

As with any 404 token, including PURSE, NFTs are fungible. Therefore, even though Alice’s **IB** is 0, her **AB** is 1,000,000 thanks to the PURSE NFT she owns. This means Alice’s **TB** of PURSE is 1,000,000 and she can still transact with PURSE as ERC20 at 1,000,000 PURSE.

Alice decides that she wants to deposit another 100,000 PURSE into Purse Staking. Since Alice has 1,000,000 PURSE to spend, she will successfully deposit to Purse Staking. However, Alice’s PURSE NFT will be removed from her address to offset the deficit in her Inactive Balance. The accounting of Alice’s balances will now be: Total Balance (**TB**) = 900,000 PURSE, where specifically Inactive Balance (**IB**) = 900,000 and Active Balance (**AB**) = 0.

When Alice deposits the 100,000 PURSE into Purse Staking, her **IB** was not enough to cover the transaction. In a situation like this, PURSE will then use the following steps to calculate the number of NFTs to remove from an address and calibrate the address’s internal accounting of balances (remember that 1,000,000 PURSE is required to maintain 1 PURSE NFT):

$$
\small \Delta \ = \ transferValue \ - \ inactiveBalance_{address}
$$

$$
\small nftsToWithdrawAndStore \ = \ [\frac{\Delta}{n}] \ + \ (\Delta \ mod \ n > 0 \ ? \ 1 : 0)
$$

$$
\small newInactiveBalance_{address} \ = \ inactiveBalance_{address} \ + \ (nftsToWithdrawAndStore \ * \ n)
$$

Where: $$\Delta$$ represents the difference between the transfer value and an address’s current inactive balance, $$n$$ represents the PURSE amount required to maintain 1 PURSE NFT, and $$[\frac{\Delta}{n}]$$ represents the integer (floor) division of $$\Delta$$ with $$n$$. If $$\Delta \ mod \ n$$ is true, it returns 1, otherwise it returns 0.

When Alice deposits 100,000 PURSE into Purse Staking, given that her $$transferValue$$ is 100,000 and her $$inactiveBalance_{address}$$ is 0, then $$nftsToWithdrawAndStore$$ will be 1, and $$newInactiveBalance_{address}$$ will be 1,000,000.&#x20;

When 1 PURSE NFT is removed from Alice’s address, 1,000,000 PURSE will be deducted from the **AB**, and the same amount will be added back to the **IB**. Alice will no longer have her PURSE NFT since it is removed, but she will still be able to carry out the transaction to deposit 100,000 PURSE, and her remaining **TB** of PURSE after the deposit will be 900,000 (**IB** = 900,000 and **AB** = 0).

In a completely different situation where Alice’s balances are: **IB** = 0 and **AB** = 2,000,000 (meaning she has 2 PURSE NFTs), and Alice proceeds to carry out the same deposit transaction with 100,000 PURSE, then her balance in the PURSE contract will be: **IB** = 900,000 and **AB** = 1,000,000, and she will lose only 1 PURSE NFT. After the deposit, Alice would have 1,900,000 PURSE remaining in her **TB**, which also includes 1 PURSE NFT in her address.

**Note that this mechanism involving NFTs is fixed into any 404-like token and is not an opt-out. It is every user’s responsibility to ensure that their balance is sufficient to maintain their NFTs.**
