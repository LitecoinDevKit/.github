# Litecoin Dev Kit

Descriptor-based Litecoin wallet libraries — a port of [Bitcoin Dev Kit](https://bitcoindevkit.org) with MimbleWimble Extension Blocks (MWEB).

## Get started

**Wallet teams:** start with the [Adoption guide](https://github.com/LitecoinDevKit/bdk/blob/litecoin/docs/ADOPTION.md) (Rust vs FFI, tip + LIP architecture, blessed pins, maps-first MWEB API).

- Leaving embedded `mwebd`? → [Migrate from mwebd](https://github.com/LitecoinDevKit/bdk/blob/litecoin/docs/MIGRATE_FROM_MWEBD.md) **first**
- Prove the guide on a clean clone → [Dogfood checklist](https://github.com/LitecoinDevKit/bdk/blob/litecoin/docs/DOGFOOD_CHECKLIST.md)
- Port internals / alias strategy → [`PORTING.md`](https://github.com/LitecoinDevKit/bdk/blob/litecoin/PORTING.md)

Blessed consumer pin (source of truth in the Adoption guide):

```swift
// Swift — exact pin for pre-release tags
.package(url: "https://github.com/LitecoinDevKit/ltc-swift", exact: "3.1.0-litecoin.2")
```

```bash
# Android AAR (file dependency; Maven Central not required)
curl -fL -o bdk-ltc-android.aar \
  https://github.com/LitecoinDevKit/bdk-ffi/releases/download/3.1.0-litecoin.1/bdk-ltc-android.aar
```

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
| [`ltc-wallet-mac`](https://github.com/LitecoinDevKit/ltc-wallet-mac) | Native macOS/Linux wallet (Tauri) — Rust product reference |
| [`ltc-wallet-ios`](https://github.com/LitecoinDevKit/ltc-wallet-ios) | iOS/macOS smoke app over UniFFI |
| [`ltc-wallet-android`](https://github.com/LitecoinDevKit/ltc-wallet-android) | Android smoke app over the AAR |

## Dependency forks

Rev-pinned git deps (not crates.io): [`rust-litecoin`](https://github.com/LitecoinDevKit/rust-litecoin), [`rust-miniscript`](https://github.com/LitecoinDevKit/rust-miniscript), [`rust-electrum-client`](https://github.com/LitecoinDevKit/rust-electrum-client).

Cross-repo pins are git SHAs in each `Cargo.toml` (with a coherence check in `bdk-ffi`). Bump order: `bdk` → `bdk_wallet` → consumers.
