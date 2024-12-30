# ibc

In IBC, blockchains do not directly pass messages to each other over the network. This is where relayer comes in. A relayer process monitors for updates on opens paths between sets of [IBC](https://ibcprotocol.org/) enabled chains. The relayer submits these updates in the form of specific message types to the counterparty chain. Clients are then used to track and verify the consensus state.

In addition to relaying packets, this relayer can open paths across chains, thus creating clients, connections and channels.

Additional information on how IBC works can be found [here](https://ibc.cosmos.network/).

## IBC Channels

{% tabs %}
{% tab title="Mainnet" %}
| source chain-id | destination | destination chain-id | source to destination channel | destination to source channel |
| --------------- | ----------- | -------------------- | ----------------------------- | ----------------------------- |
| PUNDXI          | f(x)Core    | fxcore               | channel-0                     | channel-0                     |
| PUNDXI          | Osmosis     | osmosis-1            | channel-1                     | channel-12618                 |
{% endtab %}

{% tab title="Testnet" %}
| source chain-id | destination | destination chain-id | source to destination channel | destination to source channel |
| --------------- | ----------- | -------------------- | ----------------------------- | ----------------------------- |
| payalebar       | f(x)Core    | dhobyghaut           | channel-0                     | channel-0                     |
| payalebar       | Osmosis     | osmo-test-5          | channel-3                     | channel-7744                  |
{% endtab %}
{% endtabs %}
