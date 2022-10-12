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


## NFT-Indexer

To see a user's NFTs on Skale use the following code snippet:

```ts
import {setup} from "./index";
import {config} from "dotenv"; config();
import {exit} from "process";

export const nftList = async () => {

    const {
        factory,
        skale,
        signer
    } = await setup();

    const NFTs = await factory.nftList(
        skale,
        (await signer.getAddress()).toString()
    );

    return NFTs;
}

// Calling the function:
(async () => {
    const Result = await nftList();
    console.log("NFTs:", Result);
    exit(0);
})().catch(e => {
    console.error(e);
    exit(1);
})
```

Example output:

```bash
$ tsc && node ./dist/nft_index.js
NFTs: [
  {
    uri: 'https://meta.polkamon.com/meta?id=10001419693',
    native: {
      chainId: '30',
      tokenId: '12',
      owner: '0x0d7df42014064a163DfDA404253fa9f6883b9187',
      contract: '0x34933A5958378e7141AA2305Cdb5cDf514896035',
      symbol: 'UMT',
      name: 'UserNftMinter',
      uri: 'https://meta.polkamon.com/meta?id=10001419693',
      contractType: 'ERC721'
    },
    collectionIdent: '0x34933A5958378e7141AA2305Cdb5cDf514896035'
  }
]
✨  Done in 29.54s.
```

### Transaction fee estimation

```ts
import {setup} from "./index";
import {config} from "dotenv"; config();
import {exit} from "process";
import {ChainFactoryConfigs, Chain} from "xp.network"

const estimate = async () => {
    const {
        factory,
        skale,
        signer
    } = await setup();

    // Replace with any other supported chain following the pattern
    const bsc = await factory.inner(Chain.BSC);

    const uri = "replace with your url";
    const contract = (await ChainFactoryConfigs.TestNet()).skaleParams?.erc721Minter!;
    let owner = await signer.getAddress(); // or replace with a different valid address
    owner = owner.toString();
    const tokenId = "12"; // replace with your token ID

    // The selected NFT to be transferred
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

    const skale_bsc = await factory.estimateFees(
        skale,
        bsc,
        //@ts-ignore
        selected,
        owner // If sendinw to oneself
    );

    return skale_bsc.toString();
}


// Calling the funciton
(async () => {
    const Result = await estimate();
    console.log("Estimation:", Result);
    exit(0);
})().catch(e => {
    console.error(e);
    exit(1);
})
```
Example output:
```bash
$ tsc && node ./dist/estimate.js
Estimation: 38489638594795216500
✨  Done in 7.14s.
```

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