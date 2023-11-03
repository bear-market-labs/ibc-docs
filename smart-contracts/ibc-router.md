# IBC Router

The IBC Router contract is the point of interaction for most users of IBCs. This contract routes IBC interactions to contracts of the relevant reserve asset and ibAsset.&#x20;



## State-Changing Functions

### `Execute`

```solidity
function execute(
    address recipient, 
    address curve, 
    bool useNative, 
    CommandType command, 
    bytes memory data
) external payable
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type        | Description                                                   |
| --------- | ----------- | ------------------------------------------------------------- |
| recipient | address     | Address to receive resulting tokens                           |
| curve     | address     | Contract address of the curve contract to be interacting with |
| useNative | bool        | Whether the interaction uses native ETH                       |
| command   | CommandType | Command type                                                  |
| data      | bytes       | Calldata of function call                                     |

#### CommandType

```solidity
enum CommandType {
    BUY_TOKEN,
    SELL_TOKEN,
    ADD_LIQUIDITY,
    REMOVE_LIQUIDITY,
    CLAIM_REWARD, 
    STAKE, 
    UNSTAKE
}
```

| Parameter         | Description                                      |
| ----------------- | ------------------------------------------------ |
| BUY\_TOKEN        | Command is to mint ibAssets                      |
| SELL\_TOKEN       | Command is to burn ibAssets                      |
| ADD\_LIQUIDITY    | Command is to add liquidity to the IBC           |
| REMOVE\_LIQUIDITY | Command is to remove liquidity from the IBC      |
| CLAIM\_REWARD     | Command is to claim LP & ibAsset staking rewards |
| STAKE             | Command is to stake ibAssets                     |
| UNSTAKE           | Command is to unstake ibAssets                   |
{% endtab %}
{% endtabs %}
