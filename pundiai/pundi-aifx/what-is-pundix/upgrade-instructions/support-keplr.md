# Support keplr

Add [Suggest Chain](https://docs.keplr.app/api/suggest-chain.html)

1. [Install Keplr browser extension.](https://www.keplr.app/download)
2. Open the browser console
3. Run the code below

{% tabs %}
{% tab title="Mainnet" %}
```javascript
await window.keplr.experimentalSuggestChain({
    chainId: "PUNDIX",
    chainName: "Pundi X Chain",
    rpc: "https://px-json.pundix.com:26657",
    rest: "https://px-rest.pundix.com",
    walletUrl: "https://starscan.io/pundix/validators",
    walletUrlForStaking: "https://starscan.io/pundix/validators",
    bip44: {
        coinType: 118,
    },
    bech32Config: {
        bech32PrefixAccAddr: "px",
        bech32PrefixAccPub: "pxpub",
        bech32PrefixValAddr: "pxvaloper",
        bech32PrefixValPub: "pxvaloperpub",
        bech32PrefixConsAddr: "pxvalcons",
        bech32PrefixConsPub: "pxvalconspub",
    },
    currencies: [
        {
            coinDenom: "PUNDIX",
            coinMinimalDenom: "ibc/55367B7B6572631B78A93C66EF9FDFCE87CDE372CC4ED7848DA78C1EB1DCDD78",
            coinDecimals: 18,
            coinGeckoId: "pundi-x-2",
            coinImageUrl: "https://raw.githubusercontent.com/pundix/keplr-chain-registry/add-pundix-chain/images/pundix/pundi-x-token.png",
        },
        {
            coinDenom: "PURSE",
            coinMinimalDenom: "bsc0x29a63F4B209C29B4DC47f06FFA896F32667DAD2C",
            coinDecimals: 18,
            coinGeckoId: "pundi-x-purse",
            coinImageUrl: "https://raw.githubusercontent.com/pundix/keplr-chain-registry/add-pundix-chain/images/pundix/purse-token.png",
        }
    ],
    feeCurrencies: [
        {
            coinDenom: "PUNDIX",
            coinMinimalDenom: "ibc/55367B7B6572631B78A93C66EF9FDFCE87CDE372CC4ED7848DA78C1EB1DCDD78",
            coinDecimals: 18,
            coinGeckoId: "pundi-x-2",
            coinImageUrl: "https://raw.githubusercontent.com/pundix/keplr-chain-registry/add-pundix-chain/images/pundix/pundi-x-token.png",
            gasPriceStep: {
                low: 2000000000000,
                average: 2500000000000,
                high: 3000000000000,
            },
        },
    ],
    stakeCurrency: {
        coinDenom: "PUNDIX",
        coinMinimalDenom: "ibc/55367B7B6572631B78A93C66EF9FDFCE87CDE372CC4ED7848DA78C1EB1DCDD78",
        coinDecimals: 18,
        coinGeckoId: "pundi-x-2",
        coinImageUrl: "https://raw.githubusercontent.com/pundix/keplr-chain-registry/add-pundix-chain/images/pundix/pundi-x-token.png",
    },
});
```
{% endtab %}

{% tab title="Testnet" %}
```javascript
await window.keplr.experimentalSuggestChain({
    chainId: "payalebar",
    chainName: "Pundi X Chain Testnet",
    rpc: "https://testnet-px-json.pundix.com:26657",
    rest: "https://testnet-px-rest.pundix.com",
    walletUrl: "https://testnet.starscan.io/pundix/validators",
    walletUrlForStaking: "https://testnet.starscan.io/pundix/validators",
    bip44: {
        coinType: 118,
    },
    bech32Config: {
        bech32PrefixAccAddr: "px",
        bech32PrefixAccPub: "pxpub",
        bech32PrefixValAddr: "pxvaloper",
        bech32PrefixValPub: "pxvaloperpub",
        bech32PrefixConsAddr: "pxvalcons",
        bech32PrefixConsPub: "pxvalconspub",
    },
    currencies: [
        {
            coinDenom: "PUNDIX",
            coinMinimalDenom: "ibc/169A52CA4862329131348484982CE75B3D6CC78AFB94C3107026C70CB66E7B2E",
            coinDecimals: 18,
            coinGeckoId: "pundi-x-2",
            coinImageUrl: "https://raw.githubusercontent.com/pundix/keplr-chain-registry/add-pundix-chain/images/pundix/pundi-x-token.png",
        },
        {
            coinDenom: "PURSE",
            coinMinimalDenom: "bsc0x0BEdB58eC8D603E71556ef8aA4014c68DBd57AD7",
            coinDecimals: 18,
            coinGeckoId: "pundi-x-purse",
            coinImageUrl: "https://raw.githubusercontent.com/pundix/keplr-chain-registry/add-pundix-chain/images/pundix/purse-token.png",
        }
    ],
    feeCurrencies: [
        {
            coinDenom: "PUNDIX",
            coinMinimalDenom: "ibc/169A52CA4862329131348484982CE75B3D6CC78AFB94C3107026C70CB66E7B2E",
            coinDecimals: 18,
            coinGeckoId: "pundi-x-2",
            coinImageUrl: "https://raw.githubusercontent.com/pundix/keplr-chain-registry/add-pundix-chain/images/pundix/pundi-x-token.png",
            gasPriceStep: {
                low: 2000000000000,
                average: 2500000000000,
                high: 3000000000000,
            },
        },
    ],
    stakeCurrency: {
        coinDenom: "PUNDIX",
        coinMinimalDenom: "ibc/169A52CA4862329131348484982CE75B3D6CC78AFB94C3107026C70CB66E7B2E",
        coinDecimals: 18,
        coinGeckoId: "pundi-x-2",
        coinImageUrl: "https://raw.githubusercontent.com/pundix/keplr-chain-registry/add-pundix-chain/images/pundix/pundi-x-token.png",
    },
})
```
{% endtab %}
{% endtabs %}
