# contracts

Source code for the GNGA.WEB3 Protocol's deployed smart contracts.

## GNGAToken.sol

The $GNGA ERC-20 token contract.

| | |
|---|---|
| **Network** | Polygon |
| **Contract address** | `0x162c2352877C6afc4B483e76aD3238eEf011E1f9` |
| **Verified on** | [Polygonscan](https://polygonscan.com/token/0x162c2352877C6afc4B483e76aD3238eEf011E1f9) |
| **Compiler** | Solidity `0.8.27` |
| **Optimization** | Disabled |
| **Base contracts** | OpenZeppelin Contracts `5.6.0` — `ERC20`, `ERC20Permit`, `Ownable` |

### Supply

The constructor mints the entire fixed supply once, to the deployer-specified recipient, and no other function in this contract or its OpenZeppelin base contracts can mint additional tokens:

```solidity
constructor(address recipient, address initialOwner)
    ERC20("GNGA", "GNGA")
    ERC20Permit("GNGA")
    Ownable(initialOwner)
{
    _mint(recipient, 24000000 * 10 ** decimals());
}
```

This enforces the protocol's Hard Cap (24,000,000 $GNGA) at the code level: the absence of any additional mint path, not a policy promise, is what makes supply immutable.

### Ownership

This contract inherits OpenZeppelin's `Ownable`, which grants the `owner` address the ability to call `renounceOwnership()` or `transferOwnership()`. Ownership was transferred post-deployment from the deployer wallet to **The Vault's Master Vault** (the protocol's 3-of-3 multi-signature Safe) — see [`gngaweb3/the-vault`](https://github.com/gngaweb3/the-vault) and the [Onchain Registry](https://gnga.tech/onchain-registry) for that address. No individual wallet holds owner privileges on this contract.

`Ownable` in this contract does not gate any token-supply or transfer logic — `GNGAToken.sol` defines no owner-only functions beyond what OpenZeppelin's base contracts expose (`renounceOwnership`, `transferOwnership`). It is present because the OpenZeppelin Wizard template includes it by default, not because the token relies on owner-gated functionality.

### Verifying this contract

To confirm the deployed bytecode matches this source:

1. Compile `GNGAToken.sol` with `solc 0.8.27`, optimization disabled, against OpenZeppelin Contracts `5.6.0`.
2. Compare the resulting bytecode against the verified source on [Polygonscan](https://polygonscan.com/token/0x162c2352877C6afc4B483e76aD3238eEf011E1f9).

The file in this repo is the flattened source (OpenZeppelin dependencies inlined) as used for verification — the same format Polygonscan displays under "Contract Source Code."

## License

Released under the [MIT License](./LICENSE).

---

*GNGA.WEB3 Protocol*
