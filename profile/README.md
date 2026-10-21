# Litecoin Dev Kit

Litecoin port of [Bitcoin Dev Kit](https://bitcoindevkit.org). Privacy is MWEB: peg in, send on the extension block, peg out.

**Prototype.** Litecoin Dev Kit and desktop wallet v0.4.6 have not been independently audited. Review the source, and verify any binary, before using them with funds.

- Site: [litecoindevkit.com](https://litecoindevkit.com)
- Project page: [litecoin.com/projects/litecoin-dev-kit](https://litecoin.com/projects/litecoin-dev-kit)

## Choose a path

### Desktop wallet

[`ldk-wallet`](https://github.com/LitecoinDevKit/ldk-wallet) is the Rust product reference. v0.4.6 ships for macOS Apple Silicon and Linux x86_64. It is a Rust application. Mobile packages use the UniFFI bindings.

### Adopt the library

Rust wallets, desktop apps, and servers use [`bdk_wallet`](https://github.com/LitecoinDevKit/bdk_wallet) (`litecoin`) with [`bdk`](https://github.com/LitecoinDevKit/bdk) (`litecoin`, `mweb` feature).

iOS, macOS, and Android without Rust in-process use [`bdk-ffi`](https://github.com/LitecoinDevKit/bdk-ffi) (`litecoin-mweb`). That path is experimental. Apple platforms go through [`ltc-swift`](https://github.com/LitecoinDevKit/ltc-swift). Android consumes the AAR from `bdk-ffi` releases. The iOS and Android sample apps are checklists for that API.

**Wallet teams:** start with the [Adoption guide](https://github.com/LitecoinDevKit/bdk/blob/litecoin/docs/ADOPTION.md). Pins in that guide are the source of truth.

- Leaving embedded `mwebd`? Read [Migrate from mwebd](https://github.com/LitecoinDevKit/bdk/blob/litecoin/docs/MIGRATE_FROM_MWEBD.md) first.
- Prove the guide on a clean clone: [Dogfood checklist](https://github.com/LitecoinDevKit/bdk/blob/litecoin/docs/DOGFOOD_CHECKLIST.md).
- Port internals and the alias strategy: [`PORTING.md`](https://github.com/LitecoinDevKit/bdk/blob/litecoin/PORTING.md).

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
| [`bdk-ffi`](https://github.com/LitecoinDevKit/bdk-ffi) | `litecoin-mweb` | Experimental UniFFI bindings → Android AAR + Swift xcframework |
| [`ltc-swift`](https://github.com/LitecoinDevKit/ltc-swift) | tags `3.1.0-litecoin.*` | SwiftPM package wrapping the xcframework |

## Apps

| Repo | Notes |
|------|--------|
| [`ldk-wallet`](https://github.com/LitecoinDevKit/ldk-wallet) | Desktop wallet v0.4.6 (macOS Apple Silicon, Linux x86_64). Rust product reference. Prototype; not independently audited. |
| [`ltc-wallet-ios`](https://github.com/LitecoinDevKit/ltc-wallet-ios) | Experimental iOS/macOS smoke app over UniFFI. Checklist for that API. |
| [`ltc-wallet-android`](https://github.com/LitecoinDevKit/ltc-wallet-android) | Experimental Android smoke app over the AAR. Checklist for that API. |

## Dependency forks

Rev-pinned git deps (not crates.io): [`rust-litecoin`](https://github.com/LitecoinDevKit/rust-litecoin), [`rust-miniscript`](https://github.com/LitecoinDevKit/rust-miniscript), [`rust-electrum-client`](https://github.com/LitecoinDevKit/rust-electrum-client).

Cross-repo pins are git SHAs in each `Cargo.toml` (with a coherence check in `bdk-ffi`). Bump order: `bdk` → `bdk_wallet` → consumers.
