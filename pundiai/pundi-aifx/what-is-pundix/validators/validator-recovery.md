# Validator Recovery

Run the following command to open the `priv_validator_key.json` file and store it somewhere for safe keeping:

{% hint style="danger" %}
**Do ensure that you have a back-up `priv_validator_key.json` file and that it is stored safely! Overriding this `priv_validator_key.json`file and you would have lost your consensus private key and your validator if you have one set up. DO NOT OVERRIDE THIS FILE.**
{% endhint %}

If you are in the `PundiX` dir, run this command:

```bash
cat ../.pundix/config/priv_validator_key.json

# this will be your private key to recovery your validator
{
  "address": "XXXXXXXXXXXXXXXXXXxxxxxxxXXXXXX",
  "pub_key": {
    "type": "tendermint/PubKeyEd25519",
    "value": "XXXXXXXXXXXXXXXXXXxxxxxxxXXXXXX"
  },
  "priv_key": {
    "type": "tendermint/PrivKeyEd25519",
    "value": "XXXXXXXXXXXXXXXXXXxxxxxxxXXXXXX"
  }}
```

The directory tree of the .pundix directory should look like this:

```bash
tree $HOME/.pundix

# it will look like this
/home/ubuntu/.pundix
├── config
│   ├── app.toml
│   ├── config.toml
│   ├── genesis.json
│   ├── node_key.json
│   └── priv_validator_key.json
└── data
    └── priv_validator_state.json
2 directories, 6 files
```

The command after `Initializing PundiX` from setting up node with [Full node with Binaries](https://github.com/FunctionX-SG/pundiai-docs/blob/main/px-docs/getting-started/setup-node/full-node-with-binaries.md) or [Full node with Docker](https://github.com/FunctionX-SG/pundiai-docs/blob/main/px-docs/getting-started/setup-node/full-node-with-docker.md) is to override the various files that were initialized earlier:

{% tabs %}
{% tab title="Binaries" %}
```
wget https://raw.githubusercontent.com/pundix/pundix/release/main/public/testnet/genesis.json -O ~/.pundix/config/genesis.json
wget https://raw.githubusercontent.com/pundix/pundix/release/main/public/testnet/config.toml -O ~/.pundix/config/config.toml
wget https://raw.githubusercontent.com/pundix/pundix/release/main/public/testnet/app.toml -O ~/.pundix/config/app.toml
```
{% endtab %}

{% tab title="Docker" %}
```
wget https://raw.githubusercontent.com/pundix/pundix/release/main/public/mainnet/genesis.json -O ~/.pundix/config/genesis.json
wget https://raw.githubusercontent.com/pundix/pundix/release/main/public/mainnet/config.toml -O ~/.pundix/config/config.toml
wget https://raw.githubusercontent.com/pundix/pundix/release/main/public/mainnet/app.toml -O ~/.pundix/config/app.toml
```
{% endtab %}
{% endtabs %}

The key file here is `priv_validator_key.json`. After initializing and overriding those files, override the `priv_validator_key.json` with your original `priv_validator_key.json` of the validator you want to recover. You may do this by following the command below (if you are in `.pundix/config` directory):

```bash
cat > priv_validator_key.json
```

Hit the <mark style="color:red;background-color:blue;">ENTER</mark> button on your keyboard and `copy` and `paste` the contents of your `priv_validator_key.json` file from your original validator into the command line

Your command line should look something like this:

```bash
cat > priv_validator_key.json

# this will be your private key to recovery your validator
{
  "address": "XXXXXXXXXXXXXXXXXXxxxxxxxXXXXXX",
  "pub_key": {
    "type": "tendermint/PubKeyEd25519",
    "value": "XXXXXXXXXXXXXXXXXXxxxxxxxXXXXXX"
  },
  "priv_key": {
    "type": "tendermint/PrivKeyEd25519",
    "value": "XXXXXXXXXXXXXXXXXXxxxxxxxXXXXXX"
  }
}
```

Then hit the <mark style="color:red;background-color:blue;">ENTER</mark> button on your keyboard before using <mark style="color:red;background-color:blue;">Ctrl+D</mark> on your keyboard, your file with the above contents will be created.

Run the following command and compare if the public key you generate now matches the old public key. If it does, then you have successfully recovered your original validator.

```
pundixd tendermint show-validator
```
