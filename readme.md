# EpicChain Debug Wizard

[![Build Status](https://github.com/epicchainlabs/epicchain-debug-wizard/actions/workflows/build-vscode.yml/badge.svg)](https://github.com/epicchainlabs/epicchain-debug-wizard/actions)

## Overview

Welcome to the EpicChain Debug Wizard! This advanced debugging tool is designed specifically for developers working with EpicChain smart contracts. It provides robust capabilities for identifying and resolving issues in your smart contracts, offering a seamless experience within Visual Studio and Visual Studio Code.

The EpicChain Debug Wizard leverages the same virtual machine technology as the core EpicChain platform to ensure full compatibility and accurate debugging. Our goal is to help you build, test, and deploy EpicChain smart contracts with confidence.

## Key Features

- **Seamless Integration**: Debug your EpicChain smart contracts directly within Visual Studio and Visual Studio Code.
- **Comprehensive Debugging**: Offers a range of debugging tools and features, including breakpoints, variable inspection, and step-by-step execution.
- **Compatibility**: Built on the same virtual machine as the core EpicChain platform, ensuring consistency between debugging and production environments.
- **Multi-Language Support**: Supports smart contracts written in various languages, with necessary compilers emitting debug information.

## Versioning Strategy

Our versioning strategy for the EpicChain Debug Wizard follows a structured approach to ensure clarity and consistency:

- **Version Scheme**: The debugger versions do not necessarily match the EpicChain core platform versions. For instance, Debugger v3.4 may correspond to EpicChain v3.3. For detailed information on our versioning strategy, please refer to [this document](https://github.com/epicchainlabs/epicchain-debug-wizard#versioning-strategy).
- **Pre-Release Versions**: We follow [VS Code recommended guidance](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#prerelease-extensions) for version numbers, allowing the marketplace to offer both production and pre-release versions. Minor versions will be even for production releases and odd for preview releases. 

## Installation

### System Requirements

The EpicChain Debug Wizard requires a .NET runtime to function. The required .NET Core version depends on the version of the Debug Wizard you are using:

| EpicChain Debug Wizard Version | .NET Core Version |
|--------------------------------|-------------------|
| v3.1 and later                  | [v6.0](https://dotnet.microsoft.com/download/dotnet/6.0) (for EpicChain contracts) <br /> [v3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1) (for EpicChain Legacy Contracts) |
| v3.0                            | [v5.0](https://dotnet.microsoft.com/download/dotnet/5.0) (for EpicChain contracts) <br /> [v3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1) (for EpicChain Legacy Contracts) |
| v2.0 (unsupported)              | [v5.0](https://dotnet.microsoft.com/download/dotnet/5.0) (for EpicChain contracts) <br /> [v3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1) (for EpicChain Legacy Contracts) |
| v1.0                            | [v3.1](https://dotnet.microsoft.com/download/dotnet/3.1) |
| v0.9 (unsupported)              | [v3.0](https://dotnet.microsoft.com/download/dotnet/3.0) |
| v0.5 (unsupported)              | [v2.2](https://dotnet.microsoft.com/download/dotnet/2.2) |

### Visual Studio Code Installation

1. **Marketplace Installation**: Install the EpicChain Debug Wizard from the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/vscode).
   - **Direct Installation**: [Install directly](https://marketplace.visualstudio.com/items?itemName=epic-chain.epic-debugger).
   - **Part of Toolkit**: Alternatively, you can install it as part of the [EpicChain Blockchain Toolkit](https://marketplace.visualstudio.com/items?itemName=epic-chain.epic-blockchain-toolkit).
   
2. **Requirements**: Ensure you have the appropriate [.NET runtime](https://dotnet.microsoft.com/download/dotnet-core) installed, as specified above.

### Ubuntu Installation

For Ubuntu users, additional packages are required:

```shell
sudo apt install libsnappy-dev libc6-dev -y
```

### macOS Installation

On macOS, install rocksdb via [Homebrew](https://brew.sh/):

```shell
brew install rocksdb
```

### Installing Preview Releases

1. **Build Server**: Access preview builds from our [public build server](https://dev.azure.com/epic-chain/Build/_build?definitionId=4&_a=summary).
2. **Download VSIX**: Navigate to the build you want, click "Artifacts" in the upper-right corner, and download the VSIX-package artifact.
3. **Install Manually**: Install the VSIX file manually in VSCode. For installation instructions, refer to the [official VSCode documentation](https://code.visualstudio.com/docs/editor/extension-gallery#_install-from-a-vsix).

### Visual Studio Installation

1. **Download VSIX**: Obtain the latest release of the EpicChain Debug Wizard for Visual Studio from the [GitHub release page](https://github.com/epicchainlabs/epicchain-debug-wizard/releases).
2. **Install**: Double-click the downloaded .vsix file to install it.

The debugger requires Visual Studio 2019 (Community, Professional, or Enterprise). Note that Visual Studio 2022 preview releases have not been tested. Additionally, you’ll need [.NET v5.0](https://dotnet.microsoft.com/download/dotnet/5.0) for debugging EpicChain contracts.

For more detailed documentation on using the EpicChain Debug Wizard with Visual Studio, refer to [this guide](docs/visual-studio.md).

## A Message from the Engineer

Thank you for choosing the EpicChain Debug Wizard! Your input is invaluable to us, and I’m eager to hear what you think about the tool.

If you find the EpicChain Debug Wizard helpful, please share your feedback on [Twitter](https://twitter.com/devhawk), [email](mailto:harry@epic-chain.org), or join us on the [EpicChain Discord server](https://discord.gg/G5WEPwC). Positive feedback not only motivates our team but also helps raise awareness about the tool.

If you encounter any issues or have suggestions for improvements, please file them in our [GitHub repository](https://github.com/epicchainlabs/epicchain-debug-wizard/issues). While I’m available via Twitter, Discord, and email, GitHub issues are the best way to track and manage feedback. Don’t hesitate to submit an issue if there’s anything you think could be improved or if there’s a feature you’d like to see.

Although the EpicChain Debug Wizard has primarily been a solo project up to this point, I’m excited about the prospect of future contributions and collaborations. The tool has been designed from my perspective, but I understand that other viewpoints are crucial. I built this debugger to serve the EpicChain developer community, and I’m committed to making it as accessible and effective as possible. Your insights and contributions will be key to achieving this goal.

Thank you again for your interest in the EpicChain Debug Wizard. I look forward to your feedback and working together to make this tool the best it can be.

Best regards,

\- [xmoohad], Chief Architect EpicChain
