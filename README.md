# Ethereum node on Raspberry

* **[Pre-requisites](#pre-requisites)**
* **[Setup](#setup)**

## Getting Started

These instructions will allow you to connect to an ethereum private network. 

## Pre-requisites

* You need the original genesis.json file from the private network and the enode from the bootnode

* Install go-ethereum

```sh
pi$: sudo add-apt-repository -y ppa:ethereum/ethereum
pi$: sudo apt-get update
pi$: sudo apt-get install ethereum
```
Check version
```sh
$ geth version
```

Other Operating systems: <https://github.com/ethereum/go-ethereum/wiki/Building-Ethereum>

## Setup
###  1]  Create enviroment


```sh
pi$: mkdir fileName
pi$: mkdir fileName/node
pi$: cd fileName
```
Put the same genesis.json file from the private network into "fileName" and init the node
```sh
fileName$: geth --datadir node/ init genesis.json
```
Create a new account (you can create as many you want) and save the data
```sh
fileName$: geth --datadir node/ account new
fileName$: echo 'password' >> node/password.txt
fileName$: echo 'address' >> accounts.txt
```
Create a sh file to run your node
```sh
fileName$: touch startnode.sh
```
Modify the file with this string: remove [] and write your configuration
```sh
geth --datadir node/ --syncmode 'full' --minerthreads=1 --port [] --rpc --rpcaddr '[]' --rpcport [] --rpcapi 'personal,db,eth,net,web3,txpool,miner' --bootnodes '[]' --networkid [] --gasprice '0' -unlock '[]' --password node/password.txt --mine --ipcpath "~/fileName/node/geth.ipc"
```
Make your sh file executable
```sh
fileName$: chmod +x ./startnode.sh
```

###  2]  Start the node and connect

```sh
fileName$: ./startnode.sh
```

Open a new terminal

```sh
filename$: cd node
node$: geth attach geth.ipc
```

###  3]  Wait until 50%+1 of signers give you the autorization (clique.propose("address", true))

Now you can interact with the blockchain from console.
For the full list of command check: https://ethereum.stackexchange.com/questions/28703/full-list-of-geth-terminal-commands
