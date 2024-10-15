# Cosmovisor Integration - Binaries

> `cosmovisor` is a small process manager for Cosmos SDK application binaries that monitors the governance module for incoming chain upgrade proposals. If it sees a proposal that gets approved, cosmovisor can automatically download the new binary, stop the current binary, switch from the old binary to the new one, and finally restart the node with the new binary.

## 1. Setup Cosmovisor

Installing cosmovisor:

```
go install cosmossdk.io/tools/cosmovisor/cmd/cosmovisor@latest
```

Set up the Cosmovisor environment variables. We recommend setting these in your `.profile` so it is automatically set in every session.

```
echo "# Setup Cosmovisor" >> ~/.profile
echo "export DAEMON_NAME=pundixd" >> ~/.profile
echo "export DAEMON_HOME=$HOME/.pundix" >> ~/.profile
source ~/.profile
```

After this, you must make the necessary folders for `cosmosvisor` in your `DAEMON_HOME` directory (`~/.pundix`) and copy over the current binary.

```
mkdir -p ~/.pundix/cosmovisor
mkdir -p ~/.pundix/cosmovisor/genesis/bin
mkdir -p ~/.pundix/cosmovisor/upgrades/pxv2
```

## 2. Download the Pundix release

{% hint style="info" %}
Releases can be found here [https://github.com/pundix/pundix/releases/](https://github.com/pundix/pundix/releases/)
{% endhint %}

Manually download the binary and extract it to folder:

{% tabs %}
{% tab title="Build from source" %}
```sh
git clone https://github.com/pundix/pundix.git
```

```sh
git checkout release/v0.1.x
make build
cp ./build/bin/pundixd ~/.pundix/cosmovisor/genesis/bin/
```

```sh
git checkout release/v0.2.x
make build
cp ./build/bin/pundixd ~/.pundix/cosmovisor/upgrades/pxv2/bin/
```
{% endtab %}

{% tab title="Ubuntu" %}
```sh
wget https://github.com/pundix/pundix/releases/download/v0.1.3/pundix_0.1.3_Linux_x86_64.tar.gz && tar -xvf pundix_0.1.3_Linux_x86_64.tar.gz -C ~/.pundix/cosmovisor/genesis/

wget https://github.com/pundix/pundix/releases/download/v0.2.1/pundix_0.2.1_Linux_x86_64.tar.gz && tar -xvf pundix_0.2.1_Linux_x86_64.tar.gz -C ~/.pundix/cosmovisor/upgrades/pxv2/
```
{% endtab %}
{% endtabs %}

Copying the json upgrade info, you do not need to perform this step if there is no `upgrade-info.json` file in the `~/.pundix/data/data` folder

```sh
cp ~/.pundix/data/upgrade-info.json ~/.pundix/cosmovisor/genesis/
```

To check that you did this correctly, ensure your versions of `cosmovisor` are the same:

```
cosmovisor version
```

## 3. Start your node

To keep the process always running. If you're on linux, you can do this by creating a service.

```
sudo tee /etc/systemd/system/pundixd.service > /dev/null <<EOF
[Unit]
Description=Pundix Daemon
After=network-online.target

[Service]
User=$USER
ExecStart=/root/go/bin/cosmovisor run start --home=/root/.pundix
Restart=always
RestartSec=3
LimitNOFILE=infinity

Environment="DAEMON_HOME=/root/.pundix"
Environment="DAEMON_NAME=pundixd"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="UNSAFE_SKIP_BACKUP=true"

[Install]
WantedBy=multi-user.target
EOF
```

Reload, enable and restart the node with daemon service file

```
sudo -S systemctl daemon-reload
sudo -S systemctl enable pundixd
sudo -S systemctl restart pundixd
```

You can check the status with

```
systemctl status pundixd
```

Accessing logs

```
journalctl -u pundixd -n 100
```
