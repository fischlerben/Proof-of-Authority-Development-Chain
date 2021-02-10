# Proof of Authority Development Chain
![blockchain](https://images.idgesg.net/images/article/2018/01/cloud_network_blockchain_bitcoin_storage-100745950-large.jpg)

In this project, a genesis block is created from scratch, connected to two nodes using geth, and then is used to mine for Ethereum.  Then, a custom Testnet Node is created on MyCrypto, and a test transaction is sent from the first public address we created to the second public address we created.

---

# 1. Create accounts for two nodes with a separate "datadir" for each using geth:
Navigate into your local "Blockchain-Tools" directory in order to run geth:

    ./geth account new --datadir node1newestnode
    
This produces the following text in your terminal:
![node1creation](/Screenshots/node1creation.png?raw=true)

Now, do the same thing, but for node two:

    ./geth account new --datadir node2newestnode

This produces an identical message to the above, but with a different public address.  It is important to note both of these addresses before moving on.

# 2. Use Puppeth to configure new genesis block:
Use the 2 public addresses, generated in step 1, when it asks which accounts you want to seal and which should be pre-funded.

![genesis_one](/Screenshots/genesis_one.png?raw=true)

# 3. Export genesis configuration:

![export](/Screenshots/export.png?raw=true)

The above results in the following Genesis Configuration, which is saved in the Blockchain-Tools Folder as a json file:

![config](/Screenshots/config.png?raw=true)

# 4. Exit Puppeth and use geth to initialize each node and connect to your genesis block (my network name was fischlerben):

    ./geth init newestnetworkfischlernew.json --datadir node1newestnode

The above results in the following (important to see "Successfully wrote genesis state" at the bottom):
![initialize](/Screenshots/initialize.png?raw=true)

Now do the same thing as the above, just replacing node1 with node2:

    ./geth init newestnetworkfischlernew.json --datadir node2newestnode
    
You will get the same message as above.

# 5. Launch the first node into mining mode:

    ./geth --datadir node1newestnode --unlock "0xbE0D75fbb70FCBEc1f12c35566682A22C337ab18" --mine --rpc --allow-insecure-unlock
    
The above results in the following terminal:
![mining1](/Screenshots/mining1.png?raw=true)

Now, open a new terminal window, cd into your Blockchain-Tools, and launch the second node, passing in the enode address of the first node:

    ./geth --datadir node2newestnode --mine --unlock "0x128270d52385F31d205e6C0EE92f393bdAD29428" --port 30304 --allow-insecure-unlock --bootnodes enode://9de8ab9ce1dd40aee9de3d5f37fc23575c70570dc904e2c159eee9d13e2e7cd8d7df799d1a6e09ab57b0bc4138d41772e6d482eef7ed3734370d2c7c0bcc855e@127.0.0.1:30303
    
The above results in the following terminal:
![mining2](/Screenshots/mining2.png?raw=true)

# 6. Use MyCrypto to send a test transaction using a custom network:
Set up a custom network on MyCrypto, identifying ETH as the currency and setting your Chain ID to whatever you set it as.  Then, connect to your custom network and access it via the Keystore File.

![custom_node](/Screenshots/custom_node.png?raw=true)

![mycrypto](/Screenshots/mycrypto.png?raw=true)

Send yourself some Ether by using your second node address as the address to send Ethereum to.  You should receive a confirmation page like the following:

![confirmation](/Screenshots/confirmation.png?raw=true)

![confirmation2](/Screenshots/confirmation2.png?raw=true)