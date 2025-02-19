# How the AI MM Agent Works in Detail

1. **Mempool Monitoring for Transaction Detection**

* The AI MM Agent continuously scans the **mempool** (pending transactions) to detect potential large trades or sudden changes in transaction patterns.&#x20;
* When it detects a **large transaction** or **flash loan activity**, the agent identifies the token pair (e.g., ETH/USDC or WBTC/USDC) and prepares to react within the same block.

2. **Dynamic Liquidity Adjustment**

* **Narrowing the Price Range:**
  * If the mempool reveals an upcoming large transaction, the agent narrows the price range of the LP position to ensure the trade fits within the range. This **minimizes MEV** (Maximal Extractable Value) risks and ensures that the AI MM Agent captures the fee instead of external arbitrage bots.
* **Enlarging the Price Range:**
  * In periods of **high volatility**, the agent adjusts the LP token price range to cover a wider spread, reducing the risk of impermanent loss while still maintaining adequate liquidity.

3. **Gas Optimization and Same-block Execution**

* The AI MM Agent is designed to **spend more gas** when necessary to execute critical operations within the **same block**, ensuring it stays ahead of MEV bots.
* **Pulling out and Re-depositing LP Tokens:**\
  When alerted by the mempool, the agent:
  1. Withdraws the LP position temporarily to avoid providing liquidity at an unfavorable price range.&#x20;
  2. Re-adjusts the price range for the LP tokens based on updated market conditions.&#x20;
  3. Re-inserts the liquidity back into the pool within the same block to maintain continuous market presence.

4. **Market Condition Analysis**
   * The agent leverages AI to analyze market indicators (e.g., ETH/USDC and WBTC/USDC price movements, volume spikes, and volatility).
   * It adapts the strategy to balance profitability, risk management, and MEV prevention.
5. **Continuous Profit Maximization**
   * Through active monitoring and dynamic adjustments, the AI MM Agent generates **higher fee revenue** while protecting its liquidity from arbitrage losses.
   * Profits from these operations are distributed back to **vePUNDIAI holders**, ensuring token holder incentives are aligned.
