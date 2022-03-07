# Decentralized Pet Shop

Demo of the "pet-shop" truffle box deployed on IPFS

dApp URL: https://ipfs.infura.io/ipfs/QmbSzsFWFNjMdFVZMg4pVS47LEzr897q4GaM6gVUEPL8x5
(Use Rinkeby with MetaMask to interact with the dApp)

Deployed contract's source code is verified and can be found here: https://rinkeby.etherscan.io/address/0xfe3DC7e9A2f050aC9fb2218Fb5bFbD723d365338

## Pre-requisites

1. NodeJS (version 8.9.x)

2. Truffle
```
    npm install -g truffle
```

## How to run

1. Open a terminal, *run `ganache-cli` and keep it running*
2. Open another (2nd) terminal and run the following:
```
    $ cd pet-shop
```

3. To interact with smart contract from CLI:
```
    truffle develop
    develop> compile --reset
    develop> migrate --reset
    develop> test
```

You should see the following:

```
$ truffle test
Using network 'development'.

Compiling ./test/TestAdoption.sol...


  TestAdoption
    ✓ testUserCanAdoptPet (92ms)
    ✓ testGetAdopterAddressByPetId (169ms)
    ✓ testGetAdopterAddressByPetIdInArray (136ms)


  3 passing (16s)
```

4. To access the dApp UI, run the following:
```
    npm install
    npm run dev
```

5. To deploy the smart contract on a testnet (e.g. Rinkeby), do the following:

* Create an infura account
* Modify `truffle-config.js` to provide necessary infura project information.
* Add a file at root `.secret` and enter the mnemonic that generates your accounts.
* run the following command: `$ truffle migrate network --rinkeby`

You should see something similar to the following:

```
Starting migrations...
======================
> Network name:    'rinkeby'
> Network id:      4
> Block gas limit: 29970676 (0x1c950f4)


2_deploy_contracts.js
=====================

   Deploying 'Adoption'
   --------------------
   > transaction hash:    0x51aca3ac6c9beff46d8dd7abe30cc97920fee13295dec8287c6fffda37bc2134
undefined
undefined
   > Blocks: 1            Seconds: 9
   > contract address:    0xfe3DC7e9A2f050aC9fb2218Fb5bFbD723d365338
   > block number:        10287159
   > block timestamp:     1646656336
   > account:             0xc6696eDf5e753f5B3009608F9e25ED2cb713C7fA
   > balance:             0.225799182312128075
   > gas used:            279435 (0x4438b)
   > gas price:           10 gwei
   > value sent:          0 ETH
   > total cost:          0.00279435 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00279435 ETH

Summary
=======
> Total deployments:   2
> Final cost:          0.0055887 ETH
```

## Deploying to IPFS (putting pet-shop on permanent web)

To have a full decentralized application, the files (frontend) needs to be decentralized in addition of the the computation (backend). We use IPFS: a peer-to-peer network to serve static files to the client.

```
$ mkdir dist/
$ cp -r src/* dist/
$ cp -r build/contracts/* dist/
```
You should see in the dist folder: 

```
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        2022-03-07   4:35 PM                css
d-----        2022-03-07   4:35 PM                fonts
d-----        2022-03-07   4:35 PM                images
d-----        2022-03-07   4:35 PM                js
-a----        2022-03-07   4:32 PM          73963 Adoption.json
-a----        2021-09-27   1:31 PM           2530 index.html
-a----        2022-03-07   4:32 PM          36921 Migrations.json
-a----        2021-09-27   1:31 PM           2716 pets.json
```

1. Manual way
```
$ ipfs add -r dist/

$ ipfs name publish QmbSzsFWFNjMdFVZMg4pVS47LEzr897q4GaM6gVUEPL8x5
Published to QmPXvSsJLEEdCX2P7v8ztkuoDgjCzxujXsmkocLmrJ9EfD: /ipfs/QmbSzsFWFNjMdFVZMg4pVS47LEzr897q4GaM6gVUEPL8x5
```

2. Using a package
Another way to deploy painlessly is to use a package `ipfs-deploy`:

```
$ mv dist/ site/
$ npm install -g ipfs-deploy
$ ipd site
```

https://ipfs.infura.io/ipfs/QmbSzsFWFNjMdFVZMg4pVS47LEzr897q4GaM6gVUEPL8x5

