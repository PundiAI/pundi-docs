---
description: >-
  The documentation corresponding contains details for the RPC - HTTP, WS and
  GRPC endpoints
---

# Pundi AIFX Network

#### Pundi AIFX supports different clients in order to support Cosmos and Ethereum/Web3 transactions and queries

|                                                            | Description                                                                  | Default Port |
|------------------------------------------------------------|------------------------------------------------------------------------------|--------------|
| **Cosmos gRPC**                                            | Query or send Pundi AIFX transactions using gRPC                             | `9090`       |
| **Cosmos restAPI**                                         | Query or send Pundi AIFX transactions using restAPI                          | `1317`       |
| **Web3** [**JSON-RPC**](web3/)                             | Query Web3-formatted transactions and blocks or send Web3 txs using JSON-RPC | `8545`       |
| **Web3 Websocket**                                         | Subscribe to Web3 logs and events emitted in smart contracts.                | `8546`       |
| **Tendermint** [**RPC**](jsonrpc-api.md)                   | Subscribe to Pundi AIFX logs and events emitted in smart contracts.          | `26657`      |
| **Tendermint Websocket**                                   | Query transactions, blocks, consensus state, broadcast transactions, etc.    | `26657`      |
| **Command Line Interface** ([**CLI**](../installation.md)) | Query or send Pundi AIFX transactions using your Terminal or Console.        | N/A          |

#### Various clients, tools and end points available

{% hint style="info" %}
<mark style="color:yellow;">For adding custom network to MetaMask/Defi Wallet, please use the</mark> <mark style="color:yellow;">`Web3 JSON RPC`</mark>
{% endhint %}

{% tabs %}
{% tab title="Pundi AIFX Mainnet" %}
|                         |                                                                                                          |
| ----------------------- | -------------------------------------------------------------------------------------------------------- |
| ChainId                 | `fxcore`                                                                                             |
| Native Coin             | `apundiai`                                                                                               |
| Block Explorer          | [https://pundiscan.io](https://pundiscan.io)                                             |
| Tm JSON RPC             | [https://fx-json.functionx.io:26657](https://fx-json.functionx.io:26657)                 |
| Tm JSON RPC Websocket   | [wss://fx-json.functionx.io:26657/websocket](wss://fx-json.functionx.io:26657/websocket) |
| gRPC                    | [https://fx-grpc.functionx.io:9090](https://fx-grpc.functionx.io:9090)                   |
| Rest                    | [https://fx-rest.functionx.io:1317](https://fx-rest.functionx.io:1317)                   |
| EVM ChainID             | 530                                                                                      |
| EVM Block Explorer      | [https://pundiscan.io/evm](https://pundiscan.io/evm)                                     |
| Web3 JSON RPC           | [https://fx-json-web3.functionx.io:8545](https://fx-json-web3.functionx.io:8545)         |
| Web3 JSON RPC Websocket | [wss://fx-json-web3.functionx.io:8546](wss://fx-json-web3.functionx.io:8546)             |
| Testnet Faucet          | [https://faucet.functionx.io/](https://faucet.functionx.io/)                             |
{% endtab %}

{% tab title="Pundi AIFX Testnet" %}
|                         |                                                                                                          |
|-------------------------|----------------------------------------------------------------------------------------------------------|
| ChainId                 | `dhobyghaut`                                                                                             |
| Native Coin             | `apundiai`                                                                                               |
| Block Explorer          | [https://testnet.pundiscan.io](https://testnet.pundiscan.io)                                             |
| Tm JSON RPC             | [https://testnet-fx-json.functionx.io:26657](https://testnet-fx-json.functionx.io:26657)                 |
| Tm JSON RPC Websocket   | [wss://testnet-fx-json.functionx.io:26657/websocket](wss://testnet-fx-json.functionx.io:26657/websocket) |
| gRPC                    | [https://testnet-fx-grpc.functionx.io:9090](https://testnet-fx-grpc.functionx.io:9090)                   |
| Rest                    | [https://testnet-fx-rest.functionx.io:1317](https://testnet-fx-rest.functionx.io:1317)                   |
| EVM ChainID             | 90001                                                                                                    |
| EVM Block Explorer      | [https://testnet.pundiscan.io/evm](https://testnet.pundiscan.io/evm)                                     |
| Web3 JSON RPC           | [https://testnet-fx-json-web3.functionx.io:8545](https://testnet-fx-json-web3.functionx.io:8545)         |
| Web3 JSON RPC Websocket | [wss://testnet-fx-json-web3.functionx.io:8546](wss://testnet-fx-json-web3.functionx.io:8546)             |
| Testnet Faucet          | [https://testnet-faucet.functionx.io/](https://testnet-faucet.functionx.io/)                             |
{% endtab %}
{% endtabs %}
