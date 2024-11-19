# fuel node 
Introducing Fuel Ignition

![image](https://github.com/user-attachments/assets/b06877e8-d46f-4941-8e18-26cbc06c664e)

# Fuel
## High-performance Ethereum L2
Fuel Network is a blockchain platform designed to support fast, cheap, and secure transactions  It aims to solve scalability issues on Ethereum while maintaining high security standards.

# An Overview
Fuel emerges as a revolution in the Ethereum space by introducing a modular execution layer and leveraging the UTXO model for smart contracts. This ambitious project promises to solve Ethereum’s scalability issues, offering faster and cheaper transactions while maintaining full compatibility with the EVM. Since its launch in 2020, Fuel has come a long way, proving its potential to transform the landscape of decentralized applications and decentralized finance. With a fundraising of 80 million in 2022 with big names in the sector, Fuel network is a promising project.

# What is a Fuel Node
A node on the Fuel blockchain, or “client”, is software that downloads and maintains a copy of the blockchain. It verifies the authenticity of each block and transaction, ensuring that its copy is always up-to-date and synchronised with the network.

# Consensus Mechanism
Fuel Network uses Proof of Authority (PoA) in its beta testnets.

* Validators: Entities selected for their reputation, responsible for creating blocks and validating transactions.

* Advantages of PoA: Fast transaction times and energy efficiency.

# Hardware requirements
![image](https://github.com/user-attachments/assets/a135a09e-443d-427d-bcac-3f1dcf0a2e3a)


For hosting a Fuel node, opt for a VPS 2 server. I chose Contabo for its reliability and performance, ideal to meet the technical requirements of Fuel. Check out  Contabo VPS Server for easy setup
https://contabo.com/


## Node Installation
## Prepare the environment

* Upgrade packages.




```bash
sudo apt-get update && sudo apt-get upgrade –y
```
* Install wget and curl.
```bash
sudo apt install wget curl  
```
* Install rustup.
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs/ | sh  
```
![image](https://github.com/user-attachments/assets/adf37ff7-5294-4e4d-bf11-30abf8e0f961)

* Configure your current shell. You need to create the corresponding env file in HOME/.cargo
```bash
. "$HOME/.cargo/env"  
```
* Check the version of rustup.
```bash
rustup --version  
```
![image](https://github.com/user-attachments/assets/f0f1fbd9-e744-40d7-86c3-0cc6435f8ca2)

# Install Fuel toolchain
You can use the fuelup-init script provided by the team. This will install forc, forc-client, forc-fmt, forc-lsp, forc-wallet as well as fuel-core in the ~/.fuelup/bin folder.
```bash
curl https://install.fuel.network | sh  
```
![image](https://github.com/user-attachments/assets/5f31c018-a5f5-4d3c-87b4-de3cf2b888dc)

* To use fuelup use.
```bash
source /home/(user)/.bashrc  
```
* Check the version of Fuel installed.
```bash
fuelup --version  
```
![image](https://github.com/user-attachments/assets/a1740a35-aca5-4e26-a200-6227fef8ce88)

The beta-5 network is the latest Fuel testnet. It includes public infrastructures such as beta-5 faucet Icon Link andbeta-5 graphQL playgroundIcon.

To interact correctly with the beta-5 network it is necessary to use the latest toolchain which is installed by default.

* Run the following command to verify the installation of the latest toolchain.
```bash
fuelup show  
```
![image](https://github.com/user-attachments/assets/f95dc462-e71c-424f-ae87-905c515bf033)

# Obtaining a Sepolia API key (Ethereum Testnet)
The next step is to obtain an API key from any RPC provider that supports the Sepolia network. Relayers will help to listen for events on the Ethereum network. Some examples of where to get this API key are  Alchemy
https://www.alchemy.com/
![image](https://github.com/user-attachments/assets/a237defa-ced3-4dc2-8e59-ab36cc1dbf91)

* Register on Alchemy to get your personalised Sepolia ETH RPC API keys:

* Select the Free plan.

![image](https://github.com/user-attachments/assets/b776e077-2020-47ff-8b21-57cedd123839)

* Click on the button “Create new app”.

![image](https://github.com/user-attachments/assets/59c8e022-0548-407b-97ce-913a95cf65fa)

![image](https://github.com/user-attachments/assets/07bbad91-0d55-46c4-a13a-05b485b94d0d)

* Test the API by sending the first request.
 
![image](https://github.com/user-attachments/assets/0636c2d3-e0e4-4434-9342-92d9d7adb67b)

* Copy the CLI command and use it on your server.
```bash
curl https://eth-mainnet.g.alchemy.com/v2/AvlIDj-8eJlcz2NfOK1iMbR5iK1MnAtO -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"alchemy_getAssetTransfers","params":[{"fromBlock": "0x0","category": ["external","erc20","erc721"],"fromAddress": "0x994b342dd87fc825f66e51ffa3ef71ad818b6893"}],"id":0}'  
```
![image](https://github.com/user-attachments/assets/534dae08-bd07-46f0-bb89-322f87e87bfe)

Once the process is filanised you will have access to your dapp in the dashboar and to the generated API.
![image](https://github.com/user-attachments/assets/a67dff34-8854-412d-911a-f14b2d1e33d0)

ETH RPC API: The endpoints must look like this:
```bash
https://eth-sepolia.g.alchemy.com/v2/AvlIDj-8eJlcz2NfOK1iMbR5iK1MnAtO
{"message":"Method Not Allowed","logref":null,"path":null,"_embedded":{"errors":[{"message":"Method [GET] not allowed for URI [/v2/AvlIDj-8eJlcz2NfOK1iMbR5iK1MnAtO]. Allowed methods: [POST]","logref":null,"path":null,"_embedded":{},"_links":{}}]},"_links":{"self":{"href":"/v2/AvlIDj-8eJlcz2NfOK1iMbR5iK1MnAtO","templated":false,"profile":null,"deprecation":null,"title":null,"hreflang":null,"type":null,"name":null}}}  
```
# Generate a new P2P key
* Run.
```bash
fuel-core-keygen new --key-type peering  
```
![image](https://github.com/user-attachments/assets/bb075726-8908-4db0-b4b6-c121a03b8a8f)

# Chain configuration
To run a local node with persistence, you must have a folder with the following chain configuration files.

* Create the folder and download the repository.
```bash
git clone https://github.com/FuelLabs/chain-configuration chain-configuration
mkdir .fuel-sepolia-testnet 
cp -r chain-configuration/ignition/* ~/.fuel-sepolia-testnet/  
```
# Init the node
* Start the node
```bash
fuel-core run \
--service-name=<your_node>-sepolia-testnet-node \
--keypair <P2P key> \
--relayer https://eth-sepolia.g.alchemy.com/v2/<ETH RPC API> \
--ip=0.0.0.0 --port=4000 --peering-port=30333 \
--db-path ~/.fuel-sepolia-testnet \
--snapshot ~/.fuel-sepolia-testnet \
--utxo-validation --poa-instant false --enable-p2p \
--reserved-nodes /dns4/p2p-testnet.fuel.network/tcp/30333/p2p/16Uiu2HAmDxoChB7AheKNvCVpD4PHJwuDGn8rifMBEHmEynGHvHrf \
--sync-header-batch-size 100 \
--enable-relayer \
--relayer-v2-listening-contracts=0x01855B78C1f8868DE70e84507ec735983bf262dA \
--relayer-da-deploy-height=5827607 \
--relayer-log-page-size=500 \
--sync-block-stream-buffer-size 30  
```
![image](https://github.com/user-attachments/assets/c9cc7382-6171-4bf8-81ed-ba4d0358a94d)

Congratulations, your Fuel node is up and running!
# Creating a service with SystenD
SystemD facilitates automatic and reliable management of the Fuel node, improving operational stability and efficiency.

* Automation: SystemD allows you to automatically start the Fuel node at system start-up, ensuring that it is always up and running.
* Supervision: Monitors the status of the node and restarts the service if it fails, guaranteeing continuous and reliable operation.

* Create the service.
```bash
sudo tee /etc/systemd/system/fueld.service > /dev/null << EOF
[Unit]
Description=Fuel Node Sepolia
After=network.target

[Service]
User=$USER
Type=simple
ExecStart=$(which fuel-core run) \
--service-name cumulofuel-sepolia-testnet \
--keypair <P2P key> \
--relayer https://eth-sepolia.g.alchemy.com/v2/<ETH RPC API> \
--ip=0.0.0.0 --port=5000 --peering-port=40444 \
--db-path $HOME/.fuel-sepolia-testnet \
--snapshot $HOME/.fuel-sepolia-testnet \
--utxo-validation --poa-instant false --enable-p2p \
--reserved-nodes /dns4/p2p-testnet.fuel.network/tcp/30333/p2p/16Uiu2HAmDxoChB7AheKNvCVpD4PHJwuDGn8rifMBEHmEynGHvHrf \
--sync-header-batch-size 100 \
--enable-relayer \
--relayer-v2-listening-contracts=0x01855B78C1f8868DE70e84507ec735983bf262dA \
--relayer-da-deploy-height=5827607 \
--relayer-log-page-size=500 \
--sync-block-stream-buffer-size 30

Restart=on-failure
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target 
EOF  
```
* Reloads the SystemD configuration, enables the Fuel node for automatic start, starts the service and displays its current status.
```bash
sudo systemctl daemon-reload
sudo systemctl enable fueld
sudo systemctl start fueld
sudo systemctl status fueld.service  
```
![image](https://github.com/user-attachments/assets/4ed45107-7409-4458-9b8c-4324f8b95aba)

* To view the logs run.
```bash
sudo journalctl -u fueld -f -o cat  
```
![image](https://github.com/user-attachments/assets/b89cd52b-281f-4a56-82bd-fbfbd0b41a53)

# Connect your node to the Fuel wallet
Log in to your Fuel wallet account and click on the top part where it indicates the network, click on +Add new network and type in the address of your node:
http://ip_node:4000/v1/graphql
![image](https://github.com/user-attachments/assets/5debac1b-1490-49b5-9515-a62523b2fd3b)

Click on +Add

# Learn more about Fuel Ignition
https://fuel.network/

https://x.com/fuel_network

https://discord.com/invite/xfpK4Pe

https://docs.fuel.network/guides/installation
