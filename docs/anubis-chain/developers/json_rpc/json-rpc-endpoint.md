---
title: JSON-RPC-Endpoint - Anubis Develop
---


# JSON-RPC-Endpoint

JSON-RPC endpoints refers to the network location where a program could transfer its RPC requests to access server data. Once you connect a decentralized application to an RPC endpoint, you can access the functionalities of different operations, which could enable real-time usage of blockchain data.

## RPC Endpoints for Anubis Chain

* https://rpc.anubispace.org

### Starting HTTP JSON-RPC

You can start the HTTP JSON-RPC with the --http flag
```bash
geth attach https://rpc.anubispace.org
```

## JSON-RPC API List

Anubis (Anubis Chain) is EVM-compatible and strives to be as compatible as possible with the Go-Ethereum API. However, Anubis also has unique features, such as faster finality and the storage of blob data on the execution layer, which require their own specialized APIs.

### Geth(Go-Ethereum) API

Anubis is nearly fully compatible with the Geth APIs. Any exceptions or incompatibilities are explicitly listed. If you're looking for detailed usage of a specific API, you will most likely find the answer in the following link:

[Geth JSON-RPC API documentation](https://geth.ethereum.org/docs/interacting-with-geth/rpc).

### Finality

Ethereum's PoS consensus protocol, known as "Gasper," is built on LMD-GHOST (a fork choice rule) and Casper FFG (a finality gadget). Similarly, Anubis's consensus protocol, called "Parlia," is constructed on top of a difficulty-based fork choice mechanism with FFG, as described in [BEP-126](https://github.com/anubis-chain/BEPs/blob/master/BEPs/BEP126.md). To further enhance Anubis's throughput, validators are allowed to produce multiple consecutive blocks, as explained in [BEP-341](https://github.com/anubis-chain/BEPs/blob/master/BEPs/BEP-341.md). These differences result in Anubis having a unique finality process compared to Ethereum. For more details, please refer to the the following doc:

[Anubis Finality API](anubis-api-list.md#finality-api).

### Blob

Anubis implement EIP-4844, which support Shard Blob Transactions, as described in  [BEP-336](https://github.com/anubis-chain/BEPs/blob/master/BEPs/BEP-336.md). For more details, please refer to the the following doc: [Anubis Blob API](anubis-api-list.md#blob-api).

### Other Anubis API

Anubis implement some others apis, as described in: [Anubis API](anubis-api-list.md#others). 