# InverseBondingCurve.sol

### Events

#### `CurveInitialized`

Emitted at inverse bonding curve initialization.&#x20;

```solidity
event CurveInitialized(
    address indexed from, 
    uint256 virtualReserve, 
    uint256 virtualSupply, 
    uint256 initialPrice, 
    uint256 parameterUtilization, 
    uint256 parameterInvariant
); 
```

| Parameter            | Type    | Description                                     |
| -------------------- | ------- | ----------------------------------------------- |
| from\*               | address | Address of initializer                          |
| virtualReserve       | uint256 | Virtual reserve value at initialization         |
| virtualSupply        | uint256 | Virtual supply value at initialization          |
| initialPrice         | uint256 | IBC price at initialization                     |
| parameterUtilization | uint256 | Liquidity reserve utilization at initialization |
| parameterInvariant   | uint256 | Curve invariant at initialization               |

\* = indexable



#### `LiquidityAdded`

Emitted when new liquidity has been added to the inverse bonding curve.&#x20;

```solidity
event LiquidityAdded(
    address indexed from, 
    address indexed recipient, 
    uint256 amountIn, 
    uint256 amountOut, 
    uint256 newParameterUtilization, 
    uint256 newParameterInvariant
); 
```

| Parameter               | Type    | Description                                     |
| ----------------------- | ------- | ----------------------------------------------- |
| from\*                  | address | Address of LP                                   |
| recipient\*             | address | Address that received minted LP tokens          |
| amountIn                | uint256 | Amount of ETH added                             |
| amountOut               | uint256 | Amount of LP tokens minted                      |
| newParameterUtilization | uint256 | Liquidity reserve utilization after LP addition |
| newParameterInvariant   | uint256 | Curve invariant after LP addition               |

\* = indexable



#### `LiquidityRemoved`

Emitted when liquidity has been removed from the inverse bonding curve.&#x20;

```solidity
event LiquidityRemoved(
    address indexed from, 
    address indexed recipient, 
    uint256 amountIn, 
    uint256 amountOut, 
    uint256 newParameterUtilization, 
    uint256 newParameterInvariant
); 
```

| Parameter               | Type    | Description                                    |
| ----------------------- | ------- | ---------------------------------------------- |
| from\*                  | address | Address of LP                                  |
| recipient\*             | address | Address that received removed reserves         |
| amountIn                | uint256 | Amount of LP tokens burnt                      |
| amountOut               | uint256 | Amount of ETH reserved removed                 |
| newParameterUtilization | uint256 | Liquidity reserve utilization after LP removal |
| newParameterInvariant   | uint256 | Curve invariant after LP removal               |

\* = indexable



#### `LiquidityStaked -> InverseTokenStaked?`

Emitted when IBC is staked.&#x20;

```solidity
event LiquidityStaked(address indexed from, uint256 amount); 

event InverseTokenStaked(address indexed from, uint256 amount); 
```

| Parameter | Type    | Description       |
| --------- | ------- | ----------------- |
| from\*    | address | Address of staker |
| amount    | uint256 | Stake amount      |

\* = indexable



#### `LiquidityUnstaked -> InverseTokenUnstaked?`

Emitted when IBC is unstaked.&#x20;

```solidity
event LiquidityUnstaked(address indexed from, uint256 amount); 

event InverseTokenUnstaked(address indexed from, uint256 amount); 
```

| Parameter | Type    | Description         |
| --------- | ------- | ------------------- |
| from\*    | address | Address of unstaker |
| amount    | uint256 | Unstake amount      |

\* = indexable



#### `TokenBought`

Emitted when IBC is bought / minted.&#x20;

```solidity
event TokenBought(
    address indexed from, 
    address indexed recipient, 
    uint256 amountIn, 
    uint256 amountOut
); 
```

| Parameter   | Type    | Description                |
| ----------- | ------- | -------------------------- |
| from\*      | address | Address of buyer / minter  |
| recipient\* | address | Receiver of minted IBC     |
| amountIn    | uint256 | ETH amount used in buy     |
| amountOut   | uint256 | IBC amount minted from buy |

\* = indexable



#### `TokenSold`

Emitted when IBC is sold / burnt.&#x20;

```solidity
event TokenSold(
    address indexed from, 
    address indexed recipient, 
    uint256 amountIn, 
    uint256 amountOut
); 
```

| Parameter   | Type    | Description                 |
| ----------- | ------- | --------------------------- |
| from\*      | address | Address of seller / burner  |
| recipient\* | address | Receiver of returned ETH    |
| amountIn    | uint256 | IBC amount burnt in sell    |
| amountOut   | uint256 | ETH amount returned in sell |

\* = indexable



#### `RewardClaimed`

Emitted when accrued LP and IBC staking rewards are claimed.&#x20;

```solidity
event RewardClaimed(
    address indexed from, 
    address indexed recipient, 
    uint256 inverseTokenAmount, 
    uint256 reserveAmount
); 
```

| Parameter          | Type    | Description                       |
| ------------------ | ------- | --------------------------------- |
| from\*             | address | Address of reward claimer         |
| recipient\*        | address | Address receiving claimed rewards |
| inverseTokenAmount | uint256 | Amount of rewards in IBC          |
| reserveAmount      | uint256 | Amount of rewards in ETH          |

\* = indexable



#### `FeeConfigChanged`

Emitted when fee configurations have been changed by the contract owner.&#x20;

```solidity
event FeeConfigChanged(
    ActionType actionType, 
    uint256 lpFee, 
    uint256 stakingFee, 
    uint256 protocolFee
); 
```

| Parameter   | Type       | Description                            |
| ----------- | ---------- | -------------------------------------- |
| actionType  | ActionType | Type of user action                    |
| lpFee       | uint256    | Rate of fees given to LPs              |
| stakingFee  | uint256    | Rate of fees given to IBC stakers      |
| protocolFee | uint256    | Rate of fees given to protocol creator |



#### `FeeOwnerChanged`

Emitted when the protocol creator fee receival address is changed.&#x20;

```solidity
event FeeOwnerChanged(address feeOwner); 
```

| Parameter | Type    | Description                                 |
| --------- | ------- | ------------------------------------------- |
| feeOwner  | address | New address receiving protocol creator fees |





## State-Changing Functions

#### `addLiquidity`

Adds liquidity reserves to the inverse bonding curve.&#x20;

```solidity
function addLiquidity(
    address recipient, 
    uint256 minPriceLimit
) external payable whenNotPaused 
```

| Parameter     | Type    | Description                                                                          |
| ------------- | ------- | ------------------------------------------------------------------------------------ |
| recipient     | address | Address to receive LP tokens                                                         |
| minPriceLimit | uint256 | Minimum IBC price to conduct LP - reverts if IBC price is lower than specified value |



#### `removeLiquidity`

Removes liquidity reserves from the inverse bonding curve.&#x20;

```solidity
function removeLiquidity(
    address recipient, 
    uint256 amount, 
    uint256 maxPriceLimit
) external whenNotPaused 
```

| Parameter     | Type    | Description                                                                           |
| ------------- | ------- | ------------------------------------------------------------------------------------- |
| recipient     | address | Address to receive removed ETH reserves                                               |
| amount        | uint256 | Amount of LP tokens to use in LP removal                                              |
| maxPriceLimit | uint256 | Maximum IBC price to conduct LP - reverts if IBC price is higher than specified value |



#### `buyTokens`

Buys / mints new IBC tokens with provided ETH.&#x20;

```solidity
function buyTokens(
    address recipient, 
    uint256 maxPriceLimit
) external payable whenNotPaused 
```

| Parameter     | Type    | Description                                                                                          |
| ------------- | ------- | ---------------------------------------------------------------------------------------------------- |
| recipient     | address | Address to receive minted IBC                                                                        |
| maxPriceLimit | uint256 | Maximum effective IBC buy price to conduct buy - reverts if buy price is higher than specified value |



#### `sellTokens`

Sells / burns IBC tokens to receive ETH.&#x20;

```solidity
function sellTokens(
    address recipient, 
    uint256 amount, 
    uint256 minPriceLimit
) external whenNotPaused 
```

| Parameter     | Type    | Description                                                                                            |
| ------------- | ------- | ------------------------------------------------------------------------------------------------------ |
| recipient     | address | Address to receive ETH                                                                                 |
| amount        | uint256 | Amount of IBC to burn                                                                                  |
| minPriceLimit | uint256 | Minimum effective IBC sell price to conduct sell - reverts if sell price is lower than specified value |



#### `stake`

Stakes specified amount of IBC.&#x20;

```solidity
function stake(uint256 amount) external whenNotPaused 
```

| Parameter | Type    | Description            |
| --------- | ------- | ---------------------- |
| amount    | uint256 | amount of IBC to stake |



#### `unstake`

Unstakes specified amount of IBC.&#x20;

```solidity
function unstake(uint256 amount) external whenNotPaused 
```

| Parameter | Type    | Description              |
| --------- | ------- | ------------------------ |
| amount    | uint256 | Amount of IBC to unstake |



#### `claimReward`

Claims accrued LP and staking rewards to the specified address.&#x20;

```solidity
function claimReward(address recipient) external whenNotPaused 
```

| Parameter | Type    | Description                        |
| --------- | ------- | ---------------------------------- |
| recipient | address | Address to receive claimed rewards |



#### `transfer`

Transfers LP tokens to the specified address. LP tokens must be transferred through this contract to conduct reward accrual calculations prior to transfer.&#x20;

```solidity
function transfer(
    address recipient, 
    uint256 amount
) public override whenNotPaused returns (bool) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description                      |
| --------- | ------- | -------------------------------- |
| recipient | address | Address to transfer LP tokens to |
| amount    | uint256 | Amount of LP tokens to transfer  |
{% endtab %}

{% tab title="Return Values" %}
| Type | Description                 |
| ---- | --------------------------- |
| bool | 1 -> successful, 0 -> error |
{% endtab %}
{% endtabs %}



#### `transferFrom`

Transfers LP tokens from the specified address to the specified address. LP tokens must be transferred through this contract to conduct reward accrual calculations prior to transfer.&#x20;

```solidity
function transferFrom(
    address from, 
    address to, 
    uint256 amount
) public override whenNotPaused returns (bool) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description                        |
| --------- | ------- | ---------------------------------- |
| from      | address | Address to transfer LP tokens from |
| to        | address | Address to transfer LP tokens to   |
| amount    | uint256 | Amount of LP tokens to transfer    |
{% endtab %}

{% tab title="Return Values" %}
| Type | Description                 |
| ---- | --------------------------- |
| bool | 1 -> successful, 0 -> error |
{% endtab %}
{% endtabs %}



### Read-Only Functions

#### `priceOf`

Gets the IBC spot price at the specified IBC supply.&#x20;

```solidity
function priceOf(uint256 supply) public view returns (uint256) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description                               |
| --------- | ------- | ----------------------------------------- |
| supply    | uint256 | Supply of IBC to use in price calculation |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description                          |
| ------- | ------------------------------------ |
| uint256 | Calculated price at specified supply |
{% endtab %}
{% endtabs %}



#### `inverseTokenAddress`

Gets the contract address of IBC.&#x20;

```solidity
function inverseTokenAddress() external view returns (address) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description                   |
| ------- | ----------------------------- |
| address | Contract address of IBC token |
{% endtab %}
{% endtabs %}



#### `curveParameters`

Gets the parameter values of the inverse bonding curve.&#x20;

```solidity
function curveParameters() external view returns (CurveParameter memory parameters) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Parameter  | Type           | Description                      |
| ---------- | -------------- | -------------------------------- |
| parameters | CurveParameter | Inverse bonding curve parameters |

#### CurveParameters

```solidity
struct CurveParameter {
    uint256 reserve;
    uint256 supply;
    uint256 virtualReserve;
    uint256 virtualSupply;
    uint256 price;
    uint256 parameterInvariant;
    uint256 parameterUtilization;
}
```

| Parameter            | Type    | Description                                            |
| -------------------- | ------- | ------------------------------------------------------ |
| reserve              | uint256 | Liquidity reserve of curve (includes virtual reserves) |
| supply               | uint256 | IBC minted supply (includes virtual supply)            |
| virtualReserve       | uint256 | Virtual liquidity reserve                              |
| virtualSupply        | uint256 | Virtual IBC supply                                     |
| price                | uint256 | Current spot price of IBC                              |
| parameterInvariant   | uint256 | Current curve invariant of curve                       |
| parameterUtilization | uint256 | Current liquidity reserve utilization of curve         |
{% endtab %}
{% endtabs %}



#### `feeConfig`

Gets the fee configurations of inverse bonding curve interactions.&#x20;

```solidity
function feeConfig() external view returns (
    uint256[MAX_ACTION_COUNT] memory lpFee, 
    uint256[MAX_ACTION_COUNT] memory stakingFee, 
    uint256[MAX_ACTION_COUNT] memory protocolFee
) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Parameter   | Type                         | Description                                             |
| ----------- | ---------------------------- | ------------------------------------------------------- |
| lpFee       | uint256\[MAX\_ACTION\_COUNT] | Fee rate given to LPs for user action type              |
| stakingFee  | uint256\[MAX\_ACTION\_COUNT] | Fee rate given to IBC stakers for user action type      |
| protocolFee | uint256\[MAX\_ACTION\_COUNT] | Fee rate given to protocol creator for user action type |
{% endtab %}
{% endtabs %}



#### `feeOwner`

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



#### `rewardOf`

Gets the accrued reward amounts for the specified address.&#x20;

```solidity
function rewardOf(address recipient) external view returns (
    uint256 inverseTokenForLp, 
    uint256 inverseTokenForStaking, 
    uint256 reserveForLp, 
    uint256 reserveForStaking, 
) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description                      |
| --------- | ------- | -------------------------------- |
| recipient | address | Address to check accrued rewards |
{% endtab %}

{% tab title="Return Values" %}
| Parameter              | Type    | Description                         |
| ---------------------- | ------- | ----------------------------------- |
| inverseTokenForLp      | uint256 | Accrued IBC rewards for LP position |
| inverseTokenForStaking | uint256 | Accrued IBC rewards for staked IBC  |
| reserveForLp           | uint256 | Accrued ETH rewards for LP position |
| reserveForStaking      | uint256 | Accrued ETH rewards for staked IBC  |
{% endtab %}
{% endtabs %}



#### `rewardOfProtocol`

Gets the accrued reward amounts of the protocol creator.&#x20;

```solidity
function rewardOfProtocol() external view returns (
    uint256 inverseTokenReward, 
    uint256 reserveReward
) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Parameter          | Type    | Description                             |
| ------------------ | ------- | --------------------------------------- |
| inverseTokenReward | uint256 | Accrued IBC rewards to protocol creator |
| reserveReward      | uint256 | Accrued ETH rewards to protocol creator |
{% endtab %}
{% endtabs %}



#### `stakingBalanceOf`

Gets the staked IBC amount for the specified address.&#x20;

```solidity
function stakingBalanceOf(address holder) external view returns (uint256) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description                                  |
| --------- | ------- | -------------------------------------------- |
| holder    | address | Address of holder to get IBC staking balance |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description          |
| ------- | -------------------- |
| uint256 | Amount of staked IBC |
{% endtab %}
{% endtabs %}



#### `getImplementation`

Gets the address of the implemenation contract.&#x20;

```solidity
function getImplementation() external view returns (address) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameters | Type | Description |
| ---------- | ---- | ----------- |
|            |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description                        |
| ------- | ---------------------------------- |
| address | Address of implementation contract |
{% endtab %}
{% endtabs %}



#### `totalStaked`

Gets the total staked IBC amount.&#x20;

```solidity
function totalStaked() external view returns (uint256) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description                |
| ------- | -------------------------- |
| uint256 | Total amount of staked IBC |
{% endtab %}
{% endtabs %}

