# Creating a private chain

## Genesis file

Genesis files are used to define and configure a private network. Example looks like:

```
{
    "coinbase"   : "0x0000000000000000000000000000000000000001",
    "difficulty" : "0x20000",
    "extraData"  : "",
    "gasLimit"   : "0x8000000",
    "nonce"      : "0x0000000000000042",
    "mixhash"    : "0x0000000000000000000000000000000000000000000000000000000000000000",
    "parentHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
    "timestamp"  : "0x00",
    "alloc": {},
    "config": {
          "chainId": 15,
          "homesteadBlock": 0,
          "eip155Block": 0,
          "eip158Block": 0
      }
  }

  ```


### Initialize a new chain with genesis configuration

On mac:

`geth --datadir chaindata init genesis.json`

`--datair` sets the location of your blockchain 

`init genesis.json` sets your config file (can't be in data folder)

To start geth with your custom data source:

`geth --datadir chaindata`

After that, there may be errors starting geth. We need to attach the .ipc file for geth and MIST (assuming we want to dev w/ MIST)