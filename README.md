# Proof of Authority Development Chain
![blockchain](https://images.idgesg.net/images/article/2018/01/cloud_network_blockchain_bitcoin_storage-100745950-large.jpg)

In this project, a genesis block is created from scratch, connected to two nodes using geth, and then is used to mine for Ethereum.  Then, a custom Testnet Node is created on MyCrypto, and a test transaction is sent from the first public address we created to the second public address we created.

---

# 1. Create accounts for two nodes with a separate "datadir" for each using geth:
Navigate into your local "Blockchain-Tools" directory in order to run geth:

    ./geth account new --datadir node1
    
This produces the following text in your terminal:
![node1_creation](/Screenshots/node1_creation.png?raw=true)

Now, do the same thing, but for node two:

    ./geth account new --datadir node2

This produces an identical message to the above, but with a different public address.  It is important to note both of these addresses before moving on.

# 2. Use Puppeth to configure new genesis block:
Use the 2 public addresses, generated in step 1, when it asks which accounts you want to seal and which should be pre-funded.

![genesis_one](/Screenshots/genesis_one.png?raw=true)

# 3. Export genesis configuration:

![export](/Screenshots/export.png?raw=true)

The above results in the following Genesis Configuration, which is saved in the Blockchain-Tools Folder as a json file:

![config](/Screenshots/config.png?raw=true)

# 4. Exit Puppeth and use geth to initialize each node and connect to your genesis block (my network name was fischlerben):

    ./geth init fischlerben.json --datadir node1

The above results in the following (important to see "Successfully wrote genesis state" at the bottom):
![initialize](/Screenshots/initialize.png?raw=true)

Now do the same thing as the above, just replacing node1 with node2:

    ./geth init fischlerben.json --datadir node2
    
You will get the same message as above.

# 5. Launch the first node into mining mode:

    ./geth --datadir node1 --unlock "0x3ce53A9c904a68575D59aBCa5A95410E3b7E5195" --mine --rpc --allow-insecure-unlock
    
The above results in the following terminal:
![mining1](/Screenshots/mining1.png?raw=true)

Now, open a new terminal window, cd into your Blockchain-Tools, and launch the second node, passing in the enode address of the first node:

    ./geth --datadir node2 --mine --unlock "0x62500595E256890FD546B9de97572180a664406c" --port 30304 --allow-insecure-unlock --bootnodes enode://57d23e40f7bc2b9cd2e2f1168ac81bb9996e2b8d569807468ba907280b970246e8030b8abc1481d5a16dd79af122702105347d9100c5eca2944d44cff2f38bff@127.0.0.1:30303
    
The above results in the following terminal:
![mining2](/Screenshots/mining2.png?raw=true)

# 6. Use MyCrypto to send a test transaction using a custom network:
Set up a custom network on MyCrypto, identifying ETH as the currency and setting your Chain ID to whatever you set it as.  Then, connect to your custom network and access it via the Keystore File.

![mycrypto](/Screenshots/mycrypto.png?raw=true)