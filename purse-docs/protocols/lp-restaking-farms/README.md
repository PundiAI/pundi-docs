# LP Restaking Farms

LP Restaking Farms allow users to earn PURSE by staking LP Token. Currently, a total of 2 Billion PURSE token was burnt from the liquidity reserve to support this PURSE Liquidity Mining Program.

1. Liquidity Mining Program [Part 1](https://medium.com/pursetoken/introducing-purse-liquidity-mining-program-bcefae120f0e)
2. Liquidity Mining Program [Part 2](https://medium.com/pursetoken/purse-liquidity-mining-program-part-2-b7d3de3bbe9f)

Check out on [How to Use Farms ](https://docs.pancakeswap.finance/products/yield-farming/how-to-use-farms)to get started with farming.

{% hint style="info" %}
Yield farming comes with a risk of **Impermanent Loss**. It’s not as scary as it sounds and it is worth learning about the concept before you get started.

Check out this great article about [Impermanent Loss ](https://academy.binance.com/en/articles/impermanent-loss-explained)from Binance Academy to learn more.
{% endhint %}

## PURSE Reward Token

All the PURSE reward token minted by this Restaking Farm will be pre-burn first to ensure the total supply of PURSE remains stable.&#x20;

There will be cap reward token (_Farm's Cap Reward Token_) for Restaking Farm and once the minted reward token amount (_Farm's Minted Reward Token_) reaches the cap, the contract will stop minting any new PURSE reward token. However, we will extend the PURSE Liquidity Mining Program, depending on the response from the community, such that new PURSE reward token can continuously be minted.

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-29 at 4.55.14 PM.png" alt=""><figcaption></figcaption></figure>

## Reward Calculations

Yield Farming APR calculations include both:

* **LP Reward APR** - Earned through providing liquidity on Dexes (E.g. PURSE and BUSD on PancakeSwap).
* **Farm Reward APR** - Earned through staking LP Token in the Farm.

Total APR = Farm Reward APR + LP Reward APR

### How do we calculate the APR?

#### 1. Calculating Farm Reward APR

The **Farm Reward APR** is calculated based on the formula below:

> Farm Reward APR = 28000 x 365 x PURSE Per Block x Bonus Multiplier x PURSE Token Price x 100% / TVL of Farm

For example:&#x20;

* Alice deposit 20 LP token into farmA.
* Total LP token deposited to farmA is 100.
* Given that PURSE Per Block of farmA is 200 and Bonus Multiplier of farmA is 10.&#x20;
* For each block, Alice receives 200 \* 10 \* (20/100) = 400 PURSE
* APR = 28000 \* 365 \* 200 \* 10 \* _PURSE Token Price_ \* 100% / _TVL of Farm_

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-29 at 4.56.44 PM.png" alt=""><figcaption></figcaption></figure>

#### 2. Calculating LP Reward APR

On top of farm reward, farmers receive **LP Reward** for providing liquidity to PancakeSwap liquidity pool. Here is an example of calculating **LP Reward APR**:

<figure><img src="../../.gitbook/assets/PancakeSwapTopPool.png" alt=""><figcaption><p>PancakeSwap Top Pool</p></figcaption></figure>

As shown in the BTCB/BUSD pair above:

**Volume 24H**: $9.68M\
**Volume 7D**: $13.88M\
**LP Reward Fees 24H**: $16.46K\
**LP Reward APR**: 2.90%\
**Liquidity**: $42.47M

{% hint style="info" %}
LP Reward Fees 24H can be calculated using the 0.17% trading fee structure:

LP Reward Fees 24H = Volume 24H \* 0.17% = 9.68M \* 0.17 / 100 = **$16.26K**

Details on [PancakeSwap Liquidity Pool](https://docs.pancakeswap.finance/products/pancakeswap-exchange/pancakeswap-pools)
{% endhint %}

1. Calculate the yearly LP Reward fees
   * Using the **LP Reward Fees 24H** to estimate the projected yearly LP Reward fees:\
     $16.46K \* 365 = $6,007,900
2. Calculate the LP Reward APR using **yearly LP Reward fees**
   * Yearly LP Reward Fees / Liquidity\
     \= $6,007,900 / 42,470,000 x 100%\
     \= **14.15%**
