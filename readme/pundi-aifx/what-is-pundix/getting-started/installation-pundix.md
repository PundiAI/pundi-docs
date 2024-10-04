# Install Pundi X (PundiXChain)

This guide will explain how to install the `pundixd` CLI onto your system. With this installed on a server, you can participate on the mainnet as either a [Full Node](setup-node/) or a [Validator](https://github.com/FunctionX-SG/pundiai-docs/blob/main/px-docs/validators/setting-up-a-validator-for-pundix.md).

## Hardware Requirements

We recommend the following for running PundiX:

* 4 or more CPU cores
* At least 500G of disk storage
* At least 8G of memory
* At least 10mbps network bandwidth

To see a [quick cloud setup](../pundix-tutorials/cloud-setup.md) on how to setup and deploy it on the cloud.

## Install build requirements

Install `make` and `gcc`.

On Ubuntu this can be done with the following commands:

{% tabs %}
{% tab title="Ubuntu" %}
```
sudo apt-get update
sudo apt-get install -y make gcc
```

{% hint style="info" %}
`sudo apt-get install -y make gcc` may have encountered a problem with locked files, just try `sudo apt-get install -y make gcc` again.
{% endhint %}
{% endtab %}

{% tab title="Mac" %}
Ensure you have [Homebrew](https://brew.sh/) installed.

Once you have Homebrew installed, you may run the following commands to install `make` and `gcc`:

```bash
brew install make
brew install gcc
```

We'll be needing these commands later so let's install the necessary packages:

```bash
brew install git
brew install wget
```
{% endtab %}

{% tab title="Windows" %}
Ensure you have `make` and `gcc` installed and that the paths are set correctly for git bash.

One option for installing `gcc` can be found [here](https://jmeubank.github.io/tdm-gcc/articles/2021-05/10.3.0-release).

{% hint style="info" %}
You may select tdm64-gcc-10.3.0-2

Restart gitbash after installing
{% endhint %}

One option for installing `make` is using `chocolate` , more information can be found [here](https://chocolatey.org/install).

Once you have chocolate installed, run this command:

{% hint style="info" %}
make sure to run gitbash as administrator mode if the following commands DO NOT work
{% endhint %}

```
choco install make
```

Ensure you have all the necessary dependencies and compilers.

```
gcc --version
```

It will return:

```
gcc.exe (tdm64-1) 10.3.0
Copyright (C) 2020 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE
```

For make:

```
make --version
```

It will return:

```
GNU Make 4.3
Built for Windows32
Copyright (C) 1988-2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```
{% endtab %}
{% endtabs %}

## Install Go

{% tabs %}
{% tab title="All other environments" %}
Install `go` by following the [official docs](https://golang.org/doc/install). Please select your respective environment❗

{% hint style="info" %}
For Ubuntu environment, there may be `permissions denied` issues with unzipping the go zip file, try using `sudo su` to resolve it.
{% endhint %}
{% endtab %}

{% tab title="If you are remoting into a terminal" %}
Especially if you are remoting into a Ubuntu terminal, run this command to download the `go` installer:

```
wget https://dl.google.com/go/go1.18.3.linux-amd64.tar.gz 
```

{% hint style="info" %}
After you have downloaded the package and you may proceed to step 2 of the [official docs](https://golang.org/doc/install). Choose your system OS and follow the instructions stated.
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Go 1.18+** or later is required for the PundiX. If you are remoting into a terminal, you may input the following command:
{% endhint %}

Setting environment variables:

```
mkdir -p $HOME/go/bin
echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.profile
echo "export PATH=$PATH:$(go env GOPATH)/bin" >> ~/.profile
source ~/.profile
```

## Install the binaries

Next, let's install the latest version of PundiX. Make sure you have git installed if not you will be prompted to `install git`. Follow the instruction in the terminal.

{% tabs %}
{% tab title="All Other Environments" %}
```
git clone --branch release/v0.2.x https://github.com/pundix/pundix.git
cd pundix
make go.sum
make install
```
{% endtab %}

{% tab title="Windows" %}
{% hint style="info" %}
You should run your commands in gitbash. But open pundixd.exe file using cmd prompt

Make sure the name of your folder does not have whitespaces!
{% endhint %}

```
git clone --branch release/v0.2.x https://github.com/pundix/pundix.git
cd pundix
make go.sum
make build-win
```

{% hint style="info" %}
use cmd prompt to open the pundixd.exe file

in the path ./build/bin/pundixd.exe
{% endhint %}
{% endtab %}
{% endtabs %}

Verify version:

```
# Long version
pundixd version --long

# Short version
pundixd version
```

`pundixd version --long` should output something similar to:

```
name: pundix
server_name: pundixd
version: main-82a9ac1f21783bc4b2838026b1742a2bbdf0bcb0
commit: 82a9ac1f21783bc4b2838026b1742a2bbdf0bcb0
build_tags: netgo,ledger
go: go version go1.18.1 darwin/amd64
build_deps:
...
cosmos_sdk_version: v0.45.5
```

### Build Tags

Build tags indicate special features that have been enabled in the binary.

| Build Tag | Description                                     |
| --------- | ----------------------------------------------- |
| netgo     | Name resolution will use pure Go code           |
| ledger    | Ledger devices are supported (hardware wallets) |
