# Sentrix Token List

Canonical [Uniswap-token-list-v1](https://github.com/Uniswap/token-lists) registry for Sentrix Chain (mainnet `7119`, testnet `7120`).

DEX UIs, wallets, and explorers consume this list to recognise tokens by address without users having to paste contract addresses manually.

## Hosted URLs

- **Mainnet + testnet combined:** `https://raw.githubusercontent.com/sentrix-labs/token-list/main/sentrix.tokenlist.json`

Pin a specific version for production integrations:

- **Tag-pinned:** `https://raw.githubusercontent.com/sentrix-labs/token-list/v1.0.0/sentrix.tokenlist.json`

## What's included today

| Chain | Symbol | Address | Notes |
|---|---|---|---|
| 7119 (mainnet) | `WSRX` | `0x4693b113e523A196d9579333c4ab8358e2656553` | WETH-pattern wrapper of native SRX. Deployed via `canonical-contracts`, Sourcify-verified. |
| 7120 (testnet) | `WSRX` | `0x85d5E7694AF31C2Edd0a7e66b7c6c92C59fF949A` | Testnet WSRX. Same contract logic as mainnet. |

Native SRX is intentionally NOT listed as a token — it's the chain's gas asset, not an ERC20. Wallets handle it as the chain's `nativeCurrency` field (see [ethereum-lists/chains](https://github.com/ethereum-lists/chains) entries `eip155-7119` / `eip155-7120`).

## Schema

This list follows the [Uniswap Token Lists v1 schema](https://github.com/Uniswap/token-lists/blob/main/src/tokenlist.schema.json). Every entry must have:

- `chainId` — `7119` or `7120` for Sentrix
- `address` — checksummed (EIP-55) ERC20 address
- `name`, `symbol`, `decimals`
- `logoURI` (recommended, used by DEX UIs)
- `tags` (optional, from the `tags` map at the top of the file)

The `tags` block at the file top defines the vocabulary; tokens reference tags by key (e.g. `"tags": ["wrapped"]`).

## Adding a token

1. Fork this repo.
2. Edit `sentrix.tokenlist.json`. Add your entry to the `tokens` array, alphabetised by `symbol` within each `chainId` bucket.
3. Bump the `version` field at the top:
   - Adding a token → bump `minor`
   - Renaming or removing → bump `major`
   - Logo-only / non-content changes → bump `patch`
4. Open a PR with:
   - On-chain proof: the deploying tx hash + a link to the verified contract at `verify.sentrixchain.com` or `scan.sentrixchain.com`
   - Logo URL (PNG or SVG, ideally 256×256, hosted somewhere stable — GitHub `raw.githubusercontent.com`, IPFS, or your own CDN)
   - One-line description of what the token is

## Validation

Every PR runs JSON-schema validation in CI. If your edit doesn't conform to the Uniswap schema, CI will fail with a specific schema-path error.

You can run the same validation locally before pushing:

```bash
npx ajv-cli validate -s schema.json -d sentrix.tokenlist.json
```

## Versioning policy

We follow the Uniswap token-list version semantics:

- **Major bump** — token removed or `chainId/address` changed
- **Minor bump** — new token added
- **Patch bump** — metadata-only change (name, logo, decimals correction)

Each version corresponds to a git tag (`v<major>.<minor>.<patch>`), so integrators can pin to a known-stable list and upgrade explicitly.

## Why a token-list

Without one, every wallet and DEX UI has to either:

- Hardcode known token addresses into the app bundle (brittle, ships old data)
- Trust whatever the user pastes into the address bar (phishing surface)

A maintained, versioned, schema-validated list closes both gaps. It's the same pattern used by Uniswap, PancakeSwap, SushiSwap, Trader Joe, etc.

## Future scope

- Auto-discover tokens via `SentrixV2Factory.allPairs()` walk + initial filter
- Per-list flavours (e.g. `sentrix-strict.tokenlist.json` for highest-trust, `sentrix-extended.tokenlist.json` for community-submitted)
- IPFS pinning for tag-pinned URLs

## License

[BSD-3-Clause](./LICENSE) — matches Uniswap's token-lists licence so derivatives can be vendored either direction.
