# Token IDs

Because PURSE has been upgraded from an ERC20 to a 404 token, token transfers must now take into account what constitutes an ERC20 transfer or an ERC721 transfer when `transferFrom` is executed. Both ERC20 and ERC721 tokens have a `transferFrom` function which yields the same signature hash:

```solidity
➜ keccak256("transferFrom(address,address,uint256)")
Type: bytes32
└ Data: 0x23b872dd7302113369cda2901243429419bec145408fa8b352b3dd92b66c680b
```

This means that on the level of the EVM, when PURSE is being transferred, calls to `transferFrom` will produce the same function selector of **`0x23b872dd`** regardless of whether they are intended for an ERC20 or ERC721 transfer.

In order to allow PURSE to discern if a `transferFrom` should be an ERC20’s or ERC721’s implementation, the function was overridden to make that discernment based on its uint256 argument. The maximum value for the uint256 type is: $$2^{256} - 1$$, which is an extremely large number (to put this in perspective, there are approximately $$10^{80}$$ atoms in the observable universe and the max value of `uint256` can be used to enumerate almost every known atom).

Most ERC20 transfers will not, realistically, exceed half of that maximum value, so the upper half of the range of uint256 remains to be utilized. Thus, PURSE reserves the lower half of $$2^{256} - 1$$ for ERC20’s `transferFrom` and the upper half of that number for PURSE NFT token ids.

This essentially means that when `transferFrom` is called, if the value of the `uint256` argument is a number: $$0 < x \leq 2^{255}$$, it will be executed as a ERC20 `transferFrom`. And if the value of the uint256 argument is a number: $$x > 2^{255}$$ (or $$x \geq 2^{255} \ + \ 1$$), then `transferFrom` will be executed as ERC721’s implementation.

Note that even though `transferFrom` is used here, it is always recommended to use `safeTransferFrom` when transferring as ERC721 to mitigate any possibility of permanently locking the NFT in an unintended address. For more information on this, please refer to [EIP721](https://eips.ethereum.org/EIPS/eip-721).

For clarity, $$2^{255}$$ in its full numerical representation, is: `57896044618658097711785492504343953926634992332820282019728792003956564819968`

And this means that the very first PURSE NFT token id is: `57896044618658097711785492504343953926634992332820282019728792003956564819969`
