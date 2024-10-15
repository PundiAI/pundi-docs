# Full node with Binaries

This guide will explain how to install the `pundixd` command line interface (CLI) on your system with `Binaries` option. With these installed on a server, you can participate on the mainnet or testnet as a [Validator](https://github.com/FunctionX-SG/pundiai-docs/blob/main/px-docs/validators/setting-up-a-validator-for-pundix.md).

## Install PundiX (Pundi X Chain)

{% hint style="info" %}
**You need to** [**install PundiX**](../installation-pundix.md) **before you go further.**
{% endhint %}

### Setup PundiX

Initializing PundiX:

{% tabs %}
{% tab title="Mainnet" %}
```shell
pundixd init <your_name> 
```
{% endtab %}

{% tab title="Testnet" %}
```shell
pundixd init <your_name> --chain-id payalebar
```
{% endtab %}
{% endtabs %}

Initializing pundixd will result in the creation of a few directories and most importantly the `.pundix` directory (for more information on the directory tree, refer to the validator-recovery section). This will be where your validator keys are stored and this is important for recovery of your validator.

Fetching **`genesis`** file (copy this entire line of code and hit <mark style="color:red;">ENTER</mark>):

{% tabs %}
{% tab title="Mainnet" %}
```shell
wget https://raw.githubusercontent.com/pundix/pundix/main/public/mainnet/genesis.json -O ~/.pundix/config/genesis.json
```
{% endtab %}

{% tab title="Testnet" %}
```shell
wget https://raw.githubusercontent.com/pundix/pundix/main/public/testnet/genesis.json -O ~/.pundix/config/genesis.json
```
{% endtab %}
{% endtabs %}

Set Peers

{% tabs %}
{% tab title="Mainnet" %}
```shell
pundixd config config.toml p2p.seeds 78d3eb3f15a20ab1d567660d35776abe0dee71d0@pundix-mainnet-seed-node-1.pundix.com:26656,3c37c6c42dfd9094117549794299a62d49c122eb@pundix-mainnet-seed-node-2.pundix.com:26656
pundixd config config.toml p2p.persistent_peers 8bd41ea9f8ba7cfee4d19887cab487cdfc1177f4@pundix-mainnet-node-1.pundix.com:26656,6c1738220234a5e1b3caf94403ecd651e9759952@pundix-mainnet-node-2.pundix.com:26656,23abe2346d40f82cf0606e47931e58752f8b9348@pundix-mainnet-node-3.pundix.com:26656,20d275af6d025be144765291db5337ea059cce18@pundix-mainnet-node-4.pundix.com:26656,47f97d7baf028ddfd3b223baab0fa062eae75310@pundix-mainnet-node-5.pundix.com:26656
```
{% endtab %}

{% tab title="Testnet" %}
```
pundixd config config.toml p2p.seeds c77303a511a90a41c562d5925b170d7a68975569@payalebar-seed-node-1.pundix.com:26656,777fba974bb085daea6b83b6e76c6619d96eed50@payalebar-node-1.pundix.com:26656,9a296821d069a3c599ea2be5cd8698ec927ca5ce@payalebar-node-2.pundix.com:26656
pundixd config config.toml p2p.persistent_peers "" 
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**IMPORTANT** At this stage **BEFORE** starting the node, please download the latest snapshot, refer to this [link](snapshot-guide.md).

Additionally, what is important is that your validator keys that is stored in a `.json` file for you to do a recovery in the future. For more [information](../../validators/validator-recovery.md) how to access the files.

Also, you can consider generating a new consensus key and [backing it up using a pin](full-node-with-binaries.md#secret-and-updating-consensus-key).

For a more stable way of setting up via [running a daemon](full-node-with-binaries.md#running-server-as-a-daemon)
{% endhint %}

Start Node:

```bash
nohup pundixd start 2>&1 > pundix.log &
```

Check logs:

```bash
tail -f pundix.log
```

Open another terminal in the same folder. View more startup configurations:

```bash
pundixd start -h
```

For example, Start and open the 1317 restful service port:

```bash
nohup pundixd start --api.enable true --address 0.0.0.0:1317 2>&1 > pundix.log &
```

Then excute the command line in terminal:

```bash
tail pundix.log
```

The execution of the previous command will return something like this (this is to check the status of nodes and which blocks are being synced/are syncing):

```bash
6:08PM INF indexed block height=3698 module=txindex server=node
6:08PM INF Timed out dur=945.515 height=3699 module=consensus round=0 server=node step=1
6:08PM INF received proposal module=consensus proposal={"Type":32,"block_id":{"hash":"51E98FF8FB0F6F5D4A37BEDFFDB37F849657A19D786FD89E0521A8BBFAD54733","parts":{"hash":"5108094CA9248288944168931AE1B5D9BF87EB253DEDECA60982EE2FDF253265","total":1}},"height":3699,"pol_round":-1,"round":0,"signature":"/77Seq+zrpzpjoUIofqB2/+xCRDKcUf0ekW3dXGjlgn8nWqkbfxuuS2XUhU5p2FxSEbs436f5vwOlVRJK+dHAw==","timestamp":"2022-08-25T10:08:40.924827Z"} server=node
6:08PM INF received complete proposal block hash=51E98FF8FB0F6F5D4A37BEDFFDB37F849657A19D786FD89E0521A8BBFAD54733 height=3699 module=consensus server=node
6:08PM INF finalizing commit of block hash={} height=3699 module=consensus num_txs=0 root=739ACDF1321A8A3DFACDD78CA62C056C1463DCF80C840439BD6242EDEFF3682F server=node
6:08PM INF minted coins from module account amount=4753287822151504purse from=mint module=x/bank
6:08PM INF executed block height=3699 module=state num_invalid_txs=0 num_valid_txs=0 server=node
6:08PM INF commit synced commit=436F6D6D697449447B5B313537203134322036203838203139352031383720323431203131332031383220313332203232352031333420313935203633203330203733203136362032372035312032313620363420353220323133203132382031353420383020313933203132392031303220313520313930203233305D3A4537337D
6:08PM INF committed state app_hash=9D8E0658C3BBF171B684E186C33F1E49A61B33D84034D5809A50C181660FBEE6 height=3699 module=state num_txs=0 server=node
6:08PM INF indexed block height=3699 module=txindex server=node
```

To check if pundix is synced:

```bash
curl localhost:26657/status
# or
pundixd status
```

Return:

```bash
{
  "jsonrpc": "2.0",
  "id": -1,
  "result": {
    "node_info": {
      "protocol_version": {
        "p2p": "8",
        "block": "11",
        "app": "0"
      },
      "id": "26097a71ea65ee78b3b985563a4f55fe2bbedaf3",
      "listen_addr": "tcp://0.0.0.0:26656",
      "network": "PUNDIX",
      "version": "release/v0.2.0-be6a7eb51777e533f9b2dc22e8a9d8e5529dacbd",
      "channels": "40202122233038606100",
      "moniker": "local",
      "other": {
        "tx_index": "on",
        "rpc_address": "tcp://0.0.0.0:26657"
      }
    },
    "sync_info": {
      "latest_block_hash": "F56E19ECB420A07AD483313AA2D4B5ACA002EBB2DDE2E6224B3140B6D8309D18",
      "latest_app_hash": "9EB77207A9927FDE2F5A393C8A67B137235FBCFD2A0754FD6CDB678A4B4673C3",
      "latest_block_height": "4381",
      "latest_block_time": "2022-08-25T10:20:51.144946Z",
      "earliest_block_hash": "793E56EC43863D0EAE8A758DFC64E6E17F3680F085D721763D8C26C56522CDB0",
      "earliest_app_hash": "E3B0C44298FC1C149AFBF4C8996FB92427AE41E4649B934CA495991B7852B855",
      "earliest_block_height": "1",
      "earliest_block_time": "2022-08-25T09:01:59.798536Z",
      "catching_up": false
    },
    "validator_info": {
      "address": "7C4B956EA6A2EDCA58AAF2FE21C1D7405E0A9F19",
      "pub_key": {
        "type": "tendermint/PubKeyEd25519",
        "value": "r/smZpiVw+bcV2f4e+xqV9j9P7SDtpthCv3nmVUS2qk="
      },
      "voting_power": "1"
    }
  }
}
```

To ensure that the blocks are synced up with your node, under `"sync_info"`, `"catching_up value"` should be false `"catching_up value": false`. This may take a few hours and your node has to be fully synced up before proceeding to the next step. You may cross reference the latest block you are synced to `"sync_info": "latest_block_height"` and the latest block height of our Testnet blockchain on our [Testnet blockchain explorer](https://payalebar-explorer.pundix.com/pundix/blocks) or our [Mainnet](https://explorer.pundix.com/pundix/proposals).

Stop Node (will be running in the background if not stopped):

```bash
ps -ef | grep pundixd
kill -9 PID
```

## Running Server

It is important to keep `pundixd` running at all times. There are several ways to achieve this, and the simplest solution we recommend is to register `pundixd` as a `systemd` service so that it will automatically get started upon system reboots and other events.

### Register `pundixd` as a service

First, create a service definition file in `/etc/systemd/system`.

Run this command to create the sample file above in the file path`/etc/systemd/system/pundixd.service` (if you are in the pundix directory):

```bash
cat > /etc/systemd/system/pundixd.service
```

hit the <mark style="color:red;background-color:blue;">ENTER</mark> button on your keyboard and `copy` and `paste` the contents of the file below into the command line:

### Sample file

{% code title="pundixd.service" %}
```bash
[Unit]
Description=PundiX Node
After=network.target
[Service]
Type=simple
User=root
WorkingDirectory=/root
ExecStart=/root/go/bin/pundixd start --home /root/.pundix
Restart=on-failure
RestartSec=3
LimitNOFILE=4096
[Install]
WantedBy=multi-user.target
```
{% endcode %}

Then hit the <mark style="color:red;background-color:blue;">ENTER</mark> button on your keyboard before using <mark style="color:red;background-color:blue;">Ctrl+D</mark> on your keyboard, your file with the above contents will be created. It should look like this:

{% hint style="info" %}
run the command:`which pundixd` and replace the `ExecStart` file path with the return value of the command
{% endhint %}

```bash
root@XXXXXXXXXXXXXXX:~# cat > /etc/systemd/system/pundixd.service
[Unit]
Description=pundix Node
After=network.target
[Service]
Type=simple
User=root
WorkingDirectory=/root
ExecStart=/root/go/bin/pundixd start --home /root/.pundix
Restart=on-failure
RestartSec=3
LimitNOFILE=4096
[Install]
WantedBy=multi-user.target
```

Modify the `Service` section from the given sample above to suit your settings. Note that even if we raised the number of open files for a process, we still need to include `LimitNOFILE`.

After creating a service definition file, you should execute:

```bash
systemctl daemon-reload
systemctl enable pundixd
```

### Controlling the service

Use `systemctl` to control (start, stop, restart) in Linux/Ubuntu:

```bash
# start
sudo systemctl start pundixd

# stop
sudo systemctl stop pundixd

# restart
sudo systemctl restart pundixd

# status
sudo systemctl status pundixd
```

To start the node, run `sudo systemctl start pundixd`, and thereafter run `journalctl -u pundixd -n 100 -f` to see the latest and continuous logs.

### Accessing logs

```bash
# entire log
journalctl -u pundixd -n 100

# entire log reversed
journalctl -u pundixd -r

# latest and continuous log
journalctl -u pundixd -n 100 -f
```

Concluding tips: It is always better to sync PundiX using the Daemon method because this ensures stability and that your syncing is continuously running in the background.

## Secret and updating consensus key

{% hint style="danger" %}
Use this at your own risk❗ I suggest trying it out on testnet first and also backing up your `priv_validator_key.json` if you already have this set up for a validator. The file can be found in this file path `~/.pundix/config/priv_validator_key.json`.
{% endhint %}

### Updating your consensus key and tagging it to a pin

Before setting up your validator if you would like to have a backup of your keys with a pin. You may run the following command:

```bash
pundixd tendermint unsafe-reset-priv-validator <secret>
```

{% hint style="info" %}
the `<secret>` key here must be longer than 32 characters
{% endhint %}

Running the above command will return:

```bash
WARNING: The consensus private key of the node will be replaced.
Ensure that the backup is complete.
USE AT YOUR OWN RISK. Continue? [y/N]
```

After inputting `y`, your `priv_validator_key.json` will be replaced with a new file. This means you will have a new consensus private key and it will be tagged to your `<secret>` pin.

### Checking to see if the pin works

If your `.pundix` folder is in the root directory

```bash
cat ~/.pundix/config/priv_validator_key.json
```

{% hint style="danger" %}
**Record the previous output before running the next command!**
{% endhint %}

Remove this file:

```bash
rm ~/.pundix/config/priv_validator_key.json
```

The following command will recover your original consensus key:

```bash
pundixd tendermint unsafe-reset-priv-validator <secret>
```

Match this output with the previous output above:

```bash
cat ~/.pundix/config/priv_validator_key.json
```
