# BridgeCall Interface Documentation

## Overview
The `bridgeCall` function is a precompiled contract method that facilitates cross-chain calls. It allows users to send assets and data to a destination chain while specifying execution details.

## Contract Address
**Precompiled Contract Address:** `0x0000000000000000000000000000000000001004`

## ABI Reference
[IBridgeCall ABI](https://github.com/PundiAI/fx-core/blob/main/contract/ibridgecall.sol.go#L34)

## Solidity Interface
[IBridgeCall Solidity](https://github.com/PundiAI/fx-core/blob/main/solidity/contracts/interfaces/IBridgeCall.sol)

---

## Function: `bridgeCall`

```solidity
function bridgeCall(
  string memory _dstChain,
  address _refund,
  address[] memory _tokens,
  uint256[] memory _amounts,
  address _to,
  bytes memory _data,
  uint256 _quoteId,
  uint256 _gasLimit,
  bytes memory _memo
) external payable returns (uint256 _eventNonce);
```

### Description
This function initiates a cross-chain transaction by transferring tokens and executing optional calldata on the destination chain.

### Parameters
- `_dstChain` (`string`): The target blockchain identifier where the transaction should be executed.
- `_refund` (`address`): The address to receive any refund if the transaction fails.
- `_tokens` (`address[]`): List of token addresses to be transferred.
- `_amounts` (`uint256[]`): Corresponding amounts of tokens to be transferred.
- `_to` (`address`): The recipient address on the destination chain.
- `_data` (`bytes`): Arbitrary calldata to be executed on the destination chain.
- `_quoteId` (`uint256`): Identifier for a precomputed fee quote.
- `_gasLimit` (`uint256`): Gas limit for execution on the destination chain.
- `_memo` (`bytes`): Additional metadata or message for the transaction.

### Return Value
- `_eventNonce` (`uint256`): A unique event nonce assigned to this transaction, used for tracking purposes.

### Usage Example
```solidity
IBridgeCall(0x0000000000000000000000000000000000001004).bridgeCall(
    "chainB", // Destination chain
    msg.sender, // Refund address
    [tokenA, tokenB], // Tokens to transfer
    [100 * 1e18, 200 * 1e18], // Amounts to transfer
    recipientAddress, // Destination address
    "0x", // No calldata
    12345, // Quote ID
    500000, // Gas limit
    "0x" // No memo
);
```

### Notes
- The caller must ensure they have sufficient token balances and approval for the contract to transfer tokens.
- The `_quoteId` should be obtained beforehand through a quoting mechanism.
- Refunds, if applicable, will be sent to `_refund`.
- `_gasLimit` should be set appropriately to cover execution costs on the destination chain.
- The `_eventNonce` can be used for tracking the transaction status.

---

## Related Links
- [FxCore GitHub Repository](https://github.com/PundiAI/fx-core)
- [IBridgeCall Solidity Interface](https://github.com/PundiAI/fx-core/blob/main/solidity/contracts/interfaces/IBridgeCall.sol)
- [Precompiled Contract ABI](https://github.com/PundiAI/fx-core/blob/main/contract/ibridgecall.sol.go#L34)
