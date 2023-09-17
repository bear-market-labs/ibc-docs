# IBC Token

The inverse bonding curve (IBC) token is the token minted via the first onchain implementation of the inverse bonding curve, which uses ETH as its reserve asset. The IBC token is utilized to showcase the characteristics of inverse bonding curves, and serves no utility (including governance controls) in or out of the protocol aside from fee accruals.&#x20;



### Characteristics

All IBC in existence is minted through the inverse bonding curve and thus contains the following properties:&#x20;



#### Algorithmic, inversed pricing

The price of IBC relative to ETH is algorithmically set by the inverse bonding curve. Contrary to the regular market behavior of an asset price increasing with buying demand and decreasing with selling demand, the inverse bonding curve enforces a market behavior of the exact inverse - IBC's price (denominated in ETH) decreases with buying demand and increases with selling demand.&#x20;



#### Dynamic, unbounded supply through instant liquidity

At any point in time, any user is able to mint new IBC into existence by supplying ETH to the inverse bonding curve implementation. Similarly, any user at any time can burn existing IBC via the inverse bonding curve implementation to receive ETH.&#x20;

The IBC supply starts from a genesis supply of 0 (virtual supply at initialization is not considered as no user owns it) and increases as users choose to mint. An infinite amount of IBC can be minted although requiring an infinite supplement of ETH.&#x20;



### Staking

IBC can be staked to accrue fees generated from the inverse bonding curve implementation. Fees are distributed to stakers pro-rata to their stake. IBC staking, combined with IBC's inverse pricing characteristics gives rise to an interesting result - later entrants can acquire a higher stake of distributed fees, with earlier participants having dilution rates of increasing speed as more users enter staking. This prevents potential rent-seeking behaviors from early entrants.&#x20;

