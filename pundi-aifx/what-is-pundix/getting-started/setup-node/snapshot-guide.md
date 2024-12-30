# Snapshot Guide

{% hint style="danger" %}
<mark style="color:yellow;">**WARNING**</mark>

1. First, you need to setup your node up with the pre-requisites as per the node **setup guide**
2. <mark style="color:red;">**Before you start**</mark> your node for pundix to sync, follow the steps below to use snapshot
3. If your pundix node has already started, <mark style="color:red;">**please stop it**</mark> and then follow the steps below to use the snapshot
4. Once unpacking is complete, you can start the pundix service again
{% endhint %}

## Types of PundiX Snapshots

1. A pruned-snapshot, which contains only the most recent day's data
   * Only data for the most recent day, no earlier data
   * Small amount of data and footprint
2. A full-node snapshot, which contains all the transaction data
   * Contains all transaction data, as well as current state data
   * Large amount of data and footprint
3. An archive-snapshot, which contains all transaction data as well as all state data (<mark style="color:red;">**syncing, not open yet**</mark>)
   * Contains all transaction and status data
   * The amount of data is very large and takes up a lot of space
   * In general, you DO NOT need to use an archive node

The greater the blockchain data, the more evident the reduction is syncing time will be. If the current state of the blockchain will take about 2 days to sync, this method of syncing will reduce the time to sync by at least 12 hours.

## Available snapshots

<mark style="color:orange;">**Snapshots are performed based on its type as per below**</mark><mark style="color:orange;">,</mark> keeping a record of recent snapshot for as per below. If the date on the file is not yet updated and more than a week has lapsed since the last snapshot, you may replace the date in the file name to get the latest snapshot. <mark style="color:orange;">**If the date or day of the month are single digits, make sure to prepend a 0 in front of the single digit number. Date format will be in YYYY-MM-DD.**</mark>

{% tabs %}
{% tab title="Mainnet" %}
* Pruned-shapshot (light node)
  * Snapshot frequency: once a day (10am GMT +8)
  * Snapshot record keeping: 7 most recent
  * Shapshot link: [https://px-mainnet.s3.amazonaws.com/pundix-pruned-snapshot-mainnet-2023-MM-DD.tar.gz](https://px-mainnet.s3.amazonaws.com/pundix-pruned-snapshot-mainnet-2022-08-01.tar.gz)
  * Md5 link: [https://px-mainnet.s3.amazonaws.com/pundix-pruned-snapshot-mainnet-2023-MM-DD.tar.gz.md5](https://px-mainnet.s3.amazonaws.com/pundix-pruned-snapshot-mainnet-2022-08-01.tar.gz.md5)
* Full-node snapshot (full node)
  * Snapshot frequency: every Monday (10am GMT +8)
  * Snapshot record keeping: 3 most recent
  * Shapshot link: [https://px-mainnet.s3.amazonaws.com/pundix-snapshot-mainnet-2023-MM-DD.tar.gz](https://px-mainnet.s3.amazonaws.com/pundix-snapshot-mainnet-2022-08-01.tar.gz)
  * Md5 link: [https://px-mainnet.s3.amazonaws.com/pundix-snapshot-mainnet-2023-MM-DD.tar.gz.md5](https://px-mainnet.s3.amazonaws.com/pundix-snapshot-mainnet-2022-08-01.tar.gz.md5)
* Archive node - <mark style="color:red;">**synchronising**</mark>
  * Snapshot frequency: once a day (10am GMT +8)
  * Snapshot record keeping: 3 most recent
  * ~~Shapshot link:~~ [~~https://px-mainnet.s3.amazonaws.com/pundix-archive-snapshot-mainnet-2023-MM-DD.tar.gz~~](https://px-mainnet.s3.amazonaws.com/pundix-archive-snapshot-mainnet-2022-08-01.tar.gz)
  * ~~Md5 link:~~ [~~https://px-mainnet.s3.amazonaws.com/pundix-archive-snapshot-mainnet-2023-MM-DD.tar.gz.md5~~](https://px-mainnet.s3.amazonaws.com/pundix-archive-snapshot-mainnet-2022-08-01.tar.gz.md5)
{% endtab %}

{% tab title="Testnet" %}
* Status data (pruned node)
  * Snapshot frequency: once a day (10am GMT +8)
  * Snapshot record keeping: 7 most recent
  * Shapshot link: [https://testnet-px.s3.amazonaws.com/pundix-pruned-snapshot-testnet-2023-MM-DD.tar.gz](https://testnet-px.s3.amazonaws.com/pundix-pruned-snapshot-testnet-2022-08-01.tar.gz)
  * Md5 link: [https://testnet-px.s3.amazonaws.com/pundix-pruned-snapshot-testnet-2023-MM-DD.tar.gz.md5](https://testnet-px.s3.amazonaws.com/pundix-pruned-snapshot-testnet-2022-08-01.tar.gz.md5)
* Data (full node)
  * Snapshot frequency: every Monday (10am GMT +8)
  * Snapshot record keeping: 3 most recent
  * Shapshot link: [https://testnet-px.s3.amazonaws.com/pundix-snapshot-testnet-2023-MM-DD.tar.gz](https://testnet-px.s3.amazonaws.com/pundix-snapshot-testnet-2022-08-01.tar.gz)
  * Md5 link: [https://testnet-px.s3.amazonaws.com/pundix-snapshot-testnet-2023-MM-DD.tar.gz.md5](https://px-testnet.s3.amazonaws.com/pundix-snapshot-testnet-2022-08-01.tar.gz.md5)
* Archive node - <mark style="color:red;">**synchronising**</mark>
  * Snapshot frequency: once a day (10am GMT +8)
  * Snapshot record keeping: 3 most recent
  * ~~Shapshot link:~~ [~~https://testnet-px.s3.amazonaws.com/pundix-archive-snapshot-testnet-2023-MM-DD.tar.gz~~](https://testnet-px.s3.amazonaws.com/pundix-archive-snapshot-testnet-2022-08-01.tar.gz)
  * ~~Md5 link:~~ [~~https://testnet-px.s3.amazonaws.com/pundix-archive-snapshot-testnet-2023-MM-DD.tar.gz.md5~~](https://testnet-px.s3.amazonaws.com/pundix-archive-snapshot-testnet-2022-08-01.tar.gz.md5)
{% endtab %}
{% endtabs %}

## Downloading the Snapshots

Download the snapshot to your VM. To download the snapshot tar file to your VM you can run the following command:

{% tabs %}
{% tab title="Mainnet" %}
```bash
wget -c https://px-mainnet.s3.amazonaws.com/pundix-snapshot-mainnet-2023-01-01.tar.gz
```
{% endtab %}

{% tab title="Testnet" %}
```bash
wget -c https://px-testnet.s3.amazonaws.com/pundix-snapshot-testnet-2023-01-01.tar.gz
```
{% endtab %}
{% endtabs %}

This will download the snapshot of pundix full-node data. Since it's full-node, downloading the snapshot and unpacking the file will take some time.

## MD5 checksum for downloaded file

Checksums are often used to verify data integrity but are not relied upon to verify data authenticity, below are example of the `md5sum` command to check whether the file is downloaded correctly using

```bash
$ md5sum pundix-snapshot-mainnet-2023-01-01.tar.gz
4269fe416ca2d74d3925449f5ce7d214  pundix-snapshot-mainnet-2023-01-01.tar.gz
```

Compare the md5 hash against `https://px-mainnet.s3.amazonaws.com/pundix-snapshot-mainnet-2023-01-01.tar.gz.md`

## Extracting the Snapshots

Now, to unpack the `tar` file in the PundiX Data directory run the following command:

{% tabs %}
{% tab title="Mainnet" %}
```bash
tar -xzvf pundix-snapshot-mainnet-2023-01-01.tar.gz -C ~/.pundix/
```
{% endtab %}

{% tab title="Testnet" %}
```bash
tar -xzvf pundix-snapshot-testnet-2023-01-01.tar.gz -C ~/.pundix/
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If your pundix data directory is placed on different directory then please rename to that.

When you are unpacking the snapshot, it is already contained in a data folder, you will be replacing the data folder below. Be sure to maintain the integrity of this directory tree structure.
{% endhint %}

```bash
root@host:~# ls -l ~/.pundix/data/
total 64
drwxr-xr-x 2 root root 36864 Aug  2 16:49 application.db
drwxr-xr-x 2 root root  4096 Aug  2 16:26 blockstore.db
drwx------ 2 root root  4096 Aug  2 16:44 cs.wal
drwxr-xr-x 2 root root  4096 Aug  2 15:32 evidence.db
-rw------- 1 root root    46 Aug  1 10:02 priv_validator_state.json
drwxr-xr-x 3 root root  4096 Aug  1 10:02 snapshots
drwxr-xr-x 2 root root  4096 Aug  2 16:48 state.db
drwxr-xr-x 2 root root  4096 Aug  2 16:29 tx_index.db
```
