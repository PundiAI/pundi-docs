# Full node with Docker

{% hint style="info" %}
**If you DO NOT already have docker installed, there will be a prompt for you to install it. Follow the instructions given.**
{% endhint %}

* Pull docker images

```bash
docker pull ghcr.io/pundix/pundix:latest
```

* Initializing pundix

```bash
docker run -v $HOME/.pundix:/root/.pundix ghcr.io/pundix/pundix:latest init pxlocal
```

* Download genesis (copy and run each line, line by line)

{% tabs %}
{% tab title="Mainnet" %}
```
wget https://raw.githubusercontent.com/pundix/pundix/main/public/mainnet/genesis.json -O ~/.pundix/config/genesis.json
wget https://raw.githubusercontent.com/pundix/pundix/main/public/mainnet/config.toml -O ~/.pundix/config/config.toml
wget https://raw.githubusercontent.com/pundix/pundix/main/public/mainnet/app.toml -O ~/.pundix/config/app.toml
```
{% endtab %}

{% tab title="Testnet" %}
```
wget https://raw.githubusercontent.com/pundix/pundix/main/public/testnet/genesis.json -O ~/.pundix/config/genesis.json
wget https://raw.githubusercontent.com/pundix/pundix/main/public/testnet/config.toml -O ~/.pundix/config/config.toml
wget https://raw.githubusercontent.com/pundix/pundix/main/public/testnet/app.toml -O ~/.pundix/config/app.toml
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**IMPORTANT** At this stage **BEFORE** starting the node, please download the latest snapshot, refer to this [link](snapshot-guide.md).

And at this stage, what is important is your validator keys that is stored in a `.json` file for you to do a recovery in the future. For more [information](../../validators/validator-recovery.md) how to access the files.
{% endhint %}

* Run docker

```bash
docker run --name pundix -d --restart=always -p 26656:26656 -p 26657:26657 -p 1317:1317 -p 26660:26660 -v $HOME/.pundix:/root/.pundix ghcr.io/pundix/pundix:latest start
```

To check if pundix is synced:

```bash
docker exec -it pundix /bin/sh
# the docker name is pundix and CLI is pundixd
pundixd status
```

It will return something like this:

```bash
{
  "NodeInfo": {
    "protocol_version": {
      "p2p": 8,
      "block": 11,
      "app": 0
    },
    "id": "e62e783f567dff9f78c092c170f5902636c54fe2",
    "listen_addr": "tcp://0.0.0.0:26656",
    "network": "PUNDIX",
    "version": "release/v0.1.0-e5dda26dbdb1971704002bfc731f76db177d4922",
    "channels": "40202122233038606100",
    "moniker": "local",
    "other": {
      "tx_index": "on",
      "rpc_address": "tcp://0.0.0.0:26657"
    }
  },
  "SyncInfo": {
    "latest_block_hash": "576F5764F3F12AB54FAFCC81690F5652D21E1F39DFDD43ECAE9DD34BA52F4F0A",
    "latest_app_hash": "30D0F93166E4A5F3127F1434CE39DE663D775CCCFADEF2B080E71D987964AC2C",
    "latest_block_height": "926",
    "latest_block_time": "2022-09-02T06:08:34.464451878Z",
    "earliest_block_hash": "350B1B6341D5B190AB8F12137D14D8C1FD6A2FCA4B8620D30CBDE0166104570F",
    "earliest_app_hash": "E3B0C44298FC1C149AFBF4C8996FB92427AE41E4649B934CA495991B7852B855",
    "earliest_block_height": "1",
    "earliest_block_time": "2022-09-02T05:51:52.914224Z",
    "catching_up": false
  },
  "ValidatorInfo": {
    "Address": "B4E7FA9D1A617CDAF3D4B68E7C15748E49DA4554",
    "PubKey": {
      "key": "nthpdBmgr1fGMZ+DPt0qrDRZJPtopSWlq2OTsieYkq0="
    },
    "VotingPower": 1
  }
}
```

To ensure that the blocks are synced up with your node, under `"SyncInfo"`, `"catching_up"` should be false `"catching_up": false`. This may take a few hours and your node has to be fully synced up before proceeding to the next step. You may cross reference the latest block you are synced to `"SyncInfo": "latest_block_height"` and the latest block height of our Testnet blockchain on our [Testnet blockchain explorer](https://testnet-explorer.pundix.com/pundix/blocks) or our [Mainnet](https://explorer.pundix.com/pundix/proposals).

{% hint style="danger" %}
**Make sure that every node has a unique `priv_validator.json`. DO NOT copy the `priv_validator.json` from an old node to multiple new nodes. Running two nodes with the same `priv_validator.json` will cause you to double sign.**
{% endhint %}
