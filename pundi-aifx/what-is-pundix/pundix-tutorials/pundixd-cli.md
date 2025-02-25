# Pundi X CLI Guide

## pundixd

`pundixd` is the tool that enables you to interact with the node that runs on the `pundixd`. In order to install it, follow the [installation procedure](../getting-started/installation-pundix.md).

### Setting Up pundixd

The main command used to set up `pundixd` is the following:

```bash
pundixd config <key> [value] [flags]
```

This command will change parameters in `client.toml`. It also allows you to set a default value for each given flag.

First, set up the address of the full-node you want to connect to:

```bash
pundixd config <file_name> <param> <host>:<port>
# for example
pundixd config config.toml rpc.laddr https://px-json.pundix.com:26657
# if you run your own full-node, just use tcp://localhost:26657 as the address.
pundixd config config.toml rpc.laddr tcp://localhost:26657
```

Then, let us set the default value of the `--trust-node` flag:

```bash
# set to true if you trust the full-node you are connecting to, false otherwise
pundixd config config.toml trust-node true
```

Finally, let us set the `chain-id` of the blockchain we want to interact with:

```bash
# interact with testnet
pundixd config chain-id payalebar

# interact with mainnet
pundixd config chain-id pundix
```

### Main Structure of pundixd Commands

The `pundixd` help commands are nested. So, in terminal, `pundixd` will output docs for the top level commands (status, config, query, and tx). You can access documentation for sub commands with further help commands.

The very first command to generate a list of available commands:

```bash
pundixd
```

Return:

```bash
PundiX Chain App

Usage:
  pundixd [command]

Available Commands:
  add-genesis-account Add a genesis account to genesis.json
  collect-gentxs      Collect genesis txs and output a genesis.json file
  config              Create or query an application CLI configuration file
  data                modify data or query data in database
  debug               Tool for helping with debugging your application
  export              Export state to JSON
  gentx               Generate a genesis tx carrying a self delegation
  help                Help about any command
  init                Initialize private validator, p2p, genesis, and application configuration files
  keys                Manage your application\'s keys
  query               Querying subcommands
  rollback            rollback cosmos-sdk and tendermint state by one height
  rosetta             spin up a rosetta server
  start               Run the full node
  status              Query remote node for status
  tendermint          Tendermint subcommands
  tx                  Transactions subcommands
  validate-genesis    validates the genesis file at the default location or at the location passed as an arg
  version             Print the application binary version information

Flags:
  -h, --help                 help for pundixd
      --home string          directory for config and data (default "/Users/pundix006/.pundix")
      --log_filter strings   The logging filter can discard custom log type (ABCIQuery) (default "")
      --log_format string    The logging format (json|plain) (default "plain")
      --log_level string     The logging level (trace|debug|info|warn|error|fatal|panic) (default "info")
      --trace                print out full stack trace on errors

Use "pundixd [command] --help" for more information about a command.
```

The return value will include:

* a header which explains what the command is, for example `PundiX Chain App`
* the usage for example `pundixd [command]` where you will need to input pundixd and a follow up command like `pundixd tx`
* all available commands
* and all flags which might be needed for commands

We will be going through a common command along with the various sub commands and flags. Selecting the `tx` command:

```bash
pundixd tx
```

Return:

```bash
Transactions subcommands

Usage:
  pundixd tx [flags]
  pundixd tx [command]

Available Commands:
  authz               Authorization transactions subcommands
  bank                Bank transaction subcommands
  broadcast           Broadcast transactions generated offline
  crisis              Crisis transactions subcommands
  decode              Decode a binary encoded transaction string
  distribution        Distribution transactions subcommands
  encode              Encode transactions generated offline
  erc20               ERC20 transaction subcommands
...

Additional help topics:
  pundixd tx upgrade     Upgrade transaction subcommands
  
Use "pundixd tx [command] --help" for more information about a command.
```

You may either choose to insert a `flag` or a `command` after `pundixd tx`:

```bash
pundixd tx --help
```

### Example: tx gov

If you have already start pundixd, you can use the `gov` command to interact with the governance module.

```bash
pundixd tx gov
```

It will return:

```bash
Governance transactions subcommands

Usage:
  pundixd tx gov [flags]
  pundixd tx gov [command]

Available Commands:
  deposit         Deposit tokens for an active proposal
  submit-proposal Submit a proposal along with an initial deposit
  vote            Vote for an active proposal, options: yes/no/no_with_veto/abstain
...

Use "pundixd tx gov [command] --help" for more information about a command.
```

Continuing:

```bash
pundixd tx gov submit-proposal
```

Return:

```bash
Error: invalid message: can\'t proto marshal <nil>
Usage:
  pundixd tx gov submit-proposal [flags]
  pundixd tx gov submit-proposal [command]

Available Commands:
  cancel-software-upgrade Cancel the current software upgrade proposal
  community-pool-spend    Submit a community pool spend proposal
  param-change            Submit a parameter change proposal
  register-coin           Submit a register coin proposal
  register-erc20          Submit a proposal to register an ERC20 token
  software-upgrade        Submit a software upgrade proposal
  toggle-token-conversion Submit a toggle token conversion proposal
  update-denom-alias      Submit a update denom alias proposal
...

Use "pundixd tx gov submit-proposal [command] --help" for more information about a command.
```

Now if you use the `--help` flag:

```bash
pundixd tx gov submit-proposal --help
```

Return:

```bash
Submit a proposal along with an initial deposit.
Proposal title, description, type and deposit can be given directly or through a proposal JSON file.
```

For example:

```bash
pundixd tx gov submit-proposal --proposal="path/to/proposal.json" --from mykey
```

Where proposal.json contains:

```bash
{
  "title": "Test Proposal",
  "description": "My awesome proposal",
  "type": "Text",
  "deposit": "10PUNDIX"
}
```

Which is equivalent to:

```bash
pundixd tx gov submit-proposal --title="Test Proposal" --description="My awesome proposal" --type="Text" --deposit="10PUNDIX" --from mykey

Usage:
  pundixd tx gov submit-proposal [flags]
  pundixd tx gov submit-proposal [command]
...

Use "pundixd tx gov submit-proposal [command] --help" for more information about a command.
```

### Denom

In general case, users can leave fees and gas price details as default values without input any flags.

Otherwise, a transaction fee must be set! So do remember to add `--fees` and `--gas-prices` in your command. If you did not input the `--gas-prices` flag, you will be prompted to add it in your command since you changed all gas cost into fees. This will help people set all fees in one flag.

For example transaction is `0.5PUNDIX` which after multiplying by `10^18` is `500000000000000000ibc/55367b7b6572631b78a93c66ef9fdfce87cde372cc4ed7848da78c1eb1dcdd78`. For the mainnet denom, we will use `PUNDIX` in general case. For the number, the `200000000000000000` means the result of multiplying the default value of `gas-prices` and `gas-limit`. The default value of `--gas-prices` is `2000000000000` and `gas-limit` is `100000`. `--gas-adjustment=1.2` means that there will be a 20% buffer added to the automatically assessed gas amount.

Beseides, if users want to set gas price mannually, they need to care `gas-prices`, `gas-limit` and `gas-adjustment`. A more universal command is `--gas=auto`. `--gas=auto` automatically assesses the gas used for that transaction. This depends on the transaction itself and also the state of the blockchain. For more details on gas, kindly refer to the section on gas below.

```bash
pundixd tx gov submit-proposal --title="gov proposal" --description="try to submit proposal" --type="Text" --deposit="200PUNDIX" --from=admin
```

Return:

```bash
{"body":{"messages":[{"@type":"/cosmos.gov.v1beta1.MsgSubmitProposal","content":{"@type":"/cosmos.gov.v1beta1.TextProposal","title":"BLINDGOTCHI","description":"CLAUDIOXBARROS’s pet"},"initial_deposit":[{"denom":"PUNDIX","amount":"200"}],"proposer":"px124n6hpxkkn3r9j3tzwzhax2rd5s3crwq7p94fd"}],"memo":"","timeout_height":"0","extension_options":[],"non_critical_extension_options":[]},"auth_info":{"signer_infos":[],"fee":{"amount":[{"denom":"PUNDIX","amount":"1.2"}],"gas_limit":"200000","payer":"","granter":""}},"signatures":[]}

confirm transaction before signing and broadcasting [y/N]:
```

After inputting `y`:

```bash
{"height":"1632790","txhash":"C25C5A00D7EEEE5E3B7B0557320AE7F1D33992C8ADBFB2539C1F369F2B494725","codespace":"","code":0,"data":"0A160A0F7375626D69745F70726F706F73616C120308A001","raw_log":"[{\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"submit_proposal\"},{\"key\":\"sender\",\"value\":\"px124n6hpxkkn3r9j3tzwzhax2rd5s3crwq7p94fd\"},{\"key\":\"module\",\"value\":\"governance\"},{\"key\":\"sender\",\"value\":\"px124n6hpxkkn3r9j3tzwzhax2rd5s3crwq7p94fd\"}]},{\"type\":\"proposal_deposit\",\"attributes\":[{\"key\":\"amount\",\"value\":\"200PUNDIX\"},{\"key\":\"proposal_id\",\"value\":\"160\"}]},{\"type\":\"submit_proposal\",\"attributes\":[{\"key\":\"proposal_id\",\"value\":\"160\"},{\"key\":\"proposal_type\",\"value\":\"Text\"}]},{\"type\":\"transfer\",\"attributes\":[{\"key\":\"recipient\",\"value\":\"px10d07y265gmmuvt4z0w9aw880jnsr700jqjzsmz\"},{\"key\":\"sender\",\"value\":\"px124n6hpxkkn3r9j3tzwzhax2rd5s3crwq7p94fd\"},{\"key\":\"amount\",\"value\":\"200PUNDIX\"}]}]}]","logs":[{"msg_index":0,"log":"","events":[{"type":"message","attributes":[{"key":"action","value":"submit_proposal"},{"key":"sender","value":"px124n6hpxkkn3r9j3tzwzhax2rd5s3crwq7p94fd"},{"key":"module","value":"governance"},{"key":"sender","value":"px124n6hpxkkn3r9j3tzwzhax2rd5s3crwq7p94fd"}]},{"type":"proposal_deposit","attributes":[{"key":"amount","value":"200PUNDIX"},{"key":"proposal_id","value":"160"}]},{"type":"submit_proposal","attributes":[{"key":"proposal_id","value":"160"},{"key":"proposal_type","value":"Text"}]},{"type":"transfer","attributes":[{"key":"recipient","value":"px10d07y265gmmuvt4z0w9aw880jnsr700jqjzsmz"},{"key":"sender","value":"px124n6hpxkkn3r9j3tzwzhax2rd5s3crwq7p94fd"},{"key":"amount","value":"200PUNDIX"}]}]}],"info":"","gas_wanted":"200000","gas_used":"91282","tx":null,"timestamp":""}
```

## Keys

### Key Types

There are three types of key representations that are used:

* `px`:
  * Derived from account keys generated by `pundixd keys add`
  * Used to receive funds
  * Addresses that only have a preceding `px` are wallet addresses
  * For example: `px15h6vd5f0wqps26zjlwrc6chah08ryu4hzzdwhc`
* `pxvaloper`:
  * Used to associate a validator to it's operator
  * Used to invoke staking commands
  * Addresses preceding with `pxvaloper`are validator consensus address
  * For example: `pxvaloper1carzvgq3e6y3z5kz5y6gxp3wpy3qdrv928vyah`

### Generate Keys

You'll need an account with a private and public key pair (a.k.a. `sk`,`pk` respectively) to be able to receive funds, send txs, bond tx, etc.

To generate an old **secp256k1** key, follow this [guide](https://github.com/PundiAI/pundiai-docs/blob/main/px-docs/pundix-tutorials/account-migration-guide-cli.md#2-prepare-the-0x-prefix-address-account-ethereum-format-address). New **eth\_secp256k1** will be the default key generation scheme when PundiX becomes EVM compatible.

To generate a new **eth\_secp256k1** key by default:

```bash
pundixd keys add <account_name>
# for example
pundixd keys add a1
```

It returns some information about the key and the address it was generated for:

```bash
{"name":"a1","type":"local","eip55_address":"0x8b0591eb1ada09124e87Aca7Fe79A4DAa037c7d7","address":"px13vzer6c6mgy3yn584jnlu7dym2sr037h9vjpt5","pubkey":"{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PubKey\",\"key\":\"Az5CsJXBh/Jkid6VNLii7nn05MucDkLmxLY0mYQ+N6KP\"}","mnemonic":"abuse wasp life antenna render fury flip mention zero scorpion congress behave jacket resemble tail bean verify embark drive spread practice museum candy potato","algo":"eth_secp256k1"}
```

The output of the above command will contain a **mnemonic** like \`\`. It is recommended to save the **mnemonic** in a safe place so that in case you forget the password of the operating system's credentials store, you could eventually regenerate the key from the **mnemonic** with the following command:

```bash
pundixd keys add <account_name> --recover
# for example
pundixd keys add a1 --recover
```

It require to input `y`:

```bash
override the existing name a1 [y/N]: y
```

The user need to input mnemonic:

```bash
> Enter your bip39 mnemonic
abuse wasp life antenna render fury flip mention zero scorpion congress behave jacket resemble tail bean verify embark drive spread practice museum candy potato
```

Then all the account information shows:

```bash
{"name":"a1","type":"local","eip55_address":"0x8b0591eb1ada09124e87Aca7Fe79A4DAa037c7d7","address":"px13vzer6c6mgy3yn584jnlu7dym2sr037h9vjpt5","pubkey":"{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PubKey\",\"key\":\"Az5CsJXBh/Jkid6VNLii7nn05MucDkLmxLY0mYQ+N6KP\"}","algo":"eth_secp256k1"}
```

If you check your private keys in any time, you'll now see `<account_name>`:

```bash
pundixd keys show <account_name>
# for example
pundixd keys show a1
```

Additionally and importantly, if you wish to have an added layer of protection on your keys, you may add the `--keyring-backend` flag and specify the file name. Setting your key up this way will ensure another layer of protection for signing any transactions.

```bash
# \--keyring-backend string Select keyring's backend (os|file|test) (default "file")
pundixd keys add <secondKeyName> \
  --ledger \
  --index <i> \
  --keyring-backend <file_name>
# for example
pundixd keys add a4 \
  --index 4 \
  --keyring-backend file
```

you will be prompted for a keyring passphrase (password must be at least 8 characters) :

```bash
Enter keyring passphrase:
# for example
# the input words will not show and the user need to reinput after first time
Enter keyring passphrase: a1password
Re-enter keyring passphrase: a1password
{"name":"a4","type":"local","eip55_address":"0x020064394AA8Ee00b51d285D4BFE740c9DE047aE","address":"px1qgqxgw224rhqpdga9pw5hln5pjw7q3awj5zhek","pubkey":"{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PubKey\",\"key\":\"Ai+/XyVxQQbwwpXQpukA3RYR51ts+IClxHhAPdRNoVWT\"}","mnemonic":"modify portion diamond suggest unhappy what differ youth empty suffer movie vivid jewel session visit friend autumn common ridge tennis plug voyage conduct wrap","algo":"eth_secp256k1"}
```

In the future, whenever you use this account to sign off on a transaction, you will have to add the `--keyring-backend <file_name>` flag and enter the keyring passphrase.

{% hint style="info" %}
Save a backup of your keyring passphrase in a secure place. Losing your keyring passphrase will result in the lost of all your funds created using the keyring passphrase❗

Also to access your keys in the keyring file DO NOT forget to add the `--keyring` flag.
{% endhint %}

View the validator operator's address via:

```bash
pundixd keys show <account_name> --bech=val
# for example
pundixd keys show a1 --bech=val
```

You can see all your available keys by typing:

```bash
pundixd keys list
```

**Note that this return with account address is quite different with the validator operator's address.**

View the validator pubkey for your node by typing:

```bash
pundixd tendermint show-validator
```

{% hint style="danger" %}
**This is the Tendermint signing key, NOT the operator key you will use in delegation transactions.**

**Warning: We strongly recommend NOT using the same passphrase for multiple keys. The PundiX team will not be responsible for the loss of funds.**
{% endhint %}

### Generate Multisig Public Keys

You can generate and print a multisig public key by typing:

```bash
# You need to generate multiple keys before, such as a1, a2 and a3.
pundixd keys add --multisig=name1,name2,name3[...] --multisig-threshold=K new_key_name
# for example
# pundixd keys add a2
# pundixd keys add a3
pundixd keys add --multisig=a1,a2,a3 --multisig-threshold=2 bk
```

{% hint style="info" %}
For multisig accounts, if you were to create any transaction, for example `--from=<multisig_account>`.

The `<multisig_account>` needs to be the wallet address ie `px123l3kjltjwlfgjslfg....` not the account name.

Only for those non-multisig accounts can you use the name of the account ie `--from=sheldoncooper`.
{% endhint %}

`K` is the minimum number of private keys that must have signed the transactions that carry the public key's address as signer.

The `--multisig` flag must contain the name of public keys that will be combined into a public key that will be generated and stored as `new_key_name` in the local database. All names supplied through `--multisig` must already exist in the local database. Unless the flag `--nosort` is set, the order in which the keys are supplied on the command line does not matter, for example the following commands generate two identical keys:

```bash
pundixd keys add --multisig=a1,a2,a3 --multisig-threshold=2 bk1
pundixd keys add --multisig=a3,a1,a2 --multisig-threshold=2 bk2
```

Multisig addresses can also be generated on-the-fly and printed through the which command:

```bash
# The default generated key name will be `multi`
pundixd keys show --multisig-threshold K name1 name2 name3 [...]
# for example
pundixd keys show --multisig-threshold 2 a1 a2 a3 
```

The above command will generate a multisig address and print it to the console. But this time the order of the multisig names does matter. For example the command line with `a1 a2 a3` and `a2 a1 a3` will generate two different multisig addresses. With same `--multisig-threshold=2`, the `bk` key is the same as the order `a3 a1 a2` generated.

For more information regarding how to generate, sign and broadcast transactions with a multi signature account see [Multisig Transactions](https://github.com/PundiAI/pundiai-docs/blob/main/px-docs/pundix-tutorials/pundixd-cli-commands.md#multisig-transactions).

### Migrate Keys From Legacy On-Disk Keybase To OS Built-in Secret Store

Older versions of `pundixd` used store keys in the user's home directory. If you are migrating from an old version of `pundixd` you will need to migrate your old keys into your operating system's credentials storage by running the following command:

```bash
pundixd keys migrate <old_home_dir> [flags]
```

The command will prompt for each passphrase. If a passphrase is incorrect, it will skip the respective key. The detail information of keys migration is [here](./)

## Fees & Gas

Each transaction may either use the `--fees` or `--gas` flags, but not both.

Validator's have a minimum gas price (multi-denom) configuration and they use this value when determining if they should include the transaction in a block during `CheckTx`, where `gasPrices >= minGasPrices`. Note, your transaction must use fees that are greater than or equal to **any** of the denominations the validator requires.

**Note**: With such a mechanism in place, validators may start to prioritize txs by `gas-prices` in the mempool, so providing higher fees or gas prices may yield higher tx priority.

```bash
# using the --fees flag must have an empty --gas-prices flag together
pundixd tx bank send <from_key_or_address> <to_address> <amount> --fees="0.5PUNDIX" --gas-prices=""
# for example, tx from admin to a2 adress with 0.5PUNDIX fees
pundixd tx bank send admin px1ejstvlp4294h7ncnxgl8rqatsaj4kf2s4lj3y2 100PUNDIX --fees="0.5PUNDIX" --gas-prices=""

# using the gas flag default value
pundixd tx bank send <from_key_or_address> <to_address> <amount> 
# for example, tx from admin to a2 adress 
pundixd tx bank send admin px1ejstvlp4294h7ncnxgl8rqatsaj4kf2s4lj3y2 300PUNDIX
```

To query the gas price of your current node:

```
pundixd query gas-prices
```

{% hint style="info" %}
You may want to cap the maximum gas that can be consumed by the transaction via the `--gas` flag. If you pass `--gas="auto"`, the gas supply will be automatically estimated before executing the transaction.

Gas estimate might be inaccurate as state changes could occur in between the end of the simulation and the actual execution of a transaction, thus an adjustment is applied on top of the original estimate in order to ensure the transaction is broadcasted successfully. The adjustment can be controlled via the `--gas-adjustment` flag. The default value is `1.2`.
{% endhint %}

## Account

### Get Testnet Tokens

On a testnet, getting tokens is usually done via a faucet. You may refer to this [link](testnet-faucet.md).

### Query Account Balance

After receiving tokens to your address, you can view your account's balance by typing:

```bash
pundixd q bank balances <account_px>
# for example
pundixd q bank balances px1kyn5tncnnpd8am28zqs3xhllkk5lx9wp4ce6ty
```

If the generated account has no tokens. It shows:

```bash
{"balances":[],"pagination":{"next_key":null,"total":"0"}}
```

If the account had no transaction history, the address will not be detected on the chain.

```bash
pundixd query auth account px1hfwtzv5twhulwhcf9aa4y3kr6hmhfu866zjjfa
```

It shows:

```bash
Error: rpc error: code = NotFound desc = rpc error: code = NotFound desc = account px1hfwtzv5twhulwhcf9aa4y3kr6hmhfu866zjjfa not found: key not found
Usage:
  pundixd query auth account [address] [flags]
...
```

{% hint style="info" %}
This can also happen if you fund the account before your node has fully synced with the chain. These are both normal.
{% endhint %}

### Send Tokens

The following command could be used to send coins from one account to another:

```bash
 pundixd tx bank send <from_key_or_address> <to_address> <amount>
```

{% hint style="info" %}
The `amount` argument accepts the format `<value|coin_name>`, for example `10PUNDIX` which is equivalent to `10000000000000000000ibc/55367B7B6572631B78A93C66EF9FDFCE87CDE372CC4ED7848DA78C1EB1DCDD78`.
{% endhint %}

Now, view the updated balances of the origin and destination accounts:

```bash
pundixd query account <account_px>
pundixd query account <destination_px>
```

You can also check your balance at a given block by using the `--height` flag:

```bash
pundixd query account <account_px> --height <int>
# for example
pundixd query account px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30 --height 10
```

Furthermore, you can build a transaction and print its JSON format to STDOUT by appending `--generate-only` to the list of the command line arguments. Running the following command will store build the transaction and store it in a file named "unsignedSendTx.json":

```bash
pundixd tx bank send <sender_address> <recipient_address> 10PUNDIX \
  --chain-id=<chain_id> \
  --sequence=<account_sequence> \
  --generate-only > unsignedSendTx.json
# for example
# the user has to check account "sequence" first
# pundixd query account px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30
pundixd tx bank send px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30 px1ejstvlp4294h7ncnxgl8rqatsaj4kf2s4lj3y2 10PUNDIX --generate-only --sequence=12
> unsignedSendTx.json

pundixd tx sign \
  --chain-id=<chain_id> \
  --from=<key_name> \
  unsignedSendTx.json > signedSendTx.json
# for example
pundixd tx sign unsignedSendTx.json --chain-id=PUNDIX --from=admin  > signedSendTx.json
```

{% hint style="info" %}
The `--generate-only` flag prevents `pundixd` from accessing the local keybase. Thus when such flag is supplied `<sender_key_name_or_address>` must be an address.
{% endhint %}

You can broadcast the signed transaction to a node by providing the JSON file to the following command:

```bash
pundixd tx broadcast <file_path>
# for example
pundixd tx broadcast signedSendTx.json
```

### Tx Broadcasting

When broadcasting transactions, `pundixd` accepts a `--broadcast-mode` flag. This flag can have a value of `sync` (default), `async`, or `block`, where `sync` makes the client return a `CheckTx` response, `async` makes the client return immediately, and `block` makes the client wait for the tx to be committed (or timing out).

It is important to note that the `block` mode should **NOT** be used in most circumstances. This is because broadcasting can timeout but the tx may still be included in a block. This can result in many undesirable situations. Therefore, it is best to use `sync` or `async` and query by tx hash to determine when the tx is included in a block.

## Query Transactions

### Matching a Set of Events

You can use the transaction search command to query for transactions that match a specific set of `events`, which are added on every transaction.

Each event is composed by a key-value pair in the form of `{eventType}.{eventAttribute}={value}`. Events can also be combined to query for a more specific result using the `&` symbol.

You can query transactions by `events` as follows:

```bash
pundixd query txs --events='message.sender=px1...'
# for example 
pundixd query txs --events='message.sender=px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30'
```

And for using multiple `events`:

```bash
pundixd query txs --events='message.sender=px1...&message.action=/cosmos.bank.v1beta1.MsgSend'
# for example
pundixd query txs --events='message.sender=px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30&message.action=/cosmos.bank.v1beta1.MsgSend'
```

The pagination is supported as well via `page` and `limit`:

```bash
pundixd query txs --events='message.sender=px1...' --page=1 --limit=20
# for example
pundixd query txs --events='message.sender=px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30'  --page=1 --limit=20
```

The action tag always equals the message type returned by the `Type()` function of the relevant message.

{% hint style="info" %}
You can find a list of available `events` on each of the SDK modules:

* [Staking events](https://github.com/cosmos/cosmos-sdk/blob/master/x/staking/spec/07_events.md)
* [Governance events](https://github.com/cosmos/cosmos-sdk/blob/master/x/gov/spec/04_events.md)
* [Slashing events](https://github.com/cosmos/cosmos-sdk/blob/master/x/slashing/spec/06_events.md)
* [Distribution events](https://github.com/cosmos/cosmos-sdk/blob/master/x/distribution/spec/06_events.md)
* [Bank events](https://github.com/cosmos/cosmos-sdk/blob/master/x/bank/spec/04_events.md)
{% endhint %}

### Matching a Transaction's Hash

You can also query a single transaction by its hash using the following command:

```bash
pundixd query tx [hash]
```

{% hint style="info" %}
tx hash on the block explorer are preceded with `0x`. Please omit the `0x` from the tx hash
{% endhint %}

## Staking

### Set up a Validator

Please refer to the [Validator Setup](../validators/validator-cli-guide.md) section for a more complete guide on how to set up a validator.

### Delegate to a Validator

On the upcoming mainnet, you can delegate `PUNDIX` to a validator. These [delegators](../delegators/delegator-faq.md) can receive part of the validator's fee revenue. Read more about the [incentives](../delegators/delegator-faq.md).

#### Query Validators

You can query the list of all validators of a specific chain:

```bash
pundixd query staking validators
```

If you want to get the information of a single validator you can check it with:

```bash
pundixd query staking validator <account_pxval>
# for example
pundixd query staking validator pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc
```

### Bond Tokens

On the PundiX mainnet, we delegate `PUNDIX`. Here's how you can bond tokens to a testnet validator (for example, delegate):

```bash
pundixd tx staking delegate \
  <validator_operator_address> \
  <amount> \
  --from=<key_name> \
# for example
pundixd tx staking delegate pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc 101PUNDIX --from=admin
```

`<validator_operator_address>` is the operator address of the validator to which you intend to delegate. If you are running a local testnet, you can find this with:

```bash
pundixd keys show <account_name> --bech val
```

Where `<account_name>` is the name of the key you specified when you initialized `pundixd`.

While tokens are bonded, they are pooled with all the other bonded tokens in the network. Validators and delegators obtain a percentage of shares that equal their stake in this pool.

#### Query Delegations

{% hint style="info" %}
In this section and the next, do make sure you check if the command has a plural form or not. Adding an (s) behind delegation to delegations results in a different command.
{% endhint %}

Once submitted a delegation to a validator, you can see it's information by using the following command:

```bash
pundixd query staking delegation <delegator_addr> <validator_addr>
# for example
pundixd query staking delegation px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30 pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc
```

Or if you want to check all your current delegations with disctinct validators:

```bash
pundixd query staking delegations <delegator_addr>
# for example
pundixd query staking delegations px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30
```

You can also query all of the delegations to a particular validator:

```bash
pundixd query staking delegations-to <validator_addr>
# for example
pundixd query staking delegations-to pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc
```

### Unbond Tokens

If for any reason the validator misbehaves, or you just want to unbond a certain amount of tokens, use this following command.

```bash
pundixd tx staking unbond \
  <validator_addr> \
  10PUNDIX \
  --from=<key_name> \
# for example
pundixd tx staking unbond pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc 10PUNDIX --from=admin
```

The unbonding will be automatically completed when the unbonding period has passed.

#### Query Unbonding-Delegations

Once you begin an unbonding-delegation, you can see it's information by using the following command:

```bash
pundixd query staking unbonding-delegation <delegator_addr> <validator_addr>
# for example
pundixd query staking unbonding-delegation px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30 pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc
```

If you want to check all your current unbonding-delegations with disctinct validators:

```bash
pundixd query staking unbonding-delegations <account_px>
# for example
pundixd query staking unbonding-delegations px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30
```

Additionally, as you can get all the unbonding-delegations from a particular validator:

```bash
pundixd query staking unbonding-delegations-from <account_pxval>
# for example
pundixd query staking unbonding-delegations-from pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc
```

### Redelegate Tokens

A redelegation is a type delegation that allows you to bond illiquid tokens from one validator to another:

```bash
pundixd tx staking redelegate \
  <src-validator-operator-addr> \
  <dst-validator-operator-addr> \
  10PUNDIX \
  --from=<key_name> 

# for example
pundixd tx staking redelegate pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc pxvaloper1ejstvlp4294h7ncnxgl8rqatsaj4kf2svn8vda 10PUNDIX --from=admin 
```

Here you can also redelegate a specific `shares-amount` or a `shares-fraction` with the corresponding flags.

The redelegation will be automatically completed when the unbonding period has passed.

#### Query Redelegations

Once you begin a redelegation, you can see it's information by using the following command:

```bash
pundixd query staking redelegation <delegator_addr> <src_val_addr> <dst_val_addr>
# for example
pundixd query staking redelegation px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30 pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc pxvaloper1ejstvlp4294h7ncnxgl8rqatsaj4kf2svn8vda
```

It returns:

```bash
{"redelegation_responses":[{"redelegation":{"delegator_address":"px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30","validator_src_address":"pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc","validator_dst_address":"pxvaloper1ejstvlp4294h7ncnxgl8rqatsaj4kf2svn8vda","entries":null},"entries":[{"redelegation_entry":{"creation_height":14019,"completion_time":"2022-09-16T09:41:58.105545Z","initial_balance":"10000000000000000000","shares_dst":"10000000000000000000.000000000000000000"},"balance":"10000000000000000000"}]}],"pagination":null}
```

If you want to check all your current unbonding-delegations with distinct validators:

```bash
pundixd query staking redelegations <account_px>
# for example
pundixd query staking redelegations px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30
```

It returns:

```bash
{"redelegation_responses":[{"redelegation":{"delegator_address":"px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30","validator_src_address":"pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc","validator_dst_address":"pxvaloper1ejstvlp4294h7ncnxgl8rqatsaj4kf2svn8vda","entries":null},"entries":[{"redelegation_entry":{"creation_height":14019,"completion_time":"2022-09-16T09:41:58.105545Z","initial_balance":"10000000000000000000","shares_dst":"10000000000000000000.000000000000000000"},"balance":"10000000000000000000"}]}],"pagination":{"next_key":null,"total":"0"}}
```

Additionally, as you can get all the outgoing redelegations from a particular validator:

```bash
pundixd query staking redelegations-from <account_pxval>
# for example
pundixd query staking redelegations-from pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc
```

It returns:

```bash
{"redelegation_responses":[{"redelegation":{"delegator_address":"px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30","validator_src_address":"pxvaloper1vhe2w8f9ne8yakhk75usjv2m8txkulagnr7kcc","validator_dst_address":"pxvaloper1ejstvlp4294h7ncnxgl8rqatsaj4kf2svn8vda","entries":null},"entries":[{"redelegation_entry":{"creation_height":14019,"completion_time":"2022-09-16T09:41:58.105545Z","initial_balance":"10000000000000000000","shares_dst":"10000000000000000000.000000000000000000"},"balance":"10000000000000000000"}]}],"pagination":{"next_key":null,"total":"0"}}
```

{% hint style="info" %}
However, there is a limit to how frequent you can redelegate. For more information on [redelegation](https://github.com/PundiAI/pundiai-docs/blob/main/px-docs/delegators/delegators-faq.md#redelegation).
{% endhint %}

#### Query Parameters

Parameters define high level settings for staking. You can get the current values by using:

```bash
pundixd query staking params
```

It returns:

```bash
{"unbonding_time":"1814400s","max_validators":20,"max_entries":7,"historical_entries":20000,"bond_denom":"ibc/55367B7B6572631B78A93C66EF9FDFCE87CDE372CC4ED7848DA78C1EB1DCDD78"}
```

With the above command you will get the values for:

* Unbonding time
* Maximum numbers of validators
* Coin denomination for staking

All these values will be subject to updates through a `governance` process by `ParameterChange` proposals.

#### Query Pool

A staking `Pool` defines the dynamic parameters of the current state. You can query them with the following command:

```bash
pundixd query staking pool
```

With the `pool` command you will get the values for:

* Bonded tokens
* Not-bonded tokens

## Slashing

### Unjailing

To unjail your jailed validator:

```bash
pundixd tx slashing unjail --from <validator-operator-addr>
# for example
pundixd tx slashing unjail --from px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30
```

### Signing Info

To retrieve a validator's signing info:

```bash
pundixd query slashing signing-info <validator-pubkey>
# for example
pundixd query slashing signing-info c9K95ze0trEtE1KCZ1smjhJQdVqEB8+7Ma6ht64bhDg=
```

#### Query Parameters

You can get the current slashing parameters via:

```bash
pundixd query slashing params
```

### Minting

You can query for the minting/inflation parameters via:

```bash
pundixd query mint params
```

It returns:

```bash
{"mint_denom":"bsc0x29a63f4b209c29b4dc47f06ffa896f32667dad2c","inflation_rate_change":"1.000000000000000000","inflation_max":"40.000000000000000000","inflation_min":"20.000000000000000000","goal_bonded":"0.510000000000000000","blocks_per_year":"6311520"}
```

To query for the current inflation value:

```bash
pundixd query mint inflation
```

It returns:

```bash
30.000108522380736972
```

To query for the current annual provisions value:

```bash
pundixd query mint annual-provisions
```

It returns:

```bash
30000110305612345326000.000000000000000000
```

### Checking Block Information and Validators Signatures

The following command will query for a transaction by hash in a committed block:

```bash
pundixd query block-results
```

The following command will get verified data for a the block at given height:

```bash
pundixd query block
```

{% hint style="info" %}
Using these commands and filtering out the necessary information, you will be able to deduce the uptime of other validators by checking if they missed any signatures for that block.
{% endhint %}

A sample query to check for any missing validator signature given a particular block height:

```bash
pundixd query block 644696 --node  https://testnet-px-json.pundix.com:26657   | jq '.block.last_commit'
```

## Governance

Governance is the process from which users in the PundiX can come to consensus on software upgrades, parameters of the mainnet or signaling mechanisms through text proposals. This is done through voting on proposals, which will be submitted by `PUNDIX` holders on the mainnet.

Some considerations about the voting process:

* Voting is done by bonded `PUNDIX` holders on a 100 bonded `PUNDIX` 1 vote basis
* Delegators **who DO NOT** vote will inherit the vote of their validator
* Votes are tallied at the end of the voting period (2 weeks on mainnet). Addresses can vote multiple times before the end of the voting period to update their `Option` value (incurring transaction fees each time), only the most recently casted vote will count as valid
* Voters can choose between options `Yes`, `No`, `NoWithVeto` and `Abstain`
* By the end of the voting period, a proposal is accepted if:
  * `(YesVotes / (YesVotes+NoVotes+NoWithVetoVotes)) > 1/2`
  * `(NoWithVetoVotes / (YesVotes+NoVotes+NoWithVetoVotes)) < 1/3`
  * `((YesVotes+NoVotes+NoWithVetoVotes) / totalBondedStake) >= quorum`

For more information about the governance process and how it works, please check out the Governance module [specification](https://github.com/cosmos/cosmos-sdk/tree/master/x/gov/spec).

{% hint style="info" %}
The minimum deposit for a governance proposal is `10,000PUNDIX` (through the command line, this amounts to `10000000000000000000000ibc/55367b7b6572631b78a93c66ef9fdfce87cde372cc4ed7848da78c1eb1dcdd78` after multiplying by `10^18`). Since the ibc token denom is too long, we will only use `PUNDIX` in general case.
{% endhint %}

### Create a Governance Proposal

In order to create a governance proposal, you must submit an initial deposit along with a title and description. Various modules outside of governance may implement their own proposal types and handlers (for example parameter changes), where the governance module itself supports `Text` proposals. Any module outside of governance has it's command mounted on top of `submit-proposal`.

To submit a `Text` proposal (the title and description fields will be string input so enclose the input in `""`):

```bash
pundixd tx gov submit-proposal \
  --title=<title> \
  --description=<description> \
  --type="Text" \
  --deposit="100PUNDIX" \
  --from=<name> \

# for example
pundixd tx gov submit-proposal \
  --title="Test Proposal" \
  --description="This is a test proposal" \
  --type="Text" \
  --deposit="100PUNDIX" \
  --from=admin
```

You may also provide the proposal directly through the `--proposal` flag which points to a JSON file containing the proposal. Create `proposal.json` which contains the following:

```json
{
  "title": "Param JSON",
  "description": "Update max validators",
  "changes": [
    {
      "subspace": "staking",
      "key": "MaxValidators",
      "value": 105
    }
  ],
  "deposit": [
    {
      "denom": "stake",
      "amount": "10"
    }
  ]
}
```

To submit a parameter change proposal, you must provide a proposal file as its contents are less friendly to CLI input:

```bash
pundixd tx gov submit-proposal param-change <path/to/proposal.json> \
  --from=<name> 
# for example
pundixd tx gov submit-proposal param-change ./proposal.json \
  --from=admin
```

{% hint style="info" %}
Currently parameter changes are _evaluated_ but not _validated_, so it is very important that any `value` change is valid (for example correct type and within bounds) for its respective parameter, for example `MaxValidators` should be an integer and not a decimal.

Proper vetting of a parameter change proposal should prevent this from happening (no deposits should occur during the governance process), but it should be noted regardless.
{% endhint %}

The `SoftwareUpgrade` command is currently not supported as it's not implemented and currently does not differ from the semantics of a `Text` proposal.

#### Query Proposals

Once created, you can now query information of the proposal:

```bash
pundixd query gov proposal <proposal_id>
# for example
pundixd query gov proposal 1
```

It returns:

```bash
{"proposal_id":"1","content":{"@type":"/cosmos.gov.v1beta1.TextProposal","title":"Test Proposal","description":"This is a test proposal"},"status":"PROPOSAL_STATUS_DEPOSIT_PERIOD","final_tally_result":{"yes":"0","abstain":"0","no":"0","no_with_veto":"0"},"submit_time":"2022-08-26T10:31:21.557584Z","deposit_end_time":"2022-09-09T10:31:21.557584Z","total_deposit":[{"denom":"ibc/55367B7B6572631B78A93C66EF9FDFCE87CDE372CC4ED7848DA78C1EB1DCDD78","amount":"100000000000000000000"}],"voting_start_time":"0001-01-01T00:00:00Z","voting_end_time":"0001-01-01T00:00:00Z"}
```

Or query all available proposals:

```bash
pundixd query gov proposals <proposal_id>
```

You can also query proposals filtered by `voter` or `depositor` by using the corresponding flags.

To query for the proposer of a given governance proposal:

```bash
pundixd query gov proposer <proposal_id>
# for example
pundixd query gov proposer 1
```

It returns:

```bash
{"proposal_id":"1","proposer":"px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30"}
```

### Increase Deposit

In order for a proposal to be broadcasted to the network, the amount deposited must be above a `minDeposit` value (initial value: `10000PUNDIX`). If the proposal you previously created didn't meet this requirement, you can still increase the total amount deposited to activate it. Once the minimum deposit is reached, the proposal enters voting period:

```bash
pundixd tx gov deposit <proposal_id> "10000PUNDIX" \
  --from=<name>

# for example
pundixd tx gov deposit 1 "1PUNDIX" \
  --from=admin
```

{% hint style="info" %}
Proposals that don't meet this requirement will be deleted after `MaxDepositPeriod` is reached.
{% endhint %}

#### Query Deposits

Once a new proposal is created, you can query all the deposits submitted to it:

```bash
pundixd query gov deposits <proposal_id>
# for example
pundixd query gov deposits 1
```

It returns:

```bash
{"deposits":[{"proposal_id":"1","depositor":"px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30","amount":[{"denom":"ibc/55367B7B6572631B78A93C66EF9FDFCE87CDE372CC4ED7848DA78C1EB1DCDD78","amount":"100000000000000000000"}]}],"pagination":{"next_key":null,"total":"0"}}
```

You can also query a deposit submitted by a specific address:

```bash
pundixd query gov deposit <proposal_id> <depositor_address>
# for example
pundixd query gov deposit 1 px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30
```

It returns:

```bash
{"proposal_id":"1","depositor":"px1vhe2w8f9ne8yakhk75usjv2m8txkulag20tt30","amount":[{"denom":"ibc/55367B7B6572631B78A93C66EF9FDFCE87CDE372CC4ED7848DA78C1EB1DCDD78","amount":"100000000000000000000"}]}
```

### Vote on a Proposal

After a proposal's deposit reaches the `MinDeposit` value, the voting period opens. Bonded `PUNDIX` holders can then cast vote on it:

```bash
pundixd tx gov vote <proposal_id> <Yes/No/NoWithVeto/Abstain> \
  --from=<name>
# for example
pundixd tx gov vote 1 Yes \
  --from=admin
```

#### Query Votes

Check the vote with the option you just submitted:

```bash
pundixd query gov vote <proposal_id> <voter_address>
```

You can also get all the previous votes submitted to the proposal with:

```bash
pundixd query gov votes <proposal_id>
```

#### Query proposal tally results

To check the current tally of a given proposal you can use the `tally` command:

```bash
pundixd query gov tally <proposal_id>
```

#### Query Governance Parameters

To check the current governance parameters run:

```bash
pundixd query gov params
```

To query subsets of the governance parameters run:

```bash
pundixd query gov param voting
pundixd query gov param tallying
pundixd query gov param deposit
```

### Fee Distribution

#### Query Distribution Parameters

To check the current distribution parameters, run:

```bash
pundixd query distribution params
```

#### Query Distribution Ecosystem Genesis Fund

To query all coins in the Ecosystem Genesis Fund which is under Governance control:

```bash
pundixd query distribution community-pool
```

#### Query Outstanding Rewards

To check the current total outstanding (un-withdrawn) rewards of a particular validator (validator's + delegators' rewards), run:

```bash
pundixd query distribution validator-outstanding-rewards <validator-addr>
```

#### Query Validator Commission

To check the current outstanding commission for a validator (excluding the rewards of the wallet tied to that validator address), run:

```bash
pundixd query distribution commission <validator_address>
```

#### Query Validator Slashes

To check historical slashes for a validator, run:

```bash
pundixd query distribution slashes <validator_address> <start_height> <end_height>
```

#### Query Delegator Rewards

To check current rewards for a delegation (were they to be withdrawn), run:

```bash
pundixd query distribution rewards <delegator_address> <validator_address>
```

#### Query All Delegator Rewards

To check all current rewards for a delegation (were they to be withdrawn), run:

```bash
pundixd query distribution rewards <delegator_address>
```

## Claiming Rewards

### Claiming rewards for delegators and validators

Withdraw rewards from a given delegation address, and optionally withdraw validator commission (by adding in a `--commission` flag, see below) if the delegation address given is a validator operator:

```
pundixd tx distribution withdraw-rewards <validator-addr> --from <_name>
```

Withdraw the validator's commission in addition to the rewards:

```
pundixd tx distribution withdraw-rewards <validator-addr> --from mykey --commission
```

### Multisig Transactions

Multisig transactions require signatures of multiple private keys. Thus, generating and signing a transaction from a multisig account involve cooperation among the parties involved. A multisig transaction can be initiated by any of the key holders, and at least one of them would need to import other parties' public keys into their Keybase and generate a multisig public key in order to finalize and broadcast the transaction.

For example, given a multisig key comprising the keys `p1`, `p2`, and `p3`, each of which is held by a distinct party, the user holding `p1` would require to import both `p2` and `p3` in order to generate the multisig account public key:

```bash
pundixd keys add \
  --multisig=p1,p2,p3... \
  --multisig-threshold=2 \
  new_key_name
```

A new multisig public key `bk` has been stored, and its address will be used as signer of multisig transactions:

```bash
pundixd keys show --address bk
```

You may also view multisig threshold, pubkey constituents and respective weights by viewing the JSON output of the key or passing the `--show-multisig` flag:

```bash
pundixd keys show bk -o json
pundixd keys show bk --show-multisig
```

The first step to create a multisig transaction is to initiate it on behalf of the multisig address created above:

{% hint style="info" %}
For multisig accounts, if you were to create any transaction, for example `--from=<multisig_account>` your `<multisig_account>` needs to be the wallet address ie `px123l3kjltjwlfgjslfg....`. Only for those non-multisig accounts can you use the name of the account ie `--from=heimendinger`.
{% endhint %}

```bash
pundixd tx bank send px1570v2fq3twt0f0x02vhxpuzc9jc4yl30q2qned px12u8ekfqdd75r4apyqv2xst6qw0n3wvr2asncf5 1PUNDIX \
  --generate-only > unsignedTx.json
```

The file `unsignedTx.json` contains the unsigned transaction encoded in JSON. `p1` can now sign the transaction with its own private key:

```bash
pundixd tx sign \
  unsignedTx.json \
  --multisig=<multisig_address> \
  --from=p1 \
  --output-document=p1signature.json \
  --chain-id=payalebar
```

Once the signature is generated, `p1` transmits both `unsignedTx.json` and `p1signature.json` to `p2` or `p3`, which in turn will generate their respective signature:

```bash
pundixd tx sign \
  unsignedTx.json \
  --multisig=<multisig_address> \
  --from=p2 \
  --output-document=p2signature.json \
  --chain-id=payalebar
```

{% hint style="info" %}
The Mainnet ChainID should be **pundix**
{% endhint %}

`bk` is a 2-of-3 multisig key, therefore one additional signature is sufficient. Any the key holders can now generate the multisig transaction by combining the required signature files:

```bash
pundixd tx multisign \
  unsignedTx.json \
  bk \
  p1signature.json p2signature.json > signedTx.json
```

The transaction can now be sent to the node:

```bash
pundixd tx broadcast signedTx.json
```

### Shells Completion Scripts

Completion scripts for popular UNIX shell interpreters such as `Bash` and `Zsh` can be generated through the `completion` command, which is available for both `pundixd` and `pundixd`.

If you want to generate `Bash` completion scripts run the following command:

```bash
pundixd completion > pundixd_completion
pundixd completion > pundixcli_completion
```

If you want to generate `Zsh` completion scripts run the following command:

```bash
pundixd completion --zsh > pundixd_completion
pundixd completion --zsh > pundixcli_completion
```

{% hint style="info" %}
On most UNIX systems, such scripts may be loaded in `.bashrc` or `.bash_profile` to enable Bash autocompletion:
{% endhint %}

```bash
echo '. pundixd_completion' >> ~/.bashrc
echo '. pundixcli_completion' >> ~/.bashrc
```

{% hint style="info" %}
Refer to the user's manual of your interpreter provided by your operating system for information on how to enable shell autocompletion.
{% endhint %}
