# The Inverse Bonding Curve

The inverse bonding curve implementation is the first demonstration of inverse bonding curves; used for minting assets that devalue as bought and rise in value as sold. **The tokens minted via the inverse bonding curve implementation, ibAssets, are the first asset class in history that follows the exact inverse of regular market dynamics.**&#x20;

Inverse bonding curves are a brand new DeFi primitive derived from bonding curves. The pricing algorithm enforced by the inverse bonding curve shows various unique traits, one of them being its arbitrage characteristics. Arbitrage of ibAssets forces ibAssets to devalue per every purchase, regardless of where the purchase was made (CEX, Uniswap, etc. ). **Altogether, the distinctive properties of inverse bonding curves allow for the creation of DeFi mechanisms previously unthought of, one of which is an** [**oracle-free derivatives protocol**](https://docs-staging.exponents.fi/)**.**&#x20;

The purpose of the inverse bonding curve implementation is to increase awareness and understanding of this new primitive, which will help spark DeFi innovations that leverage its features.&#x20;



## Basic Protocol Functions

Two participant types power the inverse bonding curve implementation: ibAsset Minters / Stakers and Liquidity Providers (LPs), and Curve Initializers. ibAssets (e.g. ibETH) can be minted by providing reserve assets (e.g. ETH) to the inverse bonding curve, from which new ibAssets are minted into existence and given to the minter. LPs can provide additional reserve assets to improve the market liquidity of the inverse bonding curve.&#x20;

New ibAsset types can be created for an ERC20 reserve asset of choice. Curve Initializers specify the reserve asset to be used, providing the initial reserve amounts to generate a new inverse bonding curve & ibAsset pair. Initializations are permissionless and can be executed by anyone.&#x20;



Each participant contains the following characteristics:&#x20;

### ibAsset Minters / Stakers

* Their position value increases as more ibAssets are burnt following the mint.&#x20;
* Their position value decreases as more ibAssets are minted following the mint.&#x20;
* Mints and burns incur a fee, distributed to ibAsset stakers and LPs.&#x20;
* Staked ibAssets accrue prorated fees from mints and burns and LP adds and removals.&#x20;
* Later entrants can acquire a higher stake of fees as their mint price is lower.&#x20;



### Liquidity Providers (LPs)

* Their position value increases as the price deviates from the price at the time of LP.&#x20;
* LPs can maintain only one position per account / address at any given time.&#x20;
* LPs must close their previous position in full before modifying their position size.&#x20;
* Adding and removing liquidity incur a fee, distributed to ibAsset stakers and LPs.&#x20;
* LPs accrue prorated fees from mints and burns and LP adds and removals.&#x20;
* LPs may be required to provide or receive additional ibAssets in order for LP removal.&#x20;



### Curve Initializers

* Creates new ibAssets for promising reserve assets.&#x20;
* Curve initializers can be the early users of a new ibAsset, including LPing.&#x20;
* Provides the initial reserves for a new ibAsset and receives a LP position.&#x20;
* A small fee is taken from the provided initial reserves.&#x20;
