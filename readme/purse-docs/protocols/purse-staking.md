# PURSE Staking

## Introduction

{% hint style="warning" %}
PURSE's BDL mechanism has been retired as of late September 2023.
{% endhint %}

PURSE staking allows users to earn more with their PURSE tokens and it is particularly beneficial for PURSE token holders who do not want to provide liquidity to the liquidity pool. It’s the most direct opportunity to earn on the platform as there is no impermanent loss.

To learn more about PURSE Staking rewards, visit the rewards [page](purse-staking-rewards/).

Users will have **two ways** to earn PURSE tokens:

1\. PURSE-USDT Liquidity

2\. PURSE Staking

### PURSE Staking Mechanism

Users will receive a share amount whenever they stake, and this share amount represents a user's proportional stake in the staking pool. They indicate how much of the pool's resources and potential rewards are attributed to the user.

To withdraw the staked PURSE, users are required to use the shares they own to withdraw an equivalent amount of PURSE from the staking pool.&#x20;

_**The share amount is calculated based on the ratio of the Staked Amount and the Total Staked Amount, multiplied by the Total Share Amount; and how much PURSE the user with an active stake is able to withdraw is calculated based on the ratio of the Share Withdrawal Amount and the Total Share Amount, multiplied by the Total Staked Amount.**_

#### Example

* Block 1: Alice stakes 5 PURSE, she will receive 5 Share (Share = PURSE)
* Block 2: Incoming distribution tokens of 10 PURSE
* Block 3: Bob stakes 15 PURSE, he will have receive 5 Share (Share = 15 / 15 x 5 = 5)
* Block 4: Incoming distribution tokens of 10 PURSE
* Block 5: Alice withdraw 2 Share, she will receive 8 PURSE (PURSE = 2 / 10 x 40 = 8)
* Block 6: Incoming distribution tokens of 18 PURSE
* Block 7: Bob withdraw 4 Share, he will receive 25 PURSE (PURSE = 4 / 8 x 50 = 25)

### PURSE Staking 21-Day Lock

PURSE withdrawn from PURSE Staking will be locked for a 21-day period in the vesting contract. These funds will be retrievable after the 21-day lock period.

Each time a user withdraw's PURSE from PURSE Staking, a vesting schedule will be created for the user's withdrawal in the Vesting contract. Each withdrawal does not aggregate with one another and are created as individual vesting schedules. Users can only retrieve the withdrawn amounts of PURSE at the end of a vesting schedule.

Simply:

1. Alice withdraws 10 PURSE from PURSE Staking, a 21-day vesting schedule will be created for Alice for 10 PURSE.
2. The next day, Alice decides to withdraw 1000 PURSE from PURSE Staking, another 21-day vesting schedule will be created for Alice for 1000 PURSE.
3. 21 days after the first schedule, Alice can only retrieve 10 PURSE, but not the other 1000 PURSE.
4. 21 days after the second schedule, Alice can retrieve 1000 PURSE, and the other 10 PURSE if she hasn't retrieved it since the completion of the previous vesting schedule.

{% hint style="info" %}
The section below describes the old withdrawal mechanism used by PURSE Staking. It is no longer in effect.
{% endhint %}

#### Withdrawing PURSE using Locked Share

If users un-stake the PURSE using the locked share when there’s already an existing un-staking entry, the lock period will **reset** back to 21 days. In addition, the un-staked PURSE will **not earn** any reward during this 21-Day period.

For users who have unclaimed PURSE with reward after the 21-Day period, they will have to **withdraw it manually** or it will be **withdrawn automatically when users un-stake**.

#### **Withdrawing PURSE using Unlocked Share**

For the share that users have received when staking into the previous non-upgraded contract, they will be able to withdraw the original staked PURSE with reward **anytime** without the 21-Day Lock.

#### **Withdrawing PURSE using both Unlocked and Locked Share**

The PURSE for unlocked **share will be withdrawn out first without the 21-Day Lock** and the remaining PURSE for locked share will be un-staked and locked for 21 days.

#### **Example:**

1\. Alice has a total of 10 Share (5 Unlocked Share and 5 Locked Share)

2\. Alice un-stake 8 Share (5 Unlocked Share and 3 Locked Share)

3\. PURSE for the 5 Unlocked Share will be transferred instantly to Alice and remaining PURSE for Locked Share will be locked for 21 days.
