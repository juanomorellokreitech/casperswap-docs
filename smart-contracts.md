# Smart contracts

Casperswap is a binary smart contract system.&#x20;

Core contracts provide fundamental safety guarantees for all parties interacting with Casperswap. Router contracts interact with one or more core contracts, however they are not part of the core themselves.

## **Core**

[Source code](https://github.com/Rengo-Labs/uniswap-casper-core)

The core consists of a singleton factory and many pairs, which the factory is responsible for creating and indexing.&#x20;

These contracts are quite minimal, bordering on brutalist. The rationale behind this being that contracts with a smaller surface area are easier to reason about, less bug-prone, and functionally elegant.&#x20;

Arguably, the biggest upside of this design is that many desired properties of the system can be asserted directly at code-level, leaving little to no room for error.&#x20;

On the downside, hoever, these core contracts are somewhat user-unfriendly, with direct interaction with them not being recommendable for most use cases. Instead,  the usage of a periphery contract is encouraged.

## Factory

The factory holds the generic bytecode responsible for powering pairs. Its primary job is to create a unique smart contract per token pair. It also contains the logic necessary to turn on the protocol charge.

## Pairs

Pairs serve two primary purposes: performing as automated market makers and keeping track of pool token balances. They also expose data which can be used to build decentralized price oracles.

## **Router**

[Source code](https://github.com/Rengo-Labs/uniswap-casper-router)

The periphery consists of a constellation of smart contracts designed to support domain-specific interactions with the core. Because of Casperswap's permissionless nature, the contracts described below have no special privileges, and therefore represent only a small subset of the universe of possible periphery-like contracts. They are nonetheless useful examples of how to safely and efficiently interact with Casperswap.

## Sending Tokens

Typically, smart contracts which need tokens to perform some functionality require would-be interactors to first make an approval on the token contract and then call a function that in turn calls transferFrom on the token contract.&#x20;

This is not how Casperswap pairs accept tokens however. Instead, pairs check their token balances at the end of every interaction. Following that, at the beginning of the next interaction, current balances are differenced against the stored values to determine the amount of tokens that were sent by the current interactor.&#x20;

The takeaway is that **tokens must be transferred to the pair before calling any token-requiring method** (the one exception to this rule being Flash Swaps).

## Minimum Liquidity

To ameliorate rounding errors and increase the theoretical minimum tick size for liquidity provision, pairs burn the first MINIMUM\_LIQUIDITY pool tokens. For the vast majority of pairs, this represents  a trivial value. The burning happens automatically during the first liquidity provision, with the totalSupply being forevermore bounded thereafter.
