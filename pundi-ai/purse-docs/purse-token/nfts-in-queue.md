# NFTs in Queue

PURSE NFTs that are transferred back to the PURSE contract are stored in a queue-like data structure. This queue is a First-In-First-Out (**FIFO**) structure, which means that the first PURSE NFT that is sent to this queue will be the first NFT minted on the next mint transaction. If the queue is empty, then a brand new NFT token id will be minted on the next mint transaction.

<figure><img src="../.gitbook/assets/purse404fifo.png" alt=""><figcaption></figcaption></figure>

### Example

### Scenario 7

Continuing from the previous example with Bob, since token id 9 was Bob’s most recent PURSE NFT, it was the first NFT to be removed from his address; and since token id 8 was Bob’s next most recent PURSE NFT, it follows after. These two NFTs are transferred back to the PURSE contract and are stored in the contract’s queue where they are now available for minting again. Because the queue in the PURSE contract is a FIFO structure, token id 9 which entered the queue first, will be primed as the next mintable token id. And anyone with sufficient PURSE and ETH will be eligible to mint PURSE NFT token id 9 first, followed by token id 8.

If Alice decides to call `mintERC721` on the contract, she will be minting PURSE NFT token id 9 since token id 9 is the first NFT in the contract’s FIFO queue. But if Bob is able to mint an NFT before Alice does, he will be able to get back token id 9. Similarly, after PURSE NFT token id 9 has been minted from the contract, the next address that mints a PURSE NFT will be minting token id 8. Eventually, if the queue is empty and an address mints a PURSE NFT, then a new token id will be minted to that address, which in this case would be token id 10.
