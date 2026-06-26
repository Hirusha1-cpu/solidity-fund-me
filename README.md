# Foundry Project - CROWDFUNDING SMARTCONTRACT

**Foundry is a blazing fast, portable and modular toolkit for Ethereum application development written in Rust.**

Foundry consists of:

- **Forge**: Ethereum testing framework (like Truffle, Hardhat and DappTools)
- **Cast**: Swiss army knife for interacting with EVM smart contracts, sending transactions and getting chain data.
- **Anvil**: Local Ethereum node, akin to Ganache, Hardhat Network.
- **Chisel**: Fast, utilitarian, and verbose solidity REPL.


### This is decetralized Crowdfunding Contract Project. Anyone can be fund the ETH into this contract.
### But have to fund minimum 5 (≥ $5) Dollers.
### We use chainlink price feeds  (real-world ETH/USD price oracle) for calculate price conversions.
### The collected funds can be withdraw only by owner.
```shell
1️⃣ src/PriceConverter.sol — Price Calculation Library
2️⃣ src/FundMe.sol — Main Contract 
3️⃣ script/HelperConfig.s.sol — Network Detection Logic (Core!)
4️⃣ script/DeployFundMe.s.sol — Deployment Script
5️⃣ test/FundMeTest.t.sol — Tests
```
## How to setup

### Add to .ENV
```shell
SEPOLIA_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_API_KEY
MAINNET_RPC_URL=https://eth-mainnet.g.alchemy.com/v2/YOUR_API_KEY
```
### Load ENV variables
```shell
source .env
```
### Fork test run
### Sepolia fork
```shell
forge test --fork-url $SEPOLIA_RPC_URL
```
### Mainnet fork
```shell
forge test --fork-url $MAINNET_RPC_URL
```
### Verbose output එක්ක (debug/trace logs )
```shell
forge test --fork-url $SEPOLIA_RPC_URL -vvv
```
### Specific test එකක් විතරක් run කරන්න
```shell
forge test --fork-url $SEPOLIA_RPC_URL --match-test testPriceFeedVersionIsAccurate -vvv
```
## Full Flow
```shell
1. forge clean / forge build           → compile 
2. forge test                          → local test (price feed test fail වෙයි)
3. source .env                         → RPC URLs load 
4. forge test --fork-url $SEPOLIA_RPC_URL -vvv    → Sepolia state, fork and test
5. forge test --fork-url $MAINNET_RPC_URL -vvv    → Mainnet state, fork and test
6. forge script script/DeployFundMe.s.sol --rpc-url $SEPOLIA_RPC_URL --private-key <key> --broadcast   → actual deploy (real testnet ETH ඕනේ)
```
```shell
forge test
    │
    ▼
setUp() executes before each test
    │
    ▼
DeployFundMe.run()
    │
    ├── Creates HelperConfig
    └── Deploys FundMe
    │
    ▼
HelperConfig checks block.chainid
    │
    ├── Local Anvil Network
    │      └── Uses local/mock price feed
    │
    └── Forked Network (Sepolia/Mainnet)
           └── Uses real Chainlink price feed
    │
    ▼
FundMe Contract Deployment
    │
    ├── Owner initialized
    └── Price Feed configured
    │
    ▼
Tests Execute Against Deployed Contract
```


## Commands
```shell
forge test --fork-url $SEPOLIA_RPC_URL
forge test --fork-url $MAINNET_RPC_URL
```

## Documentation

https://book.getfoundry.sh/

## Usage

### Build

```shell
$ forge build
```

### Test

```shell
$ forge test
```

### Format

```shell
$ forge fmt
```

### Gas Snapshots

```shell
$ forge snapshot
```

### Anvil

```shell
$ anvil
```

### Deploy

```shell
$ forge script script/Counter.s.sol:CounterScript --rpc-url <your_rpc_url> --private-key <your_private_key>
```

### Cast

```shell
$ cast <subcommand>
```

### Help

```shell
$ forge --help
$ anvil --help
$ cast --help
```
