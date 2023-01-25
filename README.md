# Drips Protocol contest details

- Total Prize Pool: $90,500 USDC
  - HM awards: $63,750 USDC
  - QA report awards: $7,500 USDC
  - Gas report awards: 3,750 USDC
  - Judge + presort awards: $15,000 USDC
  - Scout awards: $500 USDC
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2023-01-drips-protocol-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts January 25, 2023 20:00 UTC
- Ends February 3, 2023 20:00 UTC

## C4udit / Publicly Known Issues

The C4audit output for the contest can be found [here](https://gist.github.com/supernovahs/ed0ecfe251e3adf824bb669be981bca9) within an hour of contest opening.

*Note for C4 wardens: Anything included in the C4udit output is considered a publicly known issue and is ineligible for awards.*

# Overview

Radicle Drips is an EVM blockchain protocol for streaming and splitting ERC-20 tokens.

## Docs

See [docs](https://v2.docs.drips.network) for a high-level introduction and documentation.

## Video introduction

Watch a quick [video introduction](https://www.youtube.com/watch?v=sL3RrBDkPWA) into the codebase.

# Scope

| Contract                                                  | SLOC  | Purpose | Libraries used
| -                                                         | -     | -       | -
[Drips.sol](https://github.com/code-423n4/2023-01-drips/blob/main/src/Drips.sol)                                  | 672   | The dripping logic for DripsHub, it exposes no public functions, and it acts as a library. |
[DripsHub.sol](https://github.com/code-423n4/2023-01-drips/blob/main/src/DripsHub.sol)                            | 259   | The smart contract implementing Drips protocol, it exposes the entire protocol API. | [openzeppelin/token/ERC20/IERC20.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/token/ERC20/IERC20.sol) [openzeppelin/token/ERC20/utils/SafeERC20.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/token/ERC20/utils/SafeERC20.sol)
[Splits.sol](https://github.com/code-423n4/2023-01-drips/blob/main/src/Splits.sol)                                | 151   | The splitting logic for DripsHub, it exposes no public functions, and it acts as a library. |
[NFTDriver.sol](https://github.com/code-423n4/2023-01-drips/blob/main/src/NFTDriver.sol)                          | 149   | The DripsHub driver implementing NFT-based users identification for the protocol. | [openzeppelin/metatx/ERC2771Context.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/metatx/ERC2771Context.sol) [openzeppelin/token/ERC20/utils/SafeERC20.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/token/ERC20/utils/SafeERC20.sol) [openzeppelin/utils/StorageSlot.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/utils/StorageSlot.sol) [openzeppelin/token/ERC721/extensions/ERC721Burnable.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/token/ERC721/extensions/ERC721Burnable.sol)
[Managed.sol](https://github.com/code-423n4/2023-01-drips/blob/main/src/Managed.sol)                              |  86   | The mix-in adding upgrading, pausing and ownership management to smart contracts. | [openzeppelin/proxy/utils/UUPSUpgradeable.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/proxy/utils/UUPSUpgradeable.sol) [openzeppelin/proxy/ERC1967/ERC1967Proxy.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/proxy/ERC1967/ERC1967Proxy.sol) [openzeppelin/utils/StorageSlot.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/utils/StorageSlot.sol) [openzeppelin/utils/structs/EnumerableSet.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/utils/structs/EnumerableSet.sol)
[Caller.sol](https://github.com/code-423n4/2023-01-drips/blob/main/src/Caller.sol)                                |  77   | The generic implementation of batching, approvals and signed permissions for smart contracts. | [openzeppelin/utils/Address.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/utils/Address.sol) [openzeppelin/utils/cryptography/draft-EIP712.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/utils/cryptography/draft-EIP712.sol) [openzeppelin/metatx/ERC2771Context.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/metatx/ERC2771Context.sol) [openzeppelin/utils/structs/EnumerableSet.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/utils/structs/EnumerableSet.sol)
[AddressDriver.sol](https://github.com/code-423n4/2023-01-drips/blob/main/src/AddressDriver.sol)                  |  74   | The DripsHub driver implementing address-based users identification for the protocol. | [openzeppelin/metatx/ERC2771Context.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/metatx/ERC2771Context.sol) [openzeppelin/token/ERC20/utils/SafeERC20.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/token/ERC20/utils/SafeERC20.sol)
[ImmutableSplitsDriver.sol](https://github.com/code-423n4/2023-01-drips/blob/main/src/ImmutableSplitsDriver.sol)  |  35   | The DripsHub driver implementing simplified user identification only capable of creating splits configurations that can never be updated. | [openzeppelin/utils/StorageSlot.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.8.0/contracts/utils/StorageSlot.sol)

## Out of scope

Drips protocol is 100% on-chain and self-contained, except ERC-20 tokens it works with and drivers.
There are no off-chain actors, and no 3rd party services like oracles or DEX-es involved.

If malicious or unexpected behavior of an ERC-20 contract is a cause of loss or a tool of theft of these ERC-20 tokens, it's not considered an issue in scope.
If such ERC-20 contract can cause loss or theft of other ERC-20 tokens without collusion, it's considered an issue in scope.

The protocol is extendable with drivers, and drivers should not be able to break the protocol.
If a malicious driver causes harm to users with IDs in range managed by that driver, it's not considered an issue in scope.
By harm we mean loss or theft of funds, but also harmful changes to configuration,
e.g. the drips configuration, which may cause dripping to unwanted receivers,
or the splits configuration, which may redirect received funds to unwanted receivers.
If a malicious driver can harm users with IDs outside of range managed by that driver, it's considered an issue in scope.

# Additional Context

## Drivers

The protocol at its core operates on abstract user IDs.
A contract can be registered in DripsHub as a drivers, then it gets assigned an exclusive, large range or user IDs.
The driver is the only entity that can perform important operations for user IDs it has assigned, e.g. updating configurations or transferring funds.
The driver can then expose a custom API and introduce custom rules about controlling its user IDs.
For example the `AddressDriver` assigns 1-to-1 its user IDs to all existing addresses.
Via its API for each user ID it allows the assigned address to perform important operations in DripsHub.
Another driver is `NFTDriver`, which assigns user IDs to token IDs.
Its API only allows the current NFT holder to perform important operations for the assigned user ID.
The protocol lets anybody register new drivers, it's supposed to invite integrations with 3rd party identity systems.

## Scoping Details

```
- If you have a public code repo, please share it here: https://github.com/radicle-dev/drips-contracts
- How many contracts are in scope?:   8
- Total SLoC for these contracts?:  1503
- How many external imports are there?: 0
- How many separate interfaces and struct definitions are there for the contracts within scope?:  9 structs + 4 structs only for storage for upgradable contracts. no internal interfaces only some external interfaces like OZ for ERC20s
- Does most of your code generally use composition or inheritance?:   a mixture of both. We use in inheritance in the DripsHub but the Split and Drips logic are libraries used with composition.
- How many external calls?:   0
- What is the overall line coverage percentage provided by your tests?:  90
- Is there a need to understand a separate part of the codebase / get context in order to audit this part of the protocol?:  false
- Please describe required context:
- Does it use an oracle?:  false
- Does the token conform to the ERC20 standard?:  we don't have a token
- Are there any novel or unique curve logic or mathematical models?: https://v2.docs.drips.network/docs/the-protocol/technical-overview
- Does it use a timelock function?:  no
- Is it an NFT?: yes
- Does it have an AMM?: no
- Is it a fork of a popular project?:  false
- Does it use rollups?:   false
- Is it multi-chain?:  false
- Does it use a side-chain?: false
```

# Tests

Radicle Drips Hub uses [Foundry](https://github.com/foundry-rs/foundry) for development.
You can install it using [foundryup](https://github.com/foundry-rs/foundry#installation).

The codebase is statically checked with [Slither](https://github.com/crytic/slither) version 0.9.2.
Here are the [installation instructions](https://github.com/crytic/slither#how-to-install).

## Running tests

First, you need to install the dependencies linked in `/lib`:

```bash
# Install dependencies
forge install
```

Then you can run the tests:

```bash
# Running tests
forge test
```

All the tests are supposed to pass. Foundry by default prints the total gas usage for each test, but for a more detailed gas report table, you can use the following:

```bash
# Running tests and generate a gas report table
forge test --gas-report
```

## Running Slither

```bash
slither .
```

There are supposed to be no issues found.
