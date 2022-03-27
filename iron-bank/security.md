# Security

### Iron Bank

Iron Bank refers to the set of lending contracts that represent the Iron Bank money market. More on Iron Bank in their main documentation at [docs.ib.xyz](https://docs.ib.xyz/v/ethereum/). Markets can be added or removed via the [Iron Bank Unittroller](https://etherscan.io/address/0xAB1c342C7bf5Ec5F02ADEA1c2270670bCa144CbB). The admin for Iron Bank is the [Iron Bank Multisig](https://etherscan.io/address/0xa5fc0bbfcd05827ed582869b7254b6f141ba84eb#code). The list of multisig signers can be found [here](https://gnosis-safe.io/app/eth:0xA5fC0BbfcD05827ed582869b7254b6f141BA84Eb/settings/owners)

* [Github](https://github.com/ibdotxyz)
* [docs.ib.xyz](https://docs.ib.xyz/v/ethereum/)
* [ib.xyz](https://ib.xyz/)

### Oracles

Price Oracles are maintained by Iron Bank, more detail found [here](https://docs.ib.xyz/v/ethereum/lending-market/price-oracle)

### ibXX

ibXX (Fixed Forex assets, example; ibCHF, ibEUR, ibAUD) are erc20 tokens that are pegged to their corresponding forex pair name. They can only be borrowed via Iron Bank by supplying collateral in one of Iron Bank's accepted collateral options, list available [here](https://docs.ib.xyz/v/ethereum/lending-market/collateral-factor).

This means that each ibXX asset is backed by a $ amount equal to its fiat value. If 1 ibCHF is borrowed, it had to be backed by at least 1 CHF of value (whether that asset be in the form of BTC, CRV, ETH, etc).

Iron Bank liquidations ensure that the ibXX assets maintain their peg. Further to this is the dynamic interest rate model. Should the peg drift above the underlying price, supply can be burned in Iron Bank, increasing interest rates (forcing repayments or liquidations). If the peg drifts below the underlying price, additional supply can be minted into Iron Bank to decrease interest rates, stimulating borrowing demand.

ibXX assets are owned by the [ib_controller](https://etherscan.io/address/0xa511da90c2f4c557456cd84cd003a1f74c202d80#code), which in turn is owned by the [Keep3r multisig](https://etherscan.io/address/0x0d5dc686d0a2abbfdafdfb4d0533e886517d4e83). The list of multisig signers can be found [here](https://gnosis-safe.io/app/eth:0x0d5dc686d0a2abbfdafdfb4d0533e886517d4e83/settings/owners)

* [Github](https://github.com/keep3r-network/ff)
* [docs.fixedforex.fi](https://docs.fixedforex.fi/)
* [fixedforex.fi](https://fixedforex.fi/)

### Life cycle

ibXX (Fixed Forex assets, example: ibCHF) & cyXX (Iron Bank assets, example: cyCHF) are explicitly linked. At contract deployment an ibXX asset references a corresponding cyXX asset, this can not be changed after deployment.

ibXX assets can be `minted` only for the purpose of depositing into cyXX assets. They can not be minted and sent to any other address. This ensures that ibXX assets can only enter circulating supply by being borrowed from Iron Bank (and thus backed by collateral).

## Risk Vectors

* Keep3r Multisig can mint large supply into Iron Bank which decreases interest rates.
* Keep3r Multisig can burn large supply from Iron Bank which increases interest rates.
* Iron Bank Multisig can add a dangerous oracle that incorrectly provides price.
* Iron Bank Multisig can add a dangerous asset that can be used to drain collateral.
