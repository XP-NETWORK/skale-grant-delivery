<center>

# Skale-grant-delivery

</center>

## `Milestone 1` — Smart Contract Development

| Specification |
|-|
| 0. Researched about Moonbeam NFT token standards: [ERC-721](https://docs.skale.network/ima/1.3.x/managing-erc721)/[ERC-1155](https://docs.skale.network/ima/1.3.x/managing-erc1155) and other factors & protocols that distinguish it from other chains<br/>We have developed smart contracts that can:<br/>1. Support Singe & Batch transfers - ([ERC-721/ERC-1155](https://github.com/XP-NETWORK/XP.network-HECO-Migration/blob/f474704150da557f931e011026d0c033b391bd7a/dist/Minter.d.ts))<br/>2. [Freeze](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=freeze)/[Unfreeze](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=unfreeze) Native NFTs<br/>3. [Mint](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=mint)/[Burn](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=burn) wrapped NFTs<br/>4. [Withdraw](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=withdraw) the TX fees on the target chain in native tokens<br>5. Trust the [multisig](https://github.com/XP-NETWORK/frost-secp256k1) of the bridge oracle validators<br/>6. [Whitelist](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=whitelist) NFT smart contracts<br/>7. [Pause](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=pause)/[Unpause](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=unpause) for maintenance or if compromised<br/>10. [Add / Remove](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=validate) validator<br/>11. Set consensus [threshold](https://github.com/XP-NETWORK/XP.network-HECO-Migration/search?q=threshold)|

## `Milestone 2` — Integrating into the Live Bridge
| Length | Deliverable | Specification |
|:-:|:-:|-|
| 3 weeks | Validators, Backend, Frontend | 1. Developing validation logic relevant for the Skale part of the bridge<br/>2. Adding Skale to the Bridge NFT-Indexer<br/>3. Integrating TX fee estimation<br/>4. Plugging Skale in the heartbeat<br/>5. [Integrating with Skale rpc nodes](#25-integrated-skale-rpc-nodes)<br/>6. Integrating Skale in the bridge UI<br/>7. [Deploying smart contracts to the testnet](#27-deployed-contracts-on-the-skale-testnet)<br/>8. [Adding Skale to the bridge JS library](https://github.com/XP-NETWORK/xpjs/search?q=skale)|

## `Milestone 3` — Testing, Fixing Bugs & Documenting

| Length | Deliverable | Specification |
|:-:|:-:|-|
| 1 week | Tests & Documentation | 1. We will provide both inline documentation of the code and a basic tutorial that can interact with the deployed smart contracts and backend service.<br/>2. The code will have proper unit-test coverage 85% to ensure functionality and robustness. In the guide, we will describe how to run these tests preparing for auditing<br/>3. Deploying and testing the contracts in the testnet environment|

# TODO

## `Milestone 4` — Mainnet Integration & Deployment

| Length | Deliverable | Specification |
|:-:|:-:|-|
| 1 week | Mainnet Integration | 1. Deploying the contracts in the Mainnet environment<br/>2. Integrating the mainnet Wallet<br/>3. Integrating the mainnet NFT-Indexer<br/>4. Integrating the mainnet validators<br/>5. Testing the Integrated Skale in the mainnet<br/>6.Adding Skale to the bridge widget |


# Proofs:

### 2.5 Integrated Skale RPC nodes

|Network|RPC URL|Proof|
|:-:|:-:|:-:|
|Testnet|https://staging-v2.skalenodes.com/v1/actual-secret-cebalrai|[Link](https://github.com/XP-NETWORK/xpjs/blob/964e10733e9023ff4ed6f63a1089edc6e22d008e/src/consts.ts#L53)|
|Mainnet|https://mainnet.skalenodes.com/v1/honorable-steel-rasalhague|[Link](https://github.com/XP-NETWORK/xpjs/blob/964e10733e9023ff4ed6f63a1089edc6e22d008e/src/consts.ts#L84)
### 2.7 Deployed contracts on the Skale Testnet

|Contract Name|Contract Address|
|:-:|:-:|
|erc1155_addr| [0xeBCDdF17898bFFE81BCb3182833ba44f4dB25525](https://actual-secret-cebalrai.explorer.staging-v2.skalenodes.com/address/0xeBCDdF17898bFFE81BCb3182833ba44f4dB25525/transactions)|
|erc1155Minter| [0x9cdda01E00A5A425143F952ee894ff99B5F7999F](https://actual-secret-cebalrai.explorer.staging-v2.skalenodes.com/address/0x9cdda01E00A5A425143F952ee894ff99B5F7999F/transactions)|
|UserNftMinter| [0x34933A5958378e7141AA2305Cdb5cDf514896035](https://actual-secret-cebalrai.explorer.staging-v2.skalenodes.com/address/0x34933A5958378e7141AA2305Cdb5cDf514896035/transactions)|
|erc721_addr| [0x8CEe805FE5FA49e81266fcbC27F37D85062c1707](https://actual-secret-cebalrai.explorer.staging-v2.skalenodes.com/address/0x8CEe805FE5FA49e81266fcbC27F37D85062c1707/transactions)|
|minter_addr| [0x3fe9EfFa80625B8167B2F0d8cF5697F61D77e4a2](https://actual-secret-cebalrai.explorer.staging-v2.skalenodes.com/address/0x3fe9EfFa80625B8167B2F0d8cF5697F61D77e4a2/transactions)|


### Setting up the project:

```bash
mkdir testing-skale
cd testing-skale/
yarn init -y
yarn add "git+https://github.com/xp-network/xpjs#bleeding-edge" dotenv ethers
touch .env
echo "SK=replace_with_your_private_key_here" >> .env
```

Set up your tsconfig file to compile all the files from the `src` folder to JS in the `dist` folder, for example.

### Initializing all the common entities in the setup script

`./src/index.ts`

```ts
import {
    ChainFactoryConfigs,
    ChainFactory,
    AppConfigs,
    Chain,
} from "xp.network";
import { config } from 'dotenv'; config();
import { Wallet } from "ethers";
import {exit, env} from "process";

export const Config = {
    sk: env.SK! ? env.SK! : "",
}

export const setup = async () => {

    // For Mainnet replace TestNet with MainNet below in both lines
    const factory = ChainFactory(
        AppConfigs.TestNet(), 
        await ChainFactoryConfigs.TestNet()
    );

    const skale = await factory.inner(Chain.SKALE);

    const signer = new Wallet(
        Config.sk,
        skale.getProvider()
    );

    return {
        factory,
        skale,
        signer
    }

}
```

### Minting on Skale:

Because testnets are not always equipped with marketplaces it is useful to mint NFTs for testing like so:

`./src/mint.ts`

```ts
import {setup} from "./index";
import {config} from "dotenv"; config();
import {exit} from "process";
import {ChainFactoryConfigs} from "xp.network";
import { ContractTransaction } from "ethers";

const mint = async (url: string): Promise<ContractTransaction>  => {

    const {
        factory,
        skale,
        signer
    } = await setup();

    const toAddress = await signer.getAddress();
    const skaleUMT = (await ChainFactoryConfigs.TestNet()).skaleParams?.erc721Minter!;

    const result = await factory.mint(
        skale,
        signer,
        {
            contract: skaleUMT,
            uri:url
        }
    );

    return result;

}

// Calliing the code:
(async () => {
    const url:string = "replace with your url";
    const Result: ContractTransaction = await mint(url);
    console.log("Transfer result:", Result);
    exit(0);
})().catch(e => {
    console.error(e);
    exit(1);
});
```

Minting transaction on the chain: https://actual-secret-cebalrai.explorer.staging-v2.skalenodes.com/tx/0x954f057b6f5712e3489c19b6e9eb684504ffbd313f491df7c6875691edc5db7c/token-transfers

### Token Transfer from Skale

In this example code snippet we're transferring an NFT to BSC:

```ts
import {setup} from "./index";
import {config} from "dotenv"; config();
import {exit} from "process";
import {Chain} from "xp.network";

const transfer = async (selected: any) => {

    const {
        factory,
        skale,
        signer
    } = await setup();

    const bsc = await factory.inner(Chain.BSC);
    const toAddress = await signer.getAddress();
    console.log("To Address:", toAddress.toString());

    console.log("Selected:", selected);

    const Result = await factory.transferNft(
        skale,
        bsc,
        selected,
        signer,
        toAddress.toString()
    );

    return Result;

}

(async () => {

    const uri = "replace with your url";
    const contract = (await ChainFactoryConfigs.TestNet()).skaleParams?.erc721Minter!;
    let owner = await signer.getAddress(); // or replace with a different valid address
    owner = owner.toString();
    const tokenId = "12"; // replace with your token ID


    const selected = {
        uri,
        native: {
          chainId: '30',
          tokenId,
          owner,
          contract,
          symbol: 'UMT',
          name: 'UserNftMinter',
          uri,
          contractType: 'ERC721'
        },
        collectionIdent: contract
      }

    const Result = await transfer(selected);
    console.log("Transfer result:", Result);
    exit(0);
})().catch(e => {
    console.error(e);
    exit(1);
});
```

Transfer transaction on Skale: https://actual-secret-cebalrai.explorer.staging-v2.skalenodes.com/tx/0xe3d32b6953f1b62ee6ecd09aacf648863cc85499e4b006597ea750e05ae834bc/token-transfers

Wrapped NFT minted on BSC: https://testnet.bscscan.com/tx/0x09eb3c16b49a1fb20857a5f48fc1add289e8a83056be2a08bf8b07e5a0de1c35