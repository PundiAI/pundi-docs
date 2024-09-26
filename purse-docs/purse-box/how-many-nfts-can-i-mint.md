# How many NFTs can I mint?

Your `inactiveBalance` shows specifically how many PURSE tokens you have that are not NFTs. This would be akin to your balance of PURSE tokens that are available for conversion into NFTs.&#x20;

Once you mint one PURSE404 NFT, 1,000,000 PURSE will be deducted from your `inactiveBalance`, but your total balance remains the same. This is because in the contract, it accounts one NFT to be equivalent to 1,000,000 PURSE.

For example:

* Bob starts with 10,000,000 PURSE tokens. Before minting any PURSE BOX NFTs, his `inactiveBalance` is 10,000,000, and his total balance is also 10,000,000.
* Bob decides to mint 1 PURSE BOX NFT, so 1,000,000 PURSE tokens from his `inactiveBalance` will be deducted and converted to 1 PURSE BOX NFT.
* Bob's `inactiveBalance` is now 9,000,000, and he has 1 PURSE BOX NFT. But his total balance remains at 10,000,000.

### How to check inactive balance?

1. Visit the contract on [Etherscan](https://etherscan.io/address/0x95987b0cdC7F65d989A30B3B7132a38388c548Eb)
2. Go to `Contract` -> `Read as Proxy`

<figure><img src="https://lh7-us.googleusercontent.com/FBUHhE9t1lKFwWEHkXpCWNWw0VOiu5h8L37PqjpYf_7WA499ni_O-mlwoP7dUHlCS76UC0thQ-vlluVbhFLdggIRpzv2trps0zG56aMRbdC1-d4JeJEJcl_wAtrNYSeFuzD12aQ0Y_2aXXx1vQcIJe0" alt="" width="563"><figcaption></figcaption></figure>

3. Go to `22. inactiveBalance` and enter your `0x` address

<figure><img src="https://lh7-us.googleusercontent.com/wMtEribMA6qQ-lRrfeEE-UJK6ISmuVW0GW0aZifZeAek95oE_j6PHL-jyczg9Apou80mGRlISA1TR1ZKXp3C3CFfTVPWJ8zA6dtlHEP9KgzmDq69v9L5LX1TbSD_v8A_G7R9hqGTkB6ZVzwpV55Si48" alt=""><figcaption></figcaption></figure>
