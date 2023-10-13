# Inverse Bonded Assets (ibAssets)

ibAssets are tokens minted via IBCs. ibAssets are utilized to showcase the characteristics of IBCs, and serves no utility (including governance controls) in or out of the protocol aside from fee accruals from staking or providing liquidity.&#x20;

<figure><img src="../.gitbook/assets/IBC_Logo_Circlized.svg" alt="" width="188"><figcaption><p>Reference logo for ibAssets</p></figcaption></figure>



The first ibAsset to exist is ibETH, which uses ETH as its reserve asset. ibETH is generated at protocol genesis, being the first asset to show inversed market properties.&#x20;

<figure><img src="../.gitbook/assets/ibETH_Logo.svg" alt="" width="188"><figcaption><p>ibETH logo</p></figcaption></figure>



## Characteristics

All ibAssets in existence are minted through IBCs and thus contains the following properties:&#x20;



### Algorithmic, inversed pricing

The price of ibAssets relative to their reserve assets is algorithmically set by the IBC. Contrary to the regular market behavior of an asset price increasing with buying demand and decreasing with selling demand, the IBC enforces a market behavior of the exact inverse - prices of ibAssets (denominated in their reserve assets) decreases with buying demand and increases with selling demand.&#x20;



### Dynamic, unbounded supply through instant liquidity

At any point in time, any user is able to mint new ibAssets into existence by supplying reserve assets to the IBC implementation. Similarly, any user at any time can burn existing ibAssets via the IBC implementation to receive its reserve assets.&#x20;

The ibAsset supply starts from a genesis supply (supply minted from initial reserves) and increases as users choose to mint. An infinite amount of ibAssets can be minted although requiring an infinite supplement of reserve assets.&#x20;



### Staking

ibAssets can be staked to accrue fees generated from the IBC implementation. Fees are distributed to stakers pro-rata to their stake. ibAsset staking, combined with ibAssets' inverse pricing characteristics gives rise to an interesting result - later entrants can acquire a higher stake of distributed fees, with earlier participants having dilution rates of increasing speed as more users enter staking. This prevents potential rent-seeking behaviors from early entrants.&#x20;
