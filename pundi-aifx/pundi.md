# Pundi AIFX

`Pundi AIFX` is the name of the SDK application for Pundi AIFX omni layer. It is built using a modified pBFT consensus menchanism, with EVM support.

About the `Pundi AIFX`: The `Pundi AIFX` also known as a Hub is the first Core to be launched on the FunctionX Network. The role of a Core is to facilitate transfers between blockchains. If a blockchain connects to a Core via inter blockchain communication (IBC), it automatically gains access to all the other blockchains that are connected to that Core. The `Pundi AIFX` is a public Proof-of-Stake chain. It's native coin is the `PUNDIAI`.

* `fxcored`: The Pundi AIFX Daemon and command-line interface (CLI) runs a full-node of the `fxcored` application.

`Pundi AIFX` SDK uses the following modules:

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

Next, learn how to [install Pundi AIFX](installation.md).
