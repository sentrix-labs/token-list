# sUSDC Token List Listing

Do not add sUSDC to `sentrix.tokenlist.json` until the official Hyperlane Warp Route has been deployed and verified.

## Testnet Entry

Use `examples/susdc.token-entry.template.json` as the starting point, then replace:

- `chainId` with `7120`
- `address` with the deployed Sentrix Testnet sUSDC router/token address
- `originChainId` with `84532`
- `originToken` with Base Sepolia USDC `0x036CbD53842c5426634e7929541eC2318f3dCF7e`

## Mainnet Entry

For mainnet, replace:

- `chainId` with `7119`
- `address` with the deployed Sentrix Mainnet sUSDC router/token address
- `originChainId` with `8453`
- `originToken` with Base mainnet USDC `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`

## Required Checks

- The token name is `Sentrix Bridged USDC`.
- The symbol is `sUSDC`.
- Decimals are `6`.
- The address is checksummed and non-zero.
- The bridge deployment manifest records the same address.
- The bridge UI warning says: `sUSDC is bridged USDC on Sentrix, backed 1:1 by USDC locked on Base through the official Sentrix bridge route.`
- Bump the token list minor version when adding the token.
