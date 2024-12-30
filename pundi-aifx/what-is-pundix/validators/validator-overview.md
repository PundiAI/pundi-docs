# Validator Overview

## Introduction

PundiX (Pundi X Chain) is built on Tendermint, which relies on a set of validators that are responsible for committing new blocks in the blockchain. These validators participate in the consensus protocol by broadcasting votes which contain cryptographic signatures signed by each validator's private key.

Validators can bond their own PUNDIX and have PUNDIX "delegated", or staked, with them by token holders. The PundiX chain will have 50 validators, but over time this will increase to 100 validators according to a predefined schedule. Validators are ranked according to the amount of PUNDIX staked with them — the top 50 validator candidates with the most stake will become active PundiX validators.

Validators and their delegators will earn block rewards and transaction fees through execution of the Tendermint consensus protocol. The Transaction fees will be paid in PUNDIX whilst the block rewards will be in both PUNDIX & PURSE. Note that validators can set the commission on the fees their delegators receive as an additional incentive.

If validators double sign, are frequently offline or DO NOT participate in governance, their PUNDIX staked(including PUNDIX of users that delegated to them) may be slashed. The penalty depends on the severity of the violation.

## Hardware

There are currently no existing appropriate cloud solution for validator key management. For this reason, validators must set up a physical operation secured with restricted access. A good starting place, for example, would be co-locating in secure data centers.

Validators should expect to equip their datacenter location with excess power, connectivity, and storage backups. Expect to have several excess networking boxes for fiber, firewall, switching and small servers with excess hard drives. Hardware can be on the low end of datacenter gear to start out with.

We expect network requirements to be low initially. The current testnet requires minimal resources. Then bandwidth, CPU and memory requirements will rise as the network grows. Large hard drives are recommended for storing years of blockchain history.

## Set Up a Website

Set up a dedicated validator's website and signal your intention of becoming a validator on our blockchain network. This is important since delegators will want to have more available information about the entity they are delegating their PUNDIX to.

## Seek Legal Advice

Seek legal advice if you intend to run a Validator.

## Community

Discuss more details on being a validator on our social media platforms:

* [Forum](https://forum.pundix.com/)
* [Telegram](https://t.me/pundix)
* [Twitter](https://twitter.com/PundiXLabs)
* [Reddit](https://www.reddit.com/r/PundiX/)
* [Gitbook](https://github.com/pundix)
