<p align="center">
  <img height="100" height="auto" src="https://raw.githubusercontent.com/Nodeist/Kurulumlar/main/logos/cosmos.png">
</p>



# Cosmos Node Installation Guide
Feel free to skip this step if you already have Go and Cosmovisor.


## Install Go
We will use Go `v1.19.3` as example here. The code below also cleanly removes any previous Go installation.

```
sudo rm -rvf /usr/local/go/
wget https://golang.org/dl/go1.19.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.19.3.linux-amd64.tar.gz
rm go1.19.3.linux-amd64.tar.gz
```

### Configure Go
Unless you want to configure in a non-standard way, then set these in the `~/.profile` file.

```
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
```


### Install Cosmovisor
We will use Cosmovisor `v1.0.0` as example here.

```
go install github.com/cosmos/cosmos-sdk/cosmovisor/cmd/cosmovisor@v1.0.0
```

## Install Node
Install the current version of node binary.

```
git clone https://github.com/cosmos/gaia cosmos
cd cosmos
git checkout v7.1.0
make install
```

## Configure Node
### Initialize Node
Please replace `MONIKERNAME` with your own moniker.

```
gaiad init MONIKERNAME --chain-id cosmoshub-4
```

### Download Genesis
The genesis file link below is Nodeist's mirror download. The best practice is to find the official genesis download link.

```
wget -O genesis.json https://snapshots.nodeist.net/cosmos/genesis.json --inet4-only
mv genesis.json ~/.gaia/config
```

### Configure Peers
Here is a script for you to update `persistent_peers` setting with these peers in `config.toml`.
```
PEERS=b9b99fbf40189c604ea618c4b99c61abc1489b70@18.140.125.215:26656,7bae77119cd833ae399cbfc2584e339058dd5f47@195.201.63.87:26656,dd14fcbe8cbb56e06e3dffd3bdba3b689a4d21aa@3.84.139.214:26656,84cc83cd09a974a234a3fdb5bb4fd46fd856f8ec@142.132.135.239:26656,07fc76b0a1dfcd25e3139a339728d50507bb5d96@67.209.54.35:26656,2938b48ed9dd80451f0be7d8e21840aa383ed929@34.239.177.249:26656,98c2818b7c76e54dda43d543d9f216597403f1e9@144.217.77.98:26656,ab7370e0af17b3fb10c912e722ff05e6e6505fc4@52.76.189.151:26656,0b27d23a50a6969a22b268ec90a198c31b741b2d@65.108.103.184:27656,55debc20a243bbb6acc5db054559953bb87acb30@162.251.238.5:26656,f9243f02b606fee1c3ecbccc2056bcf303732800@198.244.179.141:26656,79ce3cda5d6a8464f4141166982a0352bed1e89f@65.108.137.37:26656,bba10290da32f3cb41e15c3a192413666ce05cee@23.88.18.129:26656,dee3771d222681139d9df18d4e127d4f52820614@65.108.142.81:26656,4437ef919ce6f55a4c2672b9808cfb7e2393df37@167.71.167.246:26656,a2bd6a63813bba08e2b8504f6eace00d088cff82@23.88.18.142:26656,dd02e65e4a4374a40ab8f85de3038757becc7f33@159.69.168.249:26656,573692f610c093ac1fc42df916103f54f9ba56ea@65.21.132.27:21986,57b3ec821a394c243a856b2c82cfb59b7830b0ac@65.108.98.218:19095,8dc4fd0007c74bdf4b7ee1e5a3ab68161cc8f845@142.132.208.213:26656,aa70e2cc756b8dd9e265e578197d3049d67d731f@93.189.30.109:26656,3c08dde641866bf332e1a9f94261a39d57247328@65.108.230.27:26656,1bfda3d59e70290a3dada9bb809dd954371850d3@54.180.225.240:26656,0fd07851d0ae3fe87526901347feacd33c645525@149.202.72.193:26615,44c95b459a0e51e5825cd678661902dc8e732e13@35.222.97.43:26656,471518432477e31ea348af246c0b54095d41352c@88.198.129.17:26656,56783b7e98eed68ec8af791248154f3cc53056d1@34.159.35.95:26656,60afd908298c1ff249bb8e60e469594c5422473d@136.243.91.221:26656,76c65af180735315774497698ccf2091fb81284e@34.141.50.37:26656,ea1779f3c46730e98727fbc0499ba45b31a40ce0@95.216.16.205:14956,dd53fa5cfb6a604feb80860d47506d0dd84baa12@142.132.210.234:26656,2441e90fcb341fcd5bebec15b54e346cdca64a9b@135.148.123.8:14956,11de8a73123ce854241cfa9687921c544b83d5d9@141.94.100.228:26656,e117b5763547ee6aa3c500978ddff5fdee531186@198.244.203.181:26656,e829d4764a5cecc44b3414777853b34407b36601@185.16.39.179:26656,322efd4fdc72a189a2fc8b2b597927831df2bbed@128.0.51.9:26656,daa6d8314246ad65037a48ec2e2266eeea9d46f8@154.53.63.50:26656,585607b08f59ba66ae31589ab52857c507e6736c@142.132.193.186:26656,344d87e04fdf04be760da5069a59d9a489b886a6@52.14.44.1:26656,37dfe1ec33e9f88f378a61a32462d57d2baa5e74@65.108.99.140:26656,58b54d8cfdc0c634ed592e2c008705791253ebbb@172.93.214.10:26656,e0ab6c5cc86959853f499236b8297344802ac5f4@5.161.139.201:26656,137f98c8e22965e672744a3f8909c0f4c8cffc53@135.148.54.43:26656,2286eeee09fcf37e768dfffc0db8c821b9231b7b@204.16.244.78:26656,dcbd6dabd184e93ea00e9eec670de5187dd38ba6@65.108.137.38:26656,c1e437f73b8889b78ea34981e7c349157ad80284@107.135.15.66:26656,c124ce0b508e8b9ed1c5b6957f362225659b5343@23.88.18.57:26656,03a3c841227b08a37baf792eabae7f68027a059b@162.55.238.6:36656,f58fa3aa606d321863effe34cfc7b22cfbfcbc2c@51.91.7.44:26656,12ec6fbf99faa088375ee776f641903fc680f0d4@51.38.52.188:26615,1395d0eea72b7f47c3d41852991249b0c661e0c7@34.122.91.134:26656,acb9c9b62c8f97ac697eb1855bb6660411bec9c7@46.4.119.169:26656,9755cab2585a2794453a5b396ef13b893393366f@65.108.212.224:46671,8707282f51ebfba828c08a7316ca84ed5667a0f5@74.118.142.175:26656,7dd34d8d3880bc48eff3e47b941d06bd1941a962@93.115.25.106:26656,fce4e4a0790d431a1170970c8773721c4901a0f0@193.122.137.246:26656,241b17dba97a2ed3c3747d12781fb86c9706e2d4@89.58.27.86:26656,703714c82c94fc1c74b6ee0d1fc3417b932be5f3@169.155.44.11:26656,30d9cdef07cdb54e9ada05132688231831f3156b@18.118.215.160:26656,a94dff85ed430f0475f41fe306c82b7eb7f6e858@51.91.153.78:31649,538348fa1eac998dad392a3f00f7b957042c3e84@15.235.53.86:11156,7b8ab74fa7c3cc10b203b990abfc86e1a0b82a79@34.254.201.211:26656,73c2a86cc0d4b51c81bd0e36cee69f1731bcda0d@23.88.69.157:26656,27ad834c62dbefc5beb74be7575515927bd07c58@193.176.85.151:26656,f28ee3d3573b3c72d4c134de6a78e96574479def@34.28.23.20:26656,1cce99042f884d669e7287e3e362bff8e385c63e@46.4.79.183:26726,ec2129be97cdd56178884f124824cc6953fc51c1@150.136.13.169:26656,4fb444050d0084c4aa81f9f55e10060063179dd9@151.80.26.241:26656,05eb7aa1fd8251ed7a650c13da406df022b298b6@195.201.56.108:26656,f701e3e0b7983c5a9e8ef34f88acd82ebd661c87@64.44.148.194:26656,4c46d32cbc4777c59a91a53fdadf8a3fa362036e@116.202.10.68:26656,89282ce1883f187a1a6d4d6b2308e129c5410d51@142.132.197.103:26656,32bdba6ced12cdf2e534566e6c3d66ee2f7ef494@84.244.95.229:26656,1da54d20c7339713f1d6d28dd2117087dd33d0ca@154.53.32.78:26656,915a5d104236764e33d5f7fd8d6c946e66766723@34.148.63.0:26656,ba3bacc714817218562f743178228f23678b2873@34.141.15.99:26656,dea13e7232642331360d4387b0ab106b014092d4@116.202.236.59:26656,5b143d463427d9ad0b621f97c0b8933643e293da@34.86.206.37:26656,213857e741833d17275ea559bb2d0342398cec99@35.245.206.45:26656,db7850e8e9bef0568904b7d5bcaec813e8e3d295@34.27.227.166:26656,d9dbd30f7e9ae99dc05645f48f4637c2f4a14645@34.107.9.71:26656,5dde13b98a2f69f54e0d5e3384fdc903bbb2dc30@172.93.214.11:26656,b79e1d3a621bdafd3a8d9a49dff8f4737d0bedc9@52.73.168.104:26656,cf52e109b7015d5c21f50ab4331fb7062160ab6c@34.79.21.52:26656,dff07399aeadf3f1b6edfac07f92a238112d3036@93.189.30.120:26656,68575d9f747fc412f43eb115f42dae651061cd8b@13.58.176.50:26656,10e3acd4baeb6cba8881d75a0bde04b5526b39ce@3.217.133.209:26656,53b3651680ec3482d736808cbb3035940107f8ab@185.146.148.119:26656,2633bc088bcf96209b695734005952906b5c45e3@3.123.191.80:26656,547a1165e390a14d70e7de0cbf1708fea80eb44d@172.104.115.76:26656,df65b335f668b9feae5f8807ec899f96acd15d79@165.227.138.32:26656,332388be4c4941870b0f609011bc0ab583c31ff9@144.91.91.4:26656,18af72a5b949343d0e242c70d87225d9c47867b6@3.121.86.113:26656,544c554326bc0771e0e2e74f31be89aa44770b79@65.21.227.95:2000,36bdcff719d773a032f1250dcb2c8669ec43816d@34.240.122.232:26656,b7e3dacac35201ecb6b3259aa9e59e5a96cba5be@51.68.10.109:26656,d35f08a60aeb2729d07e92e778b4c6f83379092e@18.138.160.68:26656,bd410d4564f7e0dd9a0eb16a64c337a059e11b80@47.103.35.130:26656,aa61bc0e8a42eda6ac1276c4279941714a4a38f4@88.99.70.38:26656,1d02b4300c6b6fd1123a20502f0b3c0ce3b73654@88.198.16.9:26656,c540af0c82963228aa865d27d9b6142fc54b571d@176.9.102.164:26656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.gaia/config/config.toml
```

## Launch Node
### Configure Cosmovisor Folder
Create Cosmovisor folders and load the node binary.

```
# Create Cosmovisor Folders
mkdir -p ~/.gaia/cosmovisor/genesis/bin
mkdir -p ~/.gaia/cosmovisor/upgrades

# Load Node Binary into Cosmovisor Folder
cp ~/go/bin/gaiad ~/.gaia/cosmovisor/genesis/bin
```

### Create Service File
Create a `gaiad.service` file in the `/etc/systemd/system` folder with the following code snippet. Make sure to replace `USER` with your Linux user name. You need `sudo` previlege to do this step.

```
[Unit]
Description="gaiad node"
After=network-online.target

[Service]
User=USER
ExecStart=/home/USER/go/bin/cosmovisor start
Restart=always
RestartSec=3
LimitNOFILE=4096
Environment="DAEMON_NAME=gaiad"
Environment="DAEMON_HOME=/home/USER/.gaia"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="UNSAFE_SKIP_BACKUP=true"

[Install]
WantedBy=multi-user.target
```

### Start Node Service
```
# Enable service
sudo systemctl enable gaiad.service

# Start service
sudo service gaiad start

# Check logs
sudo journalctl -fu gaiad
```

# Other Considerations
This installation guide is the bare minimum to get a node started. You should consider the following as you become a more experienced node operator.



> Configure firewall to close most ports while only leaving the p2p port (typically 26656) open

> Use custom ports for each node so you can run multiple nodes on the same server

> If you find a bug in this installation guide, please reach out to our [Discord Server](https://discord.gg/yV2nEunsTY) and let us know.
