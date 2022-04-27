# Technical references

The Casperswap protocol consists of 2 repositories with smart contracts

1. Casperswap core - [Github repository](https://github.com/Rengo-Labs/uniswap-casper-core)
2. Casperswap router - [Github repository](https://github.com/Rengo-Labs/uniswap-casper-core)

## **Prerequisites**

You can install the required software by running the following commands. If you already have an up-to-date Casper node, you probably already have all of the prerequisites installed so you can skip this step.

```bash
# Update package repositories
sudo apt update

# Install the command-line JSON processor
sudo apt install jq -y

# Install rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

#Install the nightly version (by default stable toolchain is installed)
rustup install nightly

#Check that nightly toolchain version is installed (this will list stable and nightly versions)
rustup toolchain list

#Set rust nightly as default
rustup default nightly

# Install wasm32-unknown-unknown
rustup target add wasm32-unknown-unknown

#rust Version
rustup --version

#Install Cmake
 sudo apt-get -y install cmake

# Note:https://cgold.readthedocs.io/en/latest/first-step/installation.html

#cmake Version
cmake --version

#Installing the Casper Crates
cargo install cargo-casper

# Add Casper repository
echo "deb https://repo.casperlabs.io/releases" bionic main | sudo tee -a /etc/apt/sources.list.d/casper.list
curl -O https://repo.casperlabs.io/casper-repo-pubkey.asc
sudo apt-key add casper-repo-pubkey.ascr
sudo apt update

# Install the Casper client software
Install Casper-client

cargo +nightly install casper-client

# To check Casper Client Version
Casper-client --version

# Commands for help
casper-client --help

casper-client <command> --help
```

### Creating Keys

```bash
# Create keys
casper-client keygen <TARGET DIRECTORY>
```

### All Test Cases

Tests require that the CasperLabs-UniswapV2-core repository to be checked out into a sibling directory of CasperLabs-UniswapV2-router.

```
git clone https://github.com/Rengo-Labs/uniswap-casper-core.git
git clone https://github.com/Rengo-Labs/uniswap-casper-router
```

To build the contracts and run the tests, first navigate back to this directory and run:

```
make all
```

To run all the tests:

```
make test
```

To clean up:

```
make clean
```

### Known contract hashes <a href="#known-contract-hashes" id="known-contract-hashes"></a>

Router contract has already being deployed. In order to interact with it you need to call it by its hash. The table below contains the contract hash (without the `hash-` prefix) for Router contract on public Casper networks:

| Network | Account info contract hash                                              | Contract owner     |
| ------- | ----------------------------------------------------------------------- | ------------------ |
| Testnet | `hash-d52d2e98554c1854fd8a9ce541a9d52dab73fd2841655513a9c8295898803ce0` | Casper Association |
