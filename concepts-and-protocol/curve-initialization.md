# Curve Initialization

The inverse bonding curve first starts off with the supplement of initial liquidity reserves ($$R_0$$), together with the specified values of initial minted supply ($$S_0$$), and the starting spot price ($$P_0$$).&#x20;



### Curve Formation

Following from a generic inverse bonding curve of $$\frac{m}{x^k}$$, the initialized curve must show a spot price of $$P_0$$ at a minted supply of $$S_0$$:&#x20;

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



### Initial Asset Mint

During curve initialization, the initializer is given newly minted assets. The minted amount is equivalent to the initial supply specified at initialization, $$S_0$$.



### Initial LP Token Mint

The initializer of the curve is also minted LP tokens, representing their contribution to the liquidity reserve. The minted LP token amount is equal to the supplied amount of liquidity reserves, minus the amount of reserves needed to fully back initial minted supply at the initial price:&#x20;

$$
R_0-P_0S_0
$$

