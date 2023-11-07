# Deployed Contracts

The smart contracts that constitute the inverse bonding curve implementation are deployed on the Ethereum blockchain, and can be found on the below networks:&#x20;



## Networks

| Classification | Name             | Chain ID |
| -------------- | ---------------- | -------- |
| Mainnet        | Ethereum Mainnet | 1        |



## Contract Addresses

{% tabs %}
{% tab title="Mainnet" %}
#### Core IBC Contracts

| Name        | Address                                      |
| ----------- | -------------------------------------------- |
| IBC Factory | `0x7957F57deafe60b2D0CCdEdBBED85da6f5374adB` |
| IBC Router  | `0x24a60379c53D90c6E154D7f20EDD25EDbd542b57` |
| IBC Admin   | `0xE42F7aeA4788CF7198149e8E5f2a557Af475C97d` |

#### ibETH-Related Contracts

| Name                              | Address                                      |
| --------------------------------- | -------------------------------------------- |
| ibETH InverseBondingCurve (Proxy) | `0x5594B3D6EbeAbbc13aFC39f569961521e9425262` |
| ibETH (ERC20)                     | `0xE73EE64adB39a443A251c910e4e3B56f7a4130DC` |
{% endtab %}
{% endtabs %}



## Admin Controls

IBCs are a novel mechanism that hasn't existed anywhere before. All novel mechanisms contain the risk of unexpected / unwanted logic executions. Although the IBC implementation has been audited, certain admin controls are added to mitigate the possibility of such risks:&#x20;

* **Pausability**: the admin can pause the implementation, disallowing further interactions.&#x20;
* **Upgradability**: the admin can upgrade the implementation code.&#x20;

These admin controls are temporary and are planned to be removed as the implementation stabilizes.&#x20;
