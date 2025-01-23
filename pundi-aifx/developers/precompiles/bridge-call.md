# BridgeCall Precompiled

Address: `0x0000000000000000000000000000000000001004`

ABI: [IBridgeCall](https://github.com/PundiAI/fx-core/blob/main/contract/ibridgecall.sol.go#L34)

Solidity: [IBridgeCall](https://github.com/PundiAI/fx-core/blob/main/solidity/contracts/interfaces/IBridgeCall.sol)

## Method

### bridgeCall

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
