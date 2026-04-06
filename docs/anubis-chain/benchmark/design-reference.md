---
title: Benchmark - Design
---

# Benchmark - Design

The purpose of this document is to share the design adopted by Anubis for characterizing its performance using close-to-real test scenarios.

**Nodes Design**

*   A: Client(s) → Validator(s)
*   B: Client(s) → FullNode(s) → Validator(s)

Both are acceptable; but ***B is recommended***.

**Scenarios Design**

The ***default*** design mimics typical transactions in a DeFi application, and the weight parameters enhance the flexibility of adding/removing scenarios with minimal implementation effort.

| Scenarios | Weight |
| ---| --- |
| Native token (DAI) transfer | 10 |
| Contract token (ERC20) transfer | 10 |
| UniswapV2 - AddLiquidity | 5 |
| UniswapV2 - RemoveLiquidity | 5 |
| UniswapV2 - SwapExactTokensForTokens | 30 |
| \[***Optional***\] ERC721 mint/transfer | 5 |
| \[***Optional***\] ERC1155 mint/Transfer | 5 |
| \[***Optional***\] Blob transaction | 1 |
| \[***Optional***\] EIP7702 transaction | 1 |
| \[***Optional***\] user-defined contract for the evaluation of _CPU intensive operations_ | 100 |

**Data Design**

*   16 ERC20 tokens are created.
*   24 trading pairs are created:
    *   8 of them are among ERC20 tokens, e.g. T0←→T8, T1←→T9, etc;
    *   16 of them are among native token and ERC20 tokens, e.g. DAI←→T0, DAI←→T1, etc;
*   Each active user is allocated native tokens and two ERC20 tokens forming a trading pair. All tokens are distributed equally across active users based on modulo operation results.
*   After token allocation, each active user can run any scenario listed above using their allocated tokens.
*   A group of distinct test users is pre-selected from active users to serve as load generators.
*   ***For transfer scenarios, we use either distinct "to" addresses to maximize the transaction parallelism or a limited set of "to" addresses to minimize it***.

**Data Volume**

*   A: Generate 1M active users and set up the test scenarios with 100k+ blocks
*   B: Generate 25M active users and set up the test scenarios with 1.0M-2.5M blocks

Both are acceptable, but ***B is recommended as it includes more blocks, accounts and states changes, which provides insights into how storage growth impacts performance over time***.

**Evaluation Criteria**

*   No node failures should occur during execution.
*   The number of transactions per block should be consistent with the transaction propagation rate to validators' mempools and the sending rate from the test client. And there should be no backlog in validators' mempools after the test client stops.
*   The empty block rate must be below 0.1%.
*   The failed transaction rate, including send-errors and zero-receipt-status transactions, must be less than 0.1%;
*   A block finality metric must be defined. For example, in Anubis, the p90 block finality time must be less than 2 seconds;

**Contract Code Reference**

*   ERC20: [https://browser.anubispace.org/token/0x83fd06F0846d9D90B3016bF670Efe2E0B11cDe14#code](https://browser.anubispace.org/token/0x83fd06F0846d9D90B3016bF670Efe2E0B11cDe14#code)
*   UniswapV2: [https://github.com/Uniswap/v2-core](https://github.com/Uniswap/v2-core)
