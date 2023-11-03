# IBC Factory

The IBC Factory contract acts as the deployer for new Inverse Bonding Curve contracts. Users can make a request to this contract to make new deployments of IBCs.&#x20;

The IBC Factory maintains the full list of all deployed IBCs (`curves`), made queryable by users.&#x20;



## Events

### `CurveCreated`

Emitted at IBC contract creation for the specified reserve asset.&#x20;

```solidity
event CurveCreated(
    address curveContract, 
    address tokenContract, 
    address proxyContract, 
    uint256 initialReserve
);
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter      | Type    | Description                                |
| -------------- | ------- | ------------------------------------------ |
| curveContract  | address | Contract address of IBC implementation     |
| tokenContract  | address | Contract address of ibAsset token contract |
| proxyContract  | address | Contract address of IBC proxy contract     |
| initialReserve | uint256 | Initial reserve amount of curve            |
{% endtab %}
{% endtabs %}



## State-Changing Functions

### `CreateCurve`

Deploys a new IBC implementation, its proxy contract, and the relevant ibAsset token contract for the specified reserve asset.&#x20;

```solidity
function createCurve(
    uint256 initialReserves, 
    address reserveTokenAddress, 
    address recipient
) external payable
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter           | Type    | Description                                          |
| ------------------- | ------- | ---------------------------------------------------- |
| initialReserves     | uint256 | Amount of initial reserves to supply to curve        |
| reserveTokenAddress | address | Contract address of the reserve asset token contract |
| recipient           | address | Address to receive initial LP position               |
{% endtab %}
{% endtabs %}



## Read-Only Functions

### `getCurve`

Gets the contract address of the specified reserve asset's IBC implementation.&#x20;

```solidity
function getCurve(address reserveToken) public view returns (address)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter    | Type    | Description                       |
| ------------ | ------- | --------------------------------- |
| reserveToken | address | Contract address of reserve asset |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description                                                         |
| ------- | ------------------------------------------------------------------- |
| address | Contract address of the specified reserve asset's IBC implemenation |
{% endtab %}
{% endtabs %}



### `allCurvesLength`

Gets the total number of IBC curves created through the IBC factory so far.&#x20;

```solidity
function allCurvesLength() public view returns (uint256)
```

{% tabs %}
{% tab title="Parameters" %}
| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |
{% endtab %}

{% tab title="Return Values" %}
| Type    | Description                                   |
| ------- | --------------------------------------------- |
| uint256 | Total number of IBC curves created by Factory |
{% endtab %}
{% endtabs %}
