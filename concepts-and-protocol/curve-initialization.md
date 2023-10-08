# Curve Initialization

The inverse bonding curve first starts off with an initializer providing initial parameter values of initial (virtual) liquidity reserves ($$R_0$$), initial (virtual) minted supply ($$S_0$$), and the starting spot price ($$P_0$$).&#x20;



### Virtual Reserves and Supply

The reserves and supply values specified at initialization are virtual - meaning no reserve assets are actually provided and no assets nor LP tokens are actually minted back to the initializer. The virtual reserves and supply are only used for calculating further interactions with the initialized curve and cannot be used to withdraw or trade against the curve's liquidity reserves, even when actual reserve assets have been provided the later user interactions.&#x20;



#### Initial Reserve Amount (Virtual)

The curve initializes to consider itself containing the specified $$R_0$$ amount of liquidity reserves. The actual reserve asset balance of itself is 0, as no reserve assets have been provided at initialization.&#x20;



#### Initial Asset Supply (Virtual)

The initialized curve starts with a minted asset supply equivalent to the initial supply specified at initialization, $$S_0$$. No user has ownership of this minted amount and this amount thus cannot be staked or accrue fees distributed to stakers.&#x20;



#### Initial LP Token Supply (Virtual)

The curve also starts with an initial minted supply of LP tokens, later used to calculate the LP token mint amounts to those providing liquidity to the initialized curve. This initial minted supply is also of a virtual value, meaning it is not owned by any user and is excluded from all fee distributions to LPs. The virtual LP token amount is calculated as:&#x20;

$$
P_0\left(R_0-P_0S_0\right)
$$

Which is equal to the initial price, times the specified amount of virtual reserves minus the amount of virtual reserves that would be needed to fully back the initial virtual minted supply at the initial price.&#x20;



### Curve Formation

Following from a generic inverse bonding curve of $$\frac{m}{x^k}$$, the initialized curve must show a spot price of $$P_0$$ at a minted virtual supply of $$S_0$$:&#x20;

$$
\frac{m}{{S_0}^k}=P_0
$$

The curve should also contain a liquidity reserve of $$L_0$$ at a minted supply of $$S_0$$:&#x20;

$$
\int_{0}^{S_0}\frac{m}{x^{k}}dx=\frac{m{S_0}^{1-k}}{1-k}=R_0
$$

Whereby combining the two yields the values for $$m$$and $$k$$:&#x20;

$$
m=P_0{S_0}^{1-\frac{P_0S_0}{R_0}},\,k=1-\frac{P_0S_0}{R_0}
$$

The curve is then defined as the below:&#x20;

$$
P(x)=P_0{\left(\frac{S_0}{S_0+x}\right)}^{1-\frac{P_0S_0}{R_0}}
$$

Where $$x$$ is the amount of assets being minted following initialization.&#x20;



### Curve Invariant

The generated inverse bonding curve is observed to have the below invariant ($$i$$) as mints and burns occur. $$i$$ does not update during mints and burns, but updates with LP additions and withdraws.

$$
i=\frac{R}{S^{u}}
$$

$$u$$ represents the utilization of provided liquidity vs. liquidity used to back minted assets at the current spot price. Similar to $$i$$, $$u$$ does not update during mints and burns, but updates with LP additions and withdrawals. $$u$$ is defined as:&#x20;

$$
u=\frac{PS}{R}
$$

With initialized values of $$R_0$$, $$S_0$$, $$P_0$$, the values $$i$$ and $$u$$ are set as:&#x20;

$$
i=\frac{R_0}{{S_0}^{u}},\,u=\frac{P_0S_0}{R_0}
$$

The newly added values of $$i$$ and $$u$$ allow the price curve to also be written as:&#x20;

$$
P(x)=\frac{iu}{{\left(S_0+x\right)}^{1-u}}
$$

The invariant is used extensively in the inverse bonding curve's implementation.&#x20;

