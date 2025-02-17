<p align="center">
  <img height="100" height="auto" src="https://raw.githubusercontent.com/Nodeist/Kurulumlar/main/logos/nibiru.png">
</p>



# Nibiru Node Installation Guide
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
cd $HOME
git clone https://github.com/NibiruChain/nibiru.git
cd nibiru
git checkout v0.16.3
make install
```

## Configure Node
### Initialize Node
Please replace `MONIKERNAME` with your own moniker.

```
nibid init MONIKERNAME --chain-id nibiru-testnet-2
```

### Download Genesis
The genesis file link below is Nodeist's mirror download. The best practice is to find the official genesis download link.

```
wget -O genesis.json https://snapshots.nodeist.net/t/nibiru/genesis.json --inet4-only
mv genesis.json ~/.nibid/config
```

### Configure Peers
Here is a script for you to update `persistent_peers` setting with these peers in `config.toml`.
```
PEERS=d256380b9344798396e8b1a9c6985f4553a2e0ca@38.242.219.209:26656,52dacee88cf2b6dc8f6e2c1876880bf370796e72@185.219.142.214:39656,32ba0f7eb69b7b984281b1b189bf1aa022915776@142.132.128.132:36656,858ddaf58e566918591802ba04ce3647c5b01707@65.109.106.91:15656,b6db04994c6eac1721014b74288c47bea5fd4870@31.223.32.35:13656,35b0fd0c923fe48bc44f5af70e999982c2c4bb9b@45.8.133.179:26656,e8633047d8eeebcfcb54f67e9f980c74cad91ed3@217.76.49.64:26656,acf44c352787a0075ee26bf9c5587d3b80a8bf85@185.173.39.82:39656,38d128d24e7d9cbdd80227004a7ca0fa129109b5@65.109.92.148:60656,2ec6cb2a83c178fb490a992a3bd6a5c142c3fc61@135.181.20.30:26656,140221bb147d287a11e6abeb0649c78f8bef2a08@65.109.160.183:12656,ae0036bf4c7d33412a655b036d5bfd37a2aa1b72@65.21.237.241:46656,80030d5945eef7519407d047479d40a2f2bf1fe6@65.109.92.241:11036,63f0d4438ebfa588c1879dafcd7f4598dd5f9f19@195.2.80.83:26656,98032241ea61ca6ac066b8fa508baace6678a7a3@190.2.155.67:26656,e67a32bac3086bced94e28d4489f005a4ce48fca@185.244.180.84:39656,8ff8d3effc84c1e5d7bdff36d8921875f7436bcd@65.108.13.185:26858,c08c4d5060697a644838403329be5742bdb4c67f@65.109.92.240:11036,eb65c95ea745d1cb5f66e2fda5d5e1029f4dc43d@5.161.43.109:26656,7643ed772567e8e69ec1dab94bbdb848043d49f2@34.138.219.117:26656,d67d2bae772c3d44123a7495d56c568a185717f8@213.239.216.252:27656,4028996039d167bfff0590c93fecd950b70c7545@144.126.152.61:26656,32c587c3d9329e6c13c5cd7797eb46b30b628bca@95.217.211.70:12656,bfe4fc33622ca87f9dca188d4a205091b2bd5587@194.163.131.165:26656,0e6b2ec046c7652437a4ae9929dc72782e3ff215@149.28.95.188:26656,95fc1114efeb871c8c28e575923f673ab5b4dba6@109.123.241.109:26656,72a84166fbd6b92d8a772843026cf6a2cd97ffbe@65.109.60.19:46656,e3705bc0ca92cf2ff75c1023d34cb403e7670980@95.217.224.252:26656,676a3ce38875bc0ff3a507c507fafa958b9115d0@5.75.136.149:26656,db8f75471ac073b201e0bd56bdaf1bd6c3760c5c@65.109.87.135:13656,b59cb14086b4861eaef6ba9bb335bd44b0f76119@161.97.150.231:26656,3ab57cd651641e80ce82c7b046931bacf638d3f0@167.235.204.231:26656,baf08cf4803c8a5f7d8d026edf65847ae9f29904@85.190.254.137:26656,d2f74fce9d5f33664ebec534b2557a94e67b5232@154.53.59.87:39656,d1f7c37c2df69166e1ffa2ed1b5870427cd17479@23.92.69.78:27656,4537639e8685efe2382c6de93c25eb4f2cca91f9@207.244.239.218:26656,8d22a2251a5fe84ac136bb7aaada10842d121d43@94.250.252.208:26656,8e16be0f98a5c965727c7ed1619604d1ba849d8b@161.97.79.100:26656,51fa995380dad2abf39b828aeb1d0a710a0029f6@80.79.6.64:26656,ffbb25d8a120cd24f8196d594c8d12e247cccf42@65.109.89.23:26656,c72e69f79dddf63d5c5d8fda2777d313500e8264@82.208.22.68:26656,c484bcbd2045a63dd6d943319179e856041182e3@142.132.151.35:15652,a98484ac9cb8235bd6a65cdf7648107e3d14dab4@116.202.231.58:39656,977da259c89314700aaadbbe1d9d4da1a50bf643@194.163.135.104:26656,594149b5209a696b5e9e648786f0ea6df30e1a2b@65.108.6.45:60656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.nibid/config/config.toml
```

## Launch Node
### Configure Cosmovisor Folder
Create Cosmovisor folders and load the node binary.

```
# Create Cosmovisor Folders
mkdir -p ~/.nibid/cosmovisor/genesis/bin
mkdir -p ~/.nibid/cosmovisor/upgrades

# Load Node Binary into Cosmovisor Folder
cp ~/go/bin/nibid ~/.nibid/cosmovisor/genesis/bin
```

### Create Service File
Create a `nibid.service` file in the `/etc/systemd/system` folder with the following code snippet. Make sure to replace `USER` with your Linux user name. You need `sudo` previlege to do this step.

```
[Unit]
Description="nibid node"
After=network-online.target

[Service]
User=USER
ExecStart=/home/USER/go/bin/cosmovisor start
Restart=always
RestartSec=3
LimitNOFILE=4096
Environment="DAEMON_NAME=nibid"
Environment="DAEMON_HOME=/home/USER/.nibid"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="UNSAFE_SKIP_BACKUP=true"

[Install]
WantedBy=multi-user.target
```

### Start Node Service
```
# Enable service
sudo systemctl enable nibid.service

# Start service
sudo service nibid start

# Check logs
sudo journalctl -fu nibid
```

# Other Considerations
This installation guide is the bare minimum to get a node started. You should consider the following as you become a more experienced node operator.



> Configure firewall to close most ports while only leaving the p2p port (typically 26656) open

> Use custom ports for each node so you can run multiple nodes on the same server

> If you find a bug in this installation guide, please reach out to our [Discord Server](https://discord.gg/yV2nEunsTY) and let us know.
