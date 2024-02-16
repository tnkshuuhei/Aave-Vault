[![Foundry][foundry-badge]][foundry]

[foundry]: https://getfoundry.sh/
[foundry-badge]: https://img.shields.io/badge/Built%20with-Foundry-FFDB1C.svg

# Aave Vault

An ERC-4626 vault which allows users to deposit/withdraw ERC-20 tokens supported by Aave v3, manages the supply and withdrawal of these assets in Aave, and allows a vault manager to take a fee on yield earned.

## Instructions

To compile/build the project, run `forge build`.

To run the test suite, run `forge test`.

## Tests

Some of the tests rely on an RPC connection for forking network state. Make sure you have an `.env` file in the root directory of the repo with the following keys and values:

```
POLYGON_RPC_URL=[Your favourite Polygon RPC URL]
AVALANCHE_RPC_URL=[Your favourite Avalanche RPC URL]
```

The fork tests all use Polygon, except tests for claiming Aave rewards, which use Avalanche.

This test suite also includes a16z's [ERC-4626 Property Tests](https://a16zcrypto.com/generalized-property-tests-for-erc4626-vaults/), which are in the `ATokenVaultProperties.t.sol` file. These tests do not use a forked network state but rather use mock contracts, found in the `test/mocks` folder.

## Deployment

Proxy on OPGoerli: https://goerli-optimism.etherscan.io/address/0xc83ad197808A948B29c8E94b3345508D296c7F7D#code

To deploy the vault contract, first check that the deployment parameters in `script/Deploy.s.sol` are configured correctly, then check that your `.env` file contains these keys:

```
PRIVATE_KEY=
OPGOERLI_RPC_UR=https://optimism-goerli.infura.io/v3/

ETHERSCAN_API_KEY=
ETHERSCAN_OPTIMISM_API_KEY=
ETHERSCAN_POLYGON_API_KEY=
ETHERSCAN_ARBITRUM_API_KEY=
```

Then run:

```bash
source .env
```

Then run one of the following commands:

OpGoerli:

```bash
forge script script/opGoerli_Deploy.s.sol:Deploy --rpc-url $OPGOERLI_RPC_UR --broadcast -vvvv --etherscan-api-key $ETHERSCAN_OPTIMISM_API_KEY --verify
```

## Audits

You can find all audit reports under the audits folder

- [01-03-2023 OpenZeppelin](./audits/01-03-2023_OpenZeppelin_Wrapped_AToken_Vault.pdf)
- [03-03-2023 PeckShield](./audits/03-03-2023_Peckshield_Wrapped_AToken_Vault.pdf)
- [18-06-2023 Certora](./certora/report/Aave-Vault-Formal-Verification.pdf)

## License

All Rights Reserved © AaveCo
