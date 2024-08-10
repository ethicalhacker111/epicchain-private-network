<!-- markdownlint-enable -->
# EpicChain Private Networks

[![Nuget](https://img.shields.io/nuget/v/EpicChain.Express)](https://www.nuget.org/packages/EpicChain.Express/)
[![Build Status](https://dev.azure.com/epicchain/Build/_apis/build/status/epicchainlabs.epicchain-private-network?branchName=master)](https://dev.azure.com/epicchain/Build/_build/latest?definitionId=2&branchName=master)

[EpicChain Private Networks and EpicChain Trace](#epicchain-private-networks-and-epicchain-trace)

- [Overview](#overview)
- [Download Links](#download-links)
- [Installation Guide](#installation-guide)
- [Usage Guide](#usage-guide)
- [New Features or Issues](#new-features-or-issues)
- [License](#license)

## Overview

EpicChain Private Networks offers an elegant and advanced private network solution, meticulously engineered for sophisticated development environments. Built on the robust core of the EpicChain platform, akin to [epicchain-cli](https://docs.epic-chain.org/docs/en-us/node/cli/setup.html) and [epicchain-gui](https://docs.epic-chain.org/docs/en-us/node/gui/install.html), our network solution ensures unparalleled compatibility between local development setups and public blockchain environments. EpicChain Trace, a premium utility, is designed to generate detailed trace files essential for the EpicChain Smart Contract Debugger, facilitating seamless debugging and analysis.

- ### Key Features

  **EpicChain Private Networks**:

  - Comprehensive blockchain instance management
  - Advanced wallet management
  - In-depth asset management
  - Sophisticated smart contract management
  - Robust blockchain checkpoint and rollback capabilities

  **EpicChain Trace**:

  - Generate detailed trace files for EpicChain Smart Contract Debugger
  - Support for specifying blocks by index or hash and transactions by hash

## Download Links

| Platform | Download Link                                                |
| -------- | ------------------------------------------------------------ |
| Windows  | [win-x64-3.7.6.zip](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-win-x64-3.7.6.zip) <br/>[win-arm64-3.7.6.zip](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-win-arm64-3.7.6.zip) |
| macOS    | [osx-x64-3.7.6.tar.xz](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-osx-x64-3.7.6.tar.xz) <br/>[osx-arm64-3.7.6.tar.xz](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-osx-arm64-3.7.6.tar.xz) |
| Linux    | [linux-x64-3.7.6.tar.gz](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-linux-x64-3.7.6.tar.gz) <br/>[linux-musl-arm64-3.7.6.tar.gz](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-linux-musl-arm64-3.7.6.tar.gz) <br/>[linux-arm64-3.7.6.tar.gz](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-linux-arm64-3.7.6.tar.gz) |

## Installation Guide

### Install via Release Package

1. Acquire the latest release package from [EpicChain Private Networks releases](https://github.com/epicchainlabs/epicchain-private-network/releases) tailored for your operating system.
2. Extract the package on your local machine with precision.
3. Execute the `epc.exe` command in your terminal from the directory where the package was extracted.

### Install via .NET Tool

#### Requirements

- [.NET 8.0](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) or a more recent version

#### Installation Steps

To install the latest iteration of EpicChain Express as a global tool, run the following command in your terminal:

```shell
dotnet tool install EpicChain.Express -g
```

To update EpicChain Express to the latest version, execute:

```shell
dotnet tool update EpicChain.Express -g
```

The process for installing and updating EpicChain Trace mirrors that of EpicChain Express:

```shell
dotnet tool install EpicChain.Trace -g
dotnet tool update EpicChain.Trace -g
```

### Additional EpicChain Private Networks Requirements

#### Ubuntu Installation

> **Note**: For installing .NET on Ubuntu, avoid using Snap due to known issues that result in segmentation faults with EpicChain Private Networks. Instead, utilize [APT](https://docs.microsoft.com/en-us/dotnet/core/install/linux-ubuntu) for a smooth installation experience.

To prepare Ubuntu, install `libsnappy-dev`, `libc6-dev`, and `librocksdb-dev` via apt-get:

```shell
sudo apt install libsnappy-dev libc6-dev librocksdb-dev -y
```

#### macOS Installation

To ensure optimal performance on macOS, install rocksdb using [Homebrew](https://brew.sh/):

```shell
brew install rocksdb
```

> **Note**: .NET 6 Arm64 fully supports Apple Silicon. If any issues arise while running EpicChain Express on Apple Silicon hardware, please [open an issue](https://github.com/epicchainlabs/epicchain-private-network/issues) in the EpicChain Express repository.

## Usage Guide

### EpicChain Private Networks

- Establish a new local EpicChain network with elegance:

  ```shell
  epc create
  ```

- View a comprehensive list of all wallets:

  ```shell
  epc wallet list
  ```

- Display the balance of the genesis account:

  Use `genesis` to reference the consensus node multi-sig account, which holds the initial NEO and GAS.

  ```shell
  epc show balances genesis
  ```

- Transfer 1 gas from the genesis account to the node1 account:

  ```shell
  epc transfer 1 gas genesis node1
  ```

For an in-depth understanding of EpicChain Private Networks' capabilities, please consult the [Command Reference](docs/command-reference.md).

### EpicChain Trace

- Generate a detailed trace file for a specific block:

  ```shell
  epictrace block 365110 --rpc-uri testnet
  ```

- Generate a trace file for a particular transaction:

  ```shell
  epictrace tx 0xef1917b8601828e1d2f3ed0954907ea611cb734771609ce0ce2b654bb5c78005 --rpc-uri testnet
  ```

> Note: EpicChain Trace relies on the [StateService plugin module](https://github.com/epicchainlabs/epicchain-modules/tree/master/src/StateService) configured with `FullState` enabled. Official JSON-RPC nodes for MainNet and TestNet (e.g., `http://mainnet1-seed.epic-chain.org:10111` and `http://testnet1-seed.epic-chain.org:20111`) are equipped to run the StateService plugin with `FullState` enabled.

## New Features or Issues

We appreciate your choice to use EpicChain Private Networks and EpicChain Trace. We invite your feedback to enhance these tools and make them even more sophisticated and user-friendly.

Please visit the [issues page](https://github.com/epicchainlabs/epicchain-private-network/issues) to report issues or propose new features. When submitting an issue, please keep your title and description concise and provide relevant context, including code snippets or examples of features and their expected behavior.

## License

EpicChain Private Networks and EpicChain Trace are distributed under the [MIT License](https://github.com/epicchainlabs/epicchain-private-network#MIT-1-ov-file).
