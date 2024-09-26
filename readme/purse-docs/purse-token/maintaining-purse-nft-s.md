# Maintaining PURSE NFT(s)

As with any 404 token, it is each user’s responsibility to ensure that they have sufficient balance to preserve any 404 NFT they have in their address. PURSE is no exception to this rule. Different 404 tokens will enforce this rule differently. In some 404 tokens, once an address does not have sufficient balance to maintain its NFTs, the NFTs get burned from the address; but in others, the address’s NFTs might get transferred out from the address and are stored somewhere temporarily. In most cases, it is an address’s most recent NFT(s) that gets affected by this rule, and the minimum balance required to maintain any 404 NFT in an address simply follows the following equation:

$$
\small minimum \ balance \ required \ = \ number \ of \ NFTs \ * \ ERC20 \ equivalent \ amount \ for \ 1 \ NFT
$$

In PURSE, 1 PURSE NFT requires 1,000,000 PURSE ERC20 to be maintained in an address. And if this condition cannot be maintained, then the address would lose that PURSE NFT. When this PURSE NFT is transferred out of the address, it does not get burned, instead it gets transferred back to the PURSE contract and is available for minting; and anyone who successfully mints a PURSE NFT thereafter will obtain the PURSE NFT that is stored in the contract. PURSE NFTs that get sent back to the contract as a result of an address having insufficient balance to maintain them are stored in a queue-like structure, this will be highlighted in the next section after the following example.

### Example

### Scenario 6

Bob’s Total Balance (**TB**) of PURSE is now at 4,000,000 PURSE, where his Inactive Balance (**IB**) = 1,000,000 PURSE and his Active Balance (**AB**) = 3,000,000 PURSE. This means Bob has 3 PURSE NFTs in his address, and his NFT token ids - in the order of oldest to newest, are: 7, 8, 9 (actual PURSE NFT token ids start at a much larger number, this is just an example).

Bob is an extremely busy person and he momentarily forgets that PURSE is now a 404 token and he is required to maintain a minimum balance of 3,000,000 PURSE in order to preserve his 3 PURSE NFTs. He proceeds to transfer 2,800,000 PURSE to Alice, and he finds that his **TB** is now at 1,200,000 PURSE, where **IB** = 200,000 PURSE, **AB** = 1,000,000 PURSE; and he only has token id 7 left in his address.

Initially, when Bob transfers 2,800,000 PURSE out of his address, the PURSE in his **IB** will be used first to carry out the transfer. Since Bob only had 1,000,000 PURSE in his **IB**, this amount will be depleted and his **IB** will be 0; next, because 1,800,000 PURSE is still needed for the transfer and Bob has 3,000,000 PURSE available in his **AB**, two of Bob’s most recent NFTs are removed from his address to offset the remaining 1,800,000 PURSE required for the transfer. The removal of Bob’s 2 most recent NFTs (token id 9 first and then token id 8) will reduce his **AB** by 2,000,000 PURSE, but increase his **IB** by the same amount; and the transfer transaction will be carried out successfully, leaving Bob’s new **TB** as 1,200,000 PURSE (**IB** = 200,000 PURSE & **AB** = 1,000,000 PURSE).

