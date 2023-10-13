# Inverse Bonding Curve

{% hint style="danger" %}
Requires a future update as contracts are yet to be finalized --- not highly dependable
{% endhint %}

## Events

### `CurveInitialized`

Emitted at inverse bonding curve initialization.&#x20;

```solidity
event CurveInitialized(
    address indexed from,
    uint256 reserve,
    uint256 supply,
    uint256 initialPrice,
    uint256 parameterUtilization,
    uint256 parameterInvariant
);
```

| Parameter            | Type    | Description                                     |
| -------------------- | ------- | ----------------------------------------------- |
| from\*               | address | Address of initializer                          |
| reserve              | uint256 | Reserve value at initialization                 |
| supply               | uint256 | Supply value at initialization                  |
| initialPrice         | uint256 | ibAsset price at initialization                 |
| parameterUtilization | uint256 | Liquidity reserve utilization at initialization |
| parameterInvariant   | uint256 | Curve invariant at initialization               |

\* = indexable



### `LiquidityAdded`

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
| amountIn                | uint256 | Amount of reserve assets added                  |
| amountOut               | uint256 | Amount of LP tokens minted                      |
| newParameterUtilization | uint256 | Liquidity reserve utilization after LP addition |
| newParameterInvariant   | uint256 | Curve invariant after LP addition               |

\* = indexable



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
    uint256 newParameterUtilization, 
    uint256 newParameterInvariant
); 
```

| Parameter               | Type    | Description                                    |
| ----------------------- | ------- | ---------------------------------------------- |
| from\*                  | address | Address of LP                                  |
| recipient\*             | address | Address that received removed reserves         |
| amountIn                | uint256 | Amount of LP tokens burnt                      |
| reserveAmountOut        | uint256 | Amount of reserve assets withdrawn             |
| inverseTokenCredit      | uint256 | ibAsset credit of LP prior to removal          |
| inverseTokenBurned      | uint256 | Amount of ibAssets burnt                       |
| newParameterUtilization | uint256 | Liquidity reserve utilization after LP removal |
| newParameterInvariant   | uint256 | Curve invariant after LP removal               |

\* = indexable



### `TokenStaked`

Emitted when ibAssets are staked.&#x20;

```solidity
event TokenStaked(address indexed from, uint256 amount); 
```

| Parameter | Type    | Description       |
| --------- | ------- | ----------------- |
| from\*    | address | Address of staker |
| amount    | uint256 | Stake amount      |

\* = indexable



### `TokenUnstaked`

Emitted when ibAssets are unstaked.&#x20;

```solidity
event TokenUnstaked(address indexed from, uint256 amount); 
```

| Parameter | Type    | Description         |
| --------- | ------- | ------------------- |
| from\*    | address | Address of unstaker |
| amount    | uint256 | Unstake amount      |

\* = indexable



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

| Parameter   | Type    | Description                      |
| ----------- | ------- | -------------------------------- |
| from\*      | address | Address of buyer / minter        |
| recipient\* | address | Receiver of minted ibAssets      |
| amountIn    | uint256 | Reserve asset amount used in buy |
| amountOut   | uint256 | ibAsset amount minted from buy   |

\* = indexable



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

| Parameter   | Type    | Description                           |
| ----------- | ------- | ------------------------------------- |
| from\*      | address | Address of seller / burner            |
| recipient\* | address | Receiver of returned reserve assets   |
| amountIn    | uint256 | ibAsset amount burnt in sell          |
| amountOut   | uint256 | Reserve asset amount returned in sell |

\* = indexable



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

| Parameter          | Type    | Description                         |
| ------------------ | ------- | ----------------------------------- |
| from\*             | address | Address of reward claimer           |
| recipient\*        | address | Address receiving claimed rewards   |
| inverseTokenAmount | uint256 | Amount of rewards in ibAssets       |
| reserveAmount      | uint256 | Amount of rewards in reserve assets |

\* = indexable



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

| Parameter   | Type       | Description                            |
| ----------- | ---------- | -------------------------------------- |
| actionType  | ActionType | Type of user action                    |
| lpFee       | uint256    | Rate of fees given to LPs              |
| stakingFee  | uint256    | Rate of fees given to ibAsset stakers  |
| protocolFee | uint256    | Rate of fees given to protocol creator |



### `FeeOwnerChanged`

Emitted when the protocol creator fee receival address is changed.&#x20;

```solidity
event FeeOwnerChanged(address feeOwner); 
```

| Parameter | Type    | Description                                 |
| --------- | ------- | ------------------------------------------- |
| feeOwner  | address | New address receiving protocol creator fees |



## Constants

```solidity
uint256 constant MIN_INPUT_AMOUNT = 1e14; // 0.0001
uint256 constant ONE_UINT = 1e18;
uint256 constant LP_FEE_PERCENT = 25e14;
uint256 constant STAKE_FEE_PERCENT = 25e14;
uint256 constant PROTOCOL_FEE_PERCENT = 5e15;
uint256 constant MAX_FEE_PERCENT = 1e17;
uint256 constant ALLOWED_INVARIANT_CHANGE = 1e10;
uint256 constant ALLOWED_INVARIANT_CHANGE_PERCENT = 1e12; //0.000001
uint256 constant ALLOWED_UTILIZATION_CHANGE_PERCENT = 1e12; //0.000001

uint256 constant DAILY_BLOCK_COUNT = 7200;

uint8 constant MAX_ACTION_COUNT = 4;
uint8 constant MAX_FEE_TYPE_COUNT = 3;
uint8 constant MAX_FEE_STATE_FOR_USER_COUNT = 2;
uint8 constant MAX_FEE_STATE_COUNT = 3;
uint8 constant MAX_EMA_STATE_COUNT = 2;

uint8 constant PREVIOUS_EMA_INDEX = 0;
uint8 constant CURRENT_EMA_INDEX = 1;
```

| Parameter                             | Type    | Description                                                          |
| ------------------------------------- | ------- | -------------------------------------------------------------------- |
| MIN\_INPUT\_AMOUNT                    | uint256 | Minimum amonut of reserves that can be used to mint ibAssets         |
| ONE\_UNIT                             | uint256 | 1                                                                    |
| LP\_FEE\_PERCENT                      | uint256 | Portion of fees given to LPs                                         |
| STAKE\_FEE\_PERCENT                   | uint256 | Portion of fees given to ibAsset stakers                             |
| PROTOCOL\_FEE\_PERCENT                | uint256 | Portion of fees given to protocol creator                            |
| MAX\_FEE\_PERCENT                     | uint256 | Maximum portion of fees that can be taken from interactions          |
| ALLOWED\_INVARIANT\_CHANGE            | uint256 | Permitted change of invariant value from rounding errors             |
| ALLOWED\_INVARIANT\_CHANGE\_PERCENT   | uint256 | Permitted change of invariant value from rounding errors             |
| ALLOWED\_UTILIZATION\_CHANGE\_PERCENT | uint256 | Permitted change of liquidity utilization value from rounding errors |
| DAILY\_BLOCK\_COUNT                   | uint256 | Number of blocks in 1 day                                            |
| MAX\_ACTION\_COUNT                    | uint8   | Maximum number of fee accruer types permitted                        |
| MAX\_FEE\_TYPE\_COUNT                 | uint8   | Maximum number of fee types permitted                                |
| MAX\_EMA\_STATE\_COUNT                | uint8   | Maximum number of EMA value types permitted                          |
| PREVIOUS\_EMA\_INDEX                  | uint8   |                                                                      |
| CURRENT\_EMA\_INDEX                   | uint8   |                                                                      |



## Contract State

### `CurveParameter`

Stores information about the variables of the IBC curve.&#x20;

```solidity
struct CurveParameter {
    uint256 reserve;
    uint256 supply;
    uint256 lpSupply;
    uint256 price;
    uint256 parameterInvariant;
    uint256 parameterUtilization;
}
```

| Parameter            | Type    | Description                                  |
| -------------------- | ------- | -------------------------------------------- |
| reserve              | uint256 | Current amount of reserve assets in curve    |
| supply               | uint256 | Current minted ibAsset supply                |
| lpSupply             | uint256 | Current total LP token supply                |
| price                | uint256 | Current spot price of ibAsset                |
| parameterInvariant   | uint256 | Current invariant value of curve             |
| parameterUtilization | uint256 | Current liquidity utilization value of curve |



### `FeeState`

Stores fee-related information.&#x20;

```solidity
Struct FeeState {
    uint256 feeForFirstStaker;
    mapping(address => uint256)[MAX_FEE_STATE_FOR_USER_COUNT] feeIndexStates;
    mapping(address => uint256)[MAX_FEE_STATE_FOR_USER_COUNT] pendingRewards;
    uint256[MAX_FEE_STATE_COUNT] globalFeeIndexes;
    uint256[MAX_FEE_STATE_COUNT] totalReward;
    uint256[MAX_FEE_STATE_COUNT] totalPendingReward;
    uint256 emaRewardUpdateBlockNumber;
    uint256[MAX_EMA_STATE_COUNT] emaReward;
    uint256[MAX_EMA_STATE_COUNT] previousReward;
}
```

| Parameter                  | Type                                                            | Description                                                               |
| -------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------- |
| feeForFirstStaker          | uint256                                                         | Accumulated fees to be given to the first ibAsset staker                  |
| feeIndexStates             | mapping(address => uint256)\[MAX\_FEE\_STATE\_FOR\_USER\_COUNT] | Mapping of user addresses to their fee index                              |
| pendingRewards             | mapping(address => uint256)\[MAX\_FEE\_STATE\_FOR\_USER\_COUNT] | Mapping of user addresses to their accrued, but yet to be claimed rewards |
| globalFeeIndexes           | uint256\[MAX\_FEE\_STATE\_COUNT]                                | Array of global fee indexes for each fee types                            |
| totalReward                | uint256\[MAX\_FEE\_STATE\_COUNT]                                | Array of total accrued rewards for each fee types                         |
| totalPendingReward         | uint256\[MAX\_FEE\_STATE\_COUNT]                                | Array of total accrued, but yet to be claimed rewards for each fee types  |
| emaRewardUpdateBlockNumber | uint256                                                         | Block number when the EMA value was last updated                          |
| emaReward                  | uint256\[MAX\_EMA\_STATE\_COUNT]                                | EMA-adjusted reward amounts per EMA type                                  |
| previousReward             | uint256\[MAX\_EMA\_STATE\_COUNT]                                | Reward amount when EMA value was last updated per EMA type                |



### `LpPosition`

Stores information about a user's LP position.&#x20;

```solidity
struct LpPosition {
    uint256 lpTokenAmount;
    uint256 inverseTokenCredit;
}
```

| Parameter          | Type    | Description                            |
| ------------------ | ------- | -------------------------------------- |
| lpTokenAmount      | uint256 | Amount of LP tokens owned by user      |
| inverseTokenCredit | uint256 | Amount of ibAsset credit owned by user |



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

| Parameter     | Type    | Description                                                                                  |
| ------------- | ------- | -------------------------------------------------------------------------------------------- |
| recipient     | address | Address to receive LP tokens                                                                 |
| reserveIn     | uint256 | Amount of reserve assets provided for liquidity add                                          |
| minPriceLimit | uint256 | Minimum ibAsset price to conduct LP - reverts if ibAsset price is lower than specified value |



### `removeLiquidity`

Removes liquidity reserves from the inverse bonding curve.&#x20;

```solidity
function removeLiquidity(
    address recipient, 
    uint256 inverseTokenIn, 
    uint256 maxPriceLimit
) external whenNotPaused 
```

| Parameter      | Type    | Description                                                                                   |
| -------------- | ------- | --------------------------------------------------------------------------------------------- |
| recipient      | address | Address to receive removed reserve assets                                                     |
| inverseTokenIn | uint256 | Amount of additional ibAssets posted for LP removal                                           |
| maxPriceLimit  | uint256 | Maximum ibAsset price to conduct LP - reverts if ibAsset price is higher than specified value |



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

| Parameter      | Type    | Description                                                                                              |
| -------------- | ------- | -------------------------------------------------------------------------------------------------------- |
| recipient      | address | Address to receive minted ibAssets                                                                       |
| reserveIn      | uint256 | Amount of reserve assets provided for minting                                                            |
| exactAmountOut | uint256 | Exact amount ibAssets to be minted                                                                       |
| maxPriceLimit  | uint256 | Maximum effective ibAsset buy price to conduct buy - reverts if buy price is higher than specified value |



### `sellTokens`

Sells / burns ibAsset tokens to receive reserve assets.&#x20;

```solidity
function sellTokens(
    address recipient, 
    uint256 inverseTokenIn, 
    uint256 minPriceLimit
) external whenNotPaused 
```

| Parameter      | Type    | Description                                                                                                |
| -------------- | ------- | ---------------------------------------------------------------------------------------------------------- |
| recipient      | address | Address to receive reserve assets                                                                          |
| inverseTokenIn | uint256 | Amount of ibAssets to burn                                                                                 |
| minPriceLimit  | uint256 | Minimum effective ibAsset sell price to conduct sell - reverts if sell price is lower than specified value |



### `stake`

Stakes specified amount of ibAssets.&#x20;

```solidity
function stake(address recipient, uint256 amount) external whenNotPaused 
```

| Parameter | Type    | Description                         |
| --------- | ------- | ----------------------------------- |
| recipient | address | Address performing the stake action |
| amount    | uint256 | Amount of ibAssets to stake         |



### `unstake`

Unstakes specified amount of ibAssets.&#x20;

```solidity
function unstake(address recipinet, uint256 amount) external whenNotPaused 
```

| Parameter | Type    | Description                           |
| --------- | ------- | ------------------------------------- |
| recipient | uint256 | Address performing the unstake action |
| amount    | uint256 | Amount of ibAssets to unstake         |



### `claimReward`

Claims accrued LP and staking rewards.&#x20;

```solidity
function claimReward(address recipient) external whenNotPaused 
```

| Parameter | Type    | Description                         |
| --------- | ------- | ----------------------------------- |
| recipient | address | Address performing the claim action |



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
    uint256 parameterUtilization;
}
```

| Parameter            | Type    | Description                                    |
| -------------------- | ------- | ---------------------------------------------- |
| reserve              | uint256 | Liquidity reserve of curve                     |
| supply               | uint256 | ibAsset minted supply                          |
| lpSupply             | uint256 | Current total supply of LP tokens              |
| price                | uint256 | Current spot price of ibAsset                  |
| parameterInvariant   | uint256 | Current curve invariant of curve               |
| parameterUtilization | uint256 | Current liquidity reserve utilization of curve |
{% endtab %}
{% endtabs %}



### `feeConfig`

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
| Parameter   | Type                                | Description                                             |
| ----------- | ----------------------------------- | ------------------------------------------------------- |
| lpFee       | uint256\[MAX\_ACTION\_COUNT] memory | Fee rate given to LPs for user action type              |
| stakingFee  | uint256\[MAX\_ACTION\_COUNT] memory | Fee rate given to ibAsset stakers for user action type  |
| protocolFee | uint256\[MAX\_ACTION\_COUNT] memory | Fee rate given to protocol creator for user action type |
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

{% tab title="Second Tab" %}
| Parameter          | Type                                                            | Description                                        |
| ------------------ | --------------------------------------------------------------- | -------------------------------------------------- |
| totalReward        | uint256\[MAX\_FEE\_TYPE\_COUNT]\[MAX\_FEE\_STATE\_COUNT] memory | Total reward amount accrued                        |
| totalPendingReward | uint256\[MAX\_FEE\_TYPE\_COUNT]\[MAX\_FEE\_STATE\_COUNT] memory | Total reward amount accrued, but yet to be claimed |
{% endtab %}
{% endtabs %}



### `stakingBalanceOf`

Gets the staked ibAsset amount for the specified address.&#x20;

```solidity
function stakingBalanceOf(address holder) external view returns (uint256) 
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type    | Description                                      |
| --------- | ------- | ------------------------------------------------ |
| holder    | address | Address of holder to get ibAsset staking balance |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description               |
| ------- | ------------------------- |
| uint256 | Amount of staked ibAssets |
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
