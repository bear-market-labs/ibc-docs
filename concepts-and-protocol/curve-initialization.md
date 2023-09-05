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



### Initial LP Token Mint

The initializer of the curve is also minted LP tokens, representing their contribution to the liquidity reserve.&#x20;



$$
\Delta L = \frac{\Delta R}{R-PS} \cdot L
$$



