# CrossChain Precompiled

Address: `0x0000000000000000000000000000000000001004`

ABI: [ICrossChain](https://github.com/PundiAI/fx-core/blob/main/contract/icrosschain.sol.go#L34)

Overview: Use cross-chain precompiled contract to call some functions of the cross-chain module, such as: crossChain, etc.

## Method

### crossChain (Deprecated)

send token from Pundi AIFX to other chain, like ethereum, pundix, etc.

{% hint style="info" %}
if token is erc20, must be approved before calling this method
{% endhint %}

```solidity
// Deprecated: please use `IBridgeCall.bridgeCall`
function crossChain(
    address _token,
    string memory _receipt,
    uint256 _amount,
    uint256 _fee,
    bytes32 _target,
    string memory _memo
) external payable returns (result bool);
```

* `_token`: the token address on the Pundi AIFX([Tokens](../cross-chain/fx-core.md))
  * if token is origin token, \_token address is `0x0000000000000000000000000000000000000000`
* `_receipt`: the receipt address on the target chain
* `_amount`: the amount of the token to be cross chain
* `_fee`: the fee of the token to be cross chain
  * if cross chain to cosmos chain, \_fee is `0`
* `_target`: the target of the token on the target chain(more detail see [Target](../cross-chain/target.md)
  * \_target represents cross chain destination, such as chain `ethereum`, `pundix`
  * destination ethereum: \_target is `eth`
  * destination other cosmos chain(example Pundix): \_target is `ibc/{id}/{prefix}`.
    * `id` is the channel id of the target chain on Pundi AIFX(examples: Pundix: 0)
    * `prefix` is the address prefix of the target chain(examples: Pundix: px)
* `_memo`: the memo of cross chain

{% hint style="info" %}
\_target convert string to bytes, if less than 32, fill in 0 in behind, until 32 bytes
{% endhint %}

crossChain event

```solidity
event CrossChain(
    address indexed sender,
    address indexed token,
    string denom,
    string receipt,
    uint256 amount,
    uint256 fee,
    bytes32 target,
    string memo
);
```

* `sender`: the sender address
* `token`: the erc20 token address on the Pundi AIFX
* `denom`: the cross chain token denom
* `receipt`: the receipt address on the target chain
* `amount`: the amount of the token to be cross chain
* `fee`: the fee of the token to be cross chain
* `target`: the target of cross chain
* `memo`: the memo of cross chain
