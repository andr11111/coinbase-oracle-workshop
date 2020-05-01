# 🔮 Coinbase Oracle Workshop 🔮
## Prerequisites
* Coinbase Pro account: https://pro.coinbase.com/
* NodeJS latest version: https://nodejs.org/
* yarn / npm: https://classic.yarnpkg.com/en/docs/install/
* ganache-cli `npm install -g ganache-cli`

## Steps
1. `git clone https://github.com/compound-finance/open-oracle`
2. `cd open-oracle && yarn install`
3. In a separate terminal run `ganache-cli` to start a local testnet
4. (back to the main terminal) Compile contracts `yarn run compile`
5. Deploy OpenOraclePriceData `yarn run deploy OpenOraclePriceData`. Remember the address of the deployed contract - we'll need it in the next step.
6. Deploy DelFiPrice contract `yarn run deploy DelFiPrice "${OpenOraclePriceData address}" "0xfCEAdAFab14d46e20144F48824d0C09B1a03F2BC":array "0xfCEAdAFab14d46e20144F48824d0C09B1a03F2BC" "00"`. Remember the address of the deployed contract - we'll need it later. `0xfCEAdAFab14d46e20144F48824d0C09B1a03F2BC` here is Coinbase Oracle public key.
7. Create Coinbase Pro [API token](https://pro.coinbase.com/profile/api)
9. Post prices on-chain:
    1. Open a separate terminal, `cd poster`
    2. Assign the values from step #7 to environment variables: 
    ```
    export API_PASSPHRASE=${your passphrase}
    export API_KEY_ID=${your key id}
    export API_SECRET=${your secret}
    ```
    3. `yarn install` (ignore the typings errors if any)
    4. Get deployed DelFiPrice contract from step #6 and a private key from the `ganache-cli` output
    5. `yarn run start --view_address=${DelFiPrice address} --poster_key={ETH private key} --sources=https://api.pro.coinbase.com/oracle`
10. Read on-chain prices:
    1. In the main terminal open saddle console `yarn run console`
    2. Get ETH price `await delFiPrice.methods.medianPrice("ETH", ["0xfCEAdAFab14d46e20144F48824d0C09B1a03F2BC"]).call()`
    3. Optionally repeat the posting step and check the updated price.
    
🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉
