# IBC Factory

## Events

### `CurveDeployed`

Emitted at IBC contract deployment for the specified reserve asset.&#x20;

```solidity
event Deployed(address cruveContract, address tokenContract, address proxyContract);
```

| Parameter     | Type    | Description                                |
| ------------- | ------- | ------------------------------------------ |
| curveContract | address | Contract address of IBC implementation     |
| tokenContract | address | Contract address of ibAsset token contract |
| proxyContract | address | Contract address of IBC proxy contract     |



## Contract State





## State-Changing Functions

### `CreateCurve`

Deploys a new IBC implementation, its proxy contract, and the relevant ibAsset token contract for the specified reserve asset.&#x20;

```solidity
function createCurve(
    uint256 initialReserves, 
    uint256 reserveTokenAddress
) external payable
```

| Parameter           | Type    | Description                                          |
| ------------------- | ------- | ---------------------------------------------------- |
| initialReserves     | uint256 | Amount of initial reserves to supply to curve        |
| reserveTokenAddress | address | Contract address of the reserve asset token contract |



## Read-Only Functions

