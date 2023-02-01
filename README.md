<center>

# Skale-grant-delivery

</center>

## `Milestone 1` — Smart Contract Development

| Specification |
|-|
| 0. Researched about Moonbeam NFT token standards: [ERC-721](https://docs.skale.network/ima/1.3.x/managing-erc721)/[ERC-1155](https://docs.skale.network/ima/1.3.x/managing-erc1155) and other factors & protocols that distinguish it from other chains<br/>We have developed smart contracts that can:<br/>1. Support Singe & Batch transfers - ([ERC-721/ERC-1155](https://github.com/XP-NETWORK/XP.network-HECO-Migration/blob/f474704150da557f931e011026d0c033b391bd7a/dist/Minter.d.ts))<br/>2. [Freeze](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=freeze)/[Unfreeze](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=unfreeze) Native NFTs<br/>3. [Mint](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=mint)/[Burn](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=burn) wrapped NFTs<br/>4. [Withdraw](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=withdraw) the TX fees on the target chain in native tokens<br>5. Trust the [multisig](https://github.com/XP-NETWORK/frost-secp256k1) of the bridge oracle validators<br/>6. [Whitelist](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=whitelist) NFT smart contracts<br/>7. [Pause](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=pause)/[Unpause](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=unpause) for maintenance or if compromised<br/>10. [Add / Remove](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=validate) validator<br/>11. Set consensus [threshold](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=threshold)|

## `Milestone 2` — Integrating into the Live Bridge
| Specification |
|:-|
| 1. Added Skale to the Bridge [NFT-Indexer](./proof.md/#22-nft-indexing)<br/>2. Integrated [TX fee estimation](./proof.md/#23-tx-fee-estimation)<br/>3. Plugged Skale in the [heartbeat](./proof.md/#24-heartbeat)<br/>4. [Integrated with Skale rpc nodes](./proof.md/#25-integrated-skale-rpc-nodes)<br/>5. Integrated Skale in the [bridge UI](./proof.md/#26-ui-integration)<br/>6. [Deployed smart contracts to the testnet](./proof.md/#27-deployed-contracts-on-the-skale-testnet)<br/>7. [Added Skale to the bridge JS library](https://github.com/XP-NETWORK/xpjs/search?q=skale)|

## `Milestone 3` — Testing, Fixing Bugs & Documenting

| Specification |
|:-|
| 1. The code contains inline documentation and a [basic tutorial](./js_tutorial.md) that can interact with the deployed smart contracts and backend service.<br/>2. The code has unit-test coverage 85% to ensure functionality and robustness.<br/>3. [Deploying](./proof.md/#27-deployed-contracts-on-the-skale-testnet) and [testing](./proof.md/#33-testnet-transactions) the contracts in the testnet environment|

## `Milestone 4` — Mainnet Integration & Deployment

| Length | Deliverable | Specification |
|:-:|:-:|-|
| 1 week | Mainnet Integration | 1. [Deployed the contracts in the Mainnet environment](./milestone4.md#1-deployed-the-contracts-in-the-mainnet-environment)<br/>2. [Integrated the mainnet Wallet](./milestone4.md#2-integrated-the-mainnet-wallet)<br/>3. [Integrated the mainnet NFT-Indexer](./milestone4.md#3-integrated-the-mainnet-nft-indexer)<br/>4. [Integrated the mainnet validators](./milestone4.md#4-integrating-the-mainnet-validators)<br/>5. [Tested the Integrated Skale in the mainnet](./milestone4.md#5-tested-the-integrated-skale-in-the-mainnet)<br/>6. [Added Skale to the bridge widget](./milestone4.md#6-added-skale-to-the-bridge-widget) |
