# Litecoin Dev Kit

Descriptor-based Litecoin wallet libraries — a port of [Bitcoin Dev Kit](https://bitcoindevkit.org) with MimbleWimble Extension Blocks (MWEB).

## Libraries

| Repo | Branch | What it is |
|------|--------|------------|
| [`bdk`](https://github.com/LitecoinDevKit/bdk) | `litecoin` | Core crates (`bdk_chain`, `bdk_electrum`, `bdk_esplora`, `bdk_mweb`, …) |
| [`bdk_wallet`](https://github.com/LitecoinDevKit/bdk_wallet) | `litecoin` | High-level wallet + MWEB facade |
| [`bdk-ffi`](https://github.com/LitecoinDevKit/bdk-ffi) | `litecoin-mweb` | UniFFI bindings → Android AAR + Swift xcframework |
| [`ltc-swift`](https://github.com/LitecoinDevKit/ltc-swift) | tags `3.1.0-litecoin.*` | SwiftPM package wrapping the xcframework |

## Apps / smoke tests

| Repo | Notes |
|------|--------|
| [`ltc-wallet-mac`](https://github.com/LitecoinDevKit/ltc-wallet-mac) | Native macOS/Linux wallet (Tauri) |
| [`ltc-wallet-ios`](https://github.com/LitecoinDevKit/ltc-wallet-ios) | iOS/macOS smoke app over UniFFI |
| [`ltc-wallet-android`](https://github.com/LitecoinDevKit/ltc-wallet-android) | Android smoke app over the AAR |

## Dependency forks

Rev-pinned git deps (not crates.io): [`rust-litecoin`](https://github.com/LitecoinDevKit/rust-litecoin), [`rust-miniscript`](https://github.com/LitecoinDevKit/rust-miniscript), [`rust-electrum-client`](https://github.com/LitecoinDevKit/rust-electrum-client).

Cross-repo pins are git SHAs in each `Cargo.toml` (with a coherence check in `bdk-ffi`). Bump order: `bdk` → `bdk_wallet` → consumers.

## Get started

```bash
# Swift
.package(url: "https://github.com/LitecoinDevKit/ltc-swift", exact: "3.1.0-litecoin.2")

# Android AAR
curl -fL -o bdk-ltc-android.aar \
  https://github.com/LitecoinDevKit/bdk-ffi/releases/download/3.1.0-litecoin.1/bdk-ltc-android.aar
```

See [`bdk/PORTING.md`](https://github.com/LitecoinDevKit/bdk/blob/litecoin/PORTING.md) for the port strategy and topology.
