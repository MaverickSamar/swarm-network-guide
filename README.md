
# Swarm Bee Network (Decentralized Storage) Full Backend Guide 

A detailed documentation with images of running a bee node on your local machine. Also some additional references and notes for bee.js library.  

## Installation and Running


Installation and Running of the Bee Node 

Skip Step 1 and 2 if you are a Ubuntu User. 
Only windows users follow step 1 and step 2. 

### Step 1
    Install Virtual Box - https://www.virtualbox.org/wiki/Downloads 

### Step 2
    Set up Virtual Box using Ubuntu LTS - https://ubuntu.com/download/desktop 


### Step 3
Install Bee Client for Swarm  
```bash
    wget https://github.com/ethersphere/bee/releases/download/v1.7.0/bee_1.7.0_amd64.deb
    sudo dpkg -i bee_1.7.0_amd64.deb 
```


#### Common Error Handling

If by any chance your dpkg is locked, and throws an error in installation, then hard reset can be done.

Remove dpkg lock, lock-frontend and caches.
``` bash 
    sudo rm /var/lib/dpkg/lock 
    sudo rm /var/lib/dpkg/lock-frontend 
    sudo rm /var/cache/apt/archives/lock 
```
Install dpkg
``` bash 
    sudo apt update 
    sudo dpkg --configure -a
```


### Step 4
Try running bee node 

```bash
    bee start 
```

Set up password and confirm it. Remember the password. 

![App Screenshot](https://via.placeholder.com/468x300?text=password confirm)

On first starting service of the bee client, an error will be thrown, 

    got error factory fail: disabled chain backend, shutting down... factory fail: disabled chain backend  

The error occurs due to unavailability of Genosis Node RPC in config file of bee(etc/bee/bee.yaml). 

 


## Configure bee.yaml



Configure bee.yaml file for file storage directory, nat-address, swap-endpoints 
```bash
    sudo nano /etc/bee/bee.yaml
``` 


 ![App Screenshot](https://via.placeholder.com/468x300?text=bee.yaml)

 
### Data Directory
    data-dir : /var/lib/bee 
This key contains value of the place where you will store your data and contribute to the network by storing other data. 

By default this location is /var/lib/bee 
![App Screenshot](https://ibb.co/TvLXZb4)

### Full Node/Light Node

    full-node : true

Set it to true if you want to participate in the Swarm Network and earn more bzz for storage. 

### Nat Address
    nat-addr : “<YourIPAddress>/1634” 
![App Screenshot](https://via.placeholder.com/468x300?text=Nat-Address)

### Swap Endpoints
 
    swap-endpoints : "Paste your RPC URL here within “”". 

swap-endpoints : https://gno.getblock.io/mainnet/?api_key=b338ee33-	b3e3-be33-bee5-b335b555b555 

### Mainnet/Testnet
    mainnet : true 

By default it is set to false, make it true to interact with the swarm network. 

You can use Goerli Testnet for faucets. 

### Swap Initial Deposit
    swap-initial-deposit : Put value according to BZZ in your account chequebook. 

You can also swap mainnet to false and swap-initial-deposit to 0 and test it over the Georli Testnet. 

### ENS - To host the website on Swarm 

Use ENS resolver-options 

    resolver-options: ["https://mainnet.infura.io/v3/<<your-api-key>>"] 

(Please go through other key-value pairs for better understanding of the changes you can make in the bee.yaml file. I have provided all the important once.)

## Get RPC Node

You can use these nodes for running your bee node. 

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

RPC Node endpoint will look like :

    https://gno.getblock.io/mainnet/?api_key=b338ee33-b3e3-be33-bee5-b335b555b555 

Note - do not share your api key.

You can also setup your own Genosis node :

    https://docs.gnosischain.com/clients/gnosis-chain-node-openethereum-and-nethermind 

I did not set up my own Genosis Node due to limited resources. 


## Fund Your Node

### For Mainnet
    https://docs.ethswarm.org/docs/installation/fund-your-node 

### For Testnet 

Join Swarm discord, Google Search
    
    Swarm discord

Click the first link 

Visit #faucet channel and verify your account. 
then

    /faucet sprinkle <Your georli/genosis Chain Address> 
## Run Bee Node

With everything set up, now type in terminal 

    bee start 

Congrats you have your bee node up and running now

![App Screenshot](https://via.placeholder.com/468x300?text=bee-start)

## Bee API Reference

Once your Bee node is running, a HTTP API is enabled for you to interact with.  

By default this is on port 1633 (Do not change value of api-addr:1633 in bee.yaml) 

    https://docs.ethswarm.org/api/
 
#### Get all items

```http
  GET /api/items
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `api_key` | `string` | **Required**. Your API key |

#### Get item

```http
  GET /api/items/${id}
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of item to fetch |

#### add(num1, num2)

Takes two numbers and returns the sum.


You can use this bee api client to upload and download data. All Post, Get, Put, etc. requests are given in the api documentation so there is no need to recall every  

You can check you bee api client -  

```bash
    curl http://localhost:1633 
```

It will return

    Ethereum Swarm Bee
    
means the node and the api are running successfully. 

### Some references

You can also take reference form HACKMD Documentation on upload with postage stamp 

    https://hackmd.io/@ethswarm/ryyP9EDHw 

 

## Bee JS Documentation


There exists a bee.js library

    https://github.com/ethersphere/bee-js  
 
NPM documentation of bee - [Documentation](https://www.npmjs.com/package/@ethersphere/bee-js)

Here are some examples of using beejs - 

### Examples

Ethersphere examples

    https://github.com/ethersphere/examples-js  

### Note
To upload files on the swarm network using your website frontend, you require a bee node running on a local machine or cloud host.  

Use axios-fetch
    
    https://github.com/lifeomic/axios-fetch

(Supported by fetch based HTTP client) 

Please Note - Bee.js is a fetch-based HTTP client that does not supports features like upload progress so you can use axios-fetch. 
