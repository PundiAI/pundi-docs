# PURSE Staking Rewards

### Rewards Algorithm

PURSE Staking uses a new algorithm to distribute a fixed reward pool among stakers according to their time-weighted contributions to the PURSE Staking pool. It integrates two new contracts: Distributor and Treasury, to facilitate this new rewards mechanism.

Staking rewards ($$R_{staking}$$) are calculated based on the time lapse since the last distribution to the Treasury by the Distributor. This is measured against the current block timestamp, and the designated number of reward tokens for each time interval.

$$
R_{staking} = R_{interval} * (T_{block \ timestamp} \ - \ T_{last \ distribution})
$$

The Distributor periodically sends the accrued staking rewards to the Treasury. And this distribution is accomplished whenever a user interacts with the PURSE Staking ecosystem through state changing functions like staking/withdrawing PURSE and claiming rewards. Transactions initiated by these functions will update the last distribution time to the current block time, ensuring precise computation of rewards for the staking pool.

The staking pool uses a `cumulativeRewardPerToken` storage variable to track the total amount of rewards that have been accumulated per unit of PURSE since the rewards distribution started. Every time there is a state changing transaction, the staking rewards is calculated and divided by the total supply staked ($$S_{total}$$), and this value is added to the `cumulativeRewardPerToken` accumulator. As this process gets repeated every time a transaction occurs, this variable shows how much rewards have been accumulated from the staked PURSE.

$$
cumulativeRewardPerToken = cumulativeRewardPerToken \ + \ \frac{R_{staking}}{S_{total}}
$$

To accurately calculate the rewards owed to each user who has staked in the pool, every user now has a `previousCumulatedRewardPerToken` variable which keeps track of the value of the `cumulativeRewardPerToken` at the point of a user's last interaction with the staking ecosystem - such as the time they stake, unstake, or claim rewards.

In calculating a user's rewards ($$R_{user}$$), the current `cumulativeRewardPerToken` is contrasted with the user's `previousCumulatedRewardPerToken` to ascertain the accrued rewards since the user's last interaction. The difference ($$\Delta CRPT$$), which represents the proportional reward rate, is then multiplied by the amount of PURSE the user has staked ($$S_{user}$$), ensuring that rewards are proportional to each user's stake in the pool.

$$
R_{user} = \Delta CRPT \ * S_{user}
$$

Rewards are not automatically distributed to users whenever a state chainging function occurs. This would be gas heavy and highly impractical; imagine having to send rewards to every single user who has staked in the pool whenever someone executes a state changing transaction, this person would also have to bear the gas cost for sending rewards to everyone else!

Instead, each user's rewards remain in the ecosystem and accumulate continuously until the user decides to claim them at their discretion. Upon claiming, the user receives all accumulated rewards up to that point, and their claimable reward balance is reset to zero. If the user maintains their PURSE stake in the pool, rewards will continue to accumulate based on that staked amount. Without an active stake, no further rewards will accrue. Likewise, if a user exits the staking pool completely and have claimable rewards remaining in the ecosystem, that amount will not continue to accrue.
