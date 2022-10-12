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
| 1. Developing validation logic relevant for the Skale part of the bridge<br/>2. Adding Skale to the Bridge [NFT-Indexer](./proof.md/#22-nft-indexing)<br/>3. Integrating [TX fee estimation](./proof.md/#23-tx-fee-estination)<br/>4. Plugging Skale in the [heartbeat](./proof.md/#24-heartbeat)<br/>5. [Integrating with Skale rpc nodes](./proof.md/#25-integrated-skale-rpc-nodes)<br/>6. Integrating Skale in the [bridge UI](./proof.md/#26-ui-integration)<br/>7. [Deploying smart contracts to the testnet](./proof.md/#27-deployed-contracts-on-the-skale-testnet)<br/>8. [Adding Skale to the bridge JS library](https://github.com/XP-NETWORK/xpjs/search?q=skale)|

## `Milestone 3` — Testing, Fixing Bugs & Documenting

| Specification |
|:-|
| 1. The code contains inline documentation and a [basic tutorial](./js_tutorial.md) that can interact with the deployed smart contracts and backend service.<br/>2. The code has unit-test coverage 85% to ensure functionality and robustness.<br/>3. [Deploying](./proof.md/#27-deployed-contracts-on-the-skale-testnet) and [testing](./proof.md/#33-testnet-transactions) the contracts in the testnet environment|

# LEFT TO DO

## `Milestone 4` — Mainnet Integration & Deployment

| Length | Deliverable | Specification |
|:-:|:-:|-|
| 1 week | Mainnet Integration | 1. Deploying the contracts in the Mainnet environment<br/>2. Integrating the mainnet Wallet<br/>3. Integrating the mainnet NFT-Indexer<br/>4. Integrating the mainnet validators<br/>5. Testing the Integrated Skale in the mainnet<br/>6.Adding Skale to the bridge widget |
