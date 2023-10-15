# Inverse Bonding Curve

{% hint style="danger" %}
Requires a future update as contracts are yet to be finalized --- not highly dependable
{% endhint %}

The Inverse Bonding Curve contract is responsible for handling mints and burns of ibAssets. The contract stores the balance of the relevant reserve assets, used for the mints and burns.&#x20;

A Inverse Bonding Curve contract is deployed per ibAsset type. New Inverse Bonding Curve contracts are deployed through the [IBC Factory](ibc-factory.md) contract.&#x20;



## Events

### `CurveInitialized`

Emitted at inverse bonding curve initialization.&#x20;

```solidity
event CurveInitialized(
    address indexed from,
    address indexed reserveTokenAddress
    uint256 reserve,
    uint256 supply,
    uint256 initialPrice,
    uint256 parameterInvariant
);
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter             | Type    | Description                       |
| --------------------- | ------- | --------------------------------- |
| from\*                | address | Address of initializer            |
| reserveTokenAddress\* | address | Contract address of reserve asset |
| reserve               | uint256 | Reserve value at initialization   |
| supply                | uint256 | Supply value at initialization    |
| initialPrice          | uint256 | ibAsset price at initialization   |
| parameterInvariant    | uint256 | Curve invariant at initialization |

\* = indexable
{% endtab %}
{% endtabs %}



### `LiquidityAdded`

Emitted when new liquidity has been added to the inverse bonding curve.&#x20;

```solidity
event LiquidityAdded(
    address indexed from, 
    address indexed recipient, 
    uint256 amountIn, 
    uint256 amountOut, 
    uint256 newParameterInvariant
); 
```

{% tabs %}
{% tab title="First Tab" %}
| Parameter             | Type    | Description                            |
| --------------------- | ------- | -------------------------------------- |
| from\*                | address | Address of LP                          |
| recipient\*           | address | Address that received minted LP tokens |
| amountIn              | uint256 | Amount of reserve assets added         |
| amountOut             | uint256 | Amount of LP tokens minted             |
| newParameterInvariant | uint256 | Curve invariant after LP addition      |

\* = indexable
{% endtab %}
{% endtabs %}



### `LiquidityRemoved`

Emitted when liquidity has been removed from the inverse bonding curve.&#x20;

```solidity
event LiquidityRemoved(
    address indexed from, 
    address indexed recipient, 
    uint256 amountIn, 
    uint256 reserveAmountOut, 
    uint256 inverseTokenCredit, 
    uint256 inverseTokenBurned, 
    uint256 newParameterInvariant
); 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter             | Type    | Description                            |
| --------------------- | ------- | -------------------------------------- |
| from\*                | address | Address of LP                          |
| recipient\*           | address | Address that received removed reserves |
| amountIn              | uint256 | Amount of LP tokens burnt              |
| reserveAmountOut      | uint256 | Amount of reserve assets withdrawn     |
| inverseTokenCredit    | uint256 | ibAsset credit of LP prior to removal  |
| inverseTokenBurned    | uint256 | Amount of ibAssets burnt               |
| newParameterInvariant | uint256 | Curve invariant after LP removal       |

\* = indexable
{% endtab %}
{% endtabs %}



### `TokenStaked`

Emitted when ibAssets are staked.&#x20;

```solidity
event TokenStaked(address indexed from, uint256 amount); 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description       |
| --------- | ------- | ----------------- |
| from\*    | address | Address of staker |
| amount    | uint256 | Stake amount      |

\* = indexable
{% endtab %}
{% endtabs %}



### `TokenUnstaked`

Emitted when ibAssets are unstaked.&#x20;

```solidity
event TokenUnstaked(address indexed from, uint256 amount); 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description         |
| --------- | ------- | ------------------- |
| from\*    | address | Address of unstaker |
| amount    | uint256 | Unstake amount      |

\* = indexable
{% endtab %}
{% endtabs %}



### `TokenBought`

Emitted when ibAssets are bought / minted.&#x20;

```solidity
event TokenBought(
    address indexed from, 
    address indexed recipient, 
    uint256 amountIn, 
    uint256 amountOut
); 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter   | Type    | Description                      |
| ----------- | ------- | -------------------------------- |
| from\*      | address | Address of buyer / minter        |
| recipient\* | address | Receiver of minted ibAssets      |
| amountIn    | uint256 | Reserve asset amount used in buy |
| amountOut   | uint256 | ibAsset amount minted from buy   |

\* = indexable
{% endtab %}
{% endtabs %}



### `TokenSold`

Emitted when ibAssets are sold / burnt.&#x20;

```solidity
event TokenSold(
    address indexed from, 
    address indexed recipient, 
    uint256 amountIn, 
    uint256 amountOut
); 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter   | Type    | Description                           |
| ----------- | ------- | ------------------------------------- |
| from\*      | address | Address of seller / burner            |
| recipient\* | address | Receiver of returned reserve assets   |
| amountIn    | uint256 | ibAsset amount burnt in sell          |
| amountOut   | uint256 | Reserve asset amount returned in sell |

\* = indexable
{% endtab %}
{% endtabs %}



### `RewardClaimed`

Emitted when accrued LP and ibAsset staking rewards are claimed.&#x20;

```solidity
event RewardClaimed(
    address indexed from, 
    address indexed recipient, 
    uint256 inverseTokenAmount, 
    uint256 reserveAmount
); 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter          | Type    | Description                         |
| ------------------ | ------- | ----------------------------------- |
| from\*             | address | Address of reward claimer           |
| recipient\*        | address | Address receiving claimed rewards   |
| inverseTokenAmount | uint256 | Amount of rewards in ibAssets       |
| reserveAmount      | uint256 | Amount of rewards in reserve assets |

\* = indexable
{% endtab %}
{% endtabs %}



## State-Changing Functions

### `addLiquidity`

Adds liquidity reserves to the inverse bonding curve.&#x20;

```solidity
function addLiquidity(
    address recipient, 
    uint256 reserveIn, 
    uint256 minPriceLimit
) external payable whenNotPaused 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter     | Type    | Description                                                                                  |
| ------------- | ------- | -------------------------------------------------------------------------------------------- |
| recipient     | address | Address to receive LP tokens                                                                 |
| reserveIn     | uint256 | Amount of reserve assets provided for liquidity add                                          |
| minPriceLimit | uint256 | Minimum ibAsset price to conduct LP - reverts if ibAsset price is lower than specified value |
{% endtab %}
{% endtabs %}



### `removeLiquidity`

Removes liquidity reserves from the inverse bonding curve.&#x20;

```solidity
function removeLiquidity(
    address recipient, 
    uint256 inverseTokenIn, 
    uint256 maxPriceLimit
) external whenNotPaused 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter      | Type    | Description                                                                                   |
| -------------- | ------- | --------------------------------------------------------------------------------------------- |
| recipient      | address | Address to receive removed reserve assets                                                     |
| inverseTokenIn | uint256 | Amount of additional ibAssets posted for LP removal                                           |
| maxPriceLimit  | uint256 | Maximum ibAsset price to conduct LP - reverts if ibAsset price is higher than specified value |
{% endtab %}
{% endtabs %}



### `buyTokens`

Buys / mints new ibAsset tokens with provided reserve assets.&#x20;

```solidity
function buyTokens(
    address recipient, 
    uint256 reserveIn, 
    uint256 exactAmountOut, 
    uint256 maxPriceLimit
) external payable whenNotPaused 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter      | Type    | Description                                                                                              |
| -------------- | ------- | -------------------------------------------------------------------------------------------------------- |
| recipient      | address | Address to receive minted ibAssets                                                                       |
| reserveIn      | uint256 | Amount of reserve assets provided for minting                                                            |
| exactAmountOut | uint256 | Exact amount ibAssets to be minted                                                                       |
| maxPriceLimit  | uint256 | Maximum effective ibAsset buy price to conduct buy - reverts if buy price is higher than specified value |
{% endtab %}
{% endtabs %}



### `sellTokens`

Sells / burns ibAsset tokens to receive reserve assets.&#x20;

```solidity
function sellTokens(
    address recipient, 
    uint256 inverseTokenIn, 
    uint256 minPriceLimit
) external whenNotPaused 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter      | Type    | Description                                                                                                |
| -------------- | ------- | ---------------------------------------------------------------------------------------------------------- |
| recipient      | address | Address to receive reserve assets                                                                          |
| inverseTokenIn | uint256 | Amount of ibAssets to burn                                                                                 |
| minPriceLimit  | uint256 | Minimum effective ibAsset sell price to conduct sell - reverts if sell price is lower than specified value |
{% endtab %}
{% endtabs %}



### `stake`

Stakes specified amount of ibAssets.&#x20;

```solidity
function stake(address recipient, uint256 amount) external whenNotPaused 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description                         |
| --------- | ------- | ----------------------------------- |
| recipient | address | Address performing the stake action |
| amount    | uint256 | Amount of ibAssets to stake         |
{% endtab %}
{% endtabs %}



### `unstake`

Unstakes specified amount of ibAssets.&#x20;

```solidity
function unstake(address recipinet, uint256 amount) external whenNotPaused 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description                           |
| --------- | ------- | ------------------------------------- |
| recipient | uint256 | Address performing the unstake action |
| amount    | uint256 | Amount of ibAssets to unstake         |
{% endtab %}
{% endtabs %}



### `claimReward`

Claims accrued LP and staking rewards.&#x20;

```solidity
function claimReward(address recipient) external whenNotPaused 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description                         |
| --------- | ------- | ----------------------------------- |
| recipient | address | Address performing the claim action |
{% endtab %}
{% endtabs %}



## Read-Only Functions

### `liquidityPositionOf`

Gets the LP position data for the specified address.&#x20;

```solidity
function liquidityPositionOf(address account) external view returns (
    uint256 lpTokenAmount, 
    uint256 inverseTokenCredit
)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description                                         |
| --------- | ------- | --------------------------------------------------- |
| account   | address | Address of account to fetch LP position information |
{% endtab %}

{% tab title="Return Values" %}
| Parameter          | Type    | Description                               |
| ------------------ | ------- | ----------------------------------------- |
| lpTokenAmount      | uint256 | Amount of LP Tokens owned by account      |
| inverseTokenCredit | uint256 | Amount of ibAsset credit owned by account |
{% endtab %}
{% endtabs %}



### `stakingBalanceOf`

Gets the staked ibAsset amount for the specified address.&#x20;

```solidity
function stakingBalanceOf(address account) external view returns (uint256) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description                                      |
| --------- | ------- | ------------------------------------------------ |
| account   | address | Address of holder to get ibAsset staking balance |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description               |
| ------- | ------------------------- |
| uint256 | Amount of staked ibAssets |
{% endtab %}
{% endtabs %}



### `inverseTokenAddress`

Gets the contract address of the relevant ibAsset token contract.&#x20;

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
| Type    | Description                                             |
| ------- | ------------------------------------------------------- |
| address | Contract address of the relevant ibAsset token contract |
{% endtab %}
{% endtabs %}



### `reserveTokenAddress`

Gets the contract address of the relevant reserve asset token contract.&#x20;

```solidity
function reserveTokenAddress() external view returns (address)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description                                                   |
| ------- | ------------------------------------------------------------- |
| address | Contract address of the relevant reserve asset token contract |
{% endtab %}
{% endtabs %}



### `curveParameters`

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
    uint256 lpSupply; 
    uint256 price;
    uint256 parameterInvariant;
}
```

| Parameter          | Type    | Description                       |
| ------------------ | ------- | --------------------------------- |
| reserve            | uint256 | Liquidity reserve of curve        |
| supply             | uint256 | ibAsset minted supply             |
| lpSupply           | uint256 | Current total supply of LP tokens |
| price              | uint256 | Current spot price of ibAsset     |
| parameterInvariant | uint256 | Current curve invariant of curve  |
{% endtab %}
{% endtabs %}



### `rewardOf`

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
| Parameter              | Type    | Description                                       |
| ---------------------- | ------- | ------------------------------------------------- |
| inverseTokenForLp      | uint256 | Accrued ibAsset rewards for LP position           |
| inverseTokenForStaking | uint256 | Accrued ibAsset rewards for staked ibAssets       |
| reserveForLp           | uint256 | Accrued reserve asset rewards for LP position     |
| reserveForStaking      | uint256 | Accrued reserve asset rewards for staked ibAssets |
{% endtab %}
{% endtabs %}



### `rewardOfProtocol`

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
| Parameter          | Type    | Description                                       |
| ------------------ | ------- | ------------------------------------------------- |
| inverseTokenReward | uint256 | Accrued ibAsset rewards to protocol creator       |
| reserveReward      | uint256 | Accrued reserve asset rewards to protocol creator |
{% endtab %}
{% endtabs %}



### `totalStaked`

Gets the total staked ibAsset amount.&#x20;

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
| Type    | Description                     |
| ------- | ------------------------------- |
| uint256 | Total amount of staked ibAssets |
{% endtab %}
{% endtabs %}



### `blockRewardEMA`

Gets the EMA-adjusted per-token reward amounts for the specified reward type.&#x20;

```solidity
function blockRewardEMA(RewardType rewardType) external view returns (
    uint256 inverseTokenReward, 
    uint256 reserveReward
)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter  | Type       | Description                |
| ---------- | ---------- | -------------------------- |
| rewardType | RewardType | Type of rewards to specify |

#### rewardType

```solidity
enum RewardType {
    LP, // 0
    STAKING, // 1
    PROTOCOL // 2
}
```

| Parameter | Description                             |
| --------- | --------------------------------------- |
| LP        | Reward type is LP rewards               |
| STAKING   | Reward type is ibAsset staking rewards  |
| PROTOCOL  | Reward type is protocol creator rewards |
{% endtab %}

{% tab title="Return Values" %}
| Parameter          | Type    | Description                                                                     |
| ------------------ | ------- | ------------------------------------------------------------------------------- |
| inverseTokenReward | uint256 | Amount of ibAsset rewards accrued per-token for the specified reward type       |
| reserveReward      | uint256 | Amount of reserve asset rewards accrued per-token for the specified reward type |
{% endtab %}
{% endtabs %}



### `rewardState`

Gets the total reward information for the entire protocol.&#x20;

```solidity
function rewardState() external view returns (
    uint256[MAX_FEE_TYPE_COUNT][MAX_FEE_STATE_COUNT] memory totalReward,
    uint256[MAX_FEE_TYPE_COUNT][MAX_FEE_STATE_COUNT] memory totalPendingReward
)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Parameter          | Type                                                            | Description                                        |
| ------------------ | --------------------------------------------------------------- | -------------------------------------------------- |
| totalReward        | uint256\[MAX\_FEE\_TYPE\_COUNT]\[MAX\_FEE\_STATE\_COUNT] memory | Total reward amount accrued                        |
| totalPendingReward | uint256\[MAX\_FEE\_TYPE\_COUNT]\[MAX\_FEE\_STATE\_COUNT] memory | Total reward amount accrued, but yet to be claimed |
{% endtab %}
{% endtabs %}



### `getImplementation`

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

