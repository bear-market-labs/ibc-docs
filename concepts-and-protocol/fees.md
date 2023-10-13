# Fees

Interactions with IBCs incur a fee which are then distributed to three entities, LPs, ibAsset stakers, and the protocol creator. The fee rates may differ based on the interaction type.



## Minting

A flat fee rate is taken from the minted ibAsset amount.&#x20;

Fee denomination: ibAsset

| Distributed To  | Fee Rate |
| --------------- | -------- |
| LPs             | 0.25%    |
| ibAsset Stakers | 0.25%    |
| Protocol        | 0.5%     |



## Burning

A flat fee rate is taken from the returned reserve asset amount.&#x20;

Fee denomination: ibAsset

| Distributed To  | Fee Rate |
| --------------- | -------- |
| LPs             | 0.25%    |
| ibAsset Stakers | 0.25%    |
| Protocol        | 0.5%     |



## Adding Liquidity

A flat fee rate is taken from the added reserve asset amount.&#x20;

Fee denomination: reserve asset

| Distributed To  | Fee Rate |
| --------------- | -------- |
| LPs             | 0.25%    |
| ibAsset Stakers | 0.25%    |
| Protocol        | 0.5%     |



## Removing Liquidity

A flat fee rate is taken from the removed reserve asset amount. Additionally if the LP is given ibAssets from their credit, a flat fee rate is also applied to this amount.&#x20;

Fee denomination: reserve asset / ibAsset

| Distributed To  | Fee Rate |
| --------------- | -------- |
| LPs             | 0.25%    |
| ibAsset Stakers | 0.25%    |
| Protocol        | 0.5%     |

