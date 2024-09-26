# Delegator CLI Guide

This document contains all the necessary information for delegators to interact with the PundiX through the Command-Line Interface (CLI).

It also contains instructions on how to manage accounts, restore accounts from the fundraiser and use a ledger nano device.

## Installing `pundixd`

`pundixd`: This is the command-line interface (CLI) to interact with a `pundixd` full-node.

{% hint style="info" %}
Please check that you have downloaded the latest stable release of `pundixd`

[**Install from source**](https://github.com/pundix/pundix)
{% endhint %}

`pundixd` can be interacted with via a terminal. To open the terminal, follow these steps:

* **Windows**: `Start` > `All Programs` > `Accessories` > `Command Prompt`
* **MacOS**: `Finder` > `Applications` > `Utilities` > `Terminal`
* **Linux**: `Ctrl` + `Alt` + `T`

## PundiX Accounts

At the core of every PundiX account, there is a seed, which takes the form of a 12 or 24-words mnemonic. From this mnemonic, it is possible to create multiple PundiX accounts, for example pairs of private key/public key. This is called an HD wallet (see [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) for more information on the HD wallet specification).

```
     Account 0                         Account 1                         Account 2

+------------------+              +------------------+               +------------------+
|                  |              |                  |               |                  |
|    Address 0     |              |    Address 1     |               |    Address 2     |
|        ^         |              |        ^         |               |        ^         |
|        |         |              |        |         |               |        |         |
|        |         |              |        |         |               |        |         |
|        |         |              |        |         |               |        |         |
|        +         |              |        +         |               |        +         |
|  Public key 0    |              |  Public key 1    |               |  Public key 2    |
|        ^         |              |        ^         |               |        ^         |
|        |         |              |        |         |               |        |         |
|        |         |              |        |         |               |        |         |
|        |         |              |        |         |               |        |         |
|        +         |              |        +         |               |        +         |
|  Private key 0   |              |  Private key 1   |               |  Private key 2   |
|        ^         |              |        ^         |               |        ^         |
+------------------+              +------------------+               +------------------+
         |                                 |                                  |
         |                                 |                                  |
         |                                 |                                  |
         +--------------------------------------------------------------------+
                                           |
                                           |
                                 +---------+---------+
                                 |                   |
                                 |  Mnemonic (Seed)  |
                                 |                   |
                                 +-------------------+
```

The funds stored in an account are controlled by the private key. This private key is generated from the mnemonic using a one-way function. If you lose the private key, you can retrieve it using the mnemonic. However, if you lose the mnemonic, you will lose access to all the derived private keys. Likewise, if someone gains access to your mnemonic, they gain access to all the associated accounts.

{% hint style="danger" %}
**DO NOT lose or share your 24-word mnemonic with anyone. To prevent theft or loss of funds, it is best to ensure that you keep multiple copies of your mnemonic, and store it in a safe, secure place that only you have access to. If someone has your mnemonic, they will be able to gain access to your private keys and control the accounts associated with them.**
{% endhint %}

The address is a public string with a human-readable prefix (for example `px1hs3tfedle32zzr5dh38gzzfn9ak2f4a9je4pf6`) that identifies your account. When someone wants to send you funds, they send it to your address. It is virtually computationally impossible to derive the private key from a public address.

### On Ledger Device

At the core of a ledger device, there is a mnemonic used to generate accounts on multiple blockchains (including the PundiX). When you first initialize your ledger device, you will create a new mnemonic. It is possible to import an existing mnemonic into a ledger device instead. Let us go ahead and see how you can import a mnemonic into your ledger device. For more on how to restore from a recovery phrase, refer [here](https://support.ledger.com/hc/en-us/articles/4404382560913-Restore-from-recovery-phrase?support=true).

{% hint style="info" %}
To import a mnemonic into a ledger, **it is preferable to use a brand new ledger device.** There can only be one mnemonic per ledger device. If you want to use a ledger that is already initialized with a seed, you can reset it by going into `Control Center`>`Settings`>`Security`>`Reset Device`. More on how to reset your ledger device can be found [here](https://support.ledger.com/hc/en-us/articles/360017582434-Reset-to-factory-settings-?docs=true). **Please note that this will wipe out the seed currently stored on the device. If you have not properly secured the associated mnemonic, you could lose your funds!!!**
{% endhint %}

The following steps need to be performed on an un-initialized ledger device:

1. Ensure ledger live is downloaded and installed.
2. Press the button next to the USB port until the Ledger logo appears to turn on the device.
3. Read the on-screen instructions. Press the right button to proceed or the left button to go back.
4. Press both simultaneously when Set up as new device is displayed.
5. **DO NOT** choose the "Config as a new device" option. Instead, choose "Restore Configuration"
6. Choose a PIN
7. Choose the 24 words option
8. Input each of the words in the correct order.

Your ledger is now correctly set up with your imported mnemonic! **DO NOT** lose this mnemonic! If your ledger is compromised, you can always restore a new device again using the same mnemonic.

Next, click [here](delegator-cli-guide.md#using-a-ledger-device) to learn how to generate an account.

### On a Computer

{% hint style="info" %}
**It is more secure to perform this action on an offline computer.**
{% endhint %}

To restore an account using a mnemonic and store the associated encrypted private key on a computer, use the following command:

```bash
# recover px address
pundixd keys add <px_key_name> --algo secp256k1 --coin-type 118 --index <index_number> --recover
```

* `<_key_name>` is the name of the account. It is a reference to the account number used to derive the key pair from the mnemonic. You will use this name to identify your account when you want to send a transaction.
* You can add the optional `--index` flag to specify the path (`0`, `1`, `2`, ...) you want to use to generate your account. By default, account `0` is generated.

The private key of account `0` will be saved in your operating system's credentials storage. Each time you want to send a transaction, you will need to unlock your system's credentials store. If you lose access to your credentials storage, you can always recover the private key with the mnemonic.

{% hint style="danger" %}
**You may not be prompted for a password each time you send a transaction since most operating systems unlock a user's credentials store upon login by default. If you want to change your credentials store security policies please refer to your operating system manual.**
{% endhint %}

## Creating an Account

To create an account, you just need to have `pundixd` installed. Before creating it, you need to know where you intend to store and interact with your private keys. The best options are to store them in a dedicated offline computer or a ledger device. Storing them on your regular online computer involves more risk, since anyone who infiltrates your computer through the internet could gain access to your private keys and steal your funds.

### Using a Ledger Device

{% hint style="danger" %}
**Only use Ledger devices that you bought brand new or that you know is NOT compromised.**
{% endhint %}

When you initialize your ledger, a 24-word mnemonic is generated and stored in the device. This mnemonic is compatible with PundiX and PundiX accounts can be derived from it. All you have to do is make your ledger compatible with `pundixd`. To do so, you need to go through the following steps:

1. Download the Ledger Live app [here](https://www.ledger.com/pages/ledger-live).
2. Connect your ledger via USB and update to the latest firmware
3. Go to the ledger live app store, and download the "PundiX" application (this can take a while). **You may have to enable `Dev Mode` in the `Settings` of Ledger Live to be able to download the "PundiX" application**.
4. Navigate to the PundiX app on your ledger device

Then, to create an account, run the following command:

```bash
# create px address
pundixd keys add <px_key_name> --algo secp256k1 --coin-type 118 --ledger --index <index_number>
```

{% hint style="info" %}
**This command will only work while the Ledger is plugged in and unlocked.**
{% endhint %}

* `<_key_name>` is the name of the account. It is a reference to the account number used to derive the key pair from the mnemonic. You will use this name to identify your account when you want to send a transaction.
* You can add the optional `--index` flag to specify the path (`0`, `1`, `2`, ...) you want to use to generate your account. By default, account `0` is generated. Just remember to take note of the accounts and index you have stored the keys in your ledger.

You can generate more accounts from the same mnemonic using the following command:

```bash
pundixd keys add brucebanner<0x_key_name> --algo secp256k1 --coin-type 118 --ledger --index 2
```

This command will prompt you to input a passphrase as well as your mnemonic. Change the account number to generate an account with a different index.

{% hint style="danger" %}
**DO NOT lose or share your 24 word mnemonics with anyone. To prevent theft or loss of funds, it is best to ensure that you keep multiple copies of your mnemonic, and store it in a secure place that only you know how to access. If someone is able to gain access to your mnemonic, they will be able to gain access to your private keys and control the accounts associated with them.**
{% endhint %}

After you have secured your mnemonic (triple check!), you can delete bash history to ensure no one can retrieve it:

```bash
history -c
rm ~/.bash_history
```

## Accessing the PundiX Network

In order to query the state and send transactions, you need a way to access the network. To do so, you can either run your own full-node, or connect to an available public node.

{% hint style="danger" %}
**DO NOT share your mnemonic (24 words) with anyone. The only person who should ever need to know it is you. No one from the PundiX team will ever send an email that asks for you to share any kind of account credentials or your mnemonics."**
{% endhint %}

### Running Your Own Full-Node

This is the most secure option, but comes with relatively high resource requirements and costs. In order to run your own full-node, you need good bandwidth and at least 500GB of disk space.

You will find the tutorial on how to install `pundixd` [here](../getting-started/installation-pundix.md), and the guide to run a full-node [here](../getting-started/setup-node/).

### Connecting to a Remote Full-Node

If you DO NOT want or cannot run your own node, you can connect to someone else's full-node. You should pick a full-node operator that you trust, because a malicious operator could return incorrect query results or censor your transactions. However, they will never be able to steal your funds, as your private keys are stored locally on your computer or ledger device. Possible options for full-node operators include validators, wallet providers or exchanges.

In order to connect to a full-node, you will need an address in the form of: `https://127.0.0.1:26657` (_This is a placeholder_). This address has to be provided by the full-node operator you choose to trust. You will use this address in the [following section](delegator-cli-guide.md#setting-up-pundixd).

## Setting Up `pundixd`

{% hint style="info" %}
Before setting up `pundixd`, ensure that you have found a way to [**access the PundiX network**](delegator-cli-guide.md#accessing-the-pundix-network)

Please check that you are always using the latest stable release of `pundixd.`
{% endhint %}

`pundixd` is the tool that enables you to interact with the node that runs on the PundiX network.

In order to set up `pundixd`, use the following command. It allows you to set a default value for each given flag. First, set up the address of the full-node you want to connect to:

```bash
pundixd config <config file name> <host>:<port>
# for example
pundixd config config.toml rpc.laddr https://127.0.0.1:26657
```

If you run your own full-node, just use `tcp://localhost:26657` as the address.

Then, let us set the default value of the `--trust-node` flag:

```bash
# Set to true if you trust the full-node you are connecting to, false otherwise
pundixd config trust-node false
```

Finally, let us set the `chain-id` of the blockchain we want to interact with (chain-id for testnet is payalebar):

```bash
pundixd config config.toml chain-id pundix
```

### Querying the State

{% hint style="info" %}
Before you can bond PUNDIX and withdraw rewards, you need to [**set up `pundixd`**](delegator-cli-guide.md#setting-up-pundixd)
{% endhint %}

`pundixd` lets you query all relevant information from the blockchain, like account balances, amount of bonded tokens, outstanding rewards, governance proposals and more. Next is a list of the most useful commands for delegators.

```bash
# query account balances and other account-related information
pundixd query account <yourAddress>

# query the list of validators
pundixd query staking validators

# query the information of a validator given their address (for example pxvaloper1hs3tfedle32zzr5dh38gzzfn9ak2f4a96gg7h6)
pundixd query staking validator <validatorAddress>

# query all delegations made from a delegator given their address (for example px1hs3tfedle32zzr5dh38gzzfn9ak2f4a9je4pf6)
pundixd query staking delegations <delegatorAddress>

# query a specific delegation made from a delegator (for example px1hs3tfedle32zzr5dh38gzzfn9ak2f4a9je4pf6) to a validator (for example pxvaloper1hs3tfedle32zzr5dh38gzzfn9ak2f4a96gg7h6) given their addresses
pundixd query staking delegation <delegatorAddress> <validatorAddress>

# query the rewards of a delegator given a delegator address (for example px1hs3tfedle32zzr5dh38gzzfn9ak2f4a9je4pf6)
pundixd query distribution rewards <delegatorAddress>

```

For more commands, just type:

```bash
pundixd query
```

For each command, you can use the `-h` or `--help` flag to get more information.

## Sending Transactions

### A Note on Gas and Fees

Transactions on the PundiX network need to include a transaction fee in order to be processed. This fee pays for the gas required to run the transaction. The formula is as such:

```
fees = ceil(gas * gas-prices)
```

The `gas` is dependent on the transaction. Different transactions require a different amount of `gas`. The amount of `gas` needed for a transaction is calculated when it is being processed, but there is a way to estimate it beforehand by using the `auto` value for the `gas` flag. Of course, this only fills in an estimate for the gas of that particular transaction. You can adjust this estimate with the flag `--gas-adjustment` (default `1.2`) if you want to be sure you have provided enough `gas` for the transaction. For the remainder of this tutorial, we will use a `--gas-adjustment` of `1.5`.

The `gas-prices` is the price of each unit of `gas`. Each validator sets a `min-gas-price` value, and will only include transactions that have a `gas-prices` greater than the `min-gas-price` they have set initially.

Transaction `fees` is the product of `gas` and `gas-prices`. As a user, you can either just fill in the `fees` required or you have to fill in both the `gas` and `gas-prices`. The higher the `gas-prices`/`fees`, the higher the chance that your transaction will be included in a block. For mainnet, the recommended `gas-prices` is `2000000000000`.

### Sending Tokens

Before you can bond PUNDIX and withdraw rewards, you need to [**set up `pundixd`**](delegator-cli-guide.md#setting-up-pundixd) and [**create an account**](delegator-cli-guide.md#creating-an-account)

{% hint style="danger" %}
**These commands need to run on an online computer. It is more secure to perform these commands using a Ledger device. For the offline procedure, click** [**here**](delegator-cli-guide.md#signing-transactions-from-an-offline-computer)**.**
{% endhint %}

```bash
# send a certain amount of tokens to an address
pundixd tx bank send <from_key_or_address> <to_address> <amount>
```

### Bonding PUNDIX and Withdrawing Rewards

{% hint style="info" %}
Before you can bond PUNDIX and withdraw rewards, you need to [**set up `pundixd`**](delegator-cli-guide.md#setting-up-pundixd) and [**create an account**](delegator-cli-guide.md#creating-an-account)

Before bonding PUNDIX, please read the [**delegator faq**](delegators-faq.md) to understand the risk and responsibilities involved with delegating.
{% endhint %}

{% hint style="danger" %}
**These commands need to run on an online computer. It is more secure to perform them commands using a ledger device. For the offline procedure, click** [**here**](delegator-cli-guide.md#signing-transactions-from-an-offline-computer)**.**
{% endhint %}

```bash
# bond a certain amount of PUNDIX to a given validator
pundixd tx staking delegate <validatorAddress> <amountToBond> --from <delegatorKeyName>
# for example
pundixd tx staking delegate pxvaloper1hs3tfedle32zzr5dh38gzzfn9ak2f4a96gg7h6 100 --from px1hs3tfedle32zzr5dh38gzzfn9ak2f4a9je4pf6

# redelegate a certain amount of PUNDIX from one validator to another
# can only be used if already bonded to a validator
# redelegation takes effect immediately, there is no waiting period to redelegate
# after a redelegation, no other redelegation can be made from the account for the next 3 weeks
pundixd tx staking redelegate <srcValidatorAddress> <destValidatorAddress> <amountToRedelegate>
# for example
pundixd tx staking redelegate pxvaloper1hs3tfedle32zzr5dh38gzzfn9ak2f4a96gg7h6 pxvaloper1hs3tfedle32zzr5dh38gzzfn9ak2f4a96gg7h6 100

# withdraw all rewards
pundixd tx distribution withdraw-all-rewards --from <delegatorKeyName> 
# for example
pundixd tx distribution withdraw-all-rewards --from px1hs3tfedle32zzr5dh38gzzfn9ak2f4a9je4pf6

# unbond a certain amount of PUNDIX from a given validator 
# you will have to wait 3 weeks before your PUNDIX is fully unbonded and transferrable 
pundixd tx staking unbond <validatorAddress> <amountToUnbond> --from <delegatorKeyName>
# for example
pundixd tx staking unbond pxvaloper1hs3tfedle32zzr5dh38gzzfn9ak2f4a96gg7h6 10 --from px1hs3tfedle32zzr5dh38gzzfn9ak2f4a9je4pf6
```

However,there is a limit to how frequent you can redelegate. For more information on [redelegation](delegators-faq.md#redelegation).

{% hint style="danger" %}
**If you are using a Ledger, you will be asked to confirm the transaction on the device before it is signed and broadcast to the network. Note that the command will only work while the Ledger is plugged in and unlocked.**
{% endhint %}

To confirm that your transaction went through, you can use the following queries:

```bash
# your balance should change after you bond PUNDIX or withdraw rewards
pundixd query account <account_px>
# for example
pundixd query account px1hs3tfedle32zzr5dh38gzzfn9ak2f4a9je4pf6

# you should have delegations after you bond PUNDIX
pundixd query staking delegations <delegatorAddress>
# for example
pundixd query staking delegations px1hs3tfedle32zzr5dh38gzzfn9ak2f4a9je4pf6

# this returns your tx if it has been included
# use the tx hash that was displayed when you created the tx
pundixd query tx <txHash>
# for example
pundixd query tx 9728A0C9D0E50AB2B1BF3DDFAE2D1E002A35B8A0E0420B140C6C4F7F3DD787D8
```

Double check with a block explorer if you interact with the network through a trusted full-node.

### Signing Transactions From an Offline Computer

If you DO NOT have a ledger device and want to interact with your private key on an offline computer, you can use the following procedure. First, generate an unsigned transaction on an **online computer** with the following command (example with a bonding transaction):

```bash
pundixd tx staking delegate <validatorAddress> <amountToBond> --from <delegatorAddress> \
 --generate-only > unsignedTX.json
# for example
pundixd tx staking delegate pxvaloper1y582mey4tt7rj4e7j7tz6q6fq6lxn6wwhnjd20 10PUNDIX --from px1sqcamj53swry6hlu3zqd2dkmt3c0je6wwqwhku \
 --generate-only > unsignedTX.json
```

In order to sign, you will also need the `chain-id`, `account-number` and `sequence`. The `chain-id` is a unique identifier for the blockchain on which you are submitting the transaction. The `account-number` is an identifier generated when your account first receives funds. The `sequence` number is used to keep track of the number of transactions you have sent and prevent replay attacks.

Get the chain-id from the genesis file, and the two other fields using the account query:

```bash
pundixd query account <yourAddress> --chain-id payalebar
# for example
pundixd query account px1sqcamj53swry6hlu3zqd2dkmt3c0je6wwqwhku --chain-id payalebar
```

Then, copy `unsignedTx.json` and transfer it (for example via USB) to the offline computer. If it is not done already, create an account on the offline computer. For additional security, you can double check the parameters of your transaction before signing it using the following command:

```bash
cat unsignedTx.json
```

Now, sign the transaction using the following command. You will need the `chain-id`, `sequence` and `account-number` obtained earlier:

```bash
pundixd tx sign unsignedTx.json --from <delegatorKeyName> --offline --chain-id payalebar --sequence <sequence> --account-number <account-number> > signedTx.json
# for example
pundixd tx sign unsignedTx.json --from px1sqcamj53swry6hlu3zqd2dkmt3c0je6wwqwhku --offline --chain-id payalebar --sequence 0 --account-number 11 > signedTx.json
```

Copy `signedTx.json` and transfer it back to the online computer. Finally, use the following command to broadcast the transaction:

```bash
pundixd tx broadcast signedTx.json
```
