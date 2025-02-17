<p align="center">
  <img height="100" height="auto" src="https://raw.githubusercontent.com/Nodeist/Kurulumlar/main/logos/nolus.png">
</p>


# Nolus State Sync
```
systemctl stop nolusd
nolusd tendermint unsafe-reset-all --home $HOME/.nolus --keep-addr-book
SNAP_RPC="https://rpc-nolus.nodeist.net:443"
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.nolus/config/config.toml
```
The above `unsafe-reset-all` command reset your `wasm` folder inside the data folder. You can download our `wasm` folder to fix it.
```
rm -r ~/.nolus/data/wasm
wget -O wasmonly.tar.lz4 https://snapshots.nodeist.net/t/nolus/wasmonly.tar.lz4 --inet4-only
lz4 -c -d wasmonly.tar.lz4  | tar -x -C $HOME/.nolus/data
rm wasmonly.tar.lz4
```

Restart the node:
```
systemctl restart nolusd && journalctl -fu nolusd -o cat
```
