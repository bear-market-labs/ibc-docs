# Minting / Burning

Just like bonding curves, users may buy (mint) / sell (burn) ibAsset to / from an initialized IBC. The IBC acts as the counterparty for such trades, utilizing its liquidity reserve as market liquidity.&#x20;

Just like regular bonding curves, the amount of reserve assets required to mint a certain amount of ibAssets is equivalent to the area under the IBC's price curve (integral of the curve). While values for minting and burning can be calculated with integration, it can also be derived from the curve's invariant with ease:&#x20;

$$
i=\frac{R}{S^u}=\frac{R+\Delta R}{{\left(S+\Delta S\right)}^u}=const.
$$



## Minting

New ibAssets can be minted (bought) by supplying reserve assets to the relevant IBC, from which the IBC of the reserve asset calculates the amount to be minted. If the amount of reserve assets supplied is $$\Delta R$$ and the amount being minted is $$\Delta S$$, the below must be satisfied.&#x20;

$$
\frac{S}{S+\Delta S}={\left(\frac{R}{R+\Delta R}\right)}^{\frac{1}{u}}
$$

Thereby yielding $$\Delta S$$ as:&#x20;

$$
\Delta S={\left(1+\frac{\Delta R}{R}\right)}^{\frac{1}{u}}S-S
$$

The spot price post-mint is the updated to become the below:&#x20;

$$
\frac{iu}{{\left(S+\Delta S\right)}^{1-u}}
$$



## Burning

Users may also burn minted ibAssets via the relevant IBC to receive reserve assets. The amount of ibAssets burnt ($$\Delta S$$) and the amount of reserve assets given ($$\Delta R$$) has the relationship of:&#x20;

$$
\frac{R}{R-\Delta R}={\left(\frac{S}{S-\Delta S}\right)}^{u}
$$

From which $$\Delta R$$ comes out as:&#x20;

$$
\Delta R=R-{\left(1-\frac{\Delta S}{S}\right)}^{u}R
$$

The post-burn price then becomes:&#x20;

$$
\frac{iu}{{\left(S-\Delta S\right)}^{1-u}}
$$
