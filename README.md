
# A flashloan on AAVE using truffle unbox aave/flashloan-box

This is the link to the documentation (https://docs.aave.com/developers/v/1.0/tutorials/performing-a-flash-loan/...-with-truffle)

There are a few adjustments to the Flashloan.sol file. I ran it to borrow DAI on the Kovan test network and managed to get it to work.

I didnot add any profit making arbitrage or liquidation language to the file so don't be disappointed. The objective was to understand the nuts and bolts of flashloans using AAVE.

## Stack/dependencies

Node
VScode
truffle
ganache-cli (for forking the mainnet if preferred)
infura (to access the Kovan testnet)
MetaMask

## How to use

Once complied and deployed (truffle compile and truffle migrate --network kovan if using testnet or truffle migrate if using local hard drive via Ganache-cli).  There is no test file (maybe I will add one later). You test the contract using the truffle console which doesn't seem ideal. The steps are
    - Go into truffle console (truffle console --network Kovan)
    - Create an instance of the contract (let f = await Flashloan.deployed())
    - Create an asset (asset = "<the address of the token you are borrowing>")
    - Create an amount in wei (amount = web3.utils.toWei()) I used 1000 for 1000DAI
    - Create your flashloan (await f.flashloan(asset, amount))
    - If successful a JSON file will be returned. You can copy the transaction hash and paste into kovan.etherscan.io to see the details of the transaction.
    Congrats you have just done a flashloan.

After you have deployed the contract to whichever testnet you are using send some DAI(or whatever token you are borrowing) to the flashloan contract to cover the fee that needs to be paid to AAVE (assuming you don't have a profitable strategy yet!). You can use a faucet (I used https://kovan.chain.link/) and 0xFf795577d9AC8bD7D90Ee22b6C1703490b6512FD as the token address (you may need to add this to your Metamask wallet).

# Overall thoughts

 - Using the truffle console to test doesn't seem efficient. I should write a truffle test file to perhaps return a transaction # or something and use truffle test --network kovan.
 - This could be a little out of date as the link is to v1 of the docs.
 - It seems like I should add some code to give the owner (msg.sender) of the contract the abiliy to transfer funds from the contract. In fact that is a warning that AAVE specifcally mentions.
 - I originally wanted to borrow ETH (or WETH) but I need to add some code to interact with a contract called the WETHGateway in order to convert WETH profits from my strategy to ETH for withdrawal. Something that needs more research on my part.

 Hope this helps someone.



