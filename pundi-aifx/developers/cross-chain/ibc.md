# ibc

In IBC, blockchains do not directly pass messages to each other over the network. This is where relayer comes in. A relayer process monitors for updates on opens paths between sets of [IBC](https://ibcprotocol.org/) enabled chains. The relayer submits these updates in the form of specific message types to the counterparty chain. Clients are then used to track and verify the consensus state.

In addition to relaying packets, this relayer can open paths across chains, thus creating clients, connections and channels.

Additional information on how IBC works can be found [here](https://ibc.cosmos.network/).

## IBC Channels

{% tabs %}
{% tab title="Mainnet" %}
| source chain-id | destination             | destination chain-id    | source to destination channel | destination to source channel |
| --------------- | ----------------------- | ----------------------- | ----------------------------- | ----------------------------- |
| fxcore          | Pundix                  | PUNDIX                  | channel-0                     | channel-0                     |
| fxcore          | CosmosHub               | cosmoshub-4             | channel-10                    | channel-585                   |
| fxcore          | Osmosis                 | osmosis-1               | channel-19                    | channel-2716                  |
| fxcore          | Axelar                  | axelar-dojo-1           | channel-21                    | channel-136                   |
| fxcore          | Chihuahua               | chihuahua-1             | channel-22                    | channel-87                    |
{% endtab %}

{% tab title="Testnet" %}
| source chain-id | destination | destination chain-id    | source to destination channel | destination to source channel |
| --------------- | ----------- | ----------------------- | ----------------------------- | ----------------------------- |
| dhobyghaut      | Pundix      | payalebar               | channel-0                     | channel-0                     |
| dhobyghaut      | Cosmos      | theta-testnet-001       | channel-90                    | channel-2631                  |
| dhobyghaut      | Osmosis     | osmo-test-5             | channel-119                   | channel-4402                  |
| dhobyghaut      | Axelar      | axelar-testnet-lisbon-3 | channel-127                   | channel-398                   |
{% endtab %}
{% endtabs %}

## IBC Transfer

When transferring from an external cosmos chain to Pundi AIFX using ibc, if the token is registered in Pundi AIFX's erc20 module, the receiver address can be filled in with the ethereum address. In this case, the ibc module automatically converts the ibc token to the ERC20 token and transfers it to the ethereum address in the Pundi AIFX's evm

## Channel Selection

If the token belongs to the osmosis chain, cross chain to Pundi AIFX, directly through Pundi AIFX and osmosis channel, such as OSMO, ATOM/OSMO; if it is a token of other chains, it needs to transfer through cosmos-hub, and then cross chain to Pundi AIFX. for example EVMOS, first crosses chain to cosmos-hub and then through cosmos-hub crosses chain to Pundi AIFX
