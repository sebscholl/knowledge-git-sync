# Installing Uninstalling Rust Lang
tags: #rust

Lastly, go to [https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install) to install `rustup` (the Rust installer).

### Setting Up macOS[​](https://tauri.app/v1/guides/getting-started/prerequisites/#setting-up-macos "Direct link to heading")

#### 1. CLang and macOS Development Dependencies[​](https://tauri.app/v1/guides/getting-started/prerequisites/#1-clang-and-macos-development-dependencies "Direct link to heading")

You will need to install CLang and macOS development dependencies. To do this, run the following command in your terminal:

```
xcode-select --install
```

#### 2. Rust[​](https://tauri.app/v1/guides/getting-started/prerequisites/#2-rust "Direct link to heading")

To install Rust on macOS, open a terminal and enter the following command:

```
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

NOTE

We have audited this bash script, and it does what it says it is supposed to do. Nevertheless, before blindly curl-bashing a script, it is always wise to look at it first. Here is the file as a plain script: [rustup.sh](https://sh.rustup.rs/)

The command downloads a script and starts the installation of the `rustup` tool, which installs the latest stable version of Rust. You might be prompted for your password. If the installation was successful, the following line will appear:

___
## References
- [Rust MacOS Pre-requisites](https://tauri.app/v1/guides/getting-started/prerequisites/#setting-up-macos)