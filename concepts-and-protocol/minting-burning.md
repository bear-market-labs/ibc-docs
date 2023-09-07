# Minting / Burning

Just like bonding curves, users may buy (mint) / sell (burn) assets to / from an initialized inverse bonding curve. The inverse bonding curve acts as the counterparty for such trades, utilizing its liquidity reserve as market liquidity.&#x20;

Just like regular bonding curves, the amount of reserve assets required to mint a certain amount of assets is equivalent to the area under the inverse bonding curve (integral of the curve). The integral can be calculated as:&#x20;

$$
\int_{0}^{\Delta S} P \cdot {\left(\frac{S}{S+x}\right)}^{1-\frac{PS}{R}}dx
$$







### Minting

New assets can be minted (bought) by supplying reserve assets to the inverse bonding curve, from which the inverse bonding curve calculates the amount to be minted. If the amount of reserve assets supplied is \Delta R,&#x20;



### Burning

with its liquidity reserve used to either receive new reserve assets from minting, or give out reserve assets from burning.&#x20;

Once an inverse bonding curve is initialized, users may mint asset by supplying&#x20;
