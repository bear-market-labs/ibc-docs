# Liquidity Providing

Similar to those in xyk automated market makers (AMMs), external capital can be provided to enhance the liquidity of an IBC. Liquidity providers (LPs), entities that perform the act of providing liquidity, provide additional reserve assets to an IBC. The provided reserve assets are then utilized by the IBC to facilitate the minting and burning of ibAssets.&#x20;

Providing liquidity on the IBC functions in a way such that the liquidity utilization value of the curve remains the same at **0.5** both before and after the liquidity add. The addition or removal of liquidity updates both the minted ibAsset supply and curve invariant values - however, the current spot price (as well as the liquidity utilization) remains unchanged.&#x20;

The added liquidity triggers the current slope of IBCs to be updated - in a way that greater market depth is given to those to mints and burns of the same size. Minting a certain supply of ibAssets after an LP thus requires **more** reserve assets than prior to the LP. Similiarly, burning a specific number of ibAssets after an LP returns **less** reserve assets than before the LP, showing the exact opposite behavior of adding liquidity on a regular xyk AMM.&#x20;



## LP Positions

Providers of liquidity are given freshly created LP positions, which contain information about the user's share of provided liquidity and its related values. An LP position entails the following data:&#x20;

* **LP Token Amount**: represents the LP's pro-rata share of total curve reserves.&#x20;
* **ibAsset Credit**: represents the amount of ibAssets that are considered to be "owned" (but not yet available) by the LP.&#x20;
* **Reward Index**: used for computing the LP rewards of the position.&#x20;



LP positions on IBCs have differing characteristics with the widely known LP tokens of xyk AMMs, the major differences being:&#x20;

* **Only Reserve Assets Required**: Only reserve assets are needed when adding liquidity.&#x20;
* **Not a Token**: LP positions are not tokenized but instead just recorded state values per LP.&#x20;
* **Non-fungible**: LP positions are not fungible LP positions due to the existence of ibAsset credit.&#x20;
* **Non-transferrable**: LP positions are not transferrable to a different account.&#x20;
* **One Position Per Account**: there can only exist one LP position per LP.&#x20;
* **Opened / Closed in Full**: positions cannot be modified and must be opened or closed in full.&#x20;
* **Restricted Withdrawals**: LPs may be required to post additional ibAssets to remove positions.&#x20;
* **Non-compounding rewards**: rewards distributed to LP positions do not auto-compound.&#x20;



### LP Token Amount

The LP token amount of an LP position represents the amount of liquidity that was provided by the LP. This value is not an actual token (e.g. ERC20) balance, but instead simply a numerical value. The LP token amount value is used when calculating the amount of liquidity an LP can later withdraw. The minting amounts of LP tokens are determined based the changes of the total LP token supply ($$L$$), which is computed as:&#x20;

$$
L=P(R-PS)
$$

Rewritten using the liquidity utilization value, this becomes:&#x20;

$$
L=P(1-u)R
$$

Where the minted LP token amount ($$\Delta L$$) is simply the difference in the total LP token supply before ($$L_{before}$$) and after ($$L_{after}$$) the LP:&#x20;

$$
\Delta L=L_{after}-L_{before}
$$

It can be seen that similar to LP tokens of a regular xyk AMM, the amount of withdrawable liquidity of a position is a simple pro-rata value of the curve's total reserves.&#x20;

An LP's LP token amount is also used as the basis for distributing rewards to LPs. This distribution is made prorated to the LP token amount of the position.&#x20;



### ibAsset Credit

To retain the same liquidity utilization value pre and post LP, as reserve assets are added the ibAsset supply must also increase via minting. This amount increase is not made readily available to the LP but instead "virtually" minted (token supply increases without an actual mint), although the virtually minted amount is considered to be under the ownership of the LP and thus "credited" to its LP position. This credited amount is later made for use when removing liquidity.&#x20;



### Reward Index

The reward index of a position is used to track how much LP rewards the position has available for claim. Two reward indexes exist, one a global value and the other a user-specific value. The global index value is updated every time the rewards are distributed to all relevant users, tracking the amount of rewards distributed per LP token amount since protocol genesis.&#x20;

During a reward claim, the accrued reward amount of an LP is calculated as:&#x20;

$$
rewardAmount=\left(globalRewardIndex - userRewardIndex\right)\times lpTokenAmount
$$

After which the user-specific index updates to the current global index value.&#x20;



### Adding Liquidity

The addition of reserve liquidity first introduces an increase in the curve's reserves. This, combined with the need to retain the liquidity utilization as a constant value tells that the addition of liquidity must cause an increase in the minted ibAsset supply. This supply increase is not made available to the LP right away, but instead minted virtually. The virtually minted supply however is "credited" to the LP, later made available at the time of LP removal.&#x20;

With the addition of $$\Delta R$$ amount of reserve assets, the below should be satisfied together with a minted ibAsset supply increase of $$\Delta S$$:&#x20;

$$
u=\frac{P\left(S+\Delta S\right)}{R+\Delta R}=\frac{PS}{R}
$$

Since the LP's action does not incur a change in spot price, the supply increase gives out as:&#x20;

$$
\Delta S=\frac{\Delta R}{R}S
$$

This $$\Delta S$$ of supply increase is thought to be minted, and is credited to the LP.&#x20;



The invariant $$i$$ also updates to a new value of $$i^{\prime}$$:&#x20;

$$
i^{\prime}=\frac{R+\Delta R}{{\left(S+\Delta S\right)}^{u}}
$$

The curve subsequently updates to:&#x20;

$$
P(x)=\frac{{i}^{\prime}{u}}{{\left(S+\Delta S+x\right)}^{1-{u}}}
$$

Showing this in graph format looks like the below.&#x20;

<figure><img src="../.gitbook/assets/LP Add.png" alt="" width="375"><figcaption></figcaption></figure>

Where the red curve representing the IBC prior to the LP addition and the blue curve corresponding to the curve after adding liquidity. As seen on the graph, the increased market depth requires users to spend more reserve assets per ibAsset minted and retrieve less reserve assets per ibAsset burnt.&#x20;



Additionally, the LP is minted LP tokens of the below amount of $$\Delta L$$:&#x20;

$$
\Delta L=\frac{\Delta R}{R}L
$$

Where $$L$$ is the total LP token supply prior to the LP.&#x20;



## Removing Liquidity

Similar to when liquidity is added, the removal of liquidity should lead to the decrease in the minted ibAsset supply in order to preserve the utilization as a constant. This amount of supply decrease (named as the LP's ibAsset debt) is dependent on the curve's state at the time of liquidity removal, and thus its value may be different from the amount of ibAsset credit that the LP has.&#x20;

If the ibAsset debt amount is greater than the LP's ibAsset credit, then the curve requires LPs to post additional ibAsset tokens to cover the difference. Once the tokens are received, the debt amount is burnt and removed from supply. The debt amount may also be lesser than the LP's credit. In this scenario the debt amount is burnt, and the remaining ibAsset credit is transferred to the LP.&#x20;



The removal of $$\Delta L$$ amount of LP tokens of a LP position from a total LP token supply of $$L$$ should result in the removal of $$\Delta R$$ amount of reserve liquidity, computed as:&#x20;

$$
\Delta R=\frac{\Delta L}{L}R
$$

And since the utilization value should remain unchanged, a supply decrease of $$\Delta S$$ should follow, in a way that satisfies:&#x20;

$$
u=\frac{P\left(S-\Delta S\right)}{R-\Delta R}=\frac{PS}{R}
$$

$$\Delta S$$ thus gives out as:&#x20;

$$
\Delta S=\frac{\Delta R}{R}S=\frac{\Delta L}{L}S
$$

If $$\Delta S$$ is calculated to be greater than the position's ibAsset credit, the difference is required to be provided by the LP. On the other hand, if the position's ibAsset credit is greater than $$\Delta S$$, the difference is sent over to the LP.&#x20;



Curve invariant $$i$$ then updates to a new value of $$i^{\prime}$$:&#x20;

$$
i^{\prime}=\frac{R-\Delta R}{{\left(S-\Delta S\right)}^{u}}
$$

After which the curve updates to:&#x20;

$$
P(x)=\frac{{i}^{\prime}{u}}{{\left(S-\Delta S+x\right)}^{1-{u}}}
$$

Showing this in graph format looks like the below.&#x20;

<figure><img src="../.gitbook/assets/LP Remove.png" alt="" width="375"><figcaption></figcaption></figure>

With the red curve showing the IBC prior to LP withdrawal and the blue curve being the IBC post-withdrawal. The new curve shows decreased market depth, with less reserve assets required to mint the same amount of ibAssets, and more reserve assets returned per ibAsset burnt.&#x20;



## LP Value

The value of a LP position changes as ibAssets are minted and burnt. Mints and burns increase and decrease the reserve balance, thus causing the differing value. In contrast to a LP position of a regular xyk AMM (e.g. Uniswap V2), **LP positions of IBCs increase in value as price deviations occur.**&#x20;

A LP position's value can be said to be of the value of withdrawable reserves plus / minus any differences of the position's debt and credit:&#x20;

$$
\text{lpValue}=\text{withdrawableReserves}-\text{priceAtWithrawal}\left(\text{debt}-\text{credit}\right)
$$

Given a LP position that has been created at a spot price of $$P_0$$ to mint $$\Delta L$$ amount of LP tokens, its value at a spot price of $$P$$ is calculated as:&#x20;

$$
\left(\frac{1}{P}+\frac{P}{{P_{0}}^{2}}\right)\Delta L
$$

Plotting this over as a lp-value-to-price graph looks like ($$P_0=1,\,\Delta L=0.5$$):&#x20;

<figure><img src="../.gitbook/assets/LP Value (1).png" alt="" width="375"><figcaption></figcaption></figure>
