---
description: >-
  **THIS DOCUMENT IS STRICTLY CONFIDENTIAL - DO NOT SHARE EXTERNALLY** BEAR
  MARKET LABS PTE. LTD. Feel Free to Reach Out At:
  https://twitter.com/ryanology045
---

# The Inverse Bonding Curve

The inverse bonding curve implementation is the first demonstration of inverse bonding curves; used for minting assets that devalue as bought and rise in value as sold. **The token minted via the inverse bonding curve implementation, IBC, is the first asset in history that follows the exact inverse of regular market dynamics.**&#x20;

Inverse bonding curves are a brand new DeFi primitive derived from bonding curves. The pricing algorithm enforced by the inverse bonding curve shows various unique traits, one of them being its arbitrage characteristics. Arbitrage of IBC forces IBC to devalue per every purchase, regardless of where the purchase was made (CEX, Uniswap, etc. ). **Altogether, these distinctive properties of inverse bonding curves allow for the creation of DeFi mechanisms previous unthought of, including but not limited to an oracle-free derivatives protocol.**&#x20;

The purpose of the inverse bonding curve implementation is to increase awareness and understanding of this new primitive, which will help spark DeFi innovations that leverage its features.&#x20;



### Basic Protocol Functions

Two participant types power the inverse bonding curve implementation: IBC Minters / Stakers and Liquidity Providers (LPs). IBC can be minted by providing reserve assets (ETH) to the inverse bonding curve, from which new IBC tokens are minted into existence and given to the minter. LPs can provide additional ETH to improve the market liquidity of the inverse bonding curve.&#x20;



Each participant contains the following characteristics:&#x20;

#### IBC Holders / Stakers

* Their position value increases as more IBC tokens are burnt following the mint.&#x20;
* Their position value decreases as more IBC tokens are minted following the mint.&#x20;
* Mints and burns incur a fee, distributed to IBC stakers and LPs.&#x20;
* Staked IBC accrues prorated fees from mints and burns and LP adds and removals.&#x20;
* Later entrants can acquire a higher stake of fees as their mint price is lower.&#x20;



#### Liquidity Providers (LPs)

* Their position value increases as the price deviates from the price at the time of LP.&#x20;
* Adding and removing liquidity incur a fee, distributed to IBC stakers and LPs.&#x20;
* LPs accrue prorated fees from mints and burns and LP adds and removals.&#x20;
* LPs may be required to provide or receive additional IBC in order for LP removal.&#x20;
