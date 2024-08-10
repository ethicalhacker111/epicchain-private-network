<!-- markdownlint-enable -->
# EpicChain Private Networks

[![Nuget](https://img.shields.io/nuget/v/EpicChain.Express)](https://www.nuget.org/packages/EpicChain.Express/)
[![Build Status](https://dev.azure.com/epicchain/Build/_apis/build/status/epicchainlabs.epicchain-private-network?branchName=master)](https://dev.azure.com/epicchain/Build/_build/latest?definitionId=2&branchName=master)

[EpicChain Express and EpicChain Trace](#epicchain-private-network-and-epicchain-trace)

- [Overview](#overview)
- [Download Links](#download-links)
- [Installation Guide](#installation-guide)
- [Usage Guide](#usage-guide)
- [New Features or Issues](#new-features-or-issues)
- [License](#license)

## Overview

EpicChain Express is a private network optimized for development scenarios, built on the same EpicChain platform core as [epicchain-cli](https://docs.epic-chain.org/docs/en-us/node/cli/setup.html) and [epicchain-gui](https://docs.epic-chain.org/docs/en-us/node/gui/install.html) to maximize compatibility between local development and public chain environments. EpicChain Trace is a tool for generating trace files for the EpicChain Smart Contract Debugger.

- ### Key Features

  **EpicChain Express**:

  - Blockchain instance management
  - Wallet management
  - Asset management
  - Smart contract management
  - Blockchain checkpoint and rollback

  **EpicChain Trace**:

  - Generate trace files for EpicChain Smart Contract Debugger
  - Support specifying blocks by index or hash and transactions by hash

## Download Links

| Platform | Download Link                                                |
| -------- | ------------------------------------------------------------ |
| Windows  | [win-x64-3.7.6.zip](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-win-x64-3.7.6.zip) <br/>[win-arm64-3.7.6.zip](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-win-arm64-3.7.6.zip) |
| macOS    | [osx-x64-3.7.6.tar.xz](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-osx-x64-3.7.6.tar.xz) <br/>[osx-arm64-3.7.6.tar.xz](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-osx-arm64-3.7.6.tar.xz) |
| Linux    | [linux-x64-3.7.6.tar.gz](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-linux-x64-3.7.6.tar.gz) <br/>[linux-musl-arm64-3.7.6.tar.gz](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-linux-musl-arm64-3.7.6.tar.gz) <br/>[linux-arm64-3.7.6.tar.gz](https://github.com/epicchainlabs/epicchain-private-network/releases/download/3.7.6/EpicChain.Express-linux-arm64-3.7.6.tar.gz) |

## Installation Guide

### Install via Release Package

1. Download the latest release package from [epicchain-private-network releases](https://github.com/epicchainlabs/epicchain-private-network/releases) for your operating system.
2. Unzip the package on your local machine.
3. Run the `epc.exe` command in the terminal from the directory where you unzipped the package.

### Install via .NET Tool

#### Requirements

- [.NET 8.0](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) or higher

#### Installation Steps

To install the latest version of EpicChain Express as a global tool, run the following command in a terminal window:

```shell
dotnet tool install EpicChain.Express -g
```

To update EpicChain Express to the latest version, run the following command:

```shell
dotnet tool update EpicChain.Express -g
```

The installation and update process for EpicChain Trace is identical:

```shell
dotnet tool install EpicChain.Trace -g
dotnet tool update EpicChain.Trace -g
```

### Additional EpicChain Express Requirements

#### Ubuntu Installation

> **Note**: While Microsoft has instructions for [installing .NET via Snap](https://docs.microsoft.com/en-us/dotnet/core/install/linux-snap), there is a [known issue](https://github.com/dotnet/runtime/issues/3775#issuecomment-534263315) with this approach that leads to a segmentation fault in EpicChain Express. Unfortunately, this issue with the .NET snap installer [has been closed and will not be fixed](https://github.com/dotnet/runtime/issues/3775#issuecomment-888676286). As such, we recommend [using APT](https://docs.microsoft.com/en-us/dotnet/core/install/linux-ubuntu) to install .NET on Ubuntu instead.

Installing on Ubuntu requires installing `libsnappy-dev`, `libc6-dev`, and `librocksdb-dev` via apt-get:

```shell
sudo apt install libsnappy-dev libc6-dev librocksdb-dev -y
```

#### macOS Installation

Installing on macOS requires installing rocksdb via [Homebrew](https://brew.sh/):

```shell
brew install rocksdb
```

> **Note**: .NET 6 Arm64 has [full support for Apple Silicon](https://devblogs.microsoft.com/dotnet/announcing-net-6/#arm64). Homebrew likewise also supports Apple Silicon. If you have any issues running EpicChain Express on Apple Silicon hardware, please [open an issue](https://github.com/epicchainlabs/epicchain-private-network/issues) in the EpicChain Express repo.

## Usage Guide

### EpicChain Express

- Create a new local EpicChain network:

  ```shell
  epc create
  ```

- List all wallets:

  ```shell
  epc wallet list
  ```

- Show genesis account balance:

  `genesis` to use the consensus node multi-sig account which holds the genesis NEO and GAS.

  ```shell
  epc show balances genesis
  ```

- Send 1 gas from genesis account to node1 account:

  ```shell
  epc transfer 1 gas genesis node1
  ```

Please review the [Command Reference](docs/command-reference.md) to get an understanding of EpicChain Express capabilities.

### EpicChain Trace

- Generate a trace file for a block:

  ```shell
  epictrace block 365110 --rpc-uri testnet
  ```

- Generate a trace file for a transaction:

  ```shell
  epictrace tx 0xef1917b8601828e1d2f3ed0954907ea611cb734771609ce0ce2b654bb5c78005 --rpc-uri testnet
  ```

> Note: EpicChain Trace depends on the [StateService plugin module](https://github.com/epicchainlabs/epicchain-modules/tree/master/src/StateService) running with `FullState` enabled. The official JSON-RPC nodes for MainNet and TestNet (such as `http://seed1.epic-chain.org:10332` and `http://seed1t5.epic-chain.org:20332`) are configured to run the StateService plugin with `FullState` enabled.

## New Features or Issues

Thank you for using EpicChain Express and EpicChain Trace! We welcome your feedback to make these tools more accessible, intuitive, and powerful.

Please visit the [issues page](https://github.com/epicchainlabs/epicchain-private-network/issues) to report problems or suggest new features. When creating a new issue, try to keep the title and description concise and provide context, such as a code snippet or an example of a feature and its expected behavior.

## License

EpicChain Express and EpicChain Trace are licensed under the [MIT License](https://github.com/epicchainlabs/epicchain-private-network#MIT-1-ov-file).
