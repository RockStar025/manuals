```bash
apt update && apt upgrade -y
```

```bash
apt install curl iptables build-essential git wget jq make gcc nano tmux htop nvme-cli pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y
```

```bash
ver="1.19.1"
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz"
rm "go$ver.linux-amd64.tar.gz"
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile
source $HOME/.bash_profile
go version
```

```bash
MONIKER="YOUR_MONIKER_HERE"
```

```bash
git clone https://github.com/NibiruChain/nibiru && cd nibiru
git checkout v0.19.2
make install
```

```bash
```

```bash
nibid init $MONIKER --chain-id nibiru-itn-1
```

```bash
wget -O $HOME/.nibid/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Nibiru/genesis.json"
```

```bash
wget -O $HOME/.nibid/config/addrbook.json "https://share.utsa.tech/nibiru/addrbook.json"
```

```bash
pruning="custom"
pruning_keep_recent="1000"
pruning_interval="10"
sed -i -e "s/^pruning *=.*/pruning = \"$pruning\"/" $HOME/.nibid/config/app.toml
sed -i -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"$pruning_keep_recent\"/" $HOME/.nibid/config/app.toml
sed -i -e "s/^pruning-interval *=.*/pruning-interval = \"$pruning_interval\"/" $HOME/.nibid/config/app.toml
```

```bash
tee /etc/systemd/system/nibid.service > /dev/null <<EOF
[Unit]
Description=nibid
After=network-online.target

[Service]
User=$USER
ExecStart=$(which nibid) start
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```

```bash
systemctl daemon-reload
systemctl enable nibid
systemctl restart nibid && journalctl -u nibid -f -o cat
```
