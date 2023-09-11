# Liquidity Provisioning

Similar to those in xyk automated market makers (AMMs), external capital can be provided to enhance the liquidity of an inverse bonding curve. Liquidity providers (LPs), entities that perform the act of providing liquidity, provide additional reserve assets to an inverse bonding curve. Provided reserve assets are then utilized by the inverse bonding curve to facilitate the minting and burning of assets.&#x20;

The added liquidity triggers the curvature of inverse bonding curves to be updated - in a way that greater market depth is given to those to mints and burns of the same size. The addition and removal of liquidity updates both the liquidity utilization and curve invariant values - however, the current spot price and the minted asset supply remains unchanged.&#x20;



### LP Tokens

Providers of liquidity are given freshly minted LP tokens, a tokenized representation of a LP's share of the reserve liquidity, minus the amount of reserve assets required to fully back all minted assets at the current spot price - this exclusion is the ensure the inverse bonding curve never flips back to a regular non-inverse bonding curve during LP withdrawals. The reserve liquidity excluding the amount for full backing is named as withdrawable liquidity.&#x20;

Holders of LP tokens are eligible to withdraw a pro-rata share of withdrawable liquidity and accrue a prorated distribution of trading fees gathered from mints and burns through the inverse bonding curve.&#x20;

It can be viewed as if LPs collectively own:&#x20;

$$
R-PS
$$



### Adding Liquidity

With the addition of $$\Delta R$$ amount of reserve assets, the liquidity utilization changes to a new value ($$u^{\prime}$$), which is:&#x20;

$$
u^{\prime}=\frac{R}{R+\Delta R}u
$$

The invariant $$i$$ also updates to a new value of $$i^{\prime}$$:&#x20;

$$
i^{\prime}=\frac{R+\Delta R}{{S}^{u^{\prime}}}
$$

The curve subsequently updates to:&#x20;

$$
P(x)=\frac{{i}^{\prime}{u}^{\prime}}{{\left(S_0+x\right)}^{1-{u}^{\prime}}}
$$

Showing this in graph format looks like the below.&#x20;

<figure><img src="../.gitbook/assets/Add LP.png" alt="" width="375"><figcaption></figcaption></figure>

Where the red curve representing the inverse bonding curve prior to the LP addition and the blue curve corresponding to the curve after adding liquidity. As seen on the graph, the increased market depth allows users to mint more assets per reserve asset used and retrieve more reserve assets per asset burnt.&#x20;



The LP is also minted LP tokens of the below amount.&#x20;

$$
\Delta L=\frac{L}{\left(1-u\right)}\cdot \frac{\Delta R}{R}
$$

Where $$\Delta L$$ is the amount of LP tokens being minted, $$L$$ being the total supply of LP tokens prior to the LP, $$R$$ being the reserve asset balance of the curve, $$\Delta R$$ being the amount of reserve assets being provided, and $$u$$ being the liquidity utilization prior to the LP.&#x20;



### Removing Liquidity

The removal of amount $$\Delta R$$ amount of liquidity changes the liquidity utilization to $$u^{\prime}$$:&#x20;

$$
u^{\prime}=\frac{R}{R-\Delta R}u
$$

The invariant $$i$$ also changes to a new value of $$i^{\prime}$$:&#x20;

$$
i^{\prime}=\frac{R-\Delta R}{{S}^{u^{\prime}}}
$$

With the new values of $$u^{\prime}$$ and $$i^{\prime}$$, the curve updates to:&#x20;

$$
P(x)=\frac{{i}^{\prime}{u}^{\prime}}{{\left(S_0+x\right)}^{1-{u}^{\prime}}}
$$

Displaying the update as a graphed format gives out:&#x20;

<figure><img src="../.gitbook/assets/Remove LP (1).png" alt="" width="375"><figcaption></figcaption></figure>

With the red curve showing the inverse bonding curve prior to LP withdrawal and the blue curve being the inverse bonding curve post-withdrawal. The new curve shows decreased market depth.



The removal of liquidity also withdraws the LP's portion of reserve liquidity, calculated as:&#x20;

$$
\Delta R=\left(1-u\right)R\cdot \frac{\Delta L}{L}
$$

Where $$\Delta R$$ is the amount of reserve assets tokens being returned, $$R$$ being the reserve asset balance of the curve, $$L$$ being the total supply of LP tokens prior to the LP removal, $$\Delta L$$ being the amount of reserve assets being provided, and $$u$$ being the liquidity utilization prior to the LP.&#x20;



### LP Value

The value of a LP position changes as assets are minted and burnt. Mints and burns increase and decrease the reserve asset balance, thus causing the differing value. In contrast to a LP position of a regular xyk AMM (e.g. Uniswap V2), **LP positions of inverse bonding curves increase in value as more assets are minted and decrease in value as assets are burnt.**&#x20;

The LP position value is directional proportional to total withdrawable liquidity. Total withdrawable liquidity is calculated as $$R-PS$$ and can be specified as the below.&#x20;

$$
\left(R+\Delta R\right)-P\left(S\right)\cdot S
$$

Which can be simplified to the below with the use of the invariant:&#x20;

$$
i{S}^{u}\left(1-u\right)
$$

Plotting this over as a value-to-asset-supply graph looks like ($$R_0=6, S_0=3, P_0=1$$):&#x20;

<figure><img src="../.gitbook/assets/LP value.png" alt="" width="375"><figcaption></figcaption></figure>

