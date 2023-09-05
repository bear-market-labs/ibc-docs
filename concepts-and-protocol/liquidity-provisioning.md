# Liquidity Provisioning

Similar to those in xyk automated market makers (AMMs), external capital can be provided to enhance the liquidity of an inverse bonding curve. Liquidity providers (LPs), entities that perform the act of providing liquidity, provide additional reserve assets to an inverse bonding curve. Provided reserve assets are then utilized by the inverse bonding curve to facilitate the minting and burning of assets.&#x20;

The added liquidity triggers the curvature of inverse bonding curves to be updated - in a way that greater market depth is given to those to mints and burns of the same size. However, the current spot price and the minted asset supply remains unchanged.&#x20;



### LP Tokens

Providers of liquidity are given freshly minted LP tokens, a tokenized representation of a LP's share of the reserve liquidity, minus the amount of reserve assets required to fully back all minted assets at the current spot price - this exclusion is the ensure the inverse bonding curve never flips back to a regular non-inverse bonding curve during LP withdrawals. The reserve liquidity excluding the amount for full backing is named as withdrawable liquidity.&#x20;

Holders of LP tokens are eligible to withdraw a pro-rata share of withdrawable liquidity and accrue a prorated distribution of trading fees gathered from mints and burns through the inverse bonding curve.&#x20;



### Adding Liquidity

Starting from an inverse bonding curve of the below, having a starting spot price of $$P_0$$ at a minted supply of $$S_0$$, and a reserve asset balance of $$R_0$$, and with $$x$$ representing the amount of tokens being minted,&#x20;

$$
P(x)=P_{0}\left(\frac{S_{0}}{S_0+x}\right)^{1-\frac{P_{0}S_{0}}{R_{0}}}
$$

The providing of $$\Delta R$$ amount of reserve assets updates the curve to be as of below shape.

$$
P(x)=P_{0}\left(\frac{S_{0}}{S_0+x}\right)^{1-\frac{P_{0}S_{0}}{R_{0}+\Delta R}}
$$

Showing this in graph format looks like the below.&#x20;



&#x20;// Image of curve graphs



Where the red curve representing the inverse bonding curve prior to the LP addition and the blue curve corresponding to the curve after adding liquidity.&#x20;



The LP is also minted LP tokens of the below amount.&#x20;

$$
\Delta L = \frac{\Delta R}{R-PS} \cdot L
$$

Where $$\Delta L$$ is the amount of LP tokens being minted, $$L$$ being the total supply of LP tokens prior to the LP, $$R$$ being the reserve asset balance of the curve, $$\Delta R$$ being the amount of reserve assets being provided, $$P$$ being the current spot price (equivalent to $$P\left(S-S_0\right)$$), and $$S$$ being the current minted asset supply.



### Removing Liquidity

The removal of liquidity withdraws the LP's portion of reserve liquidity, calculated as:&#x20;

$$
\Delta R=\frac{\Delta L}{L} \cdot \left(R-PS\right)
$$

A curve update also conducts from the previous inverse bonding curve of the below,&#x20;

$$
P(x)=P_{0}\left(\frac{S_{0}}{S_0+x}\right)^{1-\frac{P_{0}S_{0}}{R_{0}}}
$$

Updating to the new equation of:&#x20;

$$
P(x)=P_{0}\left(\frac{S_{0}}{S_0+x}\right)^{1-\frac{P_{0}S_{0}}{R_{0}-\Delta R}}
$$

Displaying the update as a graphed format gives out:&#x20;



&#x20;// Image of graphs



With the red curve being the inverse bonding curve prior to LP withdrawal and the blue curve after.&#x20;



### LP Value

The value of a LP position changes as assets are minted and burnt. Mints and burns increase and decrease the reserve asset balance, thus causing the differing value. In contrast to a LP position of a regular xyk AMM (e.g. Uniswap V2), **LP positions of inverse bonding curves increase in value as more assets are minted and decrease in value as assets are burnt.**&#x20;

The LP position value is directional proportional to total withdrawable liquidity. Total withdrawable liquidity is calculated as $$R-PS$$ and can be specified as the below.&#x20;

$$
R-PS=\int_0^S P_0{\left(\frac{S_0}{x}\right)}^{1-\frac{P_0S_0}{R_0}}dx-P_0{\left(\frac{S_0}{S}\right)}^{1-\frac{P_0S_0}{R_0}}S
$$

Which can be simplified to:&#x20;

$$
\left(R_0-P_0S_0\right)\left(\frac{S_0}{S}\right)^{-\frac{P_0S_0}{R_0}}
$$













