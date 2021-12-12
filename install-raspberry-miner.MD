# Download raspios_lite_arm64 images
https://downloads.raspberrypi.org/raspios_lite_arm64/images/

# Install Raspberry Pi OS using Raspberry Pi Imager
https://www.raspberrypi.com/software/


## Install Go manually
### Install Go

Let's go to home directory and declare `go`'s version that you want to download.

```sh
cd ~
export GOV=1.17.5 # golang version
```

After that, let's download and uncompress golang source.
https://go.dev/dl/

```sh
curl -sS https://storage.googleapis.com/golang/go$GOV.linux-arm64.tar.gz > go$GOV.linux-arm64.tar.gz
tar xvf go$GOV.linux-arm64.tar.gz
rm go$GOV.linux-arm64.tar.gz
```

lastly, let's install `go`.

```sh
sudo mv go /usr/local/go
sudo ln -s /usr/local/go/bin/go /usr/local/bin/go
sudo ln -s /usr/local/go/bin/godoc /usr/local/bin/godoc
sudo ln -s /usr/local/go/bin/gofmt /usr/local/bin/gofmt
```

Note: Find any golang source version at [Go Website](https://golang.org/dl/)

### Setup your GOPATH
The $GOPATH environment variable specifies the location of your workspace. It defaults to a directory named `go` inside your home directory, so $HOME/go on Unix.

Create your workspace directory with it's respective inner folders:

```sh
mkdir -p $HOME/go
mkdir -p $HOME/go/bin
mkdir -p $HOME/go/src
mkdir -p $HOME/go/pkg
```

Setup $GOPATH variable, add it to ~/.bashrc. After editing, run `source ~/.bashrc` or open a new tab.

```sh
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GOBIN=$GOPATH/bin
export PATH=$PATH:$GOBIN
```

## Test your Go installation
```sh
go version
```

# Skywire
## Build
```bash
# Clone.
$ git clone https://github.com/skycoin/skywire.git
$ cd skywire

# Build and Install
$ make build; make install
```

## Configure Skywire
### Expose hypervisorUI
In order to expose the hypervisor UI, generate a config file with `--is-hypervisor` or `-i` flag:

```bash
$ skywire-cli config gen -i
```
### Add remote hypervisor

Every visor can be controlled by one or more hypervisors. To allow a hypervisor to access a visor, the PubKey of the
hypervisor needs to be specified in the configuration file. You can add a remote hypervisor to the config with:

```bash
$ skywire-cli config update --hypervisor-pks <public-key>
```
## Run `skywire-visor`

`skywire-visor` hosts apps and is an applications gateway to the Skywire network.

`skywire-visor` requires a valid configuration to be provided. If you want to run a VPN client locally, run the visor
as `sudo`.

```bash
$ sudo skywire-visor -c skywire-config.json
```
