# Interoperability of Blockchains

## ac_cc

::: warning Notice
This parameter is still in testing.
:::

The `ac_cc` parameter sets the network cluster on which the chain can interact with other chains via CryptoConditions modules and MoMoM technology.

Once activated, the `ac_cc` parameter can allow features such as cross-chain fungibility -- coins on one asset chain can be directly transferred to any other asset chain that has the same `ac_cc` setting and the same set of notary nodes (same set of `notary pubkeys`) .


Most functionalities enabled by `ac_cc` can function with or without Komodo's notarization service. However, cross-chain transaction validation and its dependent features, including cross-chain fungibility, require notarization.
### ac_cc=0

Setting `ac_cc=0` disables CryptoConditions on the asset chain entirely. 

::: tip
It is better to <b>NOT</b> use `ac_cc=0` for an asset chain where CryptoConditions should not be enabled. Omitting the `ac_cc` parameter altogether will achieve the same result.
:::

### ac_cc=1

Setting `ac_cc=1` permits CryptonConditions on the asset chain, but will not allow the asset chain to interact in cross-chain CryptoConditions functionality with other asset chains.

### ac_cc=2 to 99

The values of `2` through `99` (inclusive) indicate asset chains that can validate transactions that occur on other asset chains on the same cluster (i.e. the same `ac_cc` value), but their coins are not fungible.

However, coins are not fungible, and therefore cannot be transferred between blockchains.

### ac_cc=100 to 9999

Setting the value of `ac_cc` to any value greater than or equal to `100` will permit cross-chain interaction with any asset chain that has the same `ac_cc` value and is secured by notary nodes with the same `pubkey`.

All asset chains that have the same `ac_cc (>= 100)` value form a cluster, where the base tokens of all the chains in the cluster are fungible via the burn protocol.

For example, an asset chain set to `ac_cc=201` in its parameters can interact with other asset chains with `ac_cc=201` on the same notary-node network, but cannot interact with an asset chain set to `ac_cc=301`.

### Summary of `ac_cc`

::: tip Consider a chain with -ac_cc=N
* If <b>N = 0</b>, CryptoConditions is disabled
* If <b>N > 0</b>, CryptoConditions is enabled
* If <b>N = 1</b>, on-chain CryptoConditions is active, cross-chain validation is disabled
* If <b>N >= 2 and <= 99</b>, the chain allows for cross-chain contracts between all other chains bearing the same N value. The base coins in each asset chain are non-fungible across chains.
* If <b>N >= 100</b>, the chain can form a cluster with all other chains with the same N value and on the same dPoW notarization network. The base coins of all chains in the cluster are fungible via the burn protocol.
:::

**Examples:**

A 777777 pre-mined chain with no smart contracts enabled.

```bash
./komodod -ac_name=HELLOWORLD -ac_supply=777777 &
```

A 777777 pre-mined chain with smart contracts on-chain only; no cross-chain smart contracts.

```bash
./komodod -ac_name=HELLOWORLD -ac_supply=777777 -ac_cc=1 &
```

A 777777 pre-mined chain where smart-contracts are allowed between all fellow asset chains that have -ac_cc=2 in their launch parameters. However, the cross-chain burn protocol is not active, and therefore coins cannot be transferred between chains.

```bash
./komodod -ac_name=HELLOWORLD -ac_supply=777777 -ac_cc=2 &
```

A 777777 pre-mined chain. Smart-contracts are allowed between all fellow asset chains that have -ac_cc=102 in their launch parameters. Also, all -ac_cc=102 chains can use the cross-chain burn protocol to transfer coins from one chain to another.

```bash
./komodod -ac_name=HELLOWORLD -ac_supply=777777 -ac_cc=102 &
```
