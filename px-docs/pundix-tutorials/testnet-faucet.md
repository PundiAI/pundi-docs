# Testnet Faucet

## Request Funds

1. To request for Testnet PUNDIX click on this [link](https://payalebar-faucet.functionx.io/)
2. Input your address (be sure to choose the correct wallet type for the network you wish to receive funds in)
3. Choose from the dropdown the appropriate network and coin/token type

## Viewing your wallet balances

* You may view your balance on f(x)wallet which also allows for a more seamless way of transaction. You may download f(x)wallet from the Appstore or Google Play [here](https://download.functionx.io).
* Once downloaded, enter into the settings configuration, (the button is on the top right, there is a settings icon)
  * Under general/Network Configuration, ensure your PundiX is toggled to `Testnet`
* You may view your PUNDIX balance from the f(x)Wallet or the [PundiX Testnet Explorer](https://testnet.starscan.io/pundix/blocks)/[PundiX Mainnet Explorer](https://starscan.io/pundix/blocks).
* Alternatively, to `query` your validator account balance (token holding account):

```bash
pundixd q bank balances <token holding account public address>
```
