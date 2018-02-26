# Creating a private chain (Mac)

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

On mac High Sierra, geth 1.8.1-stable

Copy the genesis code from above and paste it into a new genesis.json file.

Create a folder called chaindata in the same folder as genesis.json.

Run `geth --datadir chaindata init genesis.json`

NOTE: `--datair` sets the location of your blockchain 

NOTE: `init genesis.json` sets your config file

## Start Geth with your custom data source
After this is configured, start geth with your custom data source:

Run `geth --datadir chaindata`

After that, there may be errors starting geth. One thing I noticed is that long paths may break geth. If you see an error like `.../geth.ipc bind invalid` , you need to shorten your path.

Once that works and geth is running, open a new tab.

## Attach MIST via RPC
 We need to attach the .ipc file for geth and MIST (assuming we want to dev w/ MIST)

 For geth:

 Run `geth attach ipc:[your/path/to/geth.ipc]`


 ## Start mist using your private chain/network

 Then start MIST attached via RPC to your geth instance, open a new terminal window and enter:
 
 Run `/Applications/Mist.app/Contents/MacOs/Mist --rpc /your/path/to/geth.ipc`


If you have Sierra (10.12.2) it was reported that you need to open MIST with a command similar to this:

Run `open -a /applications/mist.app/contents/macos/mist --args --rpc /path/to/geth.ipc`


 After that command MIST open up should load with your private network.



## Summary (replace my .ipc path with your own)

1. Create genesis.json and empty chaindata folder
2. Initialize your private chain: `geth --datadir chaindata init genesis.json`
3. Start geth for your private chain: `geth --datadir chaindata`
4. Open new terminal tab: `open -a /applications/mist.app/contents/macos/mist --args --rpc /Users/benjaminmbrown/desktop/dev/ethereum-masterclass/private-eth-network/chaindata/geth.ipc`
5. Open new tab: `geth attach ipc:/Users/benjaminmbrown/desktop/dev/ethereum-masterclass/private-eth-network/chaindata/geth.ipc`

Once this is set up, in your tab from step 3, you can run `miner.start(1)` to start mining. Initially it will build the Directed Acyclic Graph (DAG) which may take a few minutes. It will display `Generating DAG in progress ...`. After mining commences, you will see the mined test ether in your wallet in MIST.


![Mining On Private Network](http://www.giphy.com/gifs/cft5QkrQcJKTQJUOd8 "Mining gif")
