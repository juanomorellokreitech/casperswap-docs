# Swaps

## **Introduction**

Token swaps in Casperswap serve as a simple way of trading one ERC-20 token for another.

From the end-user standpoint, swapping is intuitive: a user picks an input token and an output token, specify an input amount, and the protocol calculates how much of the output token they’ll receive. They can then execute the swap with just one click, immediately receiving the output token in their wallet.

In this guide, we’ll look at what happens during a swap at protocol level in order to gain a deeper understanding of how Uniswap works.

Swaps in Casperswap are different from trades on traditional platforms. Casperswap does not use an order book to represent liquidity or determine prices, instead it resorts to an automated market maker mechanism in order to provide instant feedback on rates and slippage.

As mentioned in Protocol Overview, each pair on Uniswap is underpinned by a liquidity pool. Liquidity pools are smart contracts that hold balances of two unique tokens and enforce a specific rule for depositing and withdrawing them.

This rule is the constant product formula: when either token is withdrawn (purchased), a proportional amount of the other must be deposited (sold) in order to maintain the constant.



**Anatomy of a swap**&#x20;

At the most basic level, all swaps in Uniswap V2 take place within a single function, aptly named swap:

```rust
fn swap_exact_tokens_for_tokens(
        &mut self,
        amount_in: U256,
        amount_out_min: U256,
        _path: Vec<String>,
        to: Key,
    ) -> Vec<U256>
```

## **Receiving tokens**

As implied by the function's signature, Casperswap requires swap callers to specify the amout of  output tokens they wish to receive via the amount{0,1}Out parameters, which correspond to the desired amount of token{0,1}.

## **Sending Tokens**

Less clear is the way in which Casperswap receives tokens as payment for the swap. T

ypically, smart contracts that require tokens to perform some functionality need callers to first make an approval on the token contract, upon which they call a function that in turn calls transferFrom on the token contract. This, however, is not the way in which Casperswap pairs accept tokens, with pairs checking their token balances at the end of every interaction istead. From there, at the beginning of the next interaction, current balances are differenced against the stored values in order to determine the amount of tokens that were sent by the current interactor.&#x20;

The whitepaper provides an detailed explanation justyfing the use of this particular method.

The takeaway is that tokens must be transferred to pairs before swap is called (the one exception to this rule being Flash Swaps). What this entails is that in order to safely use the swap function, it has to be called from another smart contract. The alternative (transferring tokens to the pair and then calling swap) is unsafe to execute non-atomically on the grounds that sent tokens would be vulnerable to arbitrage.
