# Minting / Burning

Just like bonding curves, users may buy (mint) / sell (burn) IBC to / from an initialized inverse bonding curve. The inverse bonding curve acts as the counterparty for such trades, utilizing its liquidity reserve as market liquidity.&#x20;

Just like regular bonding curves, the amount of ETH required to mint a certain amount of IBC is equivalent to the area under the inverse bonding curve (integral of the curve). While values for minting and burning can be calculated with integration, it can also be derived from the curve's invariant with ease.&#x20;

$$
\frac{R}{S^u}=\frac{R+\Delta R}{{\left(S+\Delta S\right)}^u}=const.
$$



### Minting

New IBC tokens can be minted (bought) by supplying ETH to the inverse bonding curve, from which the inverse bonding curve calculates the amount to be minted. If the amount of ETH supplied is $$\Delta R$$ and the amount being is $$\Delta S$$, the below must be satisfied.&#x20;

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



### Burning

Users may also burn minted IBC via the inverse bonding curve to receive ETH. The amount of IBC burnt ($$\Delta S$$) and the amount of ETH given ($$\Delta R$$) has the relationship of:&#x20;

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

