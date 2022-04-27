# Usage

You need to run the command at the folder-level of the contract you wish to execute.

## Install

Make sure `wasm32-unknown-unknown` is installed.

```
make prepare
```

It's also recommended to have [wasm-strip](https://github.com/WebAssembly/wabt) available in your PATH to reduce the size of compiled Wasm.

#### Build Individual Smart Contract

Run this command to build a Smart Contract.

```
make build-contract
```

\
**Note:** The user needs to run `make build-contract` in every project folder before running the desired contract in order to avoid errors.

#### Build All Smart Contracts

Run this command in the root folder to build all Smart Contract.

```
make all
```

#### Individual Test Cases

Run Test Cases by using this  command line.

```
make test
```

\
**Note:** User needs to be in the desired project folder to run the test cases

#### All Test Cases

Run all contract's Test Cases in the main folder by using  this command  line.

```
make test
```

### Known contract hashes

All contracts have been already deployed. In order to interact with a specific contract you will need to invoque it by its hash. The table below contains the contract hash (without the `hash-` prefix) for all the contracts on public Casper network:

| Network     | Contract Name | Account info contract hash                                              | Contract owner |
| ----------- | ------------- | ----------------------------------------------------------------------- | -------------- |
| Testnet     | ERC20         | `hash-279445c140615fd511759dfb96c610dee212769913f61a57b0f9dde42d6a8d10` | Casper         |
| Association |               |                                                                         |                |
| Testnet     | WCSPR         | `hash-4f2d1b772147b9ce3706919fe0750af6964249b0931e2115045f97e1e135e80b` | Casper         |
| Association |               |                                                                         |                |
| Testnet     | FLASHSWAPPER  | `hash-1c23f9e89033e5c2d2a21a6926411b2645c000cf43fc0db495821633da2aed6e` | Casper         |
| Association |               |                                                                         |                |
| Testnet     | PAIR          | `hash-de6ba94b699dad44e12bf98e35c1122eed7dba9eed8af6d8952875afaec8c7dd` | Casper         |
| Association |               |                                                                         |                |
| Testnet     | FACTORY       | `hash-13cc83616c3fb4e6ea22ead5e61eb6319d728783ed02eab51b1f442085e605a7` | Casper         |
| Association |               |                                                                         |                |
