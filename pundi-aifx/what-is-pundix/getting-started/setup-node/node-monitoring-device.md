# Node Monitoring Device

## Prerequisites

We recommend the following for running a node monitoring device:

* 2 or more CPU cores
* At least 40G of disk storage
* At least 4G of memory
* At least 10mbps network bandwidth
* Have to be setup in a separate environment from validator nodes/sentry nodes

{% hint style="info" %}
Before setting up a node monitoring device, you may take a look at the PundiX [installation](../installation-pundix.md) setup to setup the PundiX CLI.
{% endhint %}

## Prometheus metrics

PundiX also supports the use of Prometheus metrics. This monitoring device allows you to keep up to date with you validator nodes especially the status and performance of your validator nodes.

{% hint style="info" %}
More information on the list of available metrics and useful queries can be found [here](https://docs.tendermint.com/master/nodes/metrics.html).
{% endhint %}

## Deploy and Configure Monitoring Services

{% hint style="info" %}
Before deploying monitoring program, install docker following the [official docs](https://docs.docker.com/compose/install/).
{% endhint %}

### Configure node services

{% hint style="info" %}
**User should git clone** [**pundix**](https://github.com/pundix/pundix) **from Github first!**

The **config.toml** file is in the **/.pundix** directory and the **prometheus.yml** file is in **/pundix** directory.
{% endhint %}

To enable the Prometheus metrics, set `prometheus=true` in your config file `$HOME/.pundix/config/config.toml`. Through setting the `prometheus_listen_addr` in the config file, you may choose the port for you to monitor your node. It is defaulted to port `26660`.

In the file `./pundix/develop/prometheus/prometheus.yml` you can configure the target node(s) IP address, multiple nodes can be added in the following format.

For example:

```yaml
static_configs:
      - targets: [ "<IP_ADDRESS_1>:26660"]
        labels:
          name: validator-01
          chain_id: PUNDIX
      - targets: [ "<IP_ADDRESS_2>:26660"]
        labels:
          name: sentry-01
          chain_id: PUNDIX
      - targets: [ "<IP_ADDRESS_3>:26660"]
        labels:
          name: sentry-02
          chain_id: PUNDIX
```

### Telegram Administrator and Bot Configuration

In the file `./pundix/develop/docker-compose.yaml` under `alertmanager-bot` - `environment` are the variables `TELEGRAM_ADMIN` and `TELEGRAM_TOKEN`:

* For example:

```yaml
    alertmanager-bot:
        container_name: alertmanager-bot
        image: metalmatze/alertmanager-bot:0.4.3
        command:
          - '--alertmanager.url=http://pundix@alertmanager:9093/'
          - '--store=bolt'
          - '--bolt.path=/data/bot.db'
          - '--template.paths=/templates/default.tmpl'
          - '--listen.addr=0.0.0.0:9091'
        environment:
          TELEGRAM_ADMIN: "XXXXXX\nAdmin1USERID\nAdmin2USERID"
          TELEGRAM_TOKEN: "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
```

* `TELEGRAM_ADMIN`: The Telegram user id for the admin (not the bot itself, you, the user). The bot will only reply to messages sent from an admin. All other messages are dropped and logged on the bot's console. Your can get your user id from `@userinfobot`.
* `TELEGRAM_TOKEN`: Token you get from `@botfather`
* For more information with regards to the telegram bot, see [here](https://core.telegram.org/bots#creating-a-new-bot) and [here](https://github.com/metalmatze/alertmanager-bot):

### Access the monitoring services

Should you not want to change the default username and password, you can start the monitoring service by using the following command:

```yaml
docker-compose -f ./pundix/develop/docker-compose.yaml -p pundix-node-monitor up -d
```

* Open port `:9095` (for example `http:// <your_IP_address>:9095`) and you will see the prometheus page. Here you can see all the defined alarm rules. You can change these rules in the file `./pundix/develop/prometheus/rules/pundix-chain-alerts.yml`. The default username and password are `px` and `pundix` respectively.
* Open port `:9093` (for example `http:// <your_IP_address>:9093`) and you will see the `alertmanager` page. You can manage alarm notifications here. The default username and password are `px` and `pundix` respectively.
* Open port `:3000` (for example `http:// <your_IP_address>:3000`) and you will see the `grafana` page.
* The default username and password are both `admin`, once you have logged in you will be asked to set a new password.
* After setting a new password, you can go into Dashboards > Manage and select 'PundiX Chain Dashboard'. Here you can see a dashboard of various indicators and information of a selected node.
* You may find out the details of [`<your_IP_address>`](https://www.google.com/search?q=what+is+my+ip+address\&rlz=1C5CHFA\_enSG996SG996\&oq=what+is\&aqs=chrome.0.69i59j69i57j69i59j35i39j0i433i512j69i60l3.1255j0j7\&sourceid=chrome\&ie=UTF-8)`.`
* Authorise inbound traffic for the following ports ranges **9091, 9093, 3000** for `<your_IP_address>` in node monitoring device. you can also allow the port range **26660** for `<node_`_`monitoring_public_ip`_`>` in the validator instance.

### Changing The Default Passwords for Prometheus and Alertmanager

{% hint style="info" %}
**DO NOT use `$` in any of your passwords, as it will not work with the `alertmanager.url`**
{% endhint %}

You can change the default username and password in the file `./pundix/develop/prometheus/web-config.yml` with the following format:

```yaml
basic_auth_users:
  <username>: <password_hashed_with_bcrypt>

# for example
basic_auth_users:
  px: $2y$10$xCpE/Q5UGHxO1qKR5av2DOJGqTkb6E5G/Dc9VT1AZQxNlQJwQpb0q
```

How to hash with bcrypt:

1. install apache2
2. input this command `htpasswd -nBC 10 "" | tr -d ':\\n'`
3. type in password
4. copy hash

For more info on prometheus web-configuration see this [link](https://github.com/prometheus/exporter-toolkit/blob/master/docs/web-configuration.md#about-bcrypt).

{% hint style="info" %}
If you changed the username and password in the `web-config.yaml`file there are 3 other areas where you need to update as well.
{% endhint %}

#### Grafana

For `grafana` to be able to get data from `prometheus` you will need to update the username and password in the file `./pundix/develop/grafana/provisioning/datasources/datasource.yml`

{% hint style="info" %}
The password here is in text format and does not need to be hashed.
{% endhint %}

For example:

```yaml
# <string> basic auth username, if used
basicAuthUser: px

# <string> basic auth password, if used
basicAuthPassword: pundix
```

#### Prometheus

For `prometheus` to be able to send alerts to `alertmanager` you will need to update the username and password in the file `./pundix/develop/prometheus/prometheus.yml`

For example:

{% hint style="info" %}
The password here is in text format and does not need to be hashed.
{% endhint %}

```yaml
# Alertmanager configuration
alerting:
  alertmanagers:
    # Sets the `Authorization` header on every request with the
    # configured username and password.
    # password and password_file are mutually exclusive.
    - scheme: http
      basic_auth:
        username: px
        password: pundix
      static_configs:
        - targets:
            - alertmanager:9093
```

#### Alertmanager-bot

For the telegram bot to be able to obtain information from the `alertmanager` you will need to update the username and password within the `--alertmanager.url` in the `./pundix/develop/docker-compose.yaml` file. Also you may [update](node-monitoring-device.md#updating-node-monitoring-services) the alert-manager-bot.

For example:

{% hint style="info" %}
The password here is in text format and does not need to be hashed
{% endhint %}

Under `alertmanager-bot`, `command` you will find `--alertmanager.url`:

```yaml
command:
	-'--alertmanager.url=http://<username>:<password>@alertmanager:9093/'

EXAMPLE
alertmanager-bot:
    container_name: alertmanager-bot
    image: metalmatze/alertmanager-bot:0.4.3
    command:
      - '--alertmanager.url=http://px:pundix@alertmanager:9093/'
```

{% hint style="info" %}
**DO NOT use `$` in any of your passwords, as it will not work with the `alertmanager.url`**
{% endhint %}

#### Commands

Start monitoring service:

```bash
docker-compose -f ./pundix/develop/docker-compose.yaml -p pundix-node-monitor up -d
```

Restart monitoring service:

```bash
docker-compose -f ./pundix/develop/docker-compose.yaml -p pundix-node-monitor restart
```

Stop monitoring service:

```bash
docker-compose -f ./pundix/develop/docker-compose.yaml -p pundix-node-monitor stop
```

### Updating Node Monitoring Services

{% hint style="info" %}
Do a update by pulling the latest code with the below command, whenever you are making changes to the telegram configuration under `./pundix/develop/docker-compose.yaml`
{% endhint %}

```bash
# pull the latest code base
docker-compose -f ./pundix/develop/docker-compose.yaml -p pundix-node-monitor pull

# start the monitoring device
docker-compose -f ./pundix/develop/docker-compose.yaml -p pundix-node-monitor up -d
```

{% hint style="info" %}
Ensure you have changed your passwords and also that your data source is configured correctly
{% endhint %}

## Prometheus Rules

| Metric                                              | Rule                                                                                                                                        | Threshold | explain                                                                                                   |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | --------- | --------------------------------------------------------------------------------------------------------- |
| `tendermint_consensus_height`                       | tendermint\_consensus\_height - (tendermint\_consensus\_height offset 1m) == 0                                                              | 0         | The node did not produce blocks in 1 minute                                                               |
| `tendermint_consensus_validators`                   | avg((tendermint\_consensus\_validators{kind="val-node"} - tendermint\_consensus\_validators{kind="val-node"} offset 1m) > 0) by (chain\_id) | 0         | The number of validators has increased compared to the number of validators a minute ago                  |
| `tendermint_consensus_validators`                   | avg((tendermint\_consensus\_validators{kind="val-node"} offset 1m - tendermint\_consensus\_validators{kind="val-node"}) > 0) by (chain\_id) | 0         | The number of validators is reduced compared to the number of validators one minute ago                   |
| `tendermint_consensus_latest_block_height`          | tendermint\_consensus\_latest\_block\_height - (tendermint\_consensus\_latest\_block\_height offset 2m)                                     | 0         | The height of the node does not increase in 2 minutes                                                     |
| `tendermint_consensus_validator_last_signed_height` | tendermint\_consensus\_validator\_last\_signed\_height - (tendermint\_consensus\_validator\_last\_signed\_height offset 2m) == 0            | 0         | The verifier did not sign in 2 minutes                                                                    |
| `tendermint_consensus_validator_missed_blocks`      | tendermint\_consensus\_validator\_missed\_blocks - (tendermint\_consensus\_validator\_missed\_blocks offset 2m) >= 3                        | 3         | The total number of blocks with the verifier address not participating in the signature is greater than 3 |
| `tendermint_consensus_missing_validators`           | tendermint\_consensus\_missing\_validators > 10                                                                                             | 10        | The number of verifiers not participating in the signature exceeds the threshold of 10                    |
| `tendermint_consensus_byzantine_validators`         | tendermint\_consensus\_byzantine\_validators > 0                                                                                            | 0         | The number of Byzantine validators exceeds the threshold 0                                                |
| `tendermint_consensus_byzantine_validators`         | tendermint\_consensus\_byzantine\_validators > 0                                                                                            | 0         | The number of Byzantine validators exceeds the threshold 0                                                |
| `tendermint_consensus_block_interval_seconds_sum`   | tendermint\_consensus\_block\_interval\_seconds\_sum / tendermint\_consensus\_block\_interval\_seconds\_count > 7                           | 7         | The block generation interval exceeds 7 seconds                                                           |
| `tendermint_consensus_rounds`                       | tendermint\_consensus\_rounds != 0                                                                                                          | 0         | Consensus round is not equal to 0                                                                         |
| `tendermint_consensus_num_txs`                      | tendermint\_consensus\_num\_txs > 100                                                                                                       | 100       | The number of block packaging transactions exceeds the threshold of 100                                   |
| `tendermint_mempool_size`                           | tendermint\_mempool\_size > 100                                                                                                             | 100       | The number of unchained transactions in the memory pool exceeds the threshold of 100                      |
| `tendermint_mempool_failed_txs`                     | tendermint\_mempool\_failed\_txs - (tendermint\_mempool\_failed\_txs offset 1m) > 10                                                        | 10        | The number of failed transactions in the memory pool has increased by more than 10 in 1 minute            |
| `tendermint_consensus_fast_syncing`                 | tendermint\_consensus\_fast\_syncing - (tendermint\_consensus\_fast\_syncing offset 5m) != 0                                                | 0         | The current synchronization status of the node is not 0                                                   |
| `tendermint_p2p_peers`                              | tendermint\_p2p\_peers < 5                                                                                                                  | 5         | The number of connected nodes is below the threshold 5                                                    |
| `tendermint_p2p_peers`                              | (tendermint\_p2p\_peers offset 30s) - tendermint\_p2p\_peers > 1                                                                            | 1         | The number of currently connected nodes decreases for 1 minute                                            |
