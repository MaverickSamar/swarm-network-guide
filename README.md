Swarm Bee Network (Decentralized Storage) Full Backend Guide 

By – Samarth Ranjan 

Installation and Running of the Bee Node 

Skip Step 1 and 2 if you are a Ubuntu User. 

Step 1 – Install Virtual Box - https://www.virtualbox.org/wiki/Downloads 

Step 2 – Set up Virtual Box using Ubuntu LTS - https://ubuntu.com/download/desktop 

 

Step 3 – Install Bee Client for Swarm -  

-> wget https://github.com/ethersphere/bee/releases/download/v1.7.0/bee_1.7.0_amd64.deb 

-> sudo dpkg -i bee_1.7.0_amd64.deb 

 

Debug - If by chance dpkg is locked, and throws an error in installation 

sudo rm /var/lib/dpkg/lock 
sudo rm /var/lib/dpkg/lock-frontend 
sudo rm /var/cache/apt/archives/lock 
sudo apt update 
sudo dpkg --configure -a 

Step 4 – Try running bee node - 

-> bee start 

Set up password and confirm it. Remember the password. 

 

On first starting service of the bee client, an error will be thrown, 

got error factory fail: disabled chain backend, shutting down... factory fail: disabled chain backend  

The error occurs due to unavailability of Genosis Node RPC in config file of bee(etc/bee/bee.yaml). 

 

Step 5 – Get RPC Node - 

 

You can use these nodes for running your bee node. 

RPC Node endpoint will look like - 

https://gno.getblock.io/mainnet/?api_key=b338ee33-b3e3-be33-bee5-b335b555b555 

You can also setup your own Genosis node - 

https://docs.gnosischain.com/clients/gnosis-chain-node-openethereum-and-nethermind 

I did not set up my own Genosis Node due to limited resources. 

 

Step 6 - Configure bee.yaml file for file storage directory, nat-address, swap-endpoints 

-> sudo nano /etc/bee/bee.yaml 

 

 

data-dir : This key contains value of the place where you will store your data and contribute to the network by storing other data. 

By default this location is /var/lib/bee 

full-node : true 

Set it to true if you want to participate in the Swarm Network and earn 	more bzz for storage. 

nat-addr : “<YourIPAddress>/1634” 

 

swap-endpoints : Paste your RPC URL here within “”. 

swap-endpoints : https://gno.getblock.io/mainnet/?api_key=b338ee33-	b3e3-be33-bee5-b335b555b555 

mainnet : true 

By default it is set to false, make it true to interact with the swarm 		network. 

You can use Goerli Testnet for faucets. 

swap-initial-deposit : Put value according to BZZ in your account chequebook. 

You can also swap mainnet to false and swap-initial-deposit to 0 and 	test it over the Testnet. 

To host the website on Swarm -  

Use ENS resolver-options 

resolver-options: ["https://mainnet.infura.io/v3/<<your-api-key>>"] 

(Please go through other key-value pairs for better understanding of the 	changes you can make in the bee.yaml file. I have provided all the 		important once.) 

Step 7 – Fund Your Node. 

For Mainnet - https://docs.ethswarm.org/docs/installation/fund-your-node 

For Testnet - 

Join Swarm discord - https://discord.com/invite/wdghaQsGq5 

Visit #faucet channel 

/faucet sprinkle <Your georli/genosis Chain Address> 

Step 8 – Run Bee Node - 

With everything set up, now use  

-> bee start 

 

Congrats, Your node is running now. 

 

Additional References 

Bee API for Upload and Download 

Debug API - Once your Bee node is running, a HTTP API is enabled for you to interact with.  

By default this is on port 1633 (Do not change value of api-addr:1633 in bee.yaml) 

Visit -> https://docs.ethswarm.org/api/ 

The project was called off by the end of the the node deployment so the API references are not available with me. 

You can use this bee api client to upload and download data 

All Post, Get, Put, etc. requests are given in the api documentation so there is no need to recall every  

You can check you bee api client -  

->curl http://localhost:1633 

It will return Ethereum Swarm Bee, means the node and the api are running successfully. 

Some references - 

You can also take reference form HACKMD Documentation on upload with postage stamp 

https://hackmd.io/@ethswarm/ryyP9EDHw 

 

Bee JS Library 

There exists a bee.js library - https://github.com/ethersphere/bee-js  

Full Documentation - https://www.npmjs.com/package/@ethersphere/bee-js  

Here are some examples of using beejs - 

Ethersphere examples - https://github.com/ethersphere/examples-js  

To upload files on the swarm network using your website frontend, you require a bee node running on a local machine or cloud host.  

Use axios-fetch - https://github.com/lifeomic/axios-fetch (Supported by fetch based HTTP client) 

Note - Bee.js is a fetch-based HTTP client that does not supports features like upload progress so you can use axios-fetch. 

 

 

 

 

 

 

 

 
