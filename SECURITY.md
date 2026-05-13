# Security policy

## Threat model

`token-list` is a JSON registry consumed by wallets, DEX UIs, bridges, and aggregators. The data here drives what users **see** as legitimate tokens on Sentrix Chain, so the primary risks are:

- **Listing a malicious token** as if it were canonical
- **Typo-squatting** a legitimate token (similar symbol or name, different address)
- **Logo URLs** pointing at hostile or unstable hosts
- **chainId / address pairs** that conflict with the deployed reality

If you notice any of the above, please report it privately rather than opening a public issue — a public report amplifies the problem before it can be fixed.

## Vulnerability disclosure

Email **`security@sentrixchain.com`** with the offending entry and evidence (deployed contract address, block explorer link, source of the typo-squat claim), or open a private GitHub Security Advisory at <https://github.com/sentrix-labs/token-list/security/advisories/new>.

We respond within 72 hours.

## Listing review

New token entries are subject to manual review before they are merged. Pull requests that add a token without a deployed contract address on mainnet (`7119`) or testnet (`7120`) will be closed.

## Scope

In scope:

- `sentrix.tokenlist.json` content
- `schema.json` integrity
- The listing-review process

Out of scope:

- Smart-contract bugs in the tokens themselves (report to the token issuer)
- Sentrix Chain protocol or canonical contracts (covered in other repos)
