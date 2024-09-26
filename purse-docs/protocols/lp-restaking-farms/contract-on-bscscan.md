# Contract on BscScan

In this article, we will be explaining on the various functions in LP Restaking Farm contract. It's not encouraged for beginners to interact directly with the contract especially if you are not familiar. Head over to [How to Use Farms](how-to-use-farms.md) to learn how to stake LP Token and earn PURSE rewards.

## LP Token Pair Address

{% hint style="warning" %}
Please note that PURSE-BUSD has been deprecated.
{% endhint %}

In order to interact with the LP Restaking Farm contract, you will need the LP Token pair address.

| Pair       | Address                                    | Provider    |
| ---------- | ------------------------------------------ | ----------- |
| PURSE-USDT | 0xfc450e16016aF4e4197f5dB5Ca0d262fF8fD735a | PancakeSwap |

Address that you will also need:

* [LP Restaking Farm](https://bscscan.com/address/0x439ec8159740a9B9a579F286963Ac1C050aF31C8)

### Deposit LP Token to LP Restaking Farm Smart contract

1. Go to [PURSE-USDT LP Token](https://bscscan.com/address/0xfc450e16016aF4e4197f5dB5Ca0d262fF8fD735a) contract _Write Contract_ and under **1.approve**, enter the following: \
   spender: 0x439ec8159740a9b9a579f286963ac1c050af31c8 _(LP Restaking Farm address)_\
   value: `-1` _(No need to approve for the subsequent deposit)_

<figure><img src="../../.gitbook/assets/LPContractApprove.png" alt=""><figcaption><p>Approve LP Restaking Farm contract to spend your LP Token</p></figcaption></figure>

2\. Go to [LP Restaking Farm](https://bscscan.com/token/0x439ec8159740a9b9a579f286963ac1c050af31c8#writeProxyContract) contract _Write as Proxy_ and under **4.deposit**, enter the following:\
\_lpToken_:_ 0xfc450e16016aF4e4197f5dB5Ca0d262fF8fD735a _(PURSE-USDT LP Token)_\
\_amount: **Amount in Wei**

> You can convert LP Token to Wei using [BscScan Unit Converter](https://www.bscscan.com/unitconverter)

<figure><img src="../../.gitbook/assets/deposit.jpg" alt=""><figcaption><p>Depositing 5 LP Token to LP Restaking Farm</p></figcaption></figure>

3\. Click **Write** and confirm the transaction in your wallet.

4\. You can check your transaction by clicking **View your transaction**.

### Withdraw LP Token from LP Restaking Farm

1. Go to [LP Restaking Farm](https://bscscan.com/token/0x439ec8159740a9b9a579f286963ac1c050af31c8#writeProxyContract) contract _Write as Proxy_ and under **17.withdraw**, enter the following:\
   \_lpToken_:_ 0xfc450e16016aF4e4197f5dB5Ca0d262fF8fD735a _(PURSE-USDT LP Token)_\
   \_amount: **Amount in Wei**

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Withdrawing 5 LP Token from LP Restaking Farm</p></figcaption></figure>

3\. Click **Write** and confirm the transaction in your wallet.

4\. You can check your transaction by clicking **View your transaction**.

### **Making an emergency withdrawal**

‌Using the emergency withdraw function allows you to withdraw all your LP Token out from the farm but your PURSE rewards will be forfeited.

{% hint style="info" %}
**Using the emergency withdraw function will result in your PURSE rewards being forfeited! Do not use unless you have problem withdrawing LP Token.**
{% endhint %}

1. Go to [LP Restaking Farm](https://bscscan.com/token/0x439ec8159740a9b9a579f286963ac1c050af31c8#writeProxyContract) contract _Write as Proxy_ and under 5**.emergenctWithdraw**, enter the following:\
   \_lpToken_:_ 0xfc450e16016aF4e4197f5dB5Ca0d262fF8fD735a _(PURSE-USDT LP Token)_\


![PURSE Rewards will be forfeited if doing Emergency Withdrawal](../../.gitbook/assets/emergency.jpg)

3\. Click **Write** and confirm the transaction in your wallet.

4\. You can check your transaction by clicking **View your transaction**.
