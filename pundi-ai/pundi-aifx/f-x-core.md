# f(x)Core

`f(x)Core` is the name of the Cosmos SDK application for Pundi AIFX omnichain.&#x20;

About the FunctionX Core: The FunctionX Core also known as a Hub is the first Core to be launched on the FunctionX Network. The role of a Core is to facilitate transfers between blockchains. If a blockchain connects to a Core via inter blockchain communication (IBC), it automatically gains access to all the other blockchains that are connected to that Core. The FunctionX Core is a public Proof-of-Stake chain. It's native coin is the FX.

* `fxcored`: The f(x)Core Daemon and command-line interface (CLI) runs a full-node of the `fxcored` application.

`f(x)Core` is built on the Cosmos SDK using the following modules:

* `x/auth`: Accounts and signatures.
* `x/bank`: Token transfers.
* `x/staking`: Staking logic.
* `x/mint`: Inflation logic.
* `x/distribution`: Fee distribution logic.
* `x/slashing`: Slashing logic.
* `x/gov`: Governance logic.
* `ibc-go/modules`: Inter-blockchain communication. Hosted in the `cosmos/ibc-go` repository.
* `x/params`: Handles app-level parameters.
* `x/freegrant`: Free grant logic.
* `x/authz`: Authorization logic.
* `x/freemarket`: Free market logic.
* `x/evm`: Enable Ethereum Virtual Machine compatibility.
* `x/erc20`: Enable ERC20 token standards.
* `x/migrate`: Allows migration of address to new address scheme.

Next, learn how to [install f(x)Core](installation.md).
