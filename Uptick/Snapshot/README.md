<p align="center">
  <img height="100" height="auto" src="https://raw.githubusercontent.com/Nodeist/Kurulumlar/main/logos/uptick.png">
</p>



# Uptick Snapshot Setup
We take node snapshot every night at 00:00 UTC+3

You can browse the [logs](https://snap.nodeist.net/t/uptick/log.txt) for current snapshot date, block height, and file size information.

### Install lz4 (if needed)
```
sudo apt update
sudo apt install snapd -y
sudo snap install lz4
```

### Stop your node
```
sudo systemctl stop uptickd
```

### Reset your node
This will erase your node database. If you are already running validator, be sure you backed up your `priv_validator_key.json` prior to running the the command.

```
uptickd tendermint unsafe-reset-all --home $HOME/.uptickd --keep-addr-book
```

### Download & Install the snapshot
```
curl -L https://snap.nodeist.net/t/uptick/uptick.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.uptickd --strip-components 2
```

### Restart Service & Check Log:
```
sudo systemctl start uptickd && journalctl -u uptickd -f --no-hostname -o cat
```
