# Deployed Contracts

The smart contracts that constitute the inverse bonding curve implementation are deployed on the Ethereum blockchain, and can be found on the below networks:&#x20;



## Networks

| Classification | Name             | Chain ID |
| -------------- | ---------------- | -------- |
| Mainnet        | Ethereum Mainnet | 1        |
| Testnet        | Sepolia          | 11155111 |



## Contract Addresses

{% tabs %}
{% tab title="Mainnet" %}
#### Core IBC Contracts

| Name              | Address |
| ----------------- | ------- |
| IBC Factory Proxy | 0x...   |
| IBC Factory       | 0x...   |
| IBC Router Proxy  | 0x...   |
| IBC Router        | 0x...   |

#### ibETH-Related Contracts

| Name                            | Address |
| ------------------------------- | ------- |
| ibETH InverseBondingCurve Proxy | 0x...   |
| ibETH InverseBondingCurve       | 0x...   |
| ibETH (ERC20)                   | 0x...   |
{% endtab %}

{% tab title="Sepolia" %}
#### Core IBC Contracts

| Name              | Address |
| ----------------- | ------- |
| IBC Factory Proxy | 0x...   |
| IBC Factory       | 0x...   |
| IBC Router Proxy  | 0x...   |
| IBC Router        | 0x...   |

#### ibETH-Related Contracts

| Name                            | Address |
| ------------------------------- | ------- |
| ibETH InverseBondingCurve Proxy | 0x...   |
| ibETH InverseBondingCurve       | 0x...   |
| ibETH (ERC20)                   | 0x...   |
{% endtab %}
{% endtabs %}



## Admin Controls

IBCs are a novel mechanism that hasn't existed anywhere before. All novel mechanisms contain the risk of unexpected / unwanted logic executions. Although the IBC implementation has been audited, certain admin controls are added to mitigate the possibility of such risks:&#x20;

* **Pausability**: the admin can pause the implementation, disallowing further interactions.&#x20;
* **Upgradability**: the admin can upgrade the implementation code.&#x20;

These admin controls are temporary and are planned to be removed as the implementation stabilizes.&#x20;
