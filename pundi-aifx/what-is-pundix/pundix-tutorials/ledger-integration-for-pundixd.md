# Ledger Integration for pundixd

{% hint style="info" %}
<mark style="color:blue;">**DISCLAIMER**</mark>

Currently, the cosmos app on Ledger only supports the path **m/44/118**.

By default, the `pundixd keys add` command is defaulted to `--algo=eth_secp256k1 --coin-type=60` which is compatible with Ethereum accounts. If you want to use ledger to add a cosmos account, you must specify the flag `--algo=secp256k1 --coin-type=118`.

Without this flag, running the following command will return the following error:

`pundixd keys add mywallet --ledger --index 102 --keyring-backend file`

`Error: failed to generate ledger key: failed to recover pubkey: [APDU_CODE_DATA_INVALID] Referenced data reversibly blocked (invalidated): address rejected for path m/44'/60'/0'/0/102`
{% endhint %}

Using a hardware wallet to store your keys greatly improves the security of your crypto assets. The Ledger device acts as an enclave of the seed and private keys, and the process of signing transaction takes place within it. No private information ever leaves the Ledger device. The following is a short tutorial on using the Cosmos Ledger app with the PundiX CLI.

At the core of a Ledger device there is a mnemonic seed phrase that is used to generate private keys. This phrase is generated when you initialize your Ledger. The mnemonic is compatible with Cosmos and can be used to seed new accounts.

{% hint style="danger" %}
**DO NOT lose or share your 24 words with anyone. To prevent theft or loss of funds, it is best to keep multiple copies of your mnemonic stored in safe, secure places. If someone is able to gain access to your mnemonic, they will fully control the accounts associated with them.**
{% endhint %}

## Ledger and Cloud Setup

![Ledger and Cloud Configuration](https://github.com/PundiAI/pundiai-docs/blob/main/px-docs/.gitbook/assets/block.drawio.png)

Before you use a ledger to set up your validator, do make sure you understand this setup. You will need:

1. Your ledger which has the Cosmos app installed.
2. PundiX CLI installed on your local machine but this does not have to be a full-node or validator-node if you are remoting into a cloud server. Because your ledger is connected to your local machine, you will need PundiX CLI installed locally and we will be using this to send commands to the cloud server.
3. Your cloud server to be a full-node/validator node.
4. To run the [ssh port forwarding command](cloud-setup.md#connecting-your-localhost-to-the-cloud-instance-ssh-port-forwarding)
5. Two terminals opened, first one run the ssh port forwarding command.
6. The other one with pundixd opened locally and we will be using this terminal to run our commands.

## Install the Cosmos Ledger application

Installing the `Cosmos` application on your ledger device is required before you can use it with our PundiX CLI. To do so, you need to:

### Before you start

* Install [Ledger Live](https://shop.ledger.com/pages/ledger-live) on your machine.
* Using Ledger Live, [update your Ledger Nano S with the latest firmware](https://support.ledger.com/hc/en-us/articles/360002731113-Update-device-firmware)/[Ledger Nano X](https://support.ledger.com/hc/en-us/articles/360018784134-Set-up-your-Ledger-Nano-X?docs=true).

### Install the Cosmos (PUNDIX) app on your Ledger device

1. Open **Ledger Live** and navigate to the **Manager** tab.
2. Connect and unlock your Ledger **device**.
3. If asked, allow the manager on your device.
4. Search for the **Cosmos (PUNDIX)** app in the app catalog.
5. Click the **Install** button to install the app on your Ledger device.
   * Your Ledger device displays **Processing.**
   * Ledger Live displays **Installed.**
6. More information on how to set up your Ledger device can be found [here](https://support.ledger.com/hc/en-us/articles/360013713840-Cosmos-PUNDIX-?docs=true).

{% hint style="info" %}
To see the `Cosmos` application when you search for it, you might need to activate the `Developer Mode`, located in the Experimental features tab of the Ledger Live application.
{% endhint %}

## PundiX CLI + Ledger Nano

**You need to** [**install the Cosmos app**](ledger-integration-for-pundixd.md#install-the-cosmos-ledger-application) **on your Ledger Nano before moving on to this section**

The tool used to generate addresses and transactions on the PundiX network is `pundixd`. You will be using pundixd CLI commands for creating transactions and then using your Ledger to sign off before broadcasting the transaction to a specified node using the pundixd CLI.

### Install PundiX

{% hint style="info" %}
**You need to** [**install PundiX**](https://github.com/PundiAI/pundiai-docs/blob/main/px-docs/getting-started/installation-pundix.md) **before you proceed further**
{% endhint %}

### Add Ledger key

* Connect and unlock your Ledger device.
* Open the Cosmos app on your Ledger.
* Create an account in pundixd from your ledger key.

Be sure to change the `_name` parameter to be a meaningful name. The `--ledger` flag tells `pundixd` to use your Ledger to seed the account.

```bash
pundixd keys add <_name> --ledger --algo=secp256k1 --coin-type=118
# for example
pundixd keys add a1 --ledger --algo=secp256k1 --coin-type=118
```

Check the ledger and approve the address. Then, in terminal it returns:

```bash
{"name":"a1","type":"ledger","eip55_address":"0xA1D1b968B20A60366731EA94FEA6502D141AeF56","address":"px158gmj69jpfsrvee3a220afjs952p4m6kvm4axj","pubkey":"{\"@type\":\"/cosmos.crypto.secp256k1.PubKey\",\"key\":\"Auy/TgKCF/HJAkHnDaYv2DkKQNDhCwk1ZcMmf0HzOLaD\"}","algo":"eth_secp256k1"}
```

Cosmos uses [HD Wallets](https://www.ledger.com/academy/crypto/what-are-hierarchical-deterministic-hd-wallets). This means you can setup multiple accounts using the same Ledger seed. To create another account from your Ledger device, run the following, (changing the integer \<i> to some value >= 0 to choose the account for HD derivation):

```bash
pundixd keys add <secondKeyName> --ledger --algo=secp256k1 --coin-type=118 --index <i>
# for example
pundixd keys add a2 --ledger --algo=secp256k1 --coin-type=118 --index 2
```

Check the ledger and approve the address. Then, in terminal it returns:

```bash
{"name":"a2","type":"ledger","eip55_address":"0x66a92b3d0c101a8BE31fFb72679F0D6E2276f79A","address":"px1v65jk0gvzqdghcclldex08cddc38dau63mfk23","pubkey":"{\"@type\":\"/cosmos.crypto.secp256k1.PubKey\",\"key\":\"A27tmBBfshR4B0LaTKfwXy4fFfLfWeQIxPVq3I+KyewU\"}","algo":"eth_secp256k1"}
```

Additionally and importantly, if you wish to have an added layer of protection on your keys, you may add the `--keyring-backend` flag and specify the file name. Setting your key up this way will ensure another layer of protection for signing any transactions.

```bash
# \--keyring-backend string Select keyring's backend (os|file|test) (default "test")
pundixd keys add <NewKeyName> \
  --ledger \
  --index <i> \
  --keyring-backend <backend>

# for example:
pundixd keys add a3 \
  --ledger \
  --index 3 \
  --coin-type 118 \
  --keyring-backend file
```

You will be prompted for a keyring passphrase (password must be at least 8 characters) :

```bash
Enter keyring passphrase:
Re-enter keyring passphrase:
{"name":"a3","type":"ledger","eip55_address":"0x5ebC323260dCF8DA222C0ef167bFF1e6f3F7585e","address":"px1t67ryvnqmnud5g3vpmck00l3umelwkz7yv6gg5","pubkey":"{\"@type\":\"/cosmos.crypto.secp256k1.PubKey\",\"key\":\"AtGq1hsem5bGINWNiHsmvQybMfCMMb2XqWBgLqY/mLr2\"}","algo":"eth_secp256k1"}
```

In the future, whenever you use this account to sign off on a transaction, you will have to add the `--keyring-backend <file_name>` flag and enter the keyring passphrase.

{% hint style="info" %}
Save a backup of your keyring passphrase in a secure place. Losing your keyring passphrase will result in the lost of all your funds created using the keyring passphrase❗

Also to access your keys in the keyring file DO NOT forget to add the --keyring flag
{% endhint %}

### Confirm your address

Run this command to display your address on your Ledger device. Use the `_name` you gave your ledger key. The `-d` flag is supported in version `1.5.0` and higher.

```bash
pundixd keys show <_name> -d
# for example
pundixd keys show a1 -d
```

Confirm that the address displayed on the device matches the address displayed on the terminal.

### Connect to a full node

Next, you need to configure pundixd with the URL of a PundiX full node and the appropriate `chain_id`. In this example we connect to the public load balanced full node operated by Function X on the `payalebar` chain. But you can point your `pundixd` to any `PundiX` full node. Be sure that the `chain-id` is set to the same chain as the full node.

```bash
# configuring to a full node
pundixd config <config file name> <host>:<port>
# for example
pundixd config config.toml rpc.laddr https://127.0.0.1:26657

# configuring the chain-id
pundixd config chain-id <value>
# for example
pundixd config chain-id payalebar
```

Test your connection with a query such as:

```bash
pundixd query staking validators
```

**To run your own full node locally read more** [**here**](https://github.com/PundiAI/pundiai-docs/blob/main/px-docs/getting-started/setup-node/README.md)**.**

### Sign a transaction

You are now ready to start signing and sending transactions. Send a transaction with pundixd using the `tx bank send` command.

```bash
# show all available options
pundixd tx bank send --help
```

{% hint style="info" %}
Be sure to unlock your device with the PIN and open the Cosmos app before trying to run these commands

Use the `_name` you set for your Ledger key and PundiX will connect with the Cosmos Ledger app to then sign your transaction.
{% endhint %}

```bash
pundixd tx bank send <_name> <destinationAddress> <amount> <denomination>
```

Assuming you added the `--keyring-backend <file>` flag earlier, an example of a transaction would look like the following:

```bash
pundixd tx bank send a1 px1v65jk0gvzqdghcclldex08cddc38dau63mfk23 10PUNDIX --fees="1PUNDIX" --gas-prices="" \
  --keyring-backend file
```

{% hint style="info" %}
If you are not running a node, be sure to add in the `--node` flag to specify which node you would like to broadcast your transaction.
{% endhint %}

You will be prompted to enter the passphrase for the `--keyring-backend` flag:

```bash
Enter keyring passphrase:

Default sign-mode 'direct' not supported by Ledger, using sign-mode 'amino-json'.
gas estimate: 123878
{"body":{"messages":[{"@type":"/cosmos.bank.v1beta1.MsgSend","from_address":"px1t67ryvnqmnud5g3vpmck00l3umelwkz7yv6gg5","to_address":"px1v65jk0gvzqdghcclldex08cddc38dau63mfk23","amount":[{"denom":"ibc/55367B7B6572631B78A93C66EF9FDFCE87CDE372CC4ED7848DA78C1EB1DCDD78","amount":"10000000000000000000"}]}],"memo":"","timeout_height":"0","extension_options":[],"non_critical_extension_options":[]},"auth_info":{"signer_infos":[],"fee":{"amount":[{"denom":"ibc/55367B7B6572631B78A93C66EF9FDFCE87CDE372CC4ED7848DA78C1EB1DCDD78","amount":"1000000000000000000"}],"gas_limit":"123878","payer":"","granter":""}},"signatures":[]}

confirm transaction before signing and broadcasting [y/N]:
```

After inputting `y`, you will be prompted to review and approve the transaction on your Ledger device.`View Transaction` on your Ledger, be sure to inspect the transaction JSON displayed on the screen. You can scroll through each field and each message. You may refer [here](ledger-integration-for-pundixd.md#the-pundix-standard-transaction) to read more about the data fields of a standard transaction object. When prompted with `confirm transaction before signing`, Answer `y`.

### Receive funds

To receive funds to the `pundix` account on your Ledger device, retrieve the address for your Ledger account (the ones with `TYPE ledger`) with this command:

```bash
pundixd keys list
```

### Further documentation

Not sure what `pundixd` can do? Simply run the command without arguments to output documentation for the commands in supports.

{% hint style="info" %}
The `pundixd` help commands are nested. So `$ pundixd` will output docs for the top level commands (status, config, query, and tx). You can access documentation for sub commands with further help commands.
{% endhint %}

For example, to print the `query` commands:

```bash
pundixd query --help
# to print the `tx` (transaction) commands:
pundixd tx --help
```

## The PundiX Standard Transaction

Transactions in pundix embed the [Standard Transaction type](https://godoc.org/github.com/cosmos/cosmos-sdk/x/auth#StdTx) from the Cosmos SDK. The Ledger device displays a serialized JSON representation of this object for you to review before signing the transaction. Here are the fields and what they mean:

* `chain-id`: The chain to which you are broadcasting the tx, such as the `pundix` payalebar or `pundix` mainnet.
* `account_number`: The global id of the sending account assigned when the account receives funds for the first time.
* `sequence`: The nonce for this account, incremented with each transaction.
* `fee`: JSON object describing the transaction fee, its gas amount and coin denomination
* `memo`: optional text field used in various ways to tag transactions.
* `msgs_<index>/<field>`: The array of messages included in the transaction. Double click to drill down into nested fields of the JSON.
