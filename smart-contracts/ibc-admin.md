# IBC Admin

The IBC Admin contract is where protocol configuration changes are made. Fee configuration updates as well as contract upgrades and pauses are managed through this contract.&#x20;



## Events

### `FeeConfigChanged`

Emitted when fee configurations have been changed by the contract owner.&#x20;

```solidity
event FeeConfigChanged(
    ActionType actionType, 
    uint256 lpFee, 
    uint256 stakingFee, 
    uint256 protocolFee
); 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter   | Type       | Description                            |
| ----------- | ---------- | -------------------------------------- |
| actionType  | ActionType | Type of user action                    |
| lpFee       | uint256    | Rate of fees given to LPs              |
| stakingFee  | uint256    | Rate of fees given to ibAsset stakers  |
| protocolFee | uint256    | Rate of fees given to protocol creator |

#### ActionType

```solidity
enum ActionType {
    BUY_TOKEN,
    SELL_TOKEN,
    ADD_LIQUIDITY,
    REMOVE_LIQUIDITY
}
```

| Parameter         | Description                                      |
| ----------------- | ------------------------------------------------ |
| BUY\_TOKEN        | Action is the minting of ibAssets                |
| SELL\_TOKEN       | Action is the burning of ibAssets                |
| ADD\_LIQUIDITY    | Action is the adding of liquidity to the IBC     |
| REMOVE\_LIQUIDITY | Action is the removing of liquidity from the IBC |
{% endtab %}
{% endtabs %}



### `FeeOwnerChanged`

Emitted when the protocol creator fee receival address is changed.&#x20;

```solidity
event FeeOwnerChanged(address feeOwner); 
```

{% tabs %}
{% tab title="Parameter" %}
| Parameter | Type    | Description                                 |
| --------- | ------- | ------------------------------------------- |
| feeOwner  | address | New address receiving protocol creator fees |
{% endtab %}
{% endtabs %}



## Read-Only Functions

### `feeConfig`

Gets the fee configurations of inverse bonding curve interactions for the specified action type.&#x20;

```solidity
function feeConfig(ActionType actionType) external view returns (
    uint256 lpFee, 
    uint256 stakingFee, 
    uint256 protocolFee
)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Parameter   | Type    | Description                                             |
| ----------- | ------- | ------------------------------------------------------- |
| lpFee       | uint256 | Fee rate given to LPs for user action type              |
| stakingFee  | uint256 | Fee rate given to ibAsset stakers for user action type  |
| protocolFee | uint256 | Fee rate given to protocol creator for user action type |
{% endtab %}
{% endtabs %}



### `feeOwner`

Gets the address receiving protocol creator fees.&#x20;

```solidity
function feeOwner() external view returns (address)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description                             |
| ------- | --------------------------------------- |
| address | Address receiving protocol creator fees |
{% endtab %}
{% endtabs %}



### `weth`

Gets the contract address of the WETH token contract.&#x20;

```solidity
function weth() external view returns (address)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description                                 |
| ------- | ------------------------------------------- |
| address | Contract address of the WETH token contract |
{% endtab %}
{% endtabs %}



### `router`

Gets the contract address of the IBC Router contract.&#x20;

```solidity
function router() external view returns (address)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description                                 |
| ------- | ------------------------------------------- |
| address | Contract address of the IBC Router contract |
{% endtab %}
{% endtabs %}



### `curveImplementation`

Gets the contract address of the IBC implementation contract.&#x20;

```solidity
function curveImplementation() external view returns (address)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description                                         |
| ------- | --------------------------------------------------- |
| address | Contract address of the IBC implementation contract |
{% endtab %}
{% endtabs %}
