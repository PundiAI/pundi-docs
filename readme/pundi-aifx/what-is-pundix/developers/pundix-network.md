---
description: >-
  The documentation corresponding contains details for the RPC - HTTP, WS and
  GRPC endpoints
---

# Pundi X Network

PundiX supports different clients in order to support Cosmos transactions and queries

| <p><br></p>                                  | Description                                                               | Default Port |
| -------------------------------------------- | ------------------------------------------------------------------------- | ------------ |
| **Cosmos gRPC**                              | Query or send PundiX transactions using gRPC                              | `9090`       |
| **Cosmos restAPI**                           | Query or send PundiX transactions using restAPI                           | `1317`       |
| **Tendermint** [**RPC**](pundix-json-rpc.md) | Subscribe to PundiX logs and events emitted in smart contracts.           | `26657`      |
| **Tendermint Websocket**                     | Query transactions, blocks, consensus state, broadcast transactions, etc. | `26657`      |

Various clients, tools and end points available

{% tabs %}
{% tab title="PundiX Mainnet" %}
|                    |                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------ |
| ChainId            | `PUNDIX`                                                                             |
| Native Coin        | `ibc/55367B7B6572631B78A93C66EF9FDFCE87CDE372CC4ED7848DA78C1EB1DCDD78`(PUNDIX Token) |
| Mint Coin          | `bsc0x29a63F4B209C29B4DC47f06FFA896F32667DAD2C`(PURSE Token)                         |
| Block Explorer     | [https://starscan.io/pundix/blocks](https://starscan.io/pundix/blocks)               |
| JSON RPC           | https://px-json.pundix.com:26657                                                     |
| JSON RPC Websocket | wss://px-json.pundix.com:26657/websocket                                             |
| gRPC               | https://px-grpc.pundix.com:9090                                                      |
| REST API           | https://px-rest.pundix.com                                                           |
{% endtab %}

{% tab title="PundiX Testnet" %}
|                    |                                                                                            |
| ------------------ | ------------------------------------------------------------------------------------------ |
| ChainId            | `payalebar`                                                                                |
| Native Coin        | `ibc/169A52CA4862329131348484982CE75B3D6CC78AFB94C3107026C70CB66E7B2EPUNDIX`(PUNDIX Token) |
| Mint Coin          | `bsc0x0BEdB58eC8D603E71556ef8aA4014c68DBd57AD7`(PURSE Token)                               |
| Block Explorer     | [https://testnet.starscan.io/pundix/blocks](https://testnet.starscan.io/pundix/blocks)     |
| JSON RPC           | https://testnet-px-json.pundix.com:26657                                                   |
| JSON RPC Websocket | wss://testnet-px-json.pundix.com:26657/websocket                                           |
| gRPC               | https://testnet-px-grpc.pundix.com:9090                                                    |
| REST API           | https://testnet-px-rest.pundix.com                                                         |
| Testnet Faucet     | [https://payalebar-faucet.functionx.io/](https://payalebar-faucet.functionx.io/)           |
{% endtab %}
{% endtabs %}
