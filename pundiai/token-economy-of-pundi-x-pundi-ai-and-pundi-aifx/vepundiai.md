# vePUNDIAI

Pundi AI uses two tokens to manage its utility and governance:

* `$PUNDIAI` — ERC-20 utility and governance token of the protocol for [Pundi AI Data Platform](../pundi-aidata/), [Pundi AI Marketplace](../pundi-ai-data-marketplace-soon.md), [Pundi AIFX Omni Layer](../pundi-aifx/) and [Pundi Fun AI Agent Launcher](../pundi-fun-ai-agent-launcher-proposal/).
* `$vePUNDIAI` — ERC-721 a token in the form of an NFT (non-fungible token) specifically for epoch voting in [Pundi Fun AI Agent Launcher](../pundi-fun-ai-agent-launcher-proposal/). Any `$PUNDIAI` holder that have delegated their tokens to a validator can vote-escrow their delegation proof and receive a `$vePUNDIAI` (also known as Lock or veNFT) in exchange.

The lock period (also known as vote-escrowed period, hence the _ve_ prefix) can be up to 4 years, following the linear relationship shown below:

* 100 `$PUNDIAI` locked for 4 years will become 100 `$vePUNDIAI`
* 100 `$PUNDI` locked for 1 year will become 25 `$vePUNDIAI`

The longer the vesting time, the higher the voting power (voting weight) of the underlying locked balance.

Additionally,  we will introduce Locks (veNFTs) that can be set into Auto-Max Lock, which are treated by the protocol as being locked for the maximum duration of 4 years, and their voting power does not decay. The Auto-Max Lock feature can be turned on and off for each Lock (veNFT).

Note: $FX is redenominated to $PUNDIAI in 2025, some articles might be using this two tokens interchangbly.\
