# Introduction

Much has been written about the dual nature of 404 tokens so this document will avoid repeating what is already available on the internet. The official release of PURSE’s upgrade from an ERC20 token to a dual natured token can be found in this [link](https://medium.com/purseland/purse-debuts-revolutionary-erc-404-standard-for-enhanced-digital-asset-liquidity-and-ownership-fa26cd7446b9).&#x20;

The purpose of this document is to describe in detail how PURSE404 differs from other 404 tokens, and to provide sufficient documentation for holders to understand how PURSE (404) works.

## Rationale

PURSE (404) was inspired by [Pandora’s ERC404 token](https://www.pandora.build/) and the code for their contract can be found in their Github [repository](https://github.com/Pandora-Labs-Org/erc404). The two most popular implementations of the dual-natured token are ERC404 and DN404. Between ERC404 and DN404, the development team picked the former as the inspiration for PURSE (404) for its easy code maintenance as a single contract is used to encapsulate the dual nature logic of the 404 token, as opposed to having it spread across two contracts.

When the team was first designing PURSE as a 404 token, the question the team sought to answer was: _is it possible to upgrade an existing ERC20 token to a 404 token?_&#x20;

In short, due to the design of ERC404 and DN404 contracts, the team determined it was not able to use them directly in an upgrade since these contracts are not designed for upgrading an existing ERC20 token in the first place. Using either ERC404 or DN404 contracts to implement a 404 token would ultimately require the team to deploy a brand new token altogether, which is what the team wants to avoid.

The solution was simple: _preserve the underlying ERC20 token and build the dual nature logic on top of the existing code._

The result of this endeavour is an upgraded version of PURSE that behaves like a typical 404 dual-natured token, but with a slight difference in the accounting of balances and the way NFTs are minted. Otherwise, PURSE would behave similarly to how other 404 tokens are expected to behave.

## High-level Architecture

At a very high level, the architecture of PURSE (404) can be illustrated as such:

<figure><img src="../.gitbook/assets/purse404ArchitectureSimple.png" alt=""><figcaption></figcaption></figure>

The underlying logic for PURSE as an ERC20 token remains unchanged from before, and logic to enable PURSE to function also as an ERC721 token was added down the inheritance chain to enable PURSE to behave as a dual-natured token.

## Changes to PURSE

The following is a list of the changes in PURSE token:

* Accounting of Balances
* Minting PURSE NFT(s)
* Transferring PURSE
* Maintaining PURSE NFT(s)
* NFTs in Queue
* Token IDs
